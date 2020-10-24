---
layout: post
title: "Misuse & Abuse Cases"
date:   2099-10-24 12:00 +1300
excerpt_separator: <!--more-->
---

Most who have worked in an Agile team will be familiar with user stories and use cases. _"As a millenial in their 30s, I want access to 90s cartoons, so I can bask in nostalgia"_. Many teams go further and identify ways a system can be misused or "hacked", and worked to prevent those to make the system secure. But not enough get past misuse cases, and work to keep people _safe_.

In this post - by way of examples - I want to talk about "abuse cases", as distinct from misuse cases. In short: misuse cases are how users might unintentionally or intentionally misuse the features of your product. Abuse cases are how _humans might abuse other humans with_ your product. The features are technically working as intended, but are facilitating abuse. 

<!--more-->

Product teams should consider all three types of use cases when architecting systems, to enable good use cases, and to design ways to prevent, detect, or respond to misuse or abuse. How, you might ask?

<center><strong>Include diverse voices in your team and stakeholders, and listen to their lived experiences</strong><br />&nbsp;<br /></center>

The more diverse the voices on your team, the better placed you are to recall or imagine misuse or abuse cases. Also realise that many people **won't feel safe** to talk about this topic, and you need to be sensitive to that.

The misuse and abuse cases below contain references to the real-life stories, where applicable. I am not the first nor the best person to write about this, so please seek out other voices if this post resonates with you.

## Misuse Cases

Here are some example _unintentional_ misuse cases:

  - As a confused officer, I send a false alarm nuclear alert warning to the entire population of Hawai'i[^1]
      + Prevent: UI & UX improvements, better confirmation message, better test practices
      + Respond: ability to send "oops my bad" after false alarm
  - As a user, I unintentionally send confidential content to a public chat channel, when I wanted to send it via private message
      + Prevent / Detect: automatic rules to detect potentially confidential information (credit cards, passwords)
      + Respond: a way to delete messages
  - As a police department, I want to use the racially-biased facial recognition API to identify potential criminals[^2]
      + Prevent: preclude police from using facial recognition, build unbaised training sets, discontinue the product and consider your life choices

Here are some intentional misuse cases:

  - As a hacker, I intentionally try different usernames and passwords on the login page to access people's accounts[^3]
      + Prevent: rate limiting on the login page, enforcing good passwords, providing users with multi-factor authentication
      + Detect: detect unusual login locations or devices
      + Respond: email users when their account is accessed from a new location/device, prepare for security incidents
  - As a cheapskate, I intentionally look for bugs to give me free stuff
      + Prevent: write comprehensive software tests, start doing code reviews to prevent bugs, get independent security testing done
      + Detect: automate account balancing to identify discrepancies

These stories might be more familiar to us, especially in a security context. We want to prevent our applications from being misused.

Let's take a look at abuse cases then, where the functionality of the application itself is not strinctly being "misused"; it's being used to abuse. 

## Abuse Cases

Here are some abuse cases (all intentional):

  - As an abusive banking customer, I intentionally send multiple $0.01 payments with nasty "transaction details" to my ex, to exert power[^4]
      + Detect: make support teams aware of this scenario ahead of a victim's call coming through
      + Respond: give users the capability to report or block transactions, create a policy to suspend abusive users
  - As an abusive person, I monitor and control my home when I'm not there to intimidate my partner[^5]
      + Prevent: work with domestic violence advocates to design devices such that abused people can take control and/or feel safe at home
      + Detect: [provide means for people to report domestic violence covertly](https://shielded.co.nz/)
  - As a (mean/normal) teenager, I send nasty direct messages to a person from school I don't like[^6]
      + Detect / Prevent: [add a confirmation message when messages look mean](https://web.archive.org/web/20200721195006/https://about.instagram.com/blog/announcements/instagrams-commitment-to-lead-fight-against-online-bullying/)
      + Respond: [allow users to report abusive content](https://web.archive.org/web/20200721195006/https://about.instagram.com/blog/announcements/instagrams-commitment-to-lead-fight-against-online-bullying/)

And these examples aren't even getting into mis- or dis-information, or other types of abuse!

## Closing thoughts

When you next write a user story, think to yourself "what are we doing to make our system _safe_ for the people using it?" 

Remember - this topic brings up real pain felt by people. You can try to start this conversation with your team, but be sensitive. Don't single out team members who might be "more likely" to have answers. Don't force people to talk about it if they don't want to.

A huge caveat: I am just me, and I have only a few examples. I have led a privileged and pretty much abuse-less life! I have written this post because I have worked with too many development teams where this conversation is not being had.

### Read More

  - Start higher level with ["Embracing Evil with Evil User Stories"](https://www.pivotaltracker.com/blog/embracing-evil-user-stories) by [@jeremyjarrell](https://twitter.com/jeremyjarrell)
  - Or dive deeper into ["Misuse Cases: Use Cases with Hostile Intent"](https://www.scenarioplus.org.uk/papers/misuse_cases_hostile_intent/misuse_cases_hostile_intent.htm) by Ian Alexander
  - Or a paper from Auckland University with a different more formal take on the difference: ["Misuse Cases and Abuse Cases in Eliciting Security Requirements"](https://www.cs.auckland.ac.nz/courses/compsci725s2c/archive/termpapers/csia.pdf)

### Books

  - ["Automating Inequality"](https://www.goodreads.com/book/show/34964830-automating-inequality) by Virginia Eubanks
  - ["Shouting Ones and Zeros - Digital Technology, Ethics and Policy in New Zealand"](https://www.bwb.co.nz/books/shouting-zeros-and-ones) by many authors, edited by Andrew Chen

### References

[^1]: Depending on who you believe it was [a UI problem (in small part)](https://www.theverge.com/2018/1/16/16896368/hawaii-false-missile-alert-system-confusing-interface-poor-design) or [the officer believed it was real due to a poorly worded test-message](https://www.theregister.com/2018/01/30/hawaii_missile_drill_attack_real) (2018)

[^2]: Debatable whether this counts as "unintentional misuse" or willfully ignorant, but: [Multiple US police departments were using AWS Rekognition](https://slate.com/technology/2019/07/amazon-rekognition-surveillance-panopticon.html) until [AWS said no](https://www.theverge.com/2020/6/10/21287101/amazon-rekognition-facial-recognition-police-ban-one-year-ai-racial-bias) (2020)

[^3]: [OWASP Cheatsheet on Authentication - Protect Against Automated Attacks](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html#protect-against-automated-attacks)

[^4]: [Commonwealth Bank reveals bullies and domestic violence perpetrators use banking app for abuse](https://7news.com.au/business/banking/commonwealth-bank-reveals-bullies-and-domestic-violence-perpetrators-use-banking-app-for-abuse-c-1078630) by 7news (2020)

[^5]: ["Thermostats, Locks and Lights: Digital Tools of Domestic Abuse"](https://www.nytimes.com/2018/06/23/technology/smart-home-devices-domestic-abuse.html) by NY Times (2018)

[^6]: Netsafe NZ's ["What is online bullying?"](https://www.netsafe.org.nz/what-is-online-bullying/)


