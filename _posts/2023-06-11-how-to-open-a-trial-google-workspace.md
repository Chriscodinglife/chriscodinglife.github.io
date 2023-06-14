---
title: How To Open A Trial Google Workspace
date: 2023-06-11 7:00:00 +0000
categories: [Google, Workspace, SSO]
tags: [google workspace, admin console, trial] # TAG names should always be lowercase
author: chris
pin: true
toc: true
---

Setting up a Google Workspace environment is quick and easy, and can definitely help if you are learning IT and want to setup a test environment that is not tied to your job. _We can break stuff ....for free_

## How to Open a Trial Google Workspace

### Just some gotchas I should mention

- Google Workspace has a trial for 14 days
- The cheapest tier is about $6 USD a month
- You will need a domain (don't worry we can cover that here too)
- The domain might cost 10 to 20 bucks+ for the year
- In total you will only pay for a domain for this tutorial

### A quick rant though...

If you have ever tried opening an [Okta Developer](https://blog.chriscoding.app/posts/how-to-get-free-okta-dev/) account, one thing that might stand out to you right away is that the "Free" experience is really missing with Google Workspace. For some reason Google doesn't give devs free Google Workspace environments to test. 🤷‍♂️

Idk how a big software company like Google doesn't bother to give devs free envs for Workspace. We need a place to test. Even Microsoft provides their admin suite for developers for free?

![whynotfree](https://i.imgflip.com/7ozckg.jpg)

I'll hold back my rant for now and dive right into how you can at least setup a trial Google Workspace environment for you to test with.

## Instructions

1 - Head over to [Google Workspace](https://workspace.google.com/) and click on Get Started

![getstarted](/2023-06-11+10_37_07-Window.png)

2 - Enter your business name. In this case I will just use something like _christest_.

You can really put anything you like tbh. Also put that only you are using it and select your Region, and hit Next.

![businessname](/2023-06-11+10_41_32-Window.png)

3 - Enter your contact information and input an email address you wish to use for this test Workspace, and then hit Next

![contactinfo](/2023-06-11+10_46_25-Window.png)

4 - Now it will ask you if you have a domain. Now in the off chance you actually do have a domain, then you can set it up with yours, but in this tutorial, I will act as if I never had one. (no worries fam I gotchu) 😎

Go ahead and click on "No, I need one"

![domain](/2023-06-11+10_50_25-Window.png)

And then look for a domain name. I will keep mine simple.

**Big disclaimer here though**:

> Depending on the domain name, you might get charged more for the year. So maybe play with the names and select different ones to get a cheaper price.

I will search for "christestworkspace" and select "christestworkspace.net" under the list of choices. Feel free to select the one you like. Once you like your domain name, hit Next.

![selectdomain](/2023-06-11+10_56_50-Window.png)

![domainnext](/2023-06-11_10_59_26-Window.png)

5 - It will ask you for some business info like your location and phone number. After you put your info hit Next.

![personalinfo](/2023-06-11_11_02_01-Window.png)

6 - You can hit "No thanks" on the Educate your users section. They don't need no edumakation.

![whatisschool](/2023-06-11_11_04_20-Window.png)

7 - Go ahead and setup your username and password, and when your ready click on Agree and Continue

![setupusername](/2023-06-11_11_06_39-Window.png)

8 - Now it will ask you to login for the first time. Go ahead hit Next, and Enter your password and hit Next again/

![loginfirstime](/2023-06-11_11_08_06-Window.png)

You might get asked to verify who you are so enter your phone number to continue

![verify](/2023-06-11_11_09_35-Window.png)

9 - After you verify, you will be taken to the TOS of your account, and just hit "I Understand"

![tos](/2023-06-11_11_11_18-Window.png)

10 - ✋(HOLD ON DON'T BUY ANYTHING YET) Idk why, but immediately you might be faced with the recommendation to purchase the Business Standard Plan, and based on the date of this writing, it is costing about $14 bucks? What's worse is that on this pane you can't even select another plan. WTH Google?

![shady](/2023-06-11_11_12_37-Window.png)

More keen users might have noticed that you could have picked the Business Starter plan here under the [Pricing tab for Google Workspace](https://workspace.google.com/pricing.html)

It's 6 USD, way cheaper, but for some weird reason, you can't even make that your default plan when you want to check out if you simply clicked Get Started like we did. SHADY BUSINESS

![shadybusiness](https://i.imgflip.com/7ozh5g.jpg)

But no worries, go ahead and continue to check out, since we have 14 days to try out Google Workspace for Free. You can always downgrade your plan later to the Business Starter plan via this KB here: [Switch to Business Starter](https://support.google.com/a/answer/10069853?hl=en)

Let's click on "Try free for 14 days"

![fineillclick](/2023-06-11_11_26_47-Window.png)

You will see a "Review and Check out" Page confirming your payments, your address info, and where you can input payment information.

Feel free to enter how you want to pay.

![Paymentinfo](/2023-06-11_11_28_28-Window.png)

Neat bit I think is that you can pay with Paypal 💰

![paypal](https://i.imgflip.com/7ozih4.jpg)

If you are wondering what domain registration info private is, this is the DNS provider basically changing up your info in case you don't really want to post on the internet the address your inputting and your personal info. I'd suggest leaving that on.

When you're done click on Agree and Continue (you might need to do some extra steps if you use Paypal, I won't share screenshots of that here)

![confirmpayment](/2023-06-11_11_34_04-Window.png)

11 - Now that your payment was all setup, you can go right into your Google Workspace, so go ahead and click on Start setup

![YEAABOOOIII](/2023-06-11_11_40_46-Window.png)

You will land on your own Google Admin Console. If you are an IT admin, more than likely this will look immediately familiar too you.

## Some closing thoughts

And there you have it, with a few steps, you were able to setup a free "Dev" environment to test out your Google Workspace.

Now we can start panic testing stuff for the next 14 days until our trial is over.

![panicagain](https://i.imgflip.com/7oziyl.jpg)

## More Useful Stuff

- [Google Workspace Admin Help Page](https://support.google.com/a/?hl=en#topic=4388346)
- [Google Workspace Blog](https://workspace.google.com/blog)
- [Duet AI for Workspace](https://workspace.google.com/blog/product-announcements/duet-ai-now-available-preorder)
