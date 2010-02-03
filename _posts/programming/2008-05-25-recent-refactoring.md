---
title: A Recent Refactoring
layout: post
---
{% include post_title.md %}

Recently, while working on the rails version of my personal budget
system, I came across an interesting problem. I'll share the
refactoring I did in the hopes that it will help someone else and
solicit feedback that will help me improve it.

First off, [here's a picture of the main screen I'm working with.](/images/moneybags.png)

In this app, I have budgets, accounts, and allocations. The linked
image shows the entire budget (titled "2008"). "Bills - Checking",
"Spending - Checking", and "Savings" are accounts, and "Rent",
"Electric", "Food", and "Vacation" are allocations. The top section
has income and shows the budget's total expenses and balance.

Now even though I like to see bimonthly, monthly, and annual
information, there's no sense entering those individually, is there?
So this app only lets you enter monthly amounts and then calculates
the respective bimonthly and annual amounts. Make sense? Here's what
the schema looks like for these objects:

Budgets
* id
* name
* monthly_income

Accounts
* id
* name
* budget_id

Allocations
* id
* name
* monthly_amount
* account_id

Even though I had thoughts of [Presenter](http://blog.jayfields.com/2007/03/rails-presenter-pattern.html), I started out building the methods I needed directly in the model objects. This way, I could see exactly what I was working with, and I'm not convinced that these methods are out-of-place in the model anyway. Besides, I can always refactor to Presenter later.

### The First Cut ###

In the Budget class:

{% highlight ruby %}
def bimonthly_income
  monthly_income / 2.0
end

def annual_income
  monthly_income * 12
end

def self.generate_expense_and_balance_methods(*terms)
  Array(terms).each do |term|
    class_eval <<-EVAL
      def #{term}_expenses
        self.accounts.inject(0) do |total, account|
          total + account.#{term}_total
        end
      end

      def #{term}_balance
        #{term}_income - #{term}_expenses
      end
      EVAL
  end
end

generate_expense_and_balance_methods :bimonthly, :monthly, :annual
{% endhighlight %}

Not too bad. You can see that the budget's bimonthly and annual
incomes are calculated off of the monthly income. And I've already
gotten rid of some repetition by meta-programming the bimonthly,
monthly, and annual expense and balance methods.

Now the relevant bits of the Account class:

{% highlight ruby %}
def self.generate_total_methods(*terms)
  Array(terms).each do |term|
    class_eval <<-EVAL
      def #{term}_total
        self.allocations.inject(0) do |total, allocation|
          total + allocation.#{term}_budget
        end
      end
      EVAL
  end
end

generate_total_methods :bimonthly, :monthly, :annual
{% endhighlight %}

Ok, so I'm doing the same thing here with the bimonthly, monthly, and
annual account totals. This already looks similar to what I did for
the budget's expense methods. More on that later.

Lastly, the Allocation class:

{% highlight ruby %}
def bimonthly_budget
  monthly_budget / 2.0
end

def annual_budget
  12 * monthly_budget
end
{% endhighlight %}

Hmmm, this is similar to what I did for the budget's income methods.

### The Refactoring ###

I'm seeing lots of repetition that can be refactored. I also see that
there's a common thread of needing this bimonthly, monthly, and annual
stuff (what I creatively referred to as "terms") across several classes. So I decided to refactor that out into its own module called TermMethods:

{% highlight ruby %}
module TermMethods
  def term_methods(name)
    define_method("bimonthly_#{name}") do
      (send("monthly_#{name}") || 0) / 2.0
    end

    define_method("annual_#{name}") do
      (send("monthly_#{name}") || 0) * 12
    end
  end

  def term_totals(collection, method, name = "total")
    TERMS.each do |term|
      define_method("#{term}_#{name}") do
        send("#{collection}").inject(0) do |total, item|
          total + item.send("#{term}_#{method}")
        end
      end
    end
  end

  def term_balances(starting_balance, deduction)
    TERMS.each do |term|
      define_method("#{term}_balance") do
        send("#{term}_#{starting_balance}") - send("#{term}_#{deduction}")
      end
    end
  end

  private
  TERMS = ['bimonthly', 'monthly', 'annual']
end
{% endhighlight %}

And the results:

{% highlight ruby %}
class Budget < ActiveRecord::Base
  extend TermMethods
  ...
  term_methods :income
  term_totals :accounts, :total, :expenses
  term_balances :income, :expenses
end

class Account < ActiveRecord::Base
  extend TermMethods
  ...
  term_totals :allocations, :amount
end

class Allocation < ActiveRecord::Base
  extend CustomValidations
  ...
  term_methods :amount
end
{% endhighlight %}

These classes look much simpler to me. Of course, the TermMethods
module is a little more complex, but it still looks pretty reasonable
to me, and I haven't looked at it in a month.

I could explain it all, but isn't that one of the things RSpec is
supposed to help with? [Here's the output of my TermMethods specs](/assets/term_methods_report.html).

Well, the abstraction makes the specs a bit more technical and less straight-forward than I would like, but I still think they are fair documentation. The real test is if they make sense to *you*!

### Final Thoughts ###

The module is coupled to some implementation details, but right now, that's fine. If I need to make it more general later, I can do so when the concrete business need arises. Honestly, if I recall correctly, the only reason I have term_methods defaulting
to 0 if monthly_&lt;name&gt; isn't found is because otherwise, it throws an
error that's not intuitive to trace. I could've manually checked for and thrown an exception with an appropriate message, but it was just as easy to have the default, which I think is reasonable.

So what do you think? Meta-programming gone bad or a sensible abstraction?