---
layout: post
title:  "Typed Collaboration"
author: david
image: assets/images/typed-collaboration.png
categories: [ engineering ]
---
The way software teams communicate was designed for neither humans nor machines. It was bad for us for years, and now it is incompatible with the AI that writes most of our code. This post gives the alternative a name: **typed collaboration**.

## The old way was already bad for humans

Most teams still run on some mix of three practices:

1. Lots of meetings, and not much written down.
2. Walls of text in chat.
3. Sticky note style boards pretending to be a plan.

These made asynchronous collaboration impractical long before AI showed up. If the decision lives in a meeting, you had to be in the room. If it lives three screens back in a chat scroll, you have to have been following along. Either way, someone who wasn't there has to interrupt someone who was.

## And it is incompatible with AI

An AI's job is already very difficult. These practices make it harder — and some of them make it impossible:

* An agent cannot attend your standup, so whatever was decided there does not exist for it.
* An agent reading a wall of chat cannot reliably tell which of the forty messages was the decision, which were thinking out loud, and which were abandoned.
* A board of one-line cards isn't enough organization to start one.

## What's missing is a protocol

Watch an AI work and you can see it already has one. An AI thinks and talks in markdown. When a good agent poses a question, it is completely clear what the question blocks, what the options are, and which option the agent prefers with what certainty. When it makes a suggestion or writes a note, that content deserves a clear path to somewhere organized and permanently stored instead of dissolving into a scroll.

The problem is that our communication has no such structure to receive it. Chat is untyped: every message is just a string, and any meaning — this is a question, this blocks the work, this was decided — lives only in the heads of whoever happened to read it at the time.

**Typed collaboration** is the practice of giving every piece of team communication a type — a question, a suggestion, a task, a blocker, a note, an approval,a report, a bug, a job at a known stage. A typed suggestion gets explicitly accepted or rejected instead of scrolling away. A typed blocker gates the work until someone resolves it. A typed note is context, stored where the work is.

Once communication is typed, it can be routed, queried, and acted on by whoever reads it next like a teammate in another timezone, or an agent starting its next session.

<img src="{{ site.baseurl }}/assets/images/typed-collaboration.png" alt="Untyped chat on the left — identical gray bubbles. On the right the same communication typed: a question with options and certainty, a suggestion accepted, a task done, a blocker gating, a note stored." />

## The stakes changed

Working untyped used to cost you speed. Now it costs you your best collaborator. An AI can deliver code as fast as you can decide what to build, which makes the deciding the real work. Keep deciding informal and you exclude AI from it: the agent is reduced to a code generator that guesses at every fork, instead of the full collaborator it needs to be. The same structure that lets the AI participate is what lets a second human join mid-stream without a catch-up meeting.

## An implementation

We built [Uclusion](https://uclusion.com) as typed collaboration end to end: questions, suggestions, tasks, blockers, and notes are typed, durable artifacts that humans and AI work through together. If you want to see what the practice looks like day to day, I wrote up [how I plan with a coding agent in Uclusion, not chat]({{ site.baseurl }}/engineering/startup/2026/05/29/uclusion.html).

But however you work, give your communication types.
