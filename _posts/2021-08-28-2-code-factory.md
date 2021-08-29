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

Now 18 years ago working for an IT department, Scrum would have been a big step up. We would have had a more cohesive
team, knowledge of the projects, and more interaction with the customer to reduce the product owner bottleneck.

## SaaS is not an IT department
Militaries have a saying, "Generals always fight the last war", and in economics it's 
"Economists fight the last depression". In software development process we are all primed to win the limited 
engagement, single customer interactions of decades ago just as SaaS is making them obsolete.

Why would engineers believe the same system that works for limited engagement, single customer could be extended 
_without modification_ to unlimited engagement, masses of customers? Unfortunately, I was, for many years, one of the 
engineers swallowing this canard.

In retrospect even the nomenclature should have given it away; you can't endlessly sprint! Product owner is similarly
incomprehensible in the face of unlimited engagement. At Stanford one guy was struggling to interface with even one 
customer, but now the product owner is expected to generate all ideas, forever, for the team to satisfy an 
ever-increasing base of customers.

But suppose even the product owners were capable of this impossible feat. Never ending means the infrastructure that
we hobbled together for an IT department application is now also its own ever-growing product. The code base, far
from being 'done', endlessly requires maintenance. Interfacing with customers doesn't qualify the product owner
for any of these new technical requirements.

The final difference with an IT department is equally damning. Where the IT department projects started with a
near clean slate SaaS engineers build up domain knowledge over years. Yet pure Scrum process has no way of 
using any of these vital skills.

## Slouching towards code factory
{% include callout.html
content="Applying IT department process to non-IT software starts a clock ticking that ends in code factory."
type="warning" %}

Traditional IT department process, like Scrum, has no need for long term ownership of the product. Most single customer 
applications were done in a year or two. So there wasn't much need to worry about product direction.

SaaS product management is usually beholden to quarterly earnings, and engineering is crippled by only having a mandate
for "technical" leadership. You can end up bouncing between CTO led long term technical initiatives and PM driven short
term features without any customer satisfying strategy.

When eventually the tug of war between CTO and product management is won, you collapse from a negotiation between two 
people to a one person pure code factory. If your process has no bottom-up mechanism for ideas, you continually risk 
the very small number of decision-makers being overwhelmed.

## Responsible engineering
Even once I realized that Scrum was ill-suited to SaaS, I still thought the problem was with upper management. If
only they made better decisions! Meanwhile, upper management was thinking if only we had better engineers!
Again in retrospect putting all responsibility on management is just as naive as thinking Scrum would work for SaaS.

Even the simplest of SaaS applications is a massive under taking. Cloud resources like AWS have removed some
infrastructure work, but the overall demands for a SaaS application have only increased as the bar for UX and features
has risen.

**Preventing code factory means SaaS engineers are responsible for more than just transcribing spoon-fed requirements 
into code.** It means the team stops hiding behind Scrum and upper management when its code fails to produce value for 
customers.

But where does that responsibility end? And what about work-life balance? We look at these issues in our third blog 
in this series [Beyond Code Factory]().