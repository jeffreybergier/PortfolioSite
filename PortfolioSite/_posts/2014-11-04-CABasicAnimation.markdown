---
layout: post
title:  Learning CABasicAnimation
date:   2014-11-04
author: Jeffrey Bergier
tags: CABasicAnimation, iOS Development, iOS, Swift, Core Animation, Xcode
---

![Screen grab of simple CABasicAnimation in UIKit]({{ site.baseurl }}/blog-post-assets/2014-11-04-CABasicAnimation.jpg)

So every new iOS developer should learn how to use UIView Animation. It’s super easy and creates beautiful and smooth effects in your UI. However, I was running into an issue where the border color wasn’t animating. Well it turns out that UIView animations can’t animate any properties on the layer of a view. If we remember our history, those layers actually belong to an old Cocoa feature called Core Animation. Core animation came out before block syntax in ObjC. So it has a different, uglier and more verbose animation system. CABasicAnimation. It’s shown in the picture above. Have fun!