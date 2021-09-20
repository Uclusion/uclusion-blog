---
layout: post
title:  "The agile Goldilocks problem - the death of one size fits all forever"
author: david
image: assets/images/goldilocks.jpg
categories: [ agile ]
featured: true
---
My co-founder and I started Uclusion more than two years ago with two goals:

1. Developers should spend more time working on the right thing
2. This progress should not come at the expense of longer hours

We believe failing to deliver value is the greatest problem software developers face. Once you doubt your code
is useful, your job stops being fun no matter how pleasant it might be otherwise (plus useless code [endangers your
career]({{site.baseurl}}/agile/2021/09/01/1-on-autonomy.html)).

Our industry is suffused with unused code, half finished projects and features that negatively impact a project
by increasing complexity and maintenance.

Reducing wasted coding effort is a difficult problem that will never be fully solved but in this blog we 
argue that the lack of progress is because we don't try enough reasonable process and tools options to find solutions.

### We don't see value of our code increasing
There are any number of agile software methodologies promising to help. In fact using workers to help cut out wasted
effort and continuously improve is the [lean framework](https://en.wikipedia.org/wiki/Lean_thinking) from which they 
came.

I've been a software developer long enough to have seen the Scrum / open office experiment conducted in a variety of
settings. There were some gains made, but we argue there is not nearly enough progress to declare mission accomplished.

Scrum is fundamentally a system designed around a single product owner who has a very tight relationship with a single 
or small group of customers and development work that is not platform intensive.

So for one size fits all usage a typical SaaS product is out of luck right away - the product owner makes no sense
(even if a single person could represent 1000s of customers he still wouldn't help on the technical side), the end of
Sprint demo makes no sense (if we're just demo'ing internally why risk waiting for the end of Sprint?) and even
Definition of Done is weird on a product that may allow exceptions to get quick feedback (like
[at an early startup](https://builtin.com/software-engineering-perspectives/scrum-startup-alternative)).

However, even if your team is working in a contract shop with single customer requirements, Scrum is still exactly
specifying all the meetings in a way that may not work for you. What if your team members are spread across time
zones? - just don't do that or suck it up says Scrum. What if the customer wants to have an almost immediate feedback
loop? - no we prefer the requirements stay fixed for the iteration says Scrum.

There are now also a growing number of experiments in Scrumban that are frequently not bold enough. 
[For instance](https://engineering.iterable.com/so-long-scrum-hello-scrumban) you might drop story points, acceptance 
criteria and "failing the Sprint" without noticing the [2021 Scrum guide](https://scrumguides.org/scrum-guide.html) no 
longer has any of them. 

"Shielding" where a sustaining team might be created to reduce contact with developers or other
[external contact removed](https://andreigridnev.medium.com/simple-tactics-to-reduce-distractions-for-a-software-engineering-team-e4e56d7d0ad5)
is also played out.

>Once we tried a “silent day”, when only I, as the lead, was available in case someone outside our team had an urgent question. The team productivity on that day peaked — developers did so much work. I would be happy to do days like that at least once a sprint but most of team members preferred to keep comm channels open.

Reducing external contact just makes it that much harder for developers to have and share opinions, and going faster is 
not going to matter if there is no value in what you are coding. The above link also discusses attempts at clumping 
meetings to give more uninterrupted time but as [Paul Graham](http://www.paulgraham.com/makersschedule.html) describes 
a day with even a single scheduled meeting is not the same.

{% include callout.html
content="Current process and tools experiments are sanding the cube when we wanted a sphere."
type="warning" %}

Successful attempts at changing developer process like CI/CD are working because they are more options available, and
we move faster in discarding what doesn't work.

## The agile Goldilocks problem
The problem is that if we don't find ways to more frequently try solutions to help our specific team write code
that produces value, we will not only be eating the wrong porridge, but sitting in the wrong chair and sleeping in the 
wrong bed as well.

Designers have Figma or InVision, and any number of business processes also incorporate tools
_specifically designed for them_. But software development employs tools like sticky notes based on 1970s factory work!!

<img src="{{ site.baseurl }}/assets/images/kanban.png" alt="Kanban" style="width: 90%;" />

Finding a solution requires that we identify the parts of our process and tools that are not working and try to replace
them with options that might work.

### Meetings are too hot
The thinking behind most methodologies is that lots of meetings insure you get things right. Plus every introduction of
formal development meetings I witnessed was followed by open offices in case something comes up when you are not in a
meeting.

There is now an awareness that open office is not working or at least not working for everyone (and so
[libraries](https://www.fastcompany.com/90626329/these-architects-popularized-the-open-office-now-they-say-the-open-office-is-dead)
are being proposed instead?). What is less recognized is just how flawed meetings are as a developer communication tool.

Since we know we don't see value of our code increasing, we also know that our meetings are sometimes resulting in doing
the wrong thing or the wrong way. But we will argue that it's not a matter of having better or more meetings, the
design of meetings simply doesn't work for this purpose.

Meetings are a very good tool for brainstorming but for questions, status, feedback, suggestions, or approval they 
have two fatal flaws:
* Point in time - think of the difference between a TV show that plays once a week and one that is on demand
* Too expensive - the expense is what usually drives time boxing them but that forces other problems

As a simple example of how these flaws are fatal let's take writing this blog. My process for writing it with Ben is:
1. Approval that the blog needed to be written - online / asynchronous
2. Every two days or so publish the blog to him and notify him that I need feedback - online / asynchronous
3. Ben reads the blog and comments - online / asynchronous
4. If I need help after his feedback then we brainstorm - short meeting / real time

Now suppose I had to use meetings for the same process.
1. Approval meeting - There will need to be an agenda for the meeting so my blog might not even be included. If included
and approved I will need to estimate how long the blog will take so that we know when to schedule the next meeting. The
whole meeting is time boxed so between approvals and estimates we are out of time and end up rubber-stamping a lot.
Plus meetings tend be led by the loudest voices and recording who had what opinion is difficult in a meeting so those 
loudest voices are not even accountable. 
2. Feedback - this is all on me to organize since no one in a daily meeting would have read the blog, and I can't
afford to wait till the next demo meeting.
3. Brainstorming - not even a thing in a meeting driven process because the approval meeting would have tied me
down to my very first ideas about this blog (and you don't want to read that one).

Meetings are a technology choice, but they have so far escaped being evaluated as we would for other tools.

{% include callout.html
content="It's **not okay** for a methodology to prescribe communication technology like face-to-face / open office or
Kanban boards."
type="warning" %}

My previous employer started experimenting with remote work long before Covid and there was push back
quoting the Agile Manifesto's face-to-face principle! If Star Wars technology becomes available will we reference a
20-year-old document to tell us whether to have hologram meetings or use hyperdrive?

But just moving a meeting online doesn't guarantee success either. For instance, I was on a team had a spreadsheet 
where we voted on priorities. A few of us assigned ourselves the top item but unfortunately the spreadsheet didn't 
record the certainty or reasons behind the votes. It turned out this project's popularity was a result of recent 
incidents in production and those incidents stopped and our code was never deployed.

You really have to be willing to experiment with process and tools till you find something that works.

### Working by yourself is too cold
There is a class of problems that can be solved with limited interaction with others. Let's call
them *yesterday's problems*. Yesterday's problems have fairly obvious solutions and if you need extra hands for the
grunt work you can employ a [code factory]({{site.baseurl}}/agile/2021/08/16/code-factory.html) process.

For a large supply of yesterday's problems just pile up technical debt and let your competition do all the innovation.

However, even if you are the product manager or chief architect, today's problems are too complex to take on without a
lot of guiding opinions. I've more than once seen product architecture updates fail because one person, by himself,
chose an architecture or requirements that didn't make sense. And giving a PM unrestrained control of engineering is
just as likely to break down.

Even if you make a winning decision by yourself you may not be rewarded for it. My co-founder found that out after
a very successful skunkworks change to storage architecture. If management rewarded him it would be sending a message
for everyone to do projects fait accompli.

### How to evaluate your experiments
Sources of information to judge the value delivered by code:
* Your team - let's at least make sure we think this is good but without mandating meetings to collect that information
* Potential customers - difficult to read the market and can lead to just delayed following of competitors
* Existing customers - very tricky so let's dive into this one

The ideal use of existing customers is a hypothetical developer at Facebook who submits code that is
automatically A/B tested across the world and immediately rewarded with bonuses if it helps (example from iiSM.org).

There are a number of factors that make this ideal break down in most real world application. Consider two recent
changes released by Intellij. The first allows coding together and the second presents your Git diff as if it were
another file in the editor. The Code with Me might, like many B2B features, require years for user uptake. The inline
Git diff will have 100% uptake immediately but won't reveal anything about value delivered.

For code that prevents negative affects like downtime, security breaches or poor architecture / technical debt using an 
existing customers metric is even more difficult. You would only be able to react to very bad events.

Then there's the MVP idea - we don't have to worry too much about value delivered by code if we can get feedback
from a very cheap investment. Let's go back to the Code with Me feature to discuss this. 

You could go out on a forum and poll developers if they would use this feature but even after trying the full feature 
I'm still not sure if I will use it much less you ask me about something that doesn't exist yet. However, releasing a 
crappy "MVP" Code with Me definitely won't get you any information - the ante is higher than that.

This is why agile companies like [Spotify](https://www.youtube.com/watch?v=4GK1NDTWbkY&list=RD4GK1NDTWbkY)
or [PagerDuty](https://www.pagerduty.com/blog/scaling-engineering-org) go to such lengths to get teams more involved.

{% include callout.html
content="Of the sources of information available for determining code value, development team input is by far 
the easiest and most underused."
type="warning" %}

### How **NOT** to evaluate your experiments
What we can say for certain is that activity based metrics are a fail for measuring value. These include:
* Physical or virtual face time
* Points velocity - even the Scrum guide has dropped this
* Finishing within a release date / speed to close a bug
* Spyware laptop activity reports - even I'm not sure when I'm being productive, so I'm very skeptical this will tell us
* Participation in meetings (turn the camera off - see [this article](https://www.sciencedaily.com/releases/2021/08/210830092203.htm))
* Raw volume of lines of code - unless it's close to zero

Continuing to use activity based metrics falls somewhere between incompetence and flat out fraud unless you've 
collapsed to a code factory.

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
* Create an initiative process where anyone can suggest or vote on other initiatives
* Make PM recommended feature work also go through that initiative process instead of automatically staffing
* No meeting Wednesdays - a bit like no headache Wednesdays so if it works it needs to be followed up by stronger 
measures
* Redefine the role of Scrum Master to Process Master:
>The Scrum Master is accountable for establishing Scrum as defined in the Scrum Guide.

The Process Master is accountable for suggesting and helping with the latest process and tools for the team to try.

Some changes are not real experiments - re-orgs or musical chairs with roles, a council responsible for all 
approvals of X, a bot that asks standup or retro questions, dropping a meeting but not offering any substitute way
of communicating, etc.

### Spend more time working on the right thing
Let's review the logic:
1. We think working on the right thing is the biggest challenge developers face.
2. It's unlikely that further customer feedback, PMs or off the shelf methodology or tools will solve this problem.
3. Experimentation with process and tools is required for each team to find the way and the time to help working on
the right thing - the agile Goldilocks problem.

Whatever path your team pursues the overdue death of one size fits all process is already started. It's 2021, 
and long since time to stop going to an office still in 2001.


