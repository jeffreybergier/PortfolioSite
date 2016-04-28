---
layout: post
title:  SKScene Pinching and Zooming and Rotating
date:   2014-12-23
author: Jeffrey Bergier
tags: Srite Kit, iOS Development, iOS, Swift, Solar System, Xcode, UIPanGestureRecognizer, UIPinchGestureRecognizer, UIRotationGestureRecognizer, Panning, Rotating, Zooming, Gesture
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2014-12-24-SKScene-Panning-02.mp4">Click to download the video.</a>
</video>

The UIPanGestureRecognizer took me a long time because I had never used Gesture Recognizers like this before. However, the UIPinchGestureRecognizer and the UIRotationGestureRecognizer were very easy to implement because they work in basically the same way as the UIPanGestureRecognizer. 

Each gesture recognizer has a Property on the class that helps it keep track of where the SolarSystemNode was when the gesture began. Then as the gesture is changing, it uses this starting point as a baseline to go on.

By default only one gesture recognizer can work at a time. However, the optional gesture recognizer delegate can perform logic to determine if two or more gesture recognizer can work at the same time. The method is called gestureRecognizer(gestureRecognizer: UIGestureRecognizer, shouldRecognizeSimultaneouslyWithGestureRecognizer otherGestureRecognizer: UIGestureRecognizer) -> Bool. I always just return true so they an work at the same time.

However, this created a bug with the UIPanGestureRecognizer. If you have two fingers on the screen (to do a pinch or rotate gesture) and then you lift a finger up and place it down, the UIPanGestureRecognizer  doesn’t know which finger to track and it causes the node to jump from one finger to the other. So I had to change how the recognizer logic works. Before I was always using func locationInView(view: UIView) to find out where the users finger was and then move the node around. However, UIPanGestureRecognizer also provides func translationInView(view: UIView) which returns only the change from the original locationInView. So I created another property that is set when the gesture begins with the locationInView. Then in the changed state, I use the original starting point plus the tranlationInView to figure out how much to move the Node. That way when the finger changes (and this the location in view) in the middle of a pan gesture, the Node doesn’t “jump” from one finger to the other.

As you can see in the video, its impressively smooth. Next is to make the nodes regenerate higher quality imagery when they are zoomed in.