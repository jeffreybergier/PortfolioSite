---
layout: post
title:  Learning About Initializers
date:   2014-11-08
author: Jeffrey Bergier
tags: iOS Development, iOS, Swift, Properties, Initializers, Init, Optionals, Xcode
---

![Screen capture showing horrid initializer]({{ site.baseurl }}/blog-post-assets/2014-11-08-Learning-About-Optionals-01.jpg)

Non optional properties are allowed if they’re populated in the initializer. Apparently they have to be created before calling super on init(). However you can’t use self until after calling super. So I have to initialize two objects for one property in order to avoid the optional and all of its syntax baggage :(