---
title: Condensing Mocks in RSpec
teaser: "KungFuMaster.stub!(:find).and_return @drunken_master = stub_model(KungFuMaster)"
layout: post
---
{% include post_title.md %}

Check out this RSpec `before` block and its variants:

{% highlight ruby %}
# 1
before :each do
  @drunken_master = stub_model KungFuMaster
  KungFuMaster.stub!(:find).and_return @drunken_master
  @drunken_master.stub! :update_attributes
end

# 2
before :each do
  @drunken_master = stub_model KungFuMaster, :update_attributes => nil
  KungFuMaster.stub!(:find).and_return @drunken_master
end

# 3
before :each do
  @drunken_master = stub_model KungFuMaster
  @drunken_master.stub! :update_attributes
  KungFuMaster.stub!(:find).and_return @drunken_master
end
{% endhighlight %}

I see and do this a lot when the i-var is needed in several tests. None of them make me totally happy, though, for various small and probably anal-retentive reasons.

1. They all disrupt my flow. Forget `:update_attributes` for a minute. When I'm typing out the `:find` stub, I usually get to `and_return` before I realize I actually need a variable. So I have to go above it and set the variable before continuing.

2. \#1 maintains the order of method calls in the method under test (`find` before `update_attributes`), but separates the `:update_attributes` stub from the `@drunken_master` definition.

3. \#2 keeps the various bits of `@drunken_master` together, but the order of method calls is off, and `:update_attributes => nil` has extra noise because I have to set a return value that I don't care about, which in turn causes `:update_attributes` to look like an attribute and not a method.

4. Based on my points so far, you can probably tell what my gripes are about \#3.

None of these gripes are a big deal, and all of the examples are fine. But if I could solve my gripes easily and quickly, why wouldn't I?

Hence, this:

{% highlight ruby %}
before :each do
  KungFuMaster.stub!(:find).and_return @drunken_master = stub_model(KungFuMaster)
  @drunken_master.stub! :update_attributes
end
{% endhighlight %}

This looks better to me.

1. It doesn't disrupt my flow. I get to `and_return`, think, "Hmm...I need an i-var here," and just set the i-var and continue on my merry way.

2. The `:update_attributes` stub is in order _and_ next to the definition of `@drunken_master`. And no additional noise either.

As a bonus, it keeps things tidier when I have more objects/methods to stub.

There are times when I fall back to my "old" way.

1. When I'm stubbing `new`. Because I get an error.
2. When the stub_model is complex (which is often a code smell anyway). When I write specs, I place a lot of value on making the intent of the code as clear as possible and making it easy to read and understand what's going on. If this (or any) style reduces either of these, I go with something else.

What do you think?