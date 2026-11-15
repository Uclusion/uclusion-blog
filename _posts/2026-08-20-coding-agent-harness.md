---
layout: post
title:  "How an agent spends tokens"
author: david
image: assets/images/ai-collaboration.png
categories: [ engineering ]
last_modified_at: 2026-11-13
---
A coding agent repeatedly asks a model what to do next. Each request supplies context: instructions, conversation history, tool definitions and results. 
Until it is compacted the context only grows and the entire context gets sent on every request. The costs add up at market rates as multiples of 
three kinds of tokens.

| Kind of token | What it counts |
| --- | --- |
| Fresh input | Prompt tokens processed without a cache hit. |
| Cached input | Prompt tokens whose previously computed state can be reused. They still cost but at a lower rate. |
| Output | Tokens the model generates, including its replies and tool-call arguments. These typically cost the most. |

OpenAI's [prompt-caching guide](https://developers.openai.com/api/docs/guides/prompt-caching) explains caching and its accounting.
Anthropic's [prompt-caching guide](https://platform.claude.com/docs/en/build-with-claude/prompt-caching) explains how caching works for Claude. In both
cases the trick is that although cached tokens are billed at a reduced rate compared to fresh, they are billed every time the agent makes a call to 
the model. So fresh input added at the beginning of a session will be charged once as fresh and then again as cached on every model call until
a compaction event.

Output can also be billed more than once as the output of a subagent can be the input of a parent agent.

## Subagents can reduce cached input

Consider a repository search that produces pages of paths, code and rejected leads. The original parent agent needs the conclusion, but not every search result in all its later requests. A helper can do that exploration in its own context and return a concise result. The parent's subsequent input then carries the result instead of the whole exploration.

Some helpers are best one and done as you avoid using their bloated context again. Other helpers may have a lifecycle as their context is useful for a
time to answer further questions.

## How MCP adds to context

MCP, the Model Context Protocol, connects a coding client to external tools and data. Its [tools specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools) defines tool discovery, descriptions, argument schemas and returned content. The protocol traffic and the model's context are different things: the client decides what to put in a model request.

For example, fetching a catalog with `tools/list` does not by itself prove that every schema enters every prompt. A client may supply definitions upfront or discover a relevant subset when needed. Anthropic's [analysis of MCP context costs](https://www.anthropic.com/research/code-execution-with-mcp) distinguishes the cost of tool definitions from the intermediate results passed through the model.

However MCP connects to every subagent so a bloated catalog definition can impact context size. Claude Code can [lazy load a server's tools](https://code.claude.com/docs/en/mcp#defer-a-servers-tools) with `"alwaysLoad": false`. [Codex also lazy loads tools](https://github.com/openai/codex/pull/29486) when its model and provider support tool search, and exposes them directly otherwise. 

Fetching the full MCP catalog makes its definitions available to the client; it does not itself put the entire catalog into the model's context. With deferred tool search enabled, [Claude Code](https://code.claude.com/docs/en/mcp#scale-with-mcp-tool-search) and [Codex](https://github.com/openai/codex/blob/rust-v0.169.0/codex-rs/core/src/tools/handlers/tool_search.rs#L237) load definitions for matching candidates as needed. 

However making lazy loading tools work requires a subagent know its restricted set of tools in order to avoid loading the entire catalog.

## Making an agent collaborate is hard
By default AI agents do not work well with humans:
* A turn can end without any indication of what the human is supposed to do
* Every message from an external system causes a model call so redundant or irrelevant messages are expensive
* Default AI prompts encourage too much independence
* External system operations must avoid reading redundant data and causing expensive cached input
* The default timer that wakes up an agent, [wait implementation](https://github.com/openai/codex/blob/69231e119bfca0b14453515e97d99688ce1c47c9/codex-rs/core/src/tools/handlers/multi_agents_v2/wait.rs#L54-L107), must be tuned to avoid too many model calls

Any memory that an agent saves and injects into every context must be carefully monitored. No memory and the agent must be told the same thing
over and over. Too much memory and again cached input token costs swamp the model calls. 

These are the constraints behind Uclusion's integration. Its [workflow roles](https://github.com/Uclusion/uclusion_web_ui/blob/ab53cb2278c3fec9e84c7f34c98c93b577e4f9fa/public/scripts/skills/uclusion/README.md) scope instructions and helper work around maintained decisions, while its MCP proxy and [native Codex delivery](https://github.com/Uclusion/uclusion_web_ui/blob/ab53cb2278c3fec9e84c7f34c98c93b577e4f9fa/public/scripts/uclusionCodexNative.py) routes external updates to the conversations responsible for the work.

[Signing up](https://uclusion.com) is free.
