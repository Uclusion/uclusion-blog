---
layout: post
title:  "The agile Goldilocks problem - the death of one size fits all forever"
author: david
image: assets/images/goldilocks.jpg
categories: [ agile ]
featured: true
---
In our long careers, working on the wrong thing or the wrong way crippled our software projects again and 
again and writing code that's not useful is a known industry-wide problem.

So my co-founder and I started Uclusion more than two years ago with two goals:
1. Developers should spend more time working on the right thing
2. This progress should not come at the expense of longer hours

Imagine a perfectly autonomous software engineer - hypothetically a developer at Facebook who submits code that is
automatically A/B tested across the world and immediately rewarded with bonuses if it helps (example from iiSM.org). 
The question is how can we in the not hypothetical world have more control that we write useful code?

At first, we thought customers telling us what to do would be the key. Unfortunately dumping the problem on customers 
won't work because all too often the right feature is:
* no feature - do technical debt instead
* one that new customers need more than existing
* chosen but worked on the wrong way

Customers can't be relied on for deeper thought and product management is already fully occupied with it. If you change 
the product management to developer ratio that will only result in violating goal two and most product managers will 
have a difficult time representing technical projects.

There are any number of agile software methodologies promising to help. In fact using workers to help cut out wasted
effort and continuously improve is the [lean framework](https://en.wikipedia.org/wiki/Lean_thinking) from which they came.
Paradoxically though, codifying and freezing the process and tools of an agile methodology is the exact opposite of 
lean. For new progress insuring our code produces value, we need to change to the way developers operate without assuming 
instantaneous usage statistics (for many types of code like security or new B2B features the lag on uptake can 
routinely be years ).

But to change the way developers operate we need a lot more choices and a willingness to try them.

### The agile Goldilocks problem
The problem is that if we don't find ways to more frequently try solutions for our specific team's needs, we will not 
only be eating the wrong porridge, but sitting in the wrong chair and sleeping in the wrong bed as well.

Before Covid popularized remote work, I had only seen two major efforts to change the _way_ we work - Scrum/open office 
and CI/CD. Martin Fowler wrote about reluctance to try CI/CD [in 2006](https://martinfowler.com/articles/continuousIntegration.html):

>When I've described this practice to people, I commonly find two reactions: "it can't work (here)" and
"doing it won't make much difference". What people find out as they try it is that it's much easier than it sounds,
and that it makes a huge difference to development. Thus the third common reaction is "yes we do that - how could you
live without it?"

My previous employer started experimenting with remote work long before Covid. And there was push back 
quoting the Agile Manifesto's face-to-face principle! If Star Wars technology becomes available will we reference a 
20-year-old document to tell us whether to have hologram meetings or use hyperdrive?

{% include callout.html
content="It's **not okay** for a methodology to prescribe communication technology like face-to-face / open office or
Kanban boards."
type="warning" %}

Designers have Figma or InVision, and any number of business processes also incorporate tools
_specifically designed for them_. But software development employs tools like sticky notes based on 1970s factory work!!

<img src="{{ site.baseurl }}/assets/images/kanban.png" alt="Kanban" style="width: 90%;" />

It's this combination of a few one size fits all methodologies with technology developed in other times for other 
purposes that makes the agile Goldilocks problem so devastating.

### Meeting all the time is too hot
The thinking behind most methodologies is that lots of meetings insure you get things right. Plus every introduction of 
formal development meetings I witnessed was followed by open offices in case something comes up when you are not in a 
meeting.

And I get the logic - it's at least consistent. But now, more than ever, developers realize the issues with open office
(and are being offered 
[libraries](https://www.fastcompany.com/90626329/these-architects-popularized-the-open-office-now-they-say-the-open-office-is-dead)
instead?)
and it's time to also see the limitations of meetings as a software developer communication tool.

You can't afford to have meetings all the time and, in an agile environment, you also can't afford to have your
approvals, questions and feedback wait for the next meeting where it will be difficult to decide everything real
time anyway. 

{% include callout.html
content="Relying soley on meetings means choosing between losing the time and focus required to code and 
doing the wrong thing or the wrong way."
type="warning" %}

Plus time box pressure causes rubber-stamping new features and accruing technical debt and there is no one to blame 
since the meetings don't record opinions.

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

Creating your own process from scratch is not great either. For instance, I was on a team doing infrastructure work 
without a product owner. So the team had a spreadsheet where we voted on priorities. A few of us assigned ourselves
the top item but unfortunately the spreadsheet didn't record the certainty or reasons behind the votes. 

It turned out this project's popularity was a result of recent incidents in production. Under protest, we completed the 
project but the incidents stopped happening and our code was never deployed.

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
The good news is that our industry over-estimates the cost of experimentation. Some easy process experiments:
* Try different communications tools for a hack-a-thon
* Run a parallel process for technical debt instead of a retro
* A separate track for technical debt and fund it (by percentage of time for instance)
* "Just right" size your backlog and the amount each item is specified (renaming your 
[backlog to bets](https://basecamp.com/shapeup/2.1-chapter-07) and scheduling more 1-1s is not what I mean; we think 
software should remind the team until important items are handled online or removed instead of advocating regular 
closed door meetings)
* Have ongoing feedback instead of end of sprint demo meetings
* Drop scheduled 1-1 meetings in favor of an office hours approach (the bigger change is to eventually drop all 
mandated meetings; forced communication will always be eventually abused - trust developers to know what's useful and
try to accommodate different styles of work)
* Encourage development teams to choose their own process and tools (à la 
[Spotify](https://www.youtube.com/watch?v=4GK1NDTWbkY&list=RD4GK1NDTWbkY) except maybe the part about separating
squads by feature versus infrastructure)
* Create an initiative process where anyone can suggest or vote on other initiatives
* Make PM recommended feature work also go through that initiative process instead of automatically staffing
* No meeting Wednesdays - a bit like no headache Wednesdays so if it works it needs to be followed up by stronger 
measures
* Cameras off on Zoom meetings - see [this article](https://www.sciencedaily.com/releases/2021/08/210830092203.htm)
* Redefine the role of Scrum Master to Process Master:
>The Scrum Master is accountable for establishing Scrum as defined in the Scrum Guide.

The Process Master is accountable for suggesting and helping with the latest process and tools for the team to try.

Some changes are not real experiments - re-orgs or musical chairs with roles, a council responsible for all 
approvals of X, a bot that asks standup or retro questions, dropping meeting X but not offering any substitute way
of communicating, etc. The biggest fake experiment is around "shielding" where a sustaining team might be created
to reduce contact with developers or other 
[external contact removed](https://andreigridnev.medium.com/simple-tactics-to-reduce-distractions-for-a-software-engineering-team-e4e56d7d0ad5):

>Once we tried a “silent day”, when only I, as the lead, was available in case someone outside our team had an urgent question. The team productivity on that day peaked — developers did so much work. I would be happy to do days like that at least once a sprint but most of team members preferred to keep comm channels open.

Reducing external contact just makes it that much harder for developers to have and share opinions. The above 
link also discusses attempts at clumping meetings to give more uninterrupted time but 
as [Paul Graham](http://www.paulgraham.com/makersschedule.html) describes a day with even a single meeting is not the 
same and also doesn't take into account the help that developers have to give each other all the time.

Another example of not real experimenting are some implementations of Scrumban. [For instance](https://engineering.iterable.com/so-long-scrum-hello-scrumban)
you might drop story points, acceptance criteria and "failing the Sprint" without noticing the 
[2021 Scrum guide](https://scrumguides.org/scrum-guide.html) doesn't have any of them. If giving developers the time and
means to work on code that will more likely be useful isn't the point of your experiment, then it's easy to get
lost in a maze of tweaks. If you are stuck coding the wrong thing or the wrong way then the small details of your
process won't matter.

### Spend more time working on the right thing
Let's review the logic:
1. We think working on the right thing is the biggest challenge developers face.
2. It's unlikely that further customer feedback, PMs or off the shelf methodology or tools will solve this problem.
3. Experimentation with process and tools is required for each team to find the way and the time to help working on
the right thing - the agile Goldilocks problem.

You can spend a long time experimenting, as 
[PagerDuty](https://www.pagerduty.com/blog/scaling-engineering-org) describes. For experimenting with communications 
solutions there are many choices and most of them fully justify the manifesto's warning to stick to face-to-face. 

But these days we know a few things about how we prefer to operate online:
* Questions - almost every developer is happy when a question can be answered by online interactions and a meeting 
avoided
* Status - we are all used to checking status of nearly everything online these days 
* Feedback - again we all give and receive feedback online constantly
* Suggestions - specialized software can do better than email, but email is still easily superior to a meeting where 
everyone hears the suggestion for the first time.
* Approval - like or dislike is the bread and butter of the online world
* _Brainstorming - I would argue that only here does face-to-face really shine_

So in our opinion:

{% include callout.html
content="Giving developers more time to input on working on the right thing the right way requires converting as many
internal meetings to online, asynchronous as possible."
type="warning" %}

Whatever path your team pursues the overdue death of one size fits all process is already started. It's 2021, 
and long since time to stop going to an office still in 2001.


