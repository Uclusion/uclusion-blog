---
layout: post
title:  "Agile Technology"
author: david
categories: [ agile ]
---
Since many in the agile community are very good at organizing people there is a tendency to approach problems
exclusively from a social interaction perspective. Let's define better rules and meetings and guide developers to follow
them. Ironically the skill that many agile practitioners have in this area already creates an 80-20 situation where
further gains are difficult.

Two technological areas that might still be in a 20-80 rule for an organization are software architecture and choice of 
agile collaboration tools.

## Agile requires the right software architecture

An architecture where each pair of developers has their own service to work on is very different from a monolith. The 
more self-contained a team is the faster they will be able to proceed, for instance protected by well defined APIs. 
Unfortunately some [agile thinking](https://www.scaledagileframework.com/blog/new-advanced-topic-article-organizing-teams-and-arts-team-topologies-at-scale) 
is more concerned with business level constructs than whether or not the software is untangled at a technology level.

If for instance you have a platform team and features teams how much less agile are you right away, by design? Had 
Amazon organized that way then there would not be any AWS - instead of services it would be a platform baked into the 
core of their applications. Ignoring the technology perspective can lead to solutions where autonomous agile 
development will be very difficult.

## Agile requires the right collaboration tools

Collaboration tools can also help sub-divide a problem. The easiest example of this is a tool like source control. Even 
if we are working in the same code base the ability to branch and merge can help separate development enough to make 
agility possible.

Used correctly an issue tracker is also an important tool for agile development. If I can be assigned some small issue
that is independent of others than I can proceed with agility. Where there is still a lot of room for improvement is 
with larger projects that cannot be immediately subdivided into distinct issues.

The first take at solving that problem is to jam the square peg into the circle. Let's guess ahead of time all stories 
involved in a project and then enter them into an issue tracker. No matter how well those meetings are executed, complex 
project agile and issues trackers just don't fit.

In order to proceed agilely you need a collaboration tool where support for decisions about what to do next and how are 
built right into the tool. Before source control technology, developers could use meetings to avoid stomping on others 
code but it's a poor substitute.
