---
layout: post
title:  "Preventing Code Factory"
author: david
image: assets/images/code-factory.jpg
categories: [ agile ]
---
It was 2003 and I was working with a consulting firm doing software for Stanford IT. It was pure 
[code factory]({{site.baseurl}}/agile/2021/08/16/code-factory.html) (first blog in this series). Minimal contact with 
the customer, specs were given to me for each page of the application and while there was a team of us working together, 
none of us interacted much.

The key part of this environment is that when we finished one project we moved onto another. The previous project
was **done** and might not be touched again for decades. There was some common infrastructure and skills between 
projects that could be extended but no open source to keep those tools alive.

Now 18 years ago working for an IT department, any modern process would have been a big step up. We would have had a 
more cohesive team, knowledge of the projects, and more interaction with the customer to reduce the product owner 
bottleneck.

## SaaS is not an IT department
Militaries say, "Generals always fight the last war", and in economics it's "Economists fight the last depression". 
In software, we are all primed to win the limited engagement, single customer interactions of decades ago just as 
SaaS is making them obsolete.

It's easy to lose sight of just how different SaaS is from previous software development and for many years I believed 
simple, factory based process could be extended _without modification_ to unlimited engagement of masses of customers.

At Stanford one guy was struggling to interface with even one customer, but now the product owner is expected to 
generate all ideas, forever, for the team to satisfy an ever-increasing base of customers.

Even if product owners accomplish this feat the infrastructure that we hobbled together for a simple application is 
now also its own ever-growing product. The code base, far from being 'done', endlessly requires maintenance. 
Interfacing with customers doesn't qualify the product owner for any of these new technical requirements.

Finally, where the IT department projects started with a near clean slate, SaaS engineers build up domain knowledge 
over years. Yet software methodologies intended for shorter projects have no way of using any of these vital skills.

## Slouching towards code factory
{% include callout.html
content="Applying simple process to more complex software starts a clock ticking that ends in code factory."
type="warning" %}

At a software level all SaaS engineers are aware of the problem - multi-tenant software is vastly more complex than
single-tenant. At the business level if a single client pays you to develop software by the hour then their 
indecisiveness is actually a good thing. **In SaaS your work isn't guaranteed to generate revenue.**

SaaS product management is usually beholden to quarterly earnings, and engineering is crippled by only having a mandate
for "technical" leadership. You can end up bouncing between CTO led long term technical initiatives and PM driven short
term features without any customer satisfying strategy. 

Without a bottom-up mechanism for ideas, you risk a very small number of decision-makers becoming overwhelmed and 
pushing ideas that don't generate revenue. That's when an organization with developer autonomy may flip to full code 
factory.

## Responsible engineering
Even once I realized that top-down process was ill-suited to SaaS, I still thought the problem was with upper 
management. If only they made better decisions! Meanwhile, upper management was thinking if only we had better 
engineers!

Even the simplest of SaaS applications is a massive under taking. Cloud resources like AWS have removed some
infrastructure work, but the overall demands for a SaaS application have only increased as the bar for UX and features
has risen. It's naive to think that any simple organizational structure will suffice for such a difficult and 
competitive endeavour.

**Preventing code factory requires teams have the agency to make sure their code produces value for customers.** If that
isn't somehow part of the culture than any existing developer autonomy can disappear. 

But where does that responsibility end? And what about work-life balance? We look at these issues in our third blog 
in this series [Beyond Code Factory]().