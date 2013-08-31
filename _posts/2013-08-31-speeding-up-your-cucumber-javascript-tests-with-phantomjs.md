---
layout: post
title: "Speeding up your cucumber + capybara acceptance testing with phantom.js"
description: ""
category: 
tags: [phantom.js cucumber javascript bdd testing]
---
{% include JB/setup %}

Hello folks,

Lately I've been doing some acceptance testing for the [memcached-manager](http://github.com/thiagofm/memcached-manager) gem that involved a lot of javascript, as it's frontend is made with angular.js.

So, I just had to do something about it otherwise it would take a lot of time to run all of them as I couldn't go headless-mode. The browser suppousely had to be opened so all the javascript would be loaded.

Enter phantom.js:

> PhantomJS is a headless WebKit scriptable with a JavaScript API. It has fast and native support for various web standards: DOM handling, CSS selector, JSON, Canvas, and SVG.

This is what it's [website](http://phantomjs.org/) says.

I thought it would take sometime to configure it to work with capybara, I
was wrong. Let's start with the fun part now. Can't say how much I love
the ruby community to always make things simpler than I even expect.

# Installing

To begin, let's start by installing phantom.js itself. I use mac with
brew so this is my way of doing it:

{% highlight bash %}
brew install phantomjs
{% endhighlight %}

Now, let's add the [poltergeist](https://github.com/jonleighton/poltergeist) gem to your Gemfile, which adds support for the phantom.js
driver for capybara right out of the box:

{% highlight ruby %}
gem "poltergeist"
{% endhighlight %}

Then let's bundle install it: 

{% highlight bash %}
bundle install
{% endhighlight %}

And load & update the javascript's driver of capybara to be the poltergeist's
one inside the cucumber's `env.rb` file, mine is located at
`features/support/env.rb`:

{% highlight ruby %}
require 'capybara/poltergeist'
Capybara.javascript_driver = :poltergeist
{% endhighlight %}

Now, it's done. On every single feature you annotate/tag with
`@javascript` it will be run using the phantom.js's headless browser.
Want an example? Here it is from [memcached-manager's project](https://github.com/thiagofm/memcached-manager/blob/83f11c5ec2ff8be46c049baf7b7f13c12fc7534c/features/webapp/create_memcached_key.feature):

{% highlight gherkin %}
@webapp
@javascript
Feature: Create memcached pair
  Scenario: Success
    When I visit "#/new"
    And fill in "Key" with "foo"
    And fill in "Value" with "bar"
    And click "create"
    Then it should exist in memcached
{% endhighlight %}

# Dealing with asynchronous requests

So, what if in a `step definition` you end up using some AJAX, how do
you make phantom.js wait until you receive a response from this async
request?

Use `sleep`. Want an example? Let's take the previous feature shown to
you, the `Create memcached pair` feature. The step definition's
implementation looks like this:

{% highlight ruby %}
When /^I visit "(.*?)"$/ do |route|
  visit route
end

When /^fill in "(.*?)" with "(.*?)"$/ do |field, value|
  fill_in(field, :with => value)
end

When /^click "(.*?)"$/ do |button|
  click_button button
end

Then /^"(.*?)" key should have the "(.*?)" value in memcached$/ do |key, value|
  sleep 1
  Memcached.get(key).should == value
end
{% endhighlight %}

Simple right? With just a `sleep 1` it was possible to the key be
updated and checked.

# TravisCI config

So, it seems everybody is using `continuous integration` nowadays,
right? For TravisCI you need to activate `xvfb` which instead of showing
graphics operations in the screen, it performs on memory. After all, the
current state of art of CI's allows no screen outputs -- for now.

To make it work, just make sure you add to the `.travis.yml` file the
following lines:

{% highlight yaml %}
before_script:
  - "export DISPLAY=:99.0"
  - "sh -e /etc/init.d/xvfb start"
{% endhighlight %}

# Wrapping up

So, here we learned how to set up properly capybara to use phantom.js
and how it could give us a speedup in our testing build whenever we need  
those tricky javascript acceptance tests to be run.

That's all folks.
