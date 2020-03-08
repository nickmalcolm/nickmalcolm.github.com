---
title: "Advancements in Android's Trust and Authentication platforms"
excerpt_separator: <!--more-->
---

<div class="alert">
<strong>Note:</strong> This post was written for and originally published on the <a href="https://thisdata.com">ThisData</a> blog in 2016. Ages ago! I have reposted it here in case it's useful in the future.
</div>

Passwords and pin numbers are so annoying that most people don't use them on their mobile devices. Passwords for online accounts are often forgotten and reused. It's an environment where users expect safety, but the cost is too high. Google is trying to do something about that.  Android usually gets a bad rap in the security community, primarily because the platform relies on vendors to push out updates, leaving many many people with insecure phones. But at Google I/O this year and last, Android has proved they're taking some massive steps forward in the authentication space, and it's pretty exciting.


> 70% of users forget their password once a month, and on average try 2.4 passwords before we get the right login
> 
> \- [Regina Dugan - Google SVP](https://www.youtube.com/watch?v=lGrRYnqHegc) in 2015

In this post we're going to take a quick look at what Google has been doing in this space, and in particular their new Trust API which enables continuous authentication. <!--more--> _Caveat: I haven't owned an Android device for a few years now, so haven't been able to play with these new features. But they're cool enough that I want to write about them anyway!_.


## Smart Lock

[Smart Lock](https://get.google.com/smartlock/) is Google's most widely known initiative in removing the need for passwords. It has five different detection categories, and not all of them are available on all devices. In all cases, if it thinks it isn't you, it'll fall back to asking for a fingerprint, password, or pin to unlock your device. It has reduced on screen prompts by 50% for devices which have turned it on.
  
*   **On-body detection** - uses an accelerometer to detect that you're holding it in your hand, and that a thief hasn't snatched it from you and ran away. It also looks at _how_ you walk, so that even if it's not snatched and zoomed away from your body, it can still detect that the attacker's pattern of movement is off. But if you hand your unlocked device to someone, and they're not moving around, it'll probably stay unlocked.
* **Trusted places** - manually configure a whitelist of locations that your phone is allowed to be unlocked in. Requires intensive GPS location checking, though [their documentation](https://support.google.com/nexus/answer/6093922) makes it sound like it might also use the presence of the WiFi network instead of GPS?...
* **Trusted devices** - lets you choose some devices which, when nearby, are a sign of trust. Bluetooth watches, fitness trackers, or car speaker systems are good candidates.
* **Trusted face** - uses facial recognition to unlock your device
* **Trusted voice** - uses voice recognition to unlock your device

The only one that sounds like an OK idea to me is the trusted place in-car unlock, otherwise the locations are too broad and easy for an attacker to get in to. I'd also love to have phone-snatch detection which locks the phone, without having the flipside of an automatically unlocking phone when it thinks its held in my hand.

Any of these by themselves aren't going to provide great security, and Google knows that too. So they kept working on the problem.



 
## Project Abacus

Project Abacus was announced at Google 2015, which took the ideas and sensors above and combined them to create high-entropy source of authentication. Authentication by not what you remember, but by how you behave. It would provide a risk score which indicates how likely it is that the user is who the device thinks it is, taking in to consideration the context of what you're doing and how you're doing it. And this risk score can influence the actions you're allowed to take. It's behavioural, adaptive, contextual authentication. (Buzzword bingo!).

> An authentication method that accepts you, and rejects impostors, right on your device

But it's more than buzzwords. Google gathered some boffins from 16 universities, and handed them a dataset of 2.8 million sessions for 1500 users. Their proof of concept resulted in a method of authentication that was 10 times more accurate than a fingerprint alone.

![](/assets/images/160802-android-trust-score-combined-graph.png)

## Trust API

At I/O 2016, we got an update on Project Abacus from Dan Kaufman, head of Advanced Technology and Projects at Google. It's now been rebranded as the "Trust API", and as of June has been in private beta with "several large financial institutions". The aim is to have it available to Android developers worldwide by the end of the year.

> We have a phone with all these sensors. Why can't it just know who I am?
> <br />
> _Deepak Chandra - Google_

![](/assets/images/160802-android-trust-score-adaptive.png)

## Where to now?

Now we get to wait and see! Learning a users' behaviour as a way to make authentication easier is a really exciting area of research which is now becoming mainstream. Google is leading the charge with device & sensor based behavioural authentication. I like to think that we're doing something pretty cool at ThisData too for helping websites protect their users, so if this post has got you interested [check us out!](https://thisdata.com)


**Google I/O Videos:**
  - [Project Abacus at I/O 2015 [6:09]](https://www.youtube.com/watch?v=lGrRYnqHegc)
  - [Smart lock [starts at 12:50]](https://youtu.be/XZzLjllizYs?list=PLWz5rJ2EKKc8jQTUYvIfqA9lMvSGQWtte&t=760)
  - [Trust API at I/O 2016 [starts at 4:55]](https://www.youtube.com/watch?v=8LO59eN9om4&feature=youtu.be&t=295)