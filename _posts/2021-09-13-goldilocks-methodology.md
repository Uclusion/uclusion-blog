---
layout: post
title:  "The Agile Goldilocks Problem"
author: david
image: assets/images/goldilocks.jpg
categories: [ agile ]
featured: true
---
### Two bowls and hidden technology choices
In my software career, I've seen two approaches - endless meetings or working alone. For open source or 
the IETF, things look radically different but as soon as paying customers are on the table, reasonable collaboration 
seems off the table.

In my recent experience with having an explainer video made meetings were used only for brainstorming. The explainer
video company had approval software that captured what was being approved and by whom and feedback software that allowed
you to comment frame by frame in a story board or video.

That video process, designers and Figma or InVision like tools, and any number of business processes incorporate
modern tools. In 25 years I've seen two changes to developer communication: Scrum / open office and Covid forcing 
remote work mainstream (email, wiki and group chat / IRC were already there).

Our industry is slow to adapt process, and as Martin Fowler observed in his 2006 
[article on CI/CD](https://martinfowler.com/articles/continuousIntegration.html), it's for the wrong reasons:

>When I've described this practice to people, I commonly find two reactions: "it can't work (here)" and
"doing it won't make much difference". What people find out as they try it is that it's much easier than it sounds,
and that it makes a huge difference to development. Thus the third common reaction is "yes we do that - how could you
live without it?"

{% include callout.html
content="It's **not okay** for a methodology to prescribe communication technology like face-to-face / open office or
Kanban boards."
type="warning" %}

Face-to-face depends on a transportation system and laptops to code on during the meeting and 
also *replaces other communication technologies like Zoom*. If we lived in a Star Wars world would we consult the
agile manifesto to tell us whether to have hologram meetings or use hyperdrive? Similarly, using sticky notes doesn't 
make a Kanban board less of a technology choice.

### Meeting all the time is too hot
Deciding what we work on and how we implement is the most important process. Let's use an open floor plan to encourage 
one continuous meeting all the time! Every introduction of Scrum I witnessed was followed by open offices.

And I get the logic - it's at least consistent. But now that almost everyone realizes the issues with an all day 
meeting environment, it's time to also see the limitations of meetings as a software developer communication tool.

You can't afford to have meetings all the time and, in an agile environment, you also can't afford to have your
approvals, questions and feedback wait for the next meeting where it will be difficult to decide everything real
time anyway. 

{% include callout.html
content="Relying soley on meetings means choosing between interruptions and regularly doing the wrong thing or the 
wrong way."
type="warning" %}

### Working by yourself is too cold
There is a class of problems that can be solved with limited interaction with others. Let's call 
them *yesterday's problems*. Yesterday's problems have fairly obvious solutions and if you need extra hands for the 
grunt work you can employ a [code factory]({{site.baseurl}}/agile/2021/08/16/code-factory.html) process.

For a large supply of yesterday's problems just pile up technical debt and let your competition do all the innovation.

However, even if you are the product manager or chief architect, today's problems are too complex to take on without a 
lot of guiding opinions.

{% include callout.html
content="When a team is available, deciding by yourself only makes sense if the ROI on communication tools is not there."
type="warning" %}

### Experimenting isn't that hard
Without quoting process scripture, many decisions, like allowing in office participation, become daunting. Nor does 
watching papa and mama bear big companies communications decisions necessarily tell you what is right for you.

The good news is that our industry over-estimates the cost of process experimentation. My previous employer 
successfully experimented with remote work long before the pandemic. Some easy communications process experiments:
* Try different communications tools for a hack-a-thon
* Run a parallel process for technical debt instead of a retro
* "Just right" size your backlog and the amount each item is specified
* Have ongoing feedback instead of end of sprint demo meetings
* Drop scheduled 1-1 meetings in favor of an office hours approach
* Encourage development teams to choose their own process and tools

We have to find quick ways to try potential solutions or we will not only be eating the wrong porridge but sitting in 
the wrong chair and sleeping in the wrong bed as well.

### How to make the third bowl available
There are many communications solutions out there and many of them fully justify the manifesto's warning to stick to 
face-to-face. But these days we know a few things about how we prefer to operate online:
* Questions - almost every developer is happy when a question can be answered by online interactions and a meeting 
avoided
* Status - we are all used to checking status of nearly everything online these days 
* Feedback - again we all give and receive feedback online constantly
* Suggestions - unless forced most developers would use email to get opinions and only follow up with a meeting if
necessary. Software wise we can do better than email, but it's still easily superior to a meeting where everyone
hears the suggestion for the first time.
* Approval - like or dislike is the bread and butter of the online world
* _Brainstorming - I would argue that only here does face-to-face really shine_

So we are looking for communication tools that offer fully asynchronous, meeting free solutions for questions, status,
feedback, suggestions and approval.

{% include callout.html
content="Communications software should offer you a true alternative, instead of simulating or supplementing meetings."
type="warning" %}

Because in 2021 that's what we already expect from communications tools except when we go to an office still in 2001.


