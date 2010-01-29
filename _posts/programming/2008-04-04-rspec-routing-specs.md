---
layout: post
title: Rspec Routing Specs
---

## Rspec Routing Specs ##

I just started playing around with the rspec_scaffold generator. It seems pretty helpful, although I will still end up deleting some of the files it creates (at least until I get tired enough of it to write an automated solution). But there's an additional controller spec it creates that looks really puzzling to me. It checks routes in the following ways:

{% highlight ruby %}
route_for(:controller => "accounts", :action => "index").should == "/accounts"
{% endhighlight %}

and

{% highlight ruby %}
params_from(:get, "/accounts").should == {:controller => "accounts", :action => "index"}
{% endhighlight %}

This is interesting, and I'll have to think about it more, but at first glance, I don't find these tests useful. I don't typically do a lot of route testing in specs, and, especially for simple routes like this, I think it's a little too close to testing the framework for my taste, like testing if the object returned by @Account.find(1)@ is indeed an Account and has an id of 1 (ok, that's probably unfair, but still...). It does give me the opportunity to consider if I should be testing routing, though.

I'll think about that while deleting this file along with the auto-generated fixtures and helpers :)
