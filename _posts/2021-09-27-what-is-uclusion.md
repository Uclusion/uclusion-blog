---
layout: post
title:  "What Is Uclusion"
author: david
categories: [ agile, startup ]
image: assets/images/Uclusion_Logo_FullColor_Lg.svg
featured: true
---
There are many blogs these days explaining why a distributed team or remote work requires you have fewer meetings.
Uclusion was built with a different point of view. Years of working remotely taught us that there was a better way to
work whether you are in the office or not. We believe meetings are fundamentally flawed for most development
team communication, and we created Uclusion to provide an alternative.

## An Asynchronous Flow
The alternative daily flow that Uclusion allows is like this:
1. Get stories approved before you start them and help approve other's stories.
2. Pause stories that are blocked or require input and help others with their paused.
3. Get feedback on stories and give feedback on other's stories.
4. Maintain a status display that shows exactly where you are on all your stories.
5. Propose project level suggestions and decisions and respond to other's proposals.

All of these activities are what needs to happen **daily** in order to keep an agile project on track and 
[avoid writing unused code]({{site.baseurl}}/agile/2021/09/13/goldilocks-methodology.html). Even the 
[Scrum guide](https://scrumguides.org/scrum-guide.html) is clear on this point:
>The Daily Scrum is not the only time Developers are allowed to adjust their plan. They often meet throughout the day for more detailed discussions about adapting or re-planning the rest of the Sprint’s work.

The face-to-face / open office solution to this problem imagines that developers can be available for all of these 
impromptu meetings and also continue to code at a high level.

## Why Most Meetings Don't Work for Developers
Meetings are a very good tool for brainstorming but for questions, status, feedback, suggestions, or approval they
have two fatal flaws:
* Point in time - think of the difference between a TV show that plays once a week and one that is on demand
* Too expensive - the expense is what usually drives time boxing them but that forces other problems

As a simple example of how these flaws are fatal let's take writing this blog. My process for writing it with Ben is:
1. Approval that the blog needed to be written - online / asynchronous
2. Every two days or so publish the blog to him and notify him that I need feedback and Ben reads the blog and 
comments - online / asynchronous
3. If I need help after his feedback then we brainstorm - short meeting / real time

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

But simply moving a meeting online doesn't guarantee success either. For instance, I was on a team had a spreadsheet
where we voted on priorities. A few of us assigned ourselves the top item but unfortunately the spreadsheet didn't
record the certainty or reasons behind the votes or give us a way to change the plan later. It turned out this 
project's popularity was a result of recent incidents in production and those incidents stopped and our code was never 
deployed.

## Reducing the Cost of Collaboration
Any simple implementation of a meeting in an app will solve meeting's first problem - that they are point in time. It's
the second problem, too expensive, that requires more complex software.

For Uclusion to implement agile project management without all the meetings, we have to take all the drudge work
out of developer communication. In order to do this we have some design principles:
1. Uclusion knows as much as possible about what is happening in data input into it. For instance, unlike a generic
Kanban board, you cannot create workflow stages that are just a label like Todo or Done. If the software doesn't 
understand as much of the context as possible then drudge work cannot be automated and communication costs remain high.
2. Notifications must be sophisticated. Since Uclusion understand most of the actions a user can take, it can be smart
about who is notified, with what severity and when to automatically remove the notification.
3. Nothing should require immediate action. Uclusion has pipelined waiting stages like 'Requires Input' and 'Blocked'
and a continuous approval process. That way the development team is not forced to choose between to respond to 
everything immediately and risking making teammates idle.
4. Status should come as a result of just using Uclusion instead of being its own separate activity.

To see the results of these principles video is better:
<iframe width="514px" height="289px" src="https://www.youtube.com/embed/tzuJ0xuJTQI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>