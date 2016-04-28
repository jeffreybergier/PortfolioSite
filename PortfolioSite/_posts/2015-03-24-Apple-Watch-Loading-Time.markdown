---
layout: post
title:  Apple Watch Loading Time
date:   2015-03-24
author: Jeffrey Bergier
tags: Apple Watch, Watch, ⌚️, WatchKit, iOS Development, iOS, Swift, Xcode
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2015-03-24-Apple-Watch-Loading-Time-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2015-03-24-Apple-Watch-Loading-Time-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2015-03-24-Apple-Watch-Loading-Time-02.mp4">Click to download the video.</a>
</video>

Watch Performance Testing. Its pretty much impossible, and I’ll tell you why. But first we need to remember the core components that make up a WatchKit application.&nbsp;
	1. The iOS App.
		1. This is the heart of your user’s experience. It runs on the phone, it download data from the network, it crunches numbers, it detects motion, etc. This is what we all think of as apps.
	2.  The iOS App WatchKit Extension.
		1. This is a small app that runs **on your user’s iPhone **when your user launches your WatchApp on their watch. This is the thing you are programming when you are working in Xcode on your Watch app.
	3.  The Watch “App.”
		1. I put App in quotes because this app runs none of your code. Its important to remember this distinction because when you do performance testing during Watch App development, you are doing performance testing on item 2 in the list. You are testing the performance of the WatchKit Extension that is running on your user’s iPhone. Not what they are running on their watch.
This is a problem because iPhones don’t have trouble loading 200 really basic UITableViewCells into memory. (I know they don’t do this anyway because of DequeReusableCell). But the point remains that the bottleneck on your Watch app is probably not going to be the iPhone, its going to be the Watch.

The Watch “App” is basically a smart external display for the Watchkit Extension. When you load a table of 200 items onto the watch, your WatchKit Extension is producing 200 Table Row Controllers and quickly sending those 200 rows one by one to the Watch wirelessly with no idea when they finish (as far as I can tell). Since you have no callback when they finish, its almost impossible to do performance testing. When your WatchKit extension finish loading 200 rows and sends the rows to the Watch “App”, your WatchKit extension thinks its done all of its work and all of its state has been changed, yet the Watch still hasn’t updated its display.

When I did performance testing, making the rows, configuring the rows and then sending them to the display took the iPhone only 0.2 seconds. However, the watch took at least 3 seconds to actually update its UI. I say at least 3 seconds because there is no way to time it except with (ironically) a stopwatch and a keen eye.

Luckily, it seems the Watch is very good about doing these commands in order. So in my case, I send X number of rows to the watch and then tell the loading animation image view to hide. This always happens after the rows finish being sent to the watch because my WatchKit Extension send the hide command after the row commands.

Also, I’m not supposed to say this because I went to [REDACTED] labs. But the Simulator does a very good job of emulating the connection speed between the WatchKit Extension and the WatchKit App (display). That means that you shouldn’t have to be too worried about your app being way too slow if you don’t get to test it on hardware before launch day.