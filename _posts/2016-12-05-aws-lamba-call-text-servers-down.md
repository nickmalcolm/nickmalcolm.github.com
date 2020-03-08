---
title: "Using AWS Lambda to call and text you when your servers are down"
excerpt_separator: <!--more-->
---

<div class="alert">
<strong>Note:</strong> This post was written for and originally published on the <a href="https://thisdata.com">ThisData</a> blog in 2016. Ages ago! I have reposted it here in case it's useful in the future.
</div>

Getting a phone call in the middle of the night when your servers are on fire is a necessary evil for many developers and network administrators. If your site is being used around the world, then it needs to be available 24/7. Paid incident management tools exist, like PagerDuty, VictorOps, and OpsGenie. They handle escalating incidents through your team, and notify via multiple channels. Cabot and OpenDuty are open source equivalents you can self-host.

Our team is pretty small though, and I thought it'd be fun to see how easy it'd be to get a simple incident alarm going with AWS SNS, AWS Lambdas, and Twilio. Hint: very easy. Best of all it's serverless, so there is nothing to maintain. You don't have to worry about your incidence response server going down! In this post I'll walk you through how to achieve this yourself. 

**Ingredients:** an AWS account and a Twilio account with a voice-capable phone number.<br />
**Cooking time:** 15 minutes.<br />
**Result:** you'll get a voice call and a text message when your service is down / degraded.

<!--more-->

## Set up a new SNS

Simple Notification Service, or SNS, is Amazon's push messaging service. It is here that we create a "Topic" which describes how to notify us. 

  1. Open up the AWS console and head to SNS.
  1. Click "Topics", then the "Create new Topic" button.
  1. Name it "Incident\_Response" and give it a description like "Notifies the CTO via Lambda and text message".\
  1. Click on your newly created Topic.
  1. Click the "Create Subscription" button.
  1. Click the "Protocol" dropdown, and choose "SMS"
  1. Type in your phone number, including area code. 

Easy! You have an SNS topic which, when triggered, will send you a text message. The text message will always contain the name of the CloudWatch alarm, which provides some context to tell you what's on fire. _Fun note: this is powered by Twilio behind the scenes too, but you don't need a Twilio account!_

We could leave it at SMS messages, but they aren't enough to wake me up at night. I need a phone call buzzing.

## Create the Voice Call Lambda

Create the Lambda:
Open Lambda in the AWS console.
Click the "Create a Lambda function" button.
Choose the "Blank template" blueprint.
Configure an SNS trigger by clicking the grey box outline, and selecting "SNS" from the bottom of the dropdown menu.
Select your _"Incident\_Response"_ topic.
Tick the "Enable trigger" checkbox, which will configure all the necessary Lamba permissions and create the "subscription" in your SNS topic.
Click Next.
Call your function "notifyCTOWithVoiceCall"

Time for some code! Copypaste [this code](https://gist.github.com/nickmalcolm/6be8956dae3e955f19b8fec56336e147) into your lambda: 
<script src="https://gist.github.com/nickmalcolm/6be8956dae3e955f19b8fec56336e147.js"></script>

You'll need to update the `toNumber` variable in the code above, and add three environment variables which contain your Twilio credentials. You can also encrypt these variables using the encryption helpers.

At the top of the page, hit the "Save and Test" button. You should get a voice call which talks to you, then plays a song! If not, take a look at the "Log output" area. It should have completed successfully and show Twilio's response, or any error messages. If that looks OK, log in to Twilio and check the debugger there.

At this point you have an SNS topic which will send you an SMS message and trigger a Lambda function which calls you. Now it's time to put it to use!

## Configure your CloudWatch alarms

The easiest way I found to do an end to end test is to create an alarm you know will fail. Head over to AWS CloudWatch.

Click "Alarms" in the sidebar, then the blue "Create Alarm" button.
Search for a "CPU" metric, and choose one of your instance's "CPUUtilization" metrics.
Click "Next".
Call it "TestAlarm"
Configure a Threshold "whenever CPUUtilization is <= 100 for 1 consecutive period(s)".
Click "Create Alarm"

Since your CPU will be using below 100% (hopefully!) as soon as you click "Create Alarm" you'll get a phone call and text. The phone call will wake you up, and the text message will contain a little bit of context before you get to your emails. Too easy! 

Now you can create new alarms, or update existing ones, for those critical times when you need to be woken up. You've successfully set up a simple incident response tool which is effectively free, and you don't have any extra servers to maintain!

## Where to from here

To take this further, an easy win should be getting more context from the CloudWatch into the voice call. It'd involve looking up how CloudWatch passes those attributes into the Lambda, and then using that in our dynamically generated TwiML.
You could look at storing "on call" information in a DynamoDB, and get Lambda to look up who it should call based on the day. You could also use Dynamo, or even Twilio webhooks, to make sure the call is answered / acknowledged, and escalate to another developer when the first line of defence doesn't respond.

I hope that's helped you - let me know how you get on!
