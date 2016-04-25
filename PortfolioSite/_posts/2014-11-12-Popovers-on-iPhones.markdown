---
layout: post
title:  Popovers on iPhones
date:   2014-11-12
author: Jeffrey Bergier
tags: iOS Development, iOS, Swift, Size Classes, Xcode, Popover, iPad
---

![Screenshot of code and iOS simulator showing a popover on an iphone]({{ site.baseurl }}/blog-post-assets/2014-11-12-Popovers-on-iPhones.png)

The iPhone 6 plus has a really big screen. iPads also have really big screens.

Apple created the concept of a popover for iPads. A popover displays one view controller in a little modal window over another view controller. In iOS8 when you select a new "adaptive segue" in Interface builder, you can use popover. However, iOS is smart enough to use a modal display for iPhones and a popover display for iPads. (Except, interestingly, on iPhone 6 plus in landscape. iOS automatically chooses Popovers in that case.).

This popover for iPad and modal for iPhones behavior is probably best behavior for most views. However, this tip calculator I am making has a really simple settings screen. Its so simple, that the extra width of the 6 plus actually makes it harder to use and understand. So I was interested in using a popover on the 6 plus.

Fortunately its easy to force iOS8 to use a popover whenever you want. The code is shown in the picture and the full instructions can be found on [Alex Robinson's blog](http://rbnsn.me/posts/2014/09/08/ios-8-popover-presentations/). With this method its easy to do a check on the screen size (because iPhone 6 and 6 plus do not have special size classes in portrait) and then choose the correct presentation style.