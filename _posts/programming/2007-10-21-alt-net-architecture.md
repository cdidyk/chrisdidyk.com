---
title: ALT.NET Conference - Architecture Session
layout: post
teaser: I don't know much about software architecture. But I'm smart enough to shut up and listen when people like Martin Fowler talk about it.
---
{% include post_title.md %}

The second session I went to was on current software architecture. I don't know very much about enterprise architecture and I've had my head buried in Ruby on Rails code for the past few months -that's exactly why I went to this session!

The architecture session was an intimate one, with never more than 7 or 8 people there. The other participants really knew their stuff. Hmmm...yeah, I'd say that, for instance, [Martin Fowler](http://www.martinfowler.com), [Mike Roberts](http://www.mikebroberts.com/blogtastic/), and Mark Pollack might know what they're talking about! It was pretty ridiculous that I could participate in such a discussion with guys like that, so I am incredibly grateful for the opportunity. We covered quite a bit of ground -what follows are some highlights.

By the way, [Garo covered much of it here](http://garoyeri.blogspot.com/2007/10/altnet-conference-sessions-architecture.html), so while there is some overlap, I'm deliberately focusing on different parts of the session.


### Default Architecture ###

Martin suggested that starting with Model->Persistence Interface->Persistence is the way to go because it's proven to work. But you should know going in that it won't be performant -you will have to tweak it. But just like how developers shouldn't do premature optimization on parts of an app they think will be bottlenecks, architects shouldn't prematurely optimize the software architecture. Wait until you see where the pain is before you try to ease it.


### Desktop Applications on the Web ###

As most of the early discussion centered around desktop applications plugged into large databases, someone raised the question of whether anyone should even consider something other than Silverlight (vs. AJAX) for "desktop applications on an intranet." Since I do much of my work in Rails now, I immediately disagreed as I think that Rails *could* work very well in such a situation.

But there was a larger issue here that many people picked up on, which is that if you are writing a web app, embrace it as a web app. If you are writing a desktop app, embrace it as a desktop app. Users are comfortable enough with the web now that they have certain expectations when using a web app -and those are different from their expectations when using a desktop app! I have some more ideas on this, but maybe I will leave them to a future post.


### Frozen Databases ###

I haven't had the misfortune of running into this situation, but it occurs when you build several apps sharing a single database. Eventually, you get in a situation where the database is frozen -if you make a change to it, you will break several apps. So you should ideally have a database for each app, or maybe have the apps point to some sort of persistence facade that makes them think they are talking to one database when there could really be a whole host of databases underneath.

The really interesting turn in the discussion came when someone asked why people get sucked into the database-as-integration-point approach. The answer: it's initially simpler. But while it has a low barrier of entry, the integration effort skyrockets over time as you add more apps. In contrast, the "correct" approach takes more work to set up initially, but as you add applications over time, it plateaus and the integration effort becomes more or less constant.

In a moment of inspiration, Martin drew a graph of this on the whiteboard, and in true agile fashion, later changed the y-axis to "Integration Effort" from something else (I don't remember what), after hearing another participant use the term and deciding it was more accurate.


### Horizontal Distribution ###

Mike Roberts introduced Google's style of horizontal scalability to the discussion. Google expects failure and plans for it. Their solution allows them to buy lots of cheap hardware instead of massive expensive servers (Mike mentioned a Google white paper discussing this that I'll have to look up). Martin made the interesting comment that he doesn't care about optimizing an app to run efficiently on a single box, but about optimizing it so that when you distribute it across 10 boxes, it becomes 9 times faster.


### Transitioning From Conceptualizing to Harvesting Architectures ###

Kevin Thex mentioned that the trend several years ago was to sit down and create an architecture before development. This created bloated, overly-complex architectures that often solved problems that didn't necessarily need solving. The trend now is more of an "agile architecture" where you build what you need as you need it. This struck me as the same thing that's been going on in the framework world. Of course, in this context (because I've worked a bit with both), ASP.NET comes to mind as a rather conceptualized framework and Rails does as a harvested one.
