---
layout: post
title:  Hedging my Apple Watch Design Bet
date:   2015-03-06
author: Jeffrey Bergier
tags: Apple Watch, Watch, ⌚️, WatchKit, iOS Development, iOS, Swift, Xcode
---

<video class="cartwheel" poster="{{ site.baseurl }}/blog-post-assets/2015-03-06-Hedging-Apple-Watch-Design-Bets-01.jpg" controls="">
	<source src="{{ site.baseurl }}/blog-post-assets/2015-03-06-Hedging-Apple-Watch-Design-Bets-02.mp4" type="video/mp4">
		Unfortunately, your browser does not support the video tag. 
		<a href="{{ site.baseurl }}/blog-post-assets/2015-03-06-Hedging-Apple-Watch-Design-Bets-02.mp4">Click to download the video.</a>
</video>

Hedging my bets with Apple Watch. No one knows exactly how Watch will work. Specifically, we can’t simulate how the digital crown works. In Gratuity for iOS, I use long tables of numbers to allow the user to choose Bill Amount and Tip Amount. Well, if long tableviews don’t scroll with the digital crown, then that will be a less than stellar experience. Flicking through a long list on that small screen will really suck. So I built a fallback UI. The fallback UI has 3 buttons you can tap on. Each button represents either the Hundreds place, the tens place or the ones place of the Bill Amount. Once a place is selected, a stepper UI can be used to increase or decrease the amount. The problem is, the app is already shipped, how do I change the UI? 

What I did is I configured the iOS app and the Watch app to check, on launch, a JSON file on my server. This JSON file tells it which interface to use. Once the JSON file is downloaded and parsed, it is written to an NSUserDefaults shared container. Its important to note that the download of this file does not stop launch. The Watch will launch into the UI on disk. All this download does is change whats written to disk. So that on next launch, it might have a new interface.

In any case, I think its a pretty clever idea. Take a look at the video, you can see how simple it was. Note that the UI’s shown in there are basic and unstyled. Hopefully, I can make them look better. Also, the screen capture dropped a few frames when showing the fallback UI. Sorry about that. But I had already tried to record this thing about 6 times and I was done repeating myself.