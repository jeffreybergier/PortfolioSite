---
layout: post
title:  Playing with SpriteKit
date:   2014-12-21
author: Jeffrey Bergier
tags: SpriteKit, iOS Development, iOS, Swift, Xcode
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2014-12-21-Playing-with-SpriteKit-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2014-12-21-Playing-with-SpriteKit-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2014-12-21-Playing-with-SpriteKit-02.mp4">Click to download the video.</a>
</video>

I’ve been playing with SpriteKit and its physics engine. I thought a first easy step would be to build a little Solar System. I’m not super concerned with accuracy or making sure all the planets move at exactly the right speed. I just wanted to get planets (Nodes in SpriteKit parlance) spinning around the sun. The first hurdle was that the SpriteKit physics engine doesn’t cause individual nodes to have their own gravity based on their mass. So Nodes can’t float towards each other. The second hurdle was that the gravity on the scene can be set but you can’t change the center of gravity. Gravity always goes towards one edge of the screen.

So I thought the next thing I would have to do is “Add an Impulse” which pushes the Node in a direction. I could do the math to make sure that impulses that occur every frame would push the planet in a direction so that the distance from the sun was always maintained. I couldn’t even begin to think about how complicated this math would be :-/

Instead, I found out about SKPhysicsJoints with can attach two Nodes to each other. So now I use a joint between each planet and the sun. Then I apply impulses and the distance is always maintained. I just have to check the location of the Node to make sure I’m pushing the impulses in the right general direction. It works pretty well, but I’m worried it will be too inflexible later.
Next is to make pinching for zooming in and out work on the solar system.