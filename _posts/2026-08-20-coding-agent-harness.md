---
layout: post
title:  "Building and testing human in the loop behavior"
author: david
image: assets/images/ai-collaboration.png
categories: [ engineering ]
---
Coding models are trained to be useful. Coding harnesses turn that usefulness into momentum: inspect the repo, make a reasonable assumption, edit the code, run the tests, keep going.

If I ask for rate limiting, an agent can immediately choose a token bucket, decide where its state lives, invent a retry response, and ship a polished implementation. The code may be good. The collaboration was not. Three decisions just became expensive facts before I knew they existed.

The model is only half the system. The harness around it decides what context the model sees, which actions feel normal, when it should stop, and whether a human gets a meaningful turn before the code does.

## The harness is already steering

This pressure is not hidden. Public prompt guidance says it plainly.

OpenAI's [Codex prompting guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide) recommends:

> “Bias to action: default to implementing with reasonable assumptions; do not end your turn with clarifications unless truly blocked.”

Anthropic's published [core system prompt for Claude Opus 5](https://platform.claude.com/docs/en/release-notes/system-prompts#claude-opus-5) on claude.ai and its mobile apps says Claude:

> “tries to address even an ambiguous query before asking for clarification.”

Anthropic explicitly says these published system-prompt updates do not apply to the Claude API, so this is not a claim about Claude Code's private harness. It shows pressure at a different layer: the chat product tells Claude to address ambiguity before asking for clarification. Separate current OpenAI model guidance defines explicit [approval boundaries](https://developers.openai.com/api/docs/guides/latest-model#define-autonomy-and-approval-boundaries) for destructive, external, costly, or scope-expanding actions.

The sources sit at different layers, but the tension is the same. Instructions that prize momentum can turn clarification into friction. “Use a reasonable assumption” is often exactly right for a variable name. It is wrong for a product choice whose consequences spread through the system.

Human-in-the-loop cannot mean a human reviews whatever the agent happened to build. The human needs to be in the loop while the work is still cheap to change.

## We modify the instruction stack around the model

Uclusion does not alter OpenAI's or Anthropic's private prompts. It adds a collaboration protocol to the global or project-level instruction stack that Codex, Claude Code, and Cursor already load.

The installed bootstrap is deliberately small. It tells the harness when to load a more complete workflow. That workflow is public; you can read [the current Uclusion skill on GitHub](https://github.com/Uclusion/uclusion_web_ui/blob/master/public/scripts/skills/uclusion/SKILL.md) instead of relying on a quotation here that will go stale.

Its core sequence:

1. Turn unsettled choices into separate questions with real options.
2. If the design note is absent, write one stand-alone system story from the settled premises before editing.
3. Keep that design current.
4. Implement the settled contract and validate it under separately approved test and security boundaries.
5. Request review by naming the design note and reporting only what the implementation did differently or in addition.

A Uclusion coding agent is instructed by, "Your work is judged not solely by completion but also by whether your human partner understands and approves of what you do."

That is runtime counterpressure against the combined default behavior of the model and harness: retain the agent's ability to act, while changing what counts as forward progress. It changes the workflow, not the model's training.

## A prompt is not enough

We have [written before]({{ site.baseurl }}/engineering/2026/01/21/ai.html) that a rules file can improve almost any coding setup. But instructions alone are fragile. So Uclusion represents the workflow as state, not just prose.

When the agent asks a qualifying question, the job moves to **Requires Input**. Implementation is locked until a current human assignee answers and the agent resolves the question. When the human responds, Poke AI wakes the connected terminal and reloads the current state.

This is [typed collaboration]({{ site.baseurl }}/engineering/2026/08/03/typed-collaboration.html): a question is not merely a paragraph that sounds inquisitive. It has a type, an owner, a lifecycle, and an effect on what can happen next.

The design note tells the end-to-end story: every material claim traces back to human direction, a settled answer, an approved plan, or a hard source constraint. Forcing a design note makes both human and AI aware of the contract and anything done outside of it.

## Then we test the whole thing with real agents

A conventional test can prove that an MCP tool returns a job or that a Poke reaches a proxy. It cannot prove that a fresh coding agent, under its current default model and harness instructions, will collaborate at the moment those pressures collide.

The executable [live-agent acceptance suite](https://github.com/Uclusion/nodejs_sdk/blob/master/testAgentDev/README.md#L1-L13) publishes the exact [Claude Code, Codex, and Cursor scenario matrix](https://github.com/Uclusion/nodejs_sdk/blob/master/testAgentDev/matrix.js#L1-L33). Raw run artifacts are not published.

We run [two Codex-only question-gate scenarios](https://github.com/Uclusion/nodejs_sdk/blob/master/testAgentDev/questionGateScenarios.js#L1-L40): one with explicit choices and one with implied choices. In the harder case, Codex is handed an [underspecified rate-limiter job](https://github.com/Uclusion/nodejs_sdk/blob/master/testAgentDev/questionGateFixture.js#L39-L67) without being told, in that prompt, to stop and expose its hidden choices before editing. Passing is [measured from durable state](https://github.com/Uclusion/nodejs_sdk/blob/master/testAgentDev/questionGateFixture.js#L465-L534): the implementation task must remain untouched, the job must be locked for input, each hidden architectural fork must have its own optioned question, and already-settled premises must not be reopened as choices.

That is why we use real clients. We are testing the behavior produced by the model, its harness, our instructions, our tools, and our state machine together. Any one layer can change the result.

## What this does and does not do

Uclusion does not retrain the model. It makes collaboration an explicit part of the runtime contract. When one of those tested behaviors drifts, the gate tells us before customers do.

A system that treats understanding, questioning, deciding, implementing, and reviewing as different kinds of progress becomes a much better teammate.

[Signing up](https://uclusion.com) is free.
