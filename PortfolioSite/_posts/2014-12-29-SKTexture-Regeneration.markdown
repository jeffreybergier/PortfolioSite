---
layout: post
title:  Regenerate SKTextures when Zooming
date:   2014-12-29
author: Jeffrey Bergier
tags: SpriteKit, iOS Development, iOS, Swift, Xcode
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2014-12-29-SKTexture-Regeneration-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2014-12-29-SKTexture-Regeneration-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2014-12-29-SKTexture-Regeneration-02.mp4">Click to download the video.</a>
</video>

SKTextures now regenerate when zooming in or out. This was pretty simple to accomplish. All of the planets are embedded in a Subclass of SKSpriteNode. This subclass monitors the xScale and yScale properties. When they are changed, it iterates through the array of all its children to inform them that their parent changed its scale.

I didn’t want new SKTextures to be generated every time the scale changed. The scale will usually change many time per second, so generating textures at that rate would be silly. So instead, I use an NSTimer system to wait for the scale to stop changing before generating a new SKTexture.
Once one of the planets receives a new scale, it checks to see if the NSTimer property has been set. If it has, it does nothing. If it hasn’t it creates a new NSTimer object.

The NSTimer checks to see if it should wait for more changes in the scale. If it should wait, it changes the shouldWait property to false so that the setScale function can change it back to true. If the shouldWait property is false, the timer invalidates itself (to remove any strong references) and then changes the property to nil. At that time it updates the SKTexture with the new scale value (not shown).
This seemed like the best way to allocate the minimum number of NSTimers needed in order to accomplish the same effect as regenerating the texture after every scale change.