---
layout: post
title:  "Escaping Code Factory"
author: david
image: assets/images/code-factory.jpg
categories: [ startup ]
---
Code factories grow from a belief that developers perform better when directed as much as possible.

They might not be sweatshops but the spoon-feeding severely limits your prospects. First, developers are not trusted 
enough to change architecture, so keeping current skills will be difficult even with a side gig. 

Second, code factories limit collaboration and leadership and make achieving any position of _real_ 
responsibility difficult. (Code factory management is just baby-sitting.)

## How do you know if you work in a code factory?
* **Coding in the dark** - limited access to customers, everything need to know etc.
* **Rubber stamping** - ideas from "above" are presented without alternatives.
* **Getting 'done'** - unexplained hard deadlines and no room for feedback loops.
* **Limited teamwork** - developers do not engage much with their peers.

If your work has any of these then read on. Otherwise check out 
[Preventing Code Factory]({{site.baseurl}}/agile/2021/08/28/2-code-factory.html).

Let's take a simple user story to demonstrate how code factories work. "As an email user, I want a way to keep
my inbox organized." That story could result in anything from GMail's built-in categories to Hey's categorize
first time senders feature. This example is chosen because we all use email but in a code factory you might not 
understand your end users at all.

A code factory will insist on writing in enough detail to nail down exactly one high level implementation and then 
maybe start in on acceptance criteria to specify down to the exact screens. And even then the story might be spit 
up into dozens of stories making it difficult for any single assignee to innovate anything. Feedback, if any, will come 
only from end users complaining and the team that fields those complaints might not even be the same one that did the 
first version!

Of course a complex software product will have some tasks better suited to this kind of assembly line. What makes a 
code factory a code factory is that it tries to apply this model to everything. Even modern factories, which
sometimes need to produce 100s of customized versions or very flexibly schedule different products, can't be so rigid!

## How to find a job outside a code factory
There are plenty of organizations that show signs of not being code factories:

<table>
  <thead>
    <tr>
      <th style="padding-right: 3rem">Company</th>
      <th>Bottom up example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Google</td>
      <td>20% time policy leads to many new products</td>
    </tr>
    <tr>
      <td>Amazon</td>
      <td>Bottom up New Product Introduction process resulted in AWS</td>
    </tr>
    <tr>
      <td>Apple</td>
      <td>iPhone started as a skunkworks project</td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td>Embraces open source</td>
    </tr>
    <tr>
      <td>Netflix</td>
      <td>Freedom and responsibility culture</td>
    </tr>
    <tr>
      <td>Spotify</td>
      <td>Emphasis on team autonomy</td>
    </tr>
    <tr>
      <td>Slack</td>
      <td>Chat started as an internal tool and Salesforce 
<a target="_blank" href="https://developer.salesforce.com/blogs/engineering/2014/08/agile-methodology-salesforce-inside-look">sounds agile</a></td>
    </tr>
    <tr>
      <td>Instagram</td>
      <td>Thirteen person company when acquired by Facebook</td>
    </tr>
  </tbody>
</table>

<br />
Not being a code factory doesn't guarantee it's a good place to work but it does help insure that you keep growing
as a developer and not get stuck in your career.

However, if you decide to leave, there is no simple set of signs like "agile process", remote work or managers that code 
that guarantees avoiding code factory. Investigate the team you are interviewing with and wait for a good fit:
* Do teams ever detour from "paved road" centralized architecture?
* Do PMs make suggestions or give commands?
* Are engineering teams siloed by function?
* Does the management come from companies with a reputation for flexibility?
* How aligned is their tech stack with the latest technology?
* Do your potential teammates believe developers perform better when given instruction to minimize thinking? 

On that last question, you can try asking them about ROI on unit testing. If the response is something like, 
"Testing pyramid - that's all you need to know." or "I just check the Definition of Done." then it's possible they 
either prefer code factory or have worked at one too long. 

"We don't have time for testing because of the deadlines" is also a tip off but if they are that honest you could maybe 
just directly ask if this is a code factory.

## What if you are a team lead or manager?
Code factories are stressful for their leaders since there is a general lack of energy and initiative.

**By far the most impact can be had by fixing process**, because bad process _causes_ developers to spend time on 
things with low return. That in turn makes old technical debt remain, which eats up available time, which forces even 
more shortcuts.

<img src="{{ site.baseurl }}/assets/images/autonomy-diagram.png" alt="Autonomy" style="width: 90%;" />

You don't have to fix all of your process at once. You can start with a meeting like a retro or an event like a
hack-a-thon whose time can be reclaimed with something more effective.

Some suggestions for the new process:
1. Truly continuous so that whenever there is time, work can be done asynchronously.
2. Team and stakeholder opinions on the ROI of bottom up proposed stories is visible.
3. The project management tool works _for you_. Instagram famously ran from tasks listed in a single elaborate
Google Doc, but you can do better.
4. The new process can run in parallel but could be extended to all work.

## Good luck
It's a big step so you can check out [Ben's blog]({{site.baseurl}}/startup/2021/09/01/1-on-autonomy.html) on why escaping
code factory is so important to your career. Additionally:

{% include callout.html
content="Senior increasingly means comfortable leading collaboration."
type="warning" %}

Here's an excerpt from a Netflix senior software engineer position:
>* Work closely with our customers & partners, understand their use cases & needs, think strategically to seek the 
right problem to solve at the right time, and innovate with rigor.
* Collaborate with the team to be responsible for the entire software lifecycle.
* Work on, collaborate with, and influence the open-source community, and have an impact in the industry.

Solving problems outside a code factory spoon-fed process gives you the skills you need to get to another level. Plus 
your employer could use the help!