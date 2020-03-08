---
title: "An introduction to passwordless logins"
excerpt_separator: <!--more-->
---

<div class="alert">
<strong>Note:</strong> This post was written for and originally published on the <a href="https://thisdata.com">ThisData</a> blog in 2016. Ages ago! I have reposted it here in case it's useful in the future.
</div>

Logging in without a password? It's a pretty unusual idea, but one that is quickly gaining traction. In this post I'll give a quick introduction in to how you might achieve passwordless logins in your own applications by emailing users magic links.

<!--more-->

## What's wrong with passwords?

The traditional method of logging in to a website is by typing in a username and password, but that comes with downsides for users. Remembering passwords is hard, and many users have two to four failed attempts before they remember their password.  Some websites have frustrating and complex password rules. Whether the site has crazy rules or not, so many users set shockingly poor passwords anyway! Users face the risk of their credentials being leaked, and if they reuse passwords across multiple sites, they'll have a bad time. The pros and cons of traditional passwords continues to be thoroughly discussed, but I'll leave that for extra homework.

>  70% of users forget their password once a month, and on average try 2.4 passwords before they get the right login
> <br />
> [Regina Dugan - Google SVP](https://www.youtube.com/watch?v=lGrRYnqHegc)

More tech-savvy users mitigate those risks by using a password manager, but we're in the minority. So what if your users didn't have to remember a password at all?

## How does it work?

It's pretty simple really - instead of a user giving a username and password, they enter their email address. Your application sends them a one-time-use link, which the user clicks on to be automatically logged in to your website.

It means that if someone has access to the user's email account, they have access to your website. It also requires that a user be in a position where they can access their emails.

To keep things secure, similar to a secure password reset process, you'll want to make sure to:

  - Generate a unique, (cryptographically) random, long token, so attackers can't guess it
  - Persist that token in your database, alongside the user's ID, and an expiry time - perhaps 10 minutes
  - Email them a link which includes that token - this is the ✨magic link✨
  - When a user clicks the link, check that the token hasn't expired, create a session for that user, and immediately expire the token
  - Since the token has now expired, the link won't work anymore

For extra points:

  - [Monitor patterns of access](https://thisdata.com). If they click the login button in San Francisco, but the email gets opened in Australia, that's suspicious
  - Support two factor authentication. After they click the link, if they look a little suspicious, ask them for a 2FA code
  - Show your users where their accounts have been accessed from recently

Those extra points are true whether you have passwordless logins or not, but worth reiterating.

It's also worth pointing out that if you want an easy way to achieve this you could get started with an identity platform who support passwordless logins, like Auth0. Check out [how to secure Auth0 with ThisData](https://thisdata.com/blog/how-to-add-suspicious-login-alerts-to-auth0/).

## What are the benefits?

The biggest benefit I see is that your users don't have to set a password - which would be weak anyway - and they don't have to remember a password - because they'll forget it. It's a different way of doing things for sure, but I suspect it might result in a nice engagement improvement. If users can get into your product faster and easier, they'll be happier!

## Is anyone actually doing this?

Yes, **Slack** is one that comes to mind! When you want to log in to a Slack group on iOS, you can be emailed a link which will automatically log you in. [**Medium**, the blog platform, also let you sign in via email](https://blog.medium.com/signing-in-to-medium-by-email-aacc21134fcd#.jpvodrq8v).

![Slack do passwordless logins on their iOS app](/assets/images/160915-slack-magic-sign-in.png)

I'd argue any website that lets users reset their passwords via email is already doing it. Passwordless logins is kinda like a sped up password reset process. You don't remember the password. You enter your email address. You click a link, type some stuff, and you're logged in. That's pretty similar to how passwordless logins work!


## When shouldn't I do it?

There are a few exceptions I can think of. If you have a techsavvy audience who can type in their passwords super fast, or use password managers then it can be frustrating to make them wait for an email to arrive. But if you have a mixed audience, you could make it opt-in.

If your users might be spied on by nation-states or organized criminals then you should already have many layers of authentication, and it might not be wise to stop users from having unique & strong passwords. Emails can still be intercepted fairly easily in quite a few situations.

Or if for some reason your application doesn't have a way to send emails, then... well, you can't send emails!

## Anything else?

Nope! Go have a look at your application, look at your metrics on people forgetting their passwords or failing to log in, look at the demographic of your users, and have a really good think about whether passwordless logins is something you want to try. Let us know how you go!