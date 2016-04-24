---
layout: post
title:  Size Classes
date:   2014-10-30
author: Jeffrey Bergier
tags: Objective-C, iOS Development, iOS, Swift, Size Classes, Xcode
---

![Size Classes Device Table]({{ site.baseurl }}/blog-post-assets/2014-10-30-Size-Classes-01.png)

So size classes are a great idea. They make using auto layout in Interface Builder even more powerful. However, they have some serious shortcomings. For example, there is no way to tell the difference between an iPhone 4 in portrait from an iPhone 6+ in portrait. These are wildly different screens and require wildly different designs. Yet size classes make no distinctions. Also, iPads are identical in both Landscape and Portrait orientations. That means to make a layout different for iPads in portrait vs landscape you will have to check screen sizes in code. Lame!

[Table Credit: Designing Adaptive Layouts for iPhone.](http://mathewsanders.com/designing-adaptive-layouts-for-iphone-6-plus/ "Table Credit")