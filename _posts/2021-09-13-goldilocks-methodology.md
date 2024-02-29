---
layout: post
title:  "What's your next agile experiment?"
author: david
image: assets/images/goldilocks.jpg
categories: [ startup ]
---
Agile requires you to do three things:
1. You commit to eliminating wasted work
2. You run experiments to find new ways of working
3. You let development teams judge the outcome of those experiments

If you miss any of the three, you will not get the benefits of agile, and should consider more of a
[code factory]({{site.baseurl}}/startup/2021/08/16/code-factory.html) process with less overhead and
confusion.

## Why you need to commit to eliminating waste
Agile methodologies are based on [lean thinking](https://en.wikipedia.org/wiki/Lean_thinking) which uses worker input
to reduce wasteful practices. In software the main waste we are trying to cut down on is development of code that won't 
be used.
 
In my and my co-founder's experience the confusion for many agile teams is thinking that they can "adopt" an 
agile framework, then freeze their process, and yet still be agile. They might even continue to hold retrospective 
meetings in the spirit of continuous improvement but without ever making any real changes.
Unfortunately, this rarely works.

### The real costs of wasted effort
Part of the problem comes from not understanding the real costs of wasted development. Let's say you are working on a SaaS 
product and your team produces 5% more unused code than your competitor. Conservatively, that means each developer
spends 2 hours a week more than your competitor writing code that will never be used. 

Over time that's going to give your competitor an enormous advantage well beyond their developers coding 5% faster. 
Once code is introduced it's very difficult to remove from the system even if it is relatively unused. Until you find 
a way to remove it, you have to continue to pay for the support, maintenance and testing of code that might only be 
used by a single, small customer. 

Then there is the toll taken on developer morale or [quitting]({{site.baseurl}}/startup/2021/09/01/1-on-autonomy.html). 
You are 5% behind your competitor, but you might be 10 or 20% behind a best in class employer. This means a developer could 
have 10 to 20% more pay or free time working somewhere else, and be learning a better way of working as well.

This is why Toyota's lean thinking became popular in the first place; extreme focus on eliminating waste gave them such an 
enormous advantage. It's also why agile companies like [Netflix](https://www.youtube.com/watch?v=pl4UYZfVmTA),
[Amazon](https://www.amazon.jobs/en/principles), [Google](https://en.wikipedia.org/wiki/20%25_Project),
[Salesforce](https://developer.salesforce.com/blogs/engineering/2014/08/agile-methodology-salesforce-inside-look),
[Spotify](https://www.youtube.com/watch?v=4GK1NDTWbkY&list=RD4GK1NDTWbkY),
and [PagerDuty](https://www.pagerduty.com/blog/scaling-engineering-org) go to such lengths to have competitive process.

## Why you need to run experiments to find new ways of working
Your organization might already be involved with practices like CI/CD, an agile methodology like Scrum, open offices,
remote work, and open source. Why do we need more change than that?

Because our industry's current experiments are *old*:

CI/CD became obvious in [2006](https://martinfowler.com/articles/continuousIntegration.html), most agile
methodologies were starting to become popular in [2001](https://agilemanifesto.org), even the original architects of 
open office agree it's dead (and now propose 
[libraries](https://www.fastcompany.com/90626329/these-architects-popularized-the-open-office-now-they-say-the-open-office-is-dead)?), 
developer remote work was old enough to have a book written about it eight years ago, and open source was 
already important last century.

We even have people commonly extolling the virtues of Kanban boards based on 1970s factory work!


<img src="{{ site.baseurl }}/assets/images/kanban.png" alt="Kanban" style="width: 90%;" />

Even with more recent innovations like remote work there is an open office experiment feel to the way Zoom calls 
and relentless group chat are sometimes being used.

Full disclosure, we here at Uclusion [built a tool]({{site.baseurl}}/startup/2021/09/27/what-is-uclusion.html)
to make meeting driven process obsolete, but even we are not selling
it as a cure all.
{% include callout.html
content="One size fits all forever process is a casualty of the pandemic."
type="warning" %}
Every agile team needs to think more about the process and tools that will **specifically work for them**.

### Don't repeat the past
When choosing an experiment it's important to not just repeat the past.
[For instance](https://engineering.iterable.com/so-long-scrum-hello-scrumban) an experiment in Scrumban might drop 
story points, acceptance criteria and "failing the Sprint" without noticing the 
[2021 Scrum guide](https://scrumguides.org/scrum-guide.html) no longer has any of them.

"Shielding" where a sustaining team might be created or other
[external contact removed](https://andreigridnev.medium.com/simple-tactics-to-reduce-distractions-for-a-software-engineering-team-e4e56d7d0ad5)
is also played out.

>Once we tried a “silent day”, when only I, as the lead, was available in case someone outside our team had an urgent question. The team productivity on that day peaked — developers did so much work. I would be happy to do days like that at least once a sprint but most of team members preferred to keep comm channels open.

Similarly, reducing external contact just makes it that much harder for developers to have and share opinions, and going faster is
not going to matter if there is no value in what you are coding. And reducing developer contact with customers can 
[burn out product managers](https://www.reddit.com/r/ProductManagement/comments/puvgha/product_manager_burnout/).

The above link also discusses attempts at clumping
meetings to give more uninterrupted time but as [Paul Graham](http://www.paulgraham.com/makersschedule.html) describes
a day with even a single scheduled meeting is not the same.

Another experiment to avoid is encouraging senior developers to mostly work alone. The current state of developer
communications tools makes dropping collaboration seem reasonable, but long term anyone, even a CTO or product manager, 
who makes decisions by themselves will generate a lot of unused code.

## Why you need to let development teams judge the outcome of those experiments
>You cannot hold people responsible for results if you supervise their methods. You then become responsible for 
results and rules replace human judgment, creativity, and responsibility. -_Stephen Covey_

### What won't work
We can say for certain that activity based metrics are a fail for measuring a new way of working. These include:
* Physical or virtual face time
* Points velocity - even the Scrum guide has dropped this
* Finishing within a release date / speed to close a bug - setting aside #NoEstimates, you can't measure the 
value of a project by how quickly it was delivered
* Spyware laptop activity reports - even I'm not sure when I'm being productive, so I'm very skeptical this will tell us
* Participation in meetings (turn the camera off - see [this article](https://www.sciencedaily.com/releases/2021/08/210830092203.htm))
* Raw volume of lines of code - unless it's close to zero
* _Simple status_

Simple status is a completely circular way to evaluate a project where steady incremental progress means the project 
is going well. It gives green light status to both the ditch digging and ditch filling projects based on the 
ever-increasing and equal number of ditches they both report processing. I've seen exactly that relationship before 
between feature teams producing features with very few users and maintenance teams called in to fix the bugs those 
features caused. _Do not do this._


### What might work
The platonic ideal for developer value creation is a developer who submits code that is
automatically A/B tested across the world and immediately rewarded with bonuses if it helps, and the code is
deleted if it doesn't.

For most development teams the sources of information to judge a new way to work are more limited:
* Your team - let's at least make sure we think this is good
* New sales - hard to use since it's an extremely lagging indicator
* Existing customers - very tricky, see below

Consider two recent changes released by Intellij. The first allows coding together (Code with Me) and the second presents your Git 
diff as if it were another file in the editor (Git Diff). Code with Me might, like many B2B features, require years for user 
uptake. The Git Diff, like many UI changes, will have 100% uptake immediately but won't reveal anything about 
value delivered until reviews come in.

For code that prevents negative affects like downtime, security breaches or poor architecture / technical debt, using an 
existing customers metric is even more difficult. You would only be able to react to very bad events.

This means using customer usage statistics will frequently be impractical. 
That leads to  the MVP idea - 
we don't have to worry too much about value delivered by code if we can get feedback from a very cheap investment or
just asking on a forum.

Unfortunately, even after trying Code with Me, I still don't know if I will use it, and I can give you no useful
information if you ask me about something that doesn't even exist yet. However, I can tell you that releasing a half-baked "MVP" 
definitely won't get you any information - the ante is higher than that.

### What about direct feedback from end users?
Even if you are working for a single client, using that client's feedback to evaluate the amount of wasted code
might still not be viable. Many times the client is actually a stakeholder from the people who are paying and
not actually a real end user. First contact with real end users may require a lot of rework.

Let's be honest about what user feedback really means. Above I mention Netflix, Amazon, Google, Salesforce,
Spotify and PagerDuty as examples of agile development, but I've never been invited to give pre-release feedback even
after years of using all of their products. 

Of course, they can sometimes use A/B testing to get end user opinion between a few variations, but they cannot afford 
to release all the way to production on every design choice. 

<img src="{{ site.baseurl }}/assets/images/helpImprove.png" alt="Help improve" />

They can also poll me for information but as an existing 
customer my views may not reflect potential new customer opinion. For instance Intellij's existing customers might
hate Code with Me but implementing the feature is all about getting new users.

Hence, most agile decision-making is still coming from internal opinion as new features and products are shaped long before 
the code goes live. Since there is not a lot of data available, let's take Uclusion's own development as an example. 

I'd estimate we ran at around 40% unused code prior to using our own product. Maybe 15% of that was a result of end 
customer feedback. The other 25% came from us discarding what we internally think isn't useful or finding a better way 
to implement something.

### Trusting development teams
As you can see above, for most teams, the most relevant source of information for evaluating process and communication 
tools experiments is internal opinion. But you can still be data driven by using the opinions of as many employees as 
possible.

This is the real principle of self-organizing that almost all agile methodologies espouse: _Trust your people_.

{% include callout.html
content="So to recap, what's your next agile experiment? If you don't know you're taking a huge risk generating a lot of
code that no one will ever use."
type="warning" %}
