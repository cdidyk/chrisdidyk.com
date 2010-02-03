---
title: Iterations, Projects, and Bruce Lee
layout: post
---
{% include post_title.md %}

> "It's like a finger pointing to the moon. Don't look at the finger or you miss all that heavenly glory."-Bruce Lee, _Enter the Dragon_

I tend to view projects as marathons, not sprints, which is why it's so important to always have the big picture in mind while pushing to finish an iteration. The end goal (the moon) is to deliver a quality, feature-complete product, that can still be easily modified to meet market changes, not to deliver 20 iterations of work on schedule.

Iterations (the finger) are simply a vehicle to help me effectively reach my end goal. But if I work in iterations without keeping them in the context of the entire project, I will quickly accumulate so much technical debt that my iterations will blow up sooner or later, and I'll be forced to spend a lot of time fixing my codebase before I can resume adding value to the project.

Is this fingers and moons talk not doing it for ya? Alright, let's try another approach. This is another application of [Red-Green-Refactor](http://jamesshore.com/Blog/Red-Green-Refactor.html). When I am overly focused on delivering iterations, I run the risk of just doing Red-Green and skipping the Refactoring step. When I do my iteration work in the larger context of the project, I more easily understand that the Refactoring step is not optional, but required for the health of the project.

It's the difference between saying, "Sweet, that bit works now," and moving on, and, "Ok, it seems to work. But how happy am I with the implementation? Is it a good base to implement future stories on top of?"