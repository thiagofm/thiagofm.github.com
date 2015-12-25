---
layout: post
title: "The quest for an efficient software development environment on OSX"
description: "In this post, "
category: osx
tags: [amethyst totalspaces tiling window manager osx]
---
{% include JB/setup %}


After an experience in my past job using linux with `XMonad`, **a tiling window manager**, and discovering how much productivity beneficit I could reap by just using my screen more efficiently, I couldn't survive without that on my new job at **Wimdu**.

At first, I've obviously tried to install archlinux on a macbook pro, but after having too much issues with everything, I've decided to look instead at how could I improve my workflow in `OSX`, and this is what this blog post is about.

Even though the title mentions that this is for developers, I think most of those hacks would be great to any OSX power user that frequently switches between applications and need to work in different Applications at the same time, with great speed.

---

## What is this about

* Not really a post about text editors, terminals and things that doesn't involve tweaking the OS.
* Less mouse usage(down to zero).
* Fast workflow, easy to switch and arrange windows.


## Tweaking OSX to free up some screen

OSX isn't a Operating System designed only for software developers. It has nice defaults, comes with a terminal, Ruby and a lot of great apps installed. **Apple seems to care about developers, but we're clearly not it's biggest market.**

Given that, much of the screen space is cluttered with things that could be accessible by keyboard shortcuts, which we love.

![Dock]({{ site.url }}/assets/images/mac-dock.jpg)

With spotlight being a `CMD+SPACE` away, there isn't much need for the dock bar. This can easily be tweaked by going to Dock preferences, using the `CMD+SPACE dock` combo and ticking the `Automatically hide and show the Dock` option. Feel free to also maybe move the Dock to the right/left side of the screen as even if you are using the mouse to reach it, as it uses less space.


## Slide screen effect nausea

The slow slide screen effect I get while changing `Spaces` gives me nausea. In 365 days you probably get enough Space sliding to go to the moon. And Apple didn't make anywhere easy to deactivate that. Shame on you Apple.

![Spaces transition]({{ site.url }}/assets/images/osx-transition-spaces.jpg)

But no worries. There's an app for that(TM).

It's [TotalSpaces](http://totalspaces.binaryage.com).

![TotalSpaces]({{ site.url }}/assets/images/totalspaces.png)

Warning: with the new update of El Capitain, Apple basically killed TotalSpaces due to its increased security(and lack of a proper API to let it disable sliding in a different way). But there's still a way to circunvent that which is well documented at TotalSpaces's website. I suggest you to use it nevertheless, because it probably gives you a couple of hours back every year which you would be looking at a dizzy animation instead.


## Amethyst: tiling WM meets OSX

This hack will probably need you to focus a bit on setting it up and memorizing the new shortcuts, but it's a great one.

![Amethyst]({{ site.url }}/assets/images/amethyst.png)

[Amethyst](https://github.com/ianyh/Amethyst) helps you to position and resize windows with ease. It's more of use if you just check its [website](https://github.com/ianyh/Amethyst) than if I explain everything to you. Please check it's video and play around with it. This my substitute to **XMonad**, which is a tiling window manager for linux written in `Haskell`(!!!).

Most of the beneficit comes if you use more than one display, or a big enough display that you won't be using just one fully screened app. This is good for example when you are working on something on a text editor and want to see it updated in the browser, side by side... and perhaps even a terminal to see the server logs. The possibilities are endless. **Amethyst for the win!**

The only downside is that it still lacks support to full screened Apps, probably also due to the lack of an API from Apple to make this a possibility as Amethyst is actively developed. But then you can still use the App with the window in full size. The only space you'll miss is the OSX's top bar... which guess what, you can hide it on El Capitain!

## Hiding the top(menu?) bar

![Top bar]({{ site.url }}/assets/images/menu-bar.png)
*this is the bar that I'm reffering to*

The El Capitain update gave me a lot of trouble(brew...), but one of the greatest things is that it lets you hide the top bar. Big win. Some extra pixels of screen to the Gods of productivity and tidiness.

To hide it just go to `System Preferences > General` and tick `Automatically hide and show the menu bar`.


## Switching CTRL and Caps Lock

Even if you aren't a shortcut key freak like me, you probably use CTRL more frequently than Caps Lock. CTRL is very poorly located at the keyboard, making you move your hand too much. It also poses a risk to RSI-related problems, as it's a very unconfortable key to press if you do touchtyping.

On OSX you can easily do it by going to `System Preferences > General` and ticking `Automatically hide and show the menu bar`.

This is very helpful if you are using Amethyst with a couple of spaces, so you can easily switch between them with CTRL+Number, and that with CTRL being well positioned in your keyboard.


## Wrapping up

I'm a believer that productivity increases are in the small details. I'm very happy whenever people show me new tricks and also when they learn some with me.

Please feel free to share yours. 
