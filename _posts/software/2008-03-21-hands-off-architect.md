---
title: Can a Hands-off Architect Work in Agile?
layout: post
teaser: "If you actually have an Architect on your team, should she be in the code developing or locked out of the codebase? Does the first cause her to be too close to the implementation to make the right architectural decisions?"
---
{% include post_title.md %}

<p><span style="text-decoration: line-through;">At Dovetail, we're hiring a Software Architect</span>. One of the things we've debated is whether this architect needs to be in the code everyday. Our general consensus is that yes, she should.</p>

By being "in the trenches", I have full confidence that the architect truly understands what we developers are doing and how. To me, this translates into making architectural decisions that help our project grow organically, which is especially important since we are a pretty strict TDD shop. By that, I mean that our tests frequently drive our actual design. Yes, sometimes we gameplan our design ahead of implementation or when our app is in need of refactoring, but even then, our tests might cause us to tweak that design.

Contrast this with another flavor of TDD where you can do the design up-front and then still drive the actual implementation with tests, but in a way that absolutely will not veer from the initial design. In other words, the design is the skeleton and TDD is used to flesh it out.

Without any regard for historical meanings of "Test Driven Design" vs. "Test Driven Development" (why do I feel like I need to add little trademark symbols after those?), the first approach strikes me as "Test Driven Development" with "Test Driven Design", and the second strikes me as "Test Driven Development" without "Test Driven Design". To be clear, I'm not arguing the legitimacy of either approach, just stating where I see an important difference in the way we do things where I work.

Also, when she's hands-on, I have full confidence that the architect understands where our pain is and which parts of our app are brittle and in need of better design.

Conversely, a hands-on architect is in danger of becoming invested in the code she writes. She may be less able to take a step back and objectively look at the design and admit that maybe some code she wrote is the wrong path. Hmmm....anything else?

Ok, now let me tell you about my big fear. In the past, I have worked with someone who essentially became a hands-off architect, and the pattern we fell into was frustrating for everyone. Essentially, another developer and I would tear through a bunch of stories, and this architect would occasionally review our work and launch us on long fits of refactoring and all progress would stop. These ideas in refactoring almost always improved our code significantly, but the process was painful and is one that we can't afford to re-create.

Unfortunately, I can see either type of architect realizing this fear. After all, any software architect will have responsibilities that lie outside the codebase, and I think it's time spent outside of the codebase along with attachment to specific designs/implementations that can lead us astray.

I guess ultimately, it comes down to the actual person. My preference is a coding architect who I can pair with and learn from, but as long as our architect can fit with the way we work, make the right high-level decisions, and enable our development through her design-work and guidance, I will be happy.

My question to you is: how do you like your architect?