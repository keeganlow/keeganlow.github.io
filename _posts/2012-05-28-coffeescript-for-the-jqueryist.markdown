---
layout: post
title: "CoffeeScript for the jQueryist"
date: 2012-05-28 00:19
comments: true
categories: [CoffeeScript, Javascript, jQuery]
description: "wow"
---

In this post we'll look at some examples of how to use [CoffeeScript](http://coffeescript.org/) to perform common tasks with jQuery.

## Document Ready

First of all, if you've spent any time with jQuery at all, you're used to writing code like:

{% highlight javascript %}

$(document).ready(function() {
  // code to run as soon as the DOM is loaded
});

// or more succinctly:

$(function() {
  // code to run as soon as the DOM is loaded
});

{% endhighlight %}

Okay, well how does this look in CoffeeScript?

{% highlight coffeescript %}

$ ->
  # code to run as soon as the DOM is loaded

{% endhighlight %}

To understand this snippet, note a few properties of CoffeeScript:

1. A function that takes no arguments is written: `->`.
2. Invoking a function with arguments doesn't require the arguments to be wrapped in parentheses.
3. Semicolons aren't required after expressions.
4. Function bodies are not delimited by braces. Instead, indentation is used.

So `function() {}` becomes `->`. We can then invoke `$` with `->` as its only argument without having
to wrap `->` in parentheses.

## A Step-by-step Example

In the code samples that follow, I'm going to apply a series of changes to the following JavaScript:

{% highlight javascript %}
$('p').click(function (e) {
  e.preventDefault();
  $(this).slideUp();
});
{% endhighlight %}

Each of these changes will move us toward a typical CoffeeScript implementation. First, to get this JavaScript
to be valid CoffeeScript, a few changes must be made.

{% highlight coffeescript %}
$('p').click((e) ->
  e.preventDefault();
  $(this).slideUp();
);
{% endhighlight %}

As we saw before, in CoffeeScript indendation is used to delimit function bodies. Similar to the first example,
the `function` keyword has been removed, and the `->` operator as been inserted. `(e) ->` in CoffeeScript simply means the same thing as
`function(e)` in JavaScript. With these subtle changes, we already have valid CoffeeScript that compiles exactly to the 
JavaScript snippet we started out with. Let's keep going.

Next, we're going to clean this CoffeeScript up a bit more. Let's drop the semicolons. While this is a contentious practice in JavaScript, it's the norm in CoffeeScript. The only time you need to think about semicolons in CoffeeScript is if you're trying to pack multiple expressions onto the same line of code.

{% highlight coffeescript %}
$('p').click((e) ->
  e.preventDefault()
  $(this).slideUp()
)
{% endhighlight %}

In CoffeeScript, if you're invoking a function with parameters, you can omit the parentheses around the parameter list. In this case, we're invoking jQuery's `.click()` function with a single parameter: our anonymous callback function. 

{% highlight coffeescript %}
$('p').click (e) ->
  e.preventDefault()
  $(this).slideUp()
{% endhighlight %}

If you're wondering why we didn't drop the parentheses in `$('p')`, that's a good question. The answer is that without the parentheses around the `$()` invocation, we wouldn't be able to chain the invocation of the `.click()` method to the selector's result. In general, if you want to use method chaining, you'll have to include parentheses around your argument lists for all but the last method in the chain.

Next, we'll add a little more sugar to our CoffeeScript (pardon the pun). 

{% highlight coffeescript %}
$('p').click (e) ->
  e.preventDefault()
  $(@).slideUp()
{% endhighlight %}

CoffeeScript uses `@` as an alias for the `this` keyword. It's a little strange at first, but if minimalism is your thing, you may like it. If not, just use `this` as you normally would; CoffeeScript won't mind.

Before we leave this example, let's take a look at a slightly different implementation of this click handler. 

{% highlight javascript %}
$('p').click(function() {  
  $(this).slideUp();
  return false;
});
{% endhighlight %}

This code results in the same behavior as our original JS snippet. One implementation in CoffeeScript is:

{% highlight coffeescript %}
$('p').click ->  
  $(@).slideUp()
  false
{% endhighlight %}

This makes use of one feature of CoffeeScript that we haven't dicussed yet: implicit returns. The value of the expression at the end of a function is its return value. So in this case, having the last line of the function say `false` is the same as having `return false;` in JavaScript.


## Conclusion

If you're learning CoffeeScript, I hope this step-by-step example has been helpful. There are a lot of people with strong opinions on CoffeeScript. I'm not one of those people. CoffeeScript is a really neat little language, and that's that.
