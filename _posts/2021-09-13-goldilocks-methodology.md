---
layout: post
title:  "The agile Goldilocks problem - the death of one size fits all forever"
author: david
image: assets/images/goldilocks.jpg
categories: [ agile ]
featured: true
---
In 25 years I've yet to see a project get process right and that hurt the most. We frequently ended
up working on the wrong thing or the wrong way and this is why my co-founder and I started Uclusion more than two years
ago.

Before Covid I had only seen one major effort to change the way we work - Scrum / open office. Now with the 
rise of remote work there is a lot more questioning of process and communications tools but there is still
a lot of reluctance to try new things.

Martin Fowler observed the same thing for build process in his 2006
[article on CI/CD](https://martinfowler.com/articles/continuousIntegration.html):

>When I've described this practice to people, I commonly find two reactions: "it can't work (here)" and
"doing it won't make much difference". What people find out as they try it is that it's much easier than it sounds,
and that it makes a huge difference to development. Thus the third common reaction is "yes we do that - how could you
live without it?"

Even when software development does try new collaboration practices it's usually in an industry-wide, one size fits 
all way.

This is the agile Goldilocks problem. As convenient as standard process would be, we have to accept that
software development is a lot more complex than that. If we don't find ways to try solutions more suited to our 
specific team's needs, we will not only be eating the wrong porridge, but sitting in the wrong chair and sleeping in 
the wrong bed as well.

For example my previous employer started experimenting with remote work long before Covid. And there was push back 
quoting the Agile Manifesto's face-to-face principle! If Star Wars technology becomes available will we reference a 
20-year-old document to tell us whether to have hologram meetings or use hyperdrive?

It's okay for a software development methodology to list requirements like fast feedback or work as a team.

{% include callout.html
content="It's **not okay** for a methodology to prescribe communication technology like face-to-face / open office or
Kanban boards."
type="warning" %}

The result is that most software developers, outside open source or the IETF, are **forced to choose between endless, 
mostly ineffective meetings or working alone**.

When we had an explainer video made meetings were used only for brainstorming. The video company had approval software 
that captured what and who approved and feedback software that allowed you to comment frame by frame in a story board 
or video.

That video process, designers and Figma or InVision, and any number of business processes incorporate tools
_specifically designed for them_. But software development continually underestimates the challenges of working 
together to build the right thing and so employ tools like sticky notes based on 1970s factory work!!

<img src="{{ site.baseurl }}/assets/images/kanban.png" alt="Kanban" style="width: 90%;" />

It's this combination of very few choices with technology and ideas developed in other times for other purposes that 
makes the agile Goldilocks problem so devastating.

### Meeting all the time is too hot
Nothing is more important than deciding what we work on and how we implement it. So the thinking behind Scrum was
lots of meetings insure you get it right. Plus every introduction of Scrum I witnessed was followed by open offices in 
case something comes up when you are not in a meeting.

And I get the logic - it's at least consistent. But now, more than ever, developers realize the issues with open office
(and are being offered 
[libraries](https://www.fastcompany.com/90626329/these-architects-popularized-the-open-office-now-they-say-the-open-office-is-dead)
instead?)
and it's time to also see the limitations of meetings as a software developer communication tool.

You can't afford to have meetings all the time and, in an agile environment, you also can't afford to have your
approvals, questions and feedback wait for the next meeting where it will be difficult to decide everything real
time anyway. 

{% include callout.html
content="Relying soley on meetings means choosing between frequent interruptions and doing the wrong thing or the wrong 
way."
type="warning" %}

Scrum does offer some customization parameters. You can increase the Sprint length which reduces the frequency of 
meetings. You control your own Definition of Done. Still Scrum is fundamentally a system designed around a single 
product owner who has a very tight relationship with a single or small group of customers and development work that is 
not platform intensive.

So for one size fits all usage a typical SaaS product is out of luck right away - the product owner makes no sense 
(even if a single person could represent 1000s of customers he still wouldn't help on the technical side), the end of 
Sprint demo makes no sense (if we're just demo'ing internally why risk waiting for the end of Sprint?) and even 
Definition of Done is weird on a product that may allow exceptions to get quick feedback (for instance
[at an early startup](https://builtin.com/software-engineering-perspectives/scrum-startup-alternative)).

However, even if your team is working in a contract shop with single customer requirements, Scrum is still exactly 
specifying all the meetings in a way that may not work for you. What if your team members are spread across time 
zones? - just don't do that or suck it up says Scrum. What if the customer wants to have an almost immediate feedback
loop? - no we prefer the requirements stay fixed for the iteration says Scrum.

But inflexibly creating your own process is not great either. For instance, I was on a team doing infrastructure work 
without a product owner. So the team had a spreadsheet where we voted on priorities. A few of us assigned ourselves
the top item but unfortunately the spreadsheet didn't record the certainty or reasons behind the votes. 

It turned out this project's popularity was a result of recent incidents in production. So then we said well we will 
need to expand or drop this project but that wasn't allowed. We completed the project but the incidents stopped 
happening and our code was never deployed.

Whether you create your own process or start with off the shelf the key is continuing to experiment and look 
for the latest practices and technology to help you.

### Working by yourself is too cold
There is a class of problems that can be solved with limited interaction with others. Let's call 
them *yesterday's problems*. Yesterday's problems have fairly obvious solutions and if you need extra hands for the 
grunt work you can employ a [code factory]({{site.baseurl}}/agile/2021/08/16/code-factory.html) process.

For a large supply of yesterday's problems just pile up technical debt and let your competition do all the innovation.

However, even if you are the product manager or chief architect, today's problems are too complex to take on without a 
lot of guiding opinions. I've more than once seen product architecture updates fail because one person, by himself, 
chose an architecture or requirements that didn't make sense. And giving a PM unrestrained control of engineering is
just as likely to break down.

{% include callout.html
content="When a team is available, deciding by yourself only makes sense if the ROI on communication tools is not there."
type="warning" %}

Even if you make a winning decision by yourself you may not be rewarded for it. My co-founder found that out after
a very successful skunkworks change to storage architecture. If management rewarded him it would be sending a message
for everyone to do projects fait accompli.

But with email and meetings as his only tool for getting approval it would have been difficult to follow process. 
Neither tool records the opinion, certainty and reason of its participants or encourages any sort of 
deadline for voting. A choice between endless, mostly ineffective meetings and working alone, means, either way,
only extreme options are available.

### Experimenting isn't that hard
Without quoting process scripture, many decisions, like allowing in office participation, become daunting. Nor does 
watching papa and mama bear big companies communications decisions necessarily tell you what is right for you.

The good news is that our industry over-estimates the cost of experimentation. Some easy communications process 
experiments:
* Try different communications tools for a hack-a-thon
* Run a parallel process for technical debt instead of a retro
* "Just right" size your backlog and the amount each item is specified
* Have ongoing feedback instead of end of sprint demo meetings
* Drop scheduled 1-1 meetings in favor of an office hours approach
* Encourage development teams to choose their own process and tools (à la 
[Spotify](https://www.youtube.com/watch?v=4GK1NDTWbkY&list=RD4GK1NDTWbkY) except maybe the part about separating
squads by feature versus infrastructure)
* Create an initiative process where anyone can suggest or vote on other initiatives
* Make PM recommended feature work also go through that initiative process instead of automatically staffing

The other good news is that whether because of the rise of remote work or heightened competition in an ever-growing
industry experimentation is on the rise. 

The bad news is there are limited resources for learning what is really working for others and rapidly changing makes 
information age fast. What is available is frequently [written by people](https://www.mckinsey.com/business-functions/organization/our-insights/revisiting-agile-teams-after-an-abrupt-shift-to-remote) 
with very limited coding experience - much less first-hand experience coding remotely (and how at this point does
anyone present poll results with a straight face?).

The other bad news is you can spend a long time experimenting, as 
[PagerDuty](https://www.pagerduty.com/blog/scaling-engineering-org) describes, and getting it wrong is painful.
That's why we believe a communication tool designed for these problems can remove a lot of drudge work and speed
things up.

For experimenting with communications solutions there are many choices and most of them fully justify the 
manifesto's warning to stick to face-to-face. But these days we know a few things about how we prefer to operate online:
* Questions - almost every developer is happy when a question can be answered by online interactions and a meeting 
avoided
* Status - we are all used to checking status of nearly everything online these days 
* Feedback - again we all give and receive feedback online constantly
* Suggestions - specialized software can do better than email, but email is still easily superior to a meeting where 
everyone hears the suggestion for the first time.
* Approval - like or dislike is the bread and butter of the online world
* _Brainstorming - I would argue that only here does face-to-face really shine_

So we are looking for communication tools that offer fully asynchronous, meeting free solutions for questions, status,
feedback, suggestions and approval.

{% include callout.html
content="Communications software should offer you a true alternative, instead of simulating or supplementing meetings."
type="warning" %}

Because in 2021 that's what we already expect from communications tools except when we go to an office still in 2001.


