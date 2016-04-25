---
layout: post
title:  iOS 7 Dynamic Type
date:   2014-11-23
author: Jeffrey Bergier
tags: Objective-C, iOS Development, iOS, Swift, Size Classes, Xcode, Dynamic Type, Accessibility
---

![Gratuity on many different devices with different accessibility font sizes]({{ site.baseurl }}/blog-post-assets/2014-11-23-iOS7-Dynamic-Type-01.png)

Accessibility is important for software. Supporting Dynamic Text in iOS, plays a large part in making it possible for even more people to use your app.

The text in this app is already large, so I originally thought I wouldn't support dynamic text. However, the larger text sizes supported by iOS are definitely bigger than the text sizes I had in the tableviews. I felt it was important to support larger text sizes. Here you can see side by side shots of ever increasing dynamic text sizes. From left to right, the text gets slightly larger. You can see that tables are not wide enough and the label readjusts the text to make it fit. So I will have to change the auto layout constraint depending on the text size adjustment.

On the bottom row, the text size is controlled automatically by the System. Its preferred font for body type. As you can see it gets massively bigger on the right. I also have settings in UIPresentationController to make the pane wider as the text size goes up and eventually it makes the settings screen, full screen over the top of the main view controller.

After fixing the first issue, I plan to also add support for voiceover. I'm not sure what I'm going to do. I may just load a totally different view that is keyboard based. That may be easier to use when using voiceover than two really long tables.