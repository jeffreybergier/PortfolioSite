---
layout: post
title:  Sine and Cosine Plane Rotation
date:   2014-12-23
author: Jeffrey Bergier
tags: Srite Kit, iOS Development, iOS, Swift, Solar System, Xcode, Cosine, Sine
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2014-12-23-Sine-Cosine-Rotation-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2014-12-23-Sine-Cosine-Rotation-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2014-12-23-Sine-Cosine-Rotation-02.mp4">Click to download the video.</a>
</video>

A new way for planets to orbit. A coworker showed me how I can use Sines and Cosines to accurately move an object in a circle. I totally threw out my old code with the Joints and the impulses.

Now I just have a timer that executes a function that does some math and tells the plan to move to the new location. The great thing about this is I can control how often the timer is fired and the planets always move to the right spot. This is better than the old code which was called every frame.

I also use NSDates to calculate how long its been since this function was called and adjusts for it. This does 2 things. First, it lets me change the timing on the timer and the rotation of the planets stays the same speed. The rotation of the earth takes approx 18 seconds now matter what the timer is set for. It just moves in a more “Stop sign” shape if I set the timer to be too slow. Second, if frames are dropped, it will take that into account and the planets will move to the correct spot despite the code not being called. For example. I can set a breakpoint and stop the simulation for a few seconds. When I continue execution, all the planets move to the spot they should have been in if I had never hit a breakpoint.