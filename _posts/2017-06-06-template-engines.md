---
layout: post
title: Template Engines in Ruby on Rails
---

You may have heard of various view engines available with ruby like [Haml](http://haml.info/){:target="_blank"}, [Slim](http://slim-lang.com/){:target="_blank"}, [Liquid](http://shopify.github.io/liquid/){:target="_blank"}, [Mustache](https://mustache.github.io/mustache.5.html){:target="_blank"} and many more.

Template Engines are used for the presentation layer of the application. They take some source template & data, and then produce a formatted output.

This is not the comparison between the template engines in Ruby on Rails. This post is more about analyzing what are the advantages and disadvantages of Template Engines. It’s more about choosing one over the other based on your current need and comfort.

The default templating language in Rails is ERB (Embedded Ruby).

The template files live in /app/views/ and are named after the controller and action they’re attached to. Everything you need to use ERB is already set up for you within Rails.

ERB is good mainly if you have a web designer that will work on plain HTML and does not know either haml or slim. This way he can write HTML and you can embed ruby logic with the proper tags.

ERB and HAML are the most popular template engines within the Rails community.

If you work on both HTML and Ruby logic, you should try HAML. It is a lot more ruby-friendly, reduces char count by much and a lot more readable than ERB.

For better speed, Slim is the fastest of the three engines.

Now is up to you to choose the template engine. Choose not to compare but to fulfill your needs.

Thanks for reading, I will post more details in the coming weeks.
