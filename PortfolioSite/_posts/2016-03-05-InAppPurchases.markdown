# In-App Purchases in Swift: Part 1
## Summary

This is the first of several posts on handling In-App purchases in iOS apps in Swift. These posts will be pretty high-level: there will be more concepts than code. For the big [Gratuity](http://gratuity.saturdayapps.com) update that I just submitted to the App Store, In-App Purchase was the single largest set of code that I added. I use the IAP to enable the Split Bill feature of Gratuity. I can assure you that the code to handle the IAP is far larger than the code for the feature. I would advise to proceed with caution if you want to add IAP. You should be sure you will make money from it because its tough.

So lets get started :)

## Application Receipt

**What is it?**

The application receipt is the “single source of truth” for the purchase of the app from the App Store and for each Non-Consumable In-App Purchase. Non-Consumable is Apple’s term for an IAP that can only be purchased once and persists across devices and install. The opposite is a Consumable purchase. Those are for purchases that are more ephemeral. Think fake currency in a click-bait game: Those are consumable. Consumable IAPs are not in the receipt so you have to take more care with them. I only dealt with Non-Consumable IAPs. If you’re interested in one of the other myriad types, this post may not be super helpful.

Just remember, the receipt is the source of truth. I used that as a key part of my code. I designed the logic so that the receipt is checked during application launch. I also check the receipt whenever the user tries to start a new purchase or restore existing purchases. I also check the receipt again after any restore or purchase request finishes.≈

**Wait! its missing‽**

The receipt is not always there: this is normal. For example, when installing via Xcode (while debugging) its not there. Also, if the user installed the  app by syncing with iTunes, its not there. So don’t write logic that requires a receipt. It is normal for it not to be there.

If its not there, you should allow the app to do as much as possible for your business model without the receipt. The more your app costs, the less you should allow without a receipt. The cheaper your app is, the more you should optimize for a smoother user experience without the receipt.

Once you have determined that you need the receipt to verify purchases before allowing the user to continue, you should present a view that allows the user to tap a “Restore Purchases” button. This is the only way to get the receipt from the App Store if it is missing.

Now, you’re asking “why do we need to present the user a screen? Isn’t it a better experience if we load this receipt silently in the background?” Well… you can’t. Restoring often times requires the user to put in their app store password or Touch ID. Obviously, this is quite alarming to the user. Also, if it happens during app review (another time that the receipt WILL be missing) then they WILL reject your app.

**How Do I Verify the Receipt?**

Apple provides no “built-in” way to do this. Apple says that they don’t provide this behavior because malicious people would be able to easily circumvent all receipt validation. This is definitely true. However, it makes it pretty hard for a normal person, who probably has little to no security concerns, to do this on their own. I would have preferred an easy built-in system that beginners could use and professionals could ignore.

The receipt is saved using industry standard encryption formats. But just because they’re industry standard does not mean they are easy to deal with. Swift makes this a little harder because its newer and there is not as much stuff out there for handling encryption keys. Also, the standard OpenSSL project does not appear to work with Cocoapods and Swift.

Luckily there is a working [OpenSSL Swift Library](https://github.com/krzyzanowskim/OpenSSL) from krzyzanowskim that can be included in your Podfile. Then there is an open source project built for handling In-App Purchases called [RMStore](https://github.com/robotmedia/RMStore). This can’t be included in your Podfile because it requires the official OpenSSL project which I couldn’t get to build. Also, most of the framework is for handling purchases instead of verifying receipts.

I installed the smallest portion of RMStore .h and .m files into my project in order to verify receipts. The file I ended up including in my project are below:

![image](https://41.media.tumblr.com/32386f815e283f14da9a9033249850f5/tumblr_inline_nxirktEkgM1qa8wtk_540.png)

**But wait, RMStore Sucks at Verifying Receipts**

This is true, but it can be made better. By default, RMStore loads the Apple Receipt Certificate from the App Bundle. If the certificate is not found, RMStore just return YES to the receipt being valid. Obviously I didn’t want this. So I changed the logic so if the receipt was NIL, the validate receipt method would return NO.
![image](https://41.media.tumblr.com/942772349a0c833c0708fe7851776bd2/tumblr_inline_nxirlsMpZj1qa8wtk_540.png)

Then, just to be safe, I obscured the certificate in a string in the code. So instead of RMStore loading the certificate from bundle, I had it load the certificate from a string that I hardcoded into RMAppReceipt.m. This is totally optional, but it makes it so that a would-be pirate can’t simply replace the Apple certificate in your bundle with a certificate they made that verifies the false receipt they also made.

**RMStore is Crashing My App**

This also happens. Objective-C code without nullability annotations imports all types as implicitly unwrapped optionals! This is bad, because they cause crashes. Make sure to if let all the return types. Or you can follow the instructions at [NSHipster](http://nshipster.com/swift-1.2/) to mark all types as NULLABLE.

**Ok, the receipt is verified, where are my IAP?**
![image](https://40.media.tumblr.com/44dd01c363dfc3e3b5f3d3d52916f0b5/tumblr_inline_nxis17Ck4c1qa8wtk_540.png)

The RMStoreReceipt object can give you an Array of RMAppReceiptIAP objects. You need to get that array and then iterate through it. For every receipt inside the array, you can check if they have the same identifier as the IAP that you’re interested in. If so, then the item has already been purchased. If not, then the receipt shows no evidence of the IAP having been purchased by the user.

This verification is how I verify the user has purchased the IAP. I check it on launch, I check it when a user initiates a purchase / restore request. I also check it when a restore / purchase request finishes. I find this the easiest, most reliable way of verifying Non-Consumable IAP. Again, for other type of IAP, you may need more complicated logic.

**How do I Ask the User to Buy Something?**

Setting up the View Controller took a while. Handling the edge cases took even longer. This is coming up in the next blog post.
![image](https://41.media.tumblr.com/faf1ec15b6bf6d7c2af70d6cd70756b4/tumblr_inline_nxirxhIzI51qa8wtk_540.png)