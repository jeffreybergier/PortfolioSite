---
layout: post
title:  Lazy Properties in Swift
date:   2014-11-16
author: Jeffrey Bergier
tags: iOS Development, iOS, Swift, Lazy Properties, Properties, Xcode
---

![Lazy Property]({{ site.baseurl }}/blog-post-assets/2014-11-16-Swift-Lazy-Properties-01.jpg)

I learned how to fix the issue I faced [before]({% post_url 2014-11-08-Learning-About-Optionals %}). Lazy properties give you a way to specify a property that is not allocated into memory until its called for the first time. However, the side effect of this is they allow you to use self in the property definition because Swift knows it will be called after init(). I’m totally in love.