---
layout: post
title: Law of Demeter and Nested Routes
---

## Law of Demeter and Nested Routes ##

I'm working on implementing my budget system as a hobby Rails app, and one of the things I've run into that I haven't visited in awhile is the age-old question: how deeply do you nest routes?

In this case, I have a Budget that has many Accounts that have many Allocations, the idea being that if I have, say, a checking account that I only use for paying bills, it may have $120 total, but $70 might be allocated for paying my electricity bill and $50 for my cable bill. The budget paths are straight-forward, being things like:

<code>/budgets/1</code>

The account paths are also pretty straight-forward, i.e.:

<code>/budgets/1/accounts/2</code>

When I get to the allocation paths, I have two choices:

<code>/budgets/1/accounts/2/allocations/5</code>

or

<code>/accounts/2/allocations/5</code>

First off, I think the reason why there has been so much debate here is because neither way is always right or wrong. In fact, I think both are perfectly acceptable here. That said, I'm inclined to leave the budgets bit off the allocation paths. True, the url is more descriptive with it in there, but I tend to view this as an extension of the Law of Demeter, and Allocations and Budgets don't need to know about each other. They only need to know about Accounts.

One more twist: while I love the power of @map.resources@, I find that the sheer number of routes can get out of hand pretty quickly, so I like to minimize what I consider to be extraneous routes. So instead of:

<pre>
<code>
map.resources :budgets, :has_many => [:accounts]
map.resources :accounts, :has_many => [:allocations]
</code>
</pre>

I'm going with:

<pre>
<code>
map.resources :budgets, :has_many => [:accounts]
map.resources :allocations, :name_prefix => 'account_', :path_prefix => 'accounts/:account_id'
</code>
</pre>

simply because I don't want the stand-alone account routes. Of course, for all I know, I'll discover something in the next iteration that will cause me to completely change this whole approach! But my whole point is that the Law of Demeter applies to routing, too. It's ok to break it, but you should do so consciously.