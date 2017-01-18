---
title: A Swift transition from Laravel to Vapor
date: 2017-01-16 10:56:11
tags:
- vapor
- swift
- web-development
---

> *"If you don't like something, change it. If you can't change it, change your attitude."* - **Maya Angelou**

I've been doing web development with [Laravel](https://laravel.com) for quite some time now. Honestly speaking, I really like Laravel. It has a great ecosystem and an awesome community.

As much as I like Laravel, I cannot make myself to like PHP. It has just too much magic to my liking. And honestly, as great as Laravel is, its liberal use of facades, and some other cool tricks, makes the magic even more black. I would be fine if I have to use it in my day-to-day job. but for my own side projects, I prefer something modern and something with less magic. Also, preferably statically typed as it makes it easier to understand the underlying framework. ...

<!--more-->

I've been looking for a framework that closely resembled Laravel but in Swift programming language. Swift is probably my favorite language so far. I don't get to play with it in my daytime job but I've  ported one of my side projects, [LightPaper](http://lightpaper.42squares.in), from Objective-C and written handful of other apps such as [Snub](https://github.com/ashokgelal/Snub), [Octohub](https://www.producthunt.com/posts/octohub) etc in Swift. And I absolutely enjoy writing Swift would be an understatement!

As I was searching for a good Swift web framework, I discovered [Vapor](https://vapor.codes). I found a couple of other frameworks for Swift but Vapor is closer to the spirit of Laravel than any other frameworks. Its APIs are very readable and has so many official components that complement it nicely  - such as [Fluent](https://github.com/vapor/fluent), [Leaf](https://github.com/vapor/fluent) etc.

They have also made a great [command line toolset](https://vapor.github.io/documentation/getting-started/install-toolbox.html) to make it easy to quickly get up and running with a new Vapor project. [The documentation](https://vapor.github.io/documentation/getting-started/install-toolbox.html) is also very good and succinct. This is how you know a framework cares about the productivity of its target developers.

I instantly liked it! And I'm going to write my next project using Vapor and Swift.

So far I've only played with a couple of controllers, models, and views and also looked at their source code to understand the underlying magic. Everything is very readable and nicely commented. The (over)use of extensions does make it difficult to follow sometimes. But the combination of a statically typed language and a very good IDE (I use both XCode and [AppCode](https://www.jetbrains.com/objc/), BTW) makes it very tolerable.

In coming days, I'll be sharing more about my experiences with Vapor on this blog. I intend to write some tutorials, share some tips, and hopefully be a very active member of the community if everything goes well. We shall see soon!