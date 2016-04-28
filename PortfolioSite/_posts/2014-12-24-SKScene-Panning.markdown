---
layout: post
title:  SKScene Panning
date:   2014-12-23
author: Jeffrey Bergier
tags: Srite Kit, iOS Development, iOS, Swift, Solar System, Xcode, UIPanGestureRecognizer, Panning
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-02.mp4">Click to download the video.</a>
</video>

I got panning working! I know these innocuous looking lines of code seem simple. However, this is the first time I have ever used a UIPanGestureRecognizer at all, let alone in SpriteKit. I have always gotten away with UITapGestureRecognizer or UISwipeGestureRecognizer. Those are super simple because they work more like a button. When some qualifications are met, they call a selector on their target. Then you perform the action you want like a view appearing or disappearing.

With SpriteKit I had to first figure out how to pan the nodes. It turns out SKScene (where all the SKNodes live) doesn’t really liked to be moved around. It has an anchorPoint property that can be changed, but its a bit strange to work with. Its a CGPoint where each value is between -1 and 1. SKNodes on the other hand have a position property that is a normal CGPoint that uses points based on its SKScene coordinate system. So the first thing I had to do was create a “SolarSystemNode” that was the size of the scene that all of the planet nodes would go into. This was pretty simple, but it required me changing some of the math so the Sun and the planets still knew how to appear in the center. Once that was done I could start playing with the position of the SolarSystemNode with the gesture recognizer.

The UIPanGestureRecognizer is tougher because the selector you give it is called over and over again with very little context. So when the state of the gesture recognizer is began you have to set up the context in a property and then when the selector is called over and over in the “Changed” state, you use that context and the information from the gesture recognizer to perform the pan.

Its pretty simple after reflection, but because I had never done anything like this, it took me a few hours :p. Next is pinching to zoom in and out.