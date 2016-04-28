---
layout: post
title:  WKInterfaceController Loading Animations
date:   2015-03-13
author: Jeffrey Bergier
tags: Apple Watch, Watch, ⌚️, WatchKit, iOS Development, iOS, Swift, Xcode
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-02.mp4">Click to download the video.</a>
</video>

Advanced InterfaceController loading animations. By default, WatchKit Interface Controller loading is pretty bad. Its just a generic spinning thing that sits there until willActivate() finishes. Play the video above. The default behavior is the left most interface. I found a secret weapon to stop this behavior. There is a strange checkbox for each Interface Controller in the Storyboard. Its called “Hides when Loading” and its checked by default.

![image]({{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-03.png)

Unchecking this causes the Interface to show the storyboard verbatim until willActivate() finishes. This gives you the ability to show an empty version of your UI and then populate it with willActivate(). Because my interface is a table and I saw no way of easily building a placeholder table in storyboards, I put a new group that takes up the whole screen. It has a background image that matches the app. Then in willActivate(), at the very end, I hide the image and show the other interface elements. This is the middle screen in the video above.

![image]({{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-04.png)

However, I really wanted something more. I created a step by step animation for an indeterminate loader. I then put that image in the storyboard and started to animate it at the very top of willActivate(). However, the animation wasn’t starting until willActivate() finished. This was a problem because I wanted the loader to spin while willActivate() was doing its thing. I broke out most of willActivate() into a private function. Then in willActivate(), after I start the animation for the loader, I call that function on a background thread. That function then does the appropriate work that it needs to do. The function also calls back to the main thread before touching the UI. The screen on the right shows the effect.

![image]({{ site.baseurl }}/blog-post-assets/2015-03-13-WKInterfaceController-Loading-Animation-05.png)

The effect is a big improvement. The default loader lets the user know that something is happening, but its not branded. The middle solution is branded but doesn’t let the user know that work is being done. The advanced solution satisfies both of these problems. Also, it seems like the generic spinner is also used when the Watch has a bad connection to the phone and they are trying to communicate. Using your own loader will also train the user that the generic spinner happens when things might fall apart. Whereas your loader will happen when things are working normally. 