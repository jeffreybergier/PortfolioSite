---
layout: post
title:  Broken setThumbTintColor
date:   2014-11-28
author: Jeffrey Bergier
tags: iOS Development, iOS, Swift, Xcode, UISlider, setThumbTintColor
---

![Custom Thumb Image Code and iOS Simulator Screenshot]({{ site.baseurl }}/blog-post-assets/2014-11-28-iOS8-Broken-setThumbTintColor-01.png)

Setting the color of the Circular thing that is used to control the slider should be easy. Apple provides a setThumbTintColor method. However, it simply doesn't work. You set the thumb tint color as many times as you want and it stays white. If you search online, Stack Overflow says that you can set an image for the thumb and then set the tint color and it works. This workaround does work, but it causes the thumb to look like iOS6. It has a gradient and shadow, etc. Its very ugly. It appeared the only solution would be to create my own image and use that for the thumb in the slider.

This presented a problem for me. I don't like using bitmaps in my projects because they are pain to change whenever I change something in the app. If I decided to use a different color a different line thickness, I have to go through and update the bitmap assets. What a pain. So this was an opportunity to learn how to use core graphics to create a UIImage.

I, of course, used my favorite new thing... Lazy Properties. To create this UIImage. That way all the code for it is stored within the property itself. Its not spread around my code. It is still an optional property because UIImages created by Core Graphics are also optional. But I've never had it not work. Also, a friend brought up that this takes way longer than loading an image. I used NSDates to track how long it took to do this. Even on an iPhone 4S, it took less than 1 thousandth of a second. I'm happy with that. Lastly, because I am using Core Graphics, I took the opportunity to make something that looks cooler than just a Red Circle. Now I have this really cool looking red circle stroke that looks great in the settings screen.