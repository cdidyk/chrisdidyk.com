---
title: Why You Do Something Is Always Important
teaser: The part of a user story that answers why it should be done often gets treated lightly even though it's arguably the most important part. We usually know why we do the different things we do in our personal lives, shouldn't we also know why we're modifying the software we're developing?
layout: post
---
{% include post_title.md %}

Recently, in the context of using mindmapping for developing user stories, [Ryan Garver said](http://http://blog.selfmodifying.com/2010/02/02/user-stories-and-mind-mapping/):

> What the user does is less important than why they want to do it

His statement reminded me just how important the "Why?" is in user stories, regardless of your method of collecting them. And yet, when I see people go through the motions of a user story template, the "Why?" is usually what gets the worst treatment. Why is that?

Have you experienced the following?

- You're in a meeting with a Product Owner writing a new story. You ask why she wants the functionality, and she chuckles and gives a bullshit answer like, "So the system works as it should," or, "because that's what I want."

- You're in another meeting with a different Product Owner writing a new story. You get to the "Why?" and can't figure out what to write. You look around at the rest of the team and see that everyone else is equally confused. The Product Owner says, "Let me hold onto this one for now. I'll do some more research, and if I can come up with a good reason why we need this, I'll add it back in, and if I can't, I'll toss it."

I've experienced both situations. Guess which project was successful and which wasn't? Of course it wasn't the only factor, but don't underestimate how important the "Why?" is.

Let's step outside of software development for a minute. Are there things you do in your daily life that you do for no reason at all? If there are and you realize it, do you keep doing them anyway? Why do you take out the trash, take your kid to soccer practice, hack on an open source project, or watch kung fu movies? You may not have spent much time thinking about the reasons, but you can probably come up with them pretty quickly. Why should it be any different for a business or a piece of software?

By now, hopefully you're convinced that the reason for a user story shouldn't be an afterthought. But how do you write a good "Why?" Well, I don't have an answer for that yet, but here are some guidelines I've found useful (please add your own in the comments!):

1. __The reason shouldn't be so high-level that it's hard to connect it to the functionality.__ For example, "As a music-lover, I want to browse songs so that I save money." For better or for worse, I usually ask myself if inverting the story makes sense: "If I'm a music-lover, how might I save money? By browsing for songs?" In this case, I don't think that makes sense. Better would be "As a music-lover, I want to browse songs so that I find new music I love."

2. __The reason should match the actor.__ "As a music-lover, I want to buy a song so that SuperCorp makes more money." Just stop right there! How about: "As a music-lover, I want to buy a song so that I can listen to it whenever I want."

What all this leads to, hopefully, is innovation. Once you know the reason, you have the context needed to choose the best functionality to meet the needs of the people using your software. Even better, when you know the reasons for several stories, you start to gain a larger context that gives you the ability to dramatically improve the ways that people use your software. You might find a way to cut steps out of a user workflow or automate something that users assume has to be done manually, for example.

I like the approach that Ryan described and will try it out myself. It's similar in spirit to the example set by Cucumber (and probably developed elsewhere first) that flips the user story template around to be: So that/As a/I want to, which, unsurprisingly, I also like. By shifting the focus of a user story to the "Why?", we help ensure that the functionality we implement has a true purpose that is realized.