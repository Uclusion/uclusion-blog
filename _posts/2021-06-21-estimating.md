---
layout: post
title:  "What is Agile Planning?"
author: david
categories: [ agile ]
image: assets/images/unblind.jpg
featured: true
---
Agile and plans are almost opposites. The trick is to make as few assumptions
about the future as possible.

Of course agile is not the right approach for every project. For 
converting a legacy system to newer technology, you might not
need agile since you know exactly what you are building and only
worry about unknowns in implementation. (Though even the implementation might force agility;
imagine after starting you realize Lambdas are a better approach.)

However, if you do decide to run a project agilely it's important to not 
unknowingly create detailed plans instead.

### Avoiding Large Backlogs

When making software delivery plans the first idea might be to write down
every bit of work you can think of in a story and flush each story out as much 
as possible. Then you have a backlog that you believe is a roadmap of what
needs to be done.

There is value in making a very simple list of items that may need to get done.
The problem comes with how much time you invest into detailing each of those
items. Creating a detailed plan is the opposite of agile even if you think you
will revise it later.

Maintaining that detailed plan will slow you down and the more time spent, the
less likely you will be willing to change the plan later.

### Avoiding "Easy" Estimates

Agile assumes that knowledge of the future is hard to come by. Unfortunately,
many supposedly agile methodologies use planning techniques that pretend
the future is fairly easy to guess.

<img src="{{ site.baseurl }}/assets/images/plumbing.jpg"
alt="Plumbing estimate" style="width: 70%;" />

To see why easy estimating is not useful just look at almost any other field
has to estimate work. For instance, building a new house has a somewhat known cost
per square foot but repairs are truly agile - you never know what you might find. 
So many plumbers charge even for coming out. But even the one's that 
don't aren't going to give you an estimate without going under the house first.

Estimating software is work. The easy, no sunken costs, no risk estimate is with high
probability just flat wrong.

The better an estimate you want the more you have to pay. Maybe that involves 
a PoC but for most story estimating it means starting on a story first and 
only estimating once you have enough information.

Now you might say, "But I don't want to start a story until I'm sure how
long it will take." Okay but realize that the time you spend on creating an accurate 
estimate is overhead. **That effort is better spent first making sure the story will 
produce value and then monitoring issues during implementation.**

#### Story points voted in a meeting
Free estimates don't build on each other. If I call 5 plumbers to 
get an estimate sight unseen, they might all agree, but it doesn't make
that estimate any more valid.

Nor does a meeting give you anywhere near enough time and concentration to 
do the work to generate more than the free estimate.

#### "Spike" stories
Frequently Scrum teams will use "spike" stories to get the information so that
the story can then be estimated in the next meeting.

<img src="{{ site.baseurl }}/assets/images/spike.png" alt="Spike" 
style="width: 40%;" />

Spike stories are a bad practice. They are funding a story without fully discussing 
its value. They also encourage spending a lot of time researching all possibilities
instead of agilely trying one.

Much better to actually start a story based on its value and see how it goes 
then to muddy the waters with a story that is in between started and not.

#### Project level estimates
Again you get what you pay for. If you need an accurate project level estimate
then first go waterfall and specify absolutely everything ahead of time.

If you can live with a back of the envelope estimate then use that but be clear
about the risk you are taking. There will be more information later and your
investment strategy in the project might have to change.

#### Status with revised project level estimates
**The really naive strategy is to create a backlog that represents the entire 
project, put estimates on the whole backlog and then sum those estimates.**
Then as stories complete try to use the information about how long those
stories took to revise the project level estimate.

That's certainly a very expensive way to estimate but also unlikely to get you 
a more accurate date. The problem is that guessing correctly on story size
a few times doesn't mean you will guess correctly every time. Or put another way, 
in software development, counting ten white swans doesn't make the probability less 
that the next swan is black.

In fact, it's even worse than that because software developers would tend
to start with the stories with which they are most comfortable. And even if 
you start with the hardest story first implementation might use a simple
approach that won't hold up later.

#### What about #NoEstimates?
Once the true cost of an accurate estimate is taken into account a team
may decide to use a very inexpensive estimation like number
of features completed / number of features remaining. So long as everyone is 
aware of the level of uncertainty then it doesn't violate the principal of 
agile.

Just don't get fooled into believing you've earned knowledge of the future by 
making simple guesses.