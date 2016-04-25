---
layout: post
title:  Gradients with UIColor.clearColor()
date:   2014-11-08
author: Jeffrey Bergier
tags: iOS Development, iOS, Swift, CAGradientLayer, UIColor, Opacity, Xcode
---

![Screen grab with gradient of colors]({{ site.baseurl }}/blog-post-assets/2014-11-08-Gradients-with-ClearColor-01.jpg)

Be careful not to forget you’re a designer. I ran into issues trying to make a gradient. I was making it from my dark color to [UIColor clearColor]. It never looked right and I couldn’t figure out why. Then while trying to do the gradient in Photoshop i was reminded that gradients don’t go from the color you want to white with alpha 0. They go from the color you want to the color you want with alpha 0. So I redid the gradient in code so that I go from my dark color to the same dark color with an alpha component 0. Of course ape knew this would be common so they built it into UIColor.