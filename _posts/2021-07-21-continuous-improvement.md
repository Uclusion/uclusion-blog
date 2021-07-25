---
layout: post
title:  "Continuous Improvement"
author: ben
image: assets/images/bad-architecture.jpg
categories: [ agile ]
featured: true
---
Even [successful organizations](https://www.pagerduty.com/blog/scaling-engineering-org) struggle to organize software 
engineering - causing ordinary developers stress and career damage. 

However, if you are a software developer on a team that holds traditional retrospectives or any other form of 
self-organizing, you have a mandate to continuously improve. So why are you still painfully sitting through 
retrospectives that probably go nowhere!

Here's why they go nowhere:
1. Anything prioritized with feature stories will lose. Like Google's famous 
   [20% project](https://en.wikipedia.org/wiki/20%25_Project), you need this work on its own track.
2. No off the shelf, overhead meeting filled process is going to cut it for continuous improvement. How easy it would 
   be if that worked!
   
Unfortunately, the results of failing at self-organizing are pretty dire.

## Feature Factories and Gold-Plated Infrastructure
John Cutlefish's description of a [feature factory](https://cutle.fish/blog/12-signs-youre-working-in-a-feature-factory) 
is very accurate. The tools for data driven decisions that his employer sells are cool but won't get you to continuous 
improvement by themselves. You need more than data to make technical debt decisions and innovation by throwing 
everything at the wall takes too long - though it's better than not seeing what sticks.

Wrestling control away from PMs and giving the keys to the kingdom to engineering likely gets the flip side of 
feature factories, gold-plated infrastructure. Here the engineering team builds wonderfully ingenious architectures 
that don't really serve much purpose. We've all seen them - libraries built ignoring open source, fail over strategies
to solve end of the world events, or seven layers of caching to solve a non-existent performance problem.

What feature factories and gold-plating have in common is that they are based on the ideas of the few approved without 
much feedback.

## Self-Organizing for Technical Debt and Innovation
Not _all_ decisions can be made top-down; it simply doesn't scale. That's why VCs loosely couple with startups, 
large organizations like the 
[US Army](https://www.amazon.com/Team-Teams-Rules-Engagement-Complex/dp/1591847486/ref=sr_1_1?dchild=1&gclid=CjwKCAjwruSHBhAtEiwA_qCpprh9En4ltV31tCE_uoO2WjsJud2Jj977DyzugST2iG2aPOd5svWejhoC7FYQAvD_BwE&hvadid=241895014260&hvdev=c&hvlocphy=9032183&hvnetw=g&hvqmt=e&hvrand=7887596021403679128&hvtargid=kwd-79779609946&hydadcr=22532_10344436&keywords=team+of+teams&qid=1626958316&sr=8-1)
and [Amazon engineering](https://medium.com/swlh/working-at-amazon-software-engineer-4d491f2d0f7e) prize leadership,
and the reason [retrospectives exist]({{ site.baseurl }}/agile/2021/06/29/planning.html).

You absolutely can build a new product top down but **improving it requires more than feature factories**. In many 
organizations this means a single engineer, skunk works style, does the heavy lifting for technical debt, there's a
'tech debt month', or a team does innovation in a hackathon.

These extraordinary efforts will achieve only temporary improvement, a brief respite from the stress. For _continuous_ 
improvement, you need some effort all the time, sustainably.

### Mandatory Meetings are not Self-Organizing
We have a [blog on that]({{ site.baseurl }}/agile/2021/07/07/face-to-face.html) as well. The short answer though is
that self-organizing cannot be introduced top-down. It can be encouraged. You can make it a principle of your
organization. 

But mandating _how_ to self-organize is like telling people who to vote for to promote democracy! Few people feel
responsibility for the results of a process forced on them.

### What about the Boss?
If you are the boss then we recommend discussing with your team what process and tools might best serve them. If you are
not the boss then we recommend starting by replacing retrospectives with something that works. Here's how you negotiate
that:
* Scrum recommends a `three hours for a one-month Sprint` retrospective. That's basically a work day (who codes after
  a three hour meeting?) and let's conservatively throw in another day for whatever was supposed to come out of that 
  meeting.
* Ask to drop retrospectives but allow people 2 days a month (one day a two-week Sprint) for improvement as they see 
  fit.

## Pick the Tools and Process that Work
You're looking for a process and tools for initiative approval and organizing work among a group of peers. You may 
have meetings from time to time, but your project management tool should be designed to make sure you don't waste
those meetings on overhead. 

Good luck! We at Uclusion are rooting for you (and we've spent years bootstrapping a tool to help you into existence).


