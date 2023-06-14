---
title: How To Setup SAML SSO With Okta And Google
date: 2023-06-11 7:00:00 +0000
categories: [Google, Workspace, Okta, SSO]
tags: [google workspace, admin console, trial, okta, developer] # TAG names should always be lowercase
author: chris
pin: true
toc: true
---

In this post I want to talk about how you can setup SAML SSO with your Okta as your main IDP and google as your App/Service Provider.

I am hoping after this guide, you will at least feel way more confident with setting up SAML apps in your Okta environment, and you can flex those 💪 IT muscles at your job, and be like Normon Osborn over here:

![osborn](https://i.imgflip.com/7p05gm.jpg)

## Prerequisites and Gotchas

- An Okta Account (If you don't have one check out my [Okta Dev tutorial](https://blog.chriscoding.app/posts/how-to-get-free-okta-dev/))
- A Google Workspace Env (If you don't have one follow my [Workspace Setup Guide here](https://blog.chriscoding.app/posts/how-to-open-a-trial-google-workspace/))
- I will only go over how to use the "out-of-the-box" Google app in Okta's App Catalog, so this tutorial won't show any custom SAML app setups.

## NERD ALERT

Ok I didn't want to do it but I thought from a (sort of) technical perspective, it's worth knowing what is exactly going on under the hood when you setup a SAML Google app in Okta and a user uses SSO to log in to their Gmail account.

The best analogy I ever came across to help me understand this is the following:

> Your new to California and you know Okta who is incredibly famous. Okta knows Google, and they are really tight friends for years, and Google who owns a cool Dance Club called SpaceWork. You want to get into SpaceWork cuz it's the coolest spot now to hang out at. You know Okta, but you don't know Google, and Google doesn't know you. Luckily for you, because Google and Okta are cool, so Okta tells you to go to Google with a letter he gives you and gives you a name tag to put on your chest as well, where in the letter Okta tells Google that your cool and should be let into the club. So you hop in your car, drive over to Google SpaceWork from Okta and hand the letter over to Google, and he lets you in!

![googleokta](/midjourney1.png)

![SSOBASICALLY](https://i.imgflip.com/7p06lm.jpg)

Let's break down then this analogy and compare it to what happens in real life:

- Your the user (the new person in California)
- Your user account is in Okta, so lets call that user chris@thisoktaenv.com and the Okta URL is thisoktaenv.com
- Google and Okta formed a trust some time prior to you using SSO, and this is actually with an X509 certificate and a SSO issuer URL provided by Okta to Google
- In reality for SSO to work, there has to be an account for chris@thisoktaenv.com in both Okta and Google, so someone had to manually create both, most likely an IT admin or an app admin
- When you sign in to Google via Okta, _Okta redirects you to Google with the same X509 certificate used earlier to form that trust_, and when Google sees you came from thisoktaenv.com with the same X509 certificate, Google can trust your session and log you into your Google account (this is the "letter" in the analogy above).

> Usually third party apps like Google might only need some kind of certificate and SSO URL, but other vendors will let you know if you need more information in order to create the initial trust with that app {: .prompt-info }

Nice so in this case here are some fancy technical terms to throw around that are worth knowing:

- Okta in this case is the Identity Provider or IdP
- Google is the Service Provider or SP
- SAML assertion, when compared to the analogy, is when Okta passes over the "name tag" or usually the NameID, in the form of an email over to Google to match you with the appropriate Google account.
- Most Service Providers a IdPs now a days use SAML 2.0
- In Okta, Google will be considered an "app"

So here is basic flow chart of how SSO is usually setup in this case Google and Okta, and what we will be doing today:

![ssosetup](/2023-06-12_18_27_55-Window.png)

## How To Setup SSO

Now on to the good stuff. Luckily for us Okta has already setup a good portion of the actual SAML setup for us in a preconfigured "app". So let's dive right in, and go ahead and log onto your Okta Admin account and your Google Workspace Admin account to get started

1 - Click on the Hamburger menu item on the top left, then click on Applications > Applications > then Browse App Catalog

![appcatalog](/2023-06-12_18_32_44-Window.png)

2 - Search for the term `Google` and look for app "Google Workspace". In the next window, click on the " Add Integration" button

![googleapp](/2023-06-13_17_59_13-Window.png)

![addapp](/2023-06-13_18_48_07-Window.png)

3 - Here we will need to setup the initial app settings such as the Google domain and which apps we want to show to our users like Gmail and Drive. If you haven't already, log into your Google Workspace. Take your domain for your Google Workspace and enter it into the `Your Google Apps company domain` setting in Okta.

Leave the `Display the following links` check boxes alone, but uncheck the `Automatically log in when user lands on login page` setting.

If you are unfamiliar with your domain name for your Google Workspace you can go to the [https://admin.google.com/ac/domains/manage](https://admin.google.com/ac/domains/manage) to see what it is.

We can leave the Application Label as is, and go ahead and hit Next

![domainadd](/2023-06-13_18_58_13-Window.png)

4 - In the Sign On methods options, select the SAML 2.0 setting, and then leave everything as default and hit Done.

![setsaml](/2023-06-13_19_03_04-Window.png)

![donesaml](/2023-06-13_19_04_25-Window.png)

5 - You just created your first app in Okta! (Unless you already have been creating apps) From here you are taken the App settings page. Pretty much if not most of what we need to setup is already done on Okta's side, but now we need to configure Google to trust our Okta account.

> The great bit about IdPs and SPs is that they are paid to make sure you as a customer have a fluid experience in setting up their app and using it, because at the end of the day they want to make sure you stay as a customer. So a lot of vendors will usually have this "out-of-the-box" experience with setting up SSO with their apps in your preferred IdP, in our case, Okta. {: .prompt-tip }

> Even if you don't have a prebuilt app in your Okta catalog for a given vendor, most if not all the time, the vendor will have someone you can work with to get your SSO setup and configured with your IdP and their app. Always reach out to their support team for help and their knowledge base articles as they are the best resources for getting SSO up and running. {: .prompt-tip }

In the app settings page, go to the Sign On Tab and scroll down and click on `View SAML setup instructions`.

![Signontab](/2023-06-13_19_12_48-Window.png)

![samlinstructions](/2023-06-13_19_13_22-Window.png)

6 - This new page you were redirected to might contain a lot of info but scroll down and look for the `SSO profile values` section. These will be values you will need to setup in your Google Workspace.

![ssovalues](/2023-06-13_19_20_08-Window.png)

7 - Click on the Link for your Verification certificate. This will automatically download a .cert file that contains your Okta Google app x509 certificate. You can use an IDE such as Visual Studio Code to inspect your certificate file. We will use this certificate soon.

![certdownload](/2023-06-13_19_46_07-Window.png)

![vscodecert](/2023-06-13_19_51_53-Window.png)

8 - Head over to your Google Workspace and click on the hamburger menu button on the upper left, go to Security > Authentication > SSO with third party IDP

![accessSSOingoogle](/2023-06-13_19_42_31-Window.png)

9 - Here is where you can setup the Trust between Okta and Google by providing Google your certificate and other values. Click on `Add SSO Profile`

![addssoprofile](/2023-06-13_19_54_04-Window.png)

10 - Here under the `Third-Party SSO profile for your organization` setting, check box the `Set up SSO with third-party identity provider`. Then fill in the `Sign-in page URL`, `Sign-out page URL`, and `Change password URL`. Then remember to also upload your downloaded certificate via the `Upload Certificate` button. After setting everything, hit Save.

In this case you won't need the IDP entity ID setting.

![setupssoingoogle](/2023-06-13_19_57_53-Window.png)

And with that, you just setup a trust between Okta and Google!

![party](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzcxMzc4ZTI2MGEwNzc4NGZkNWVkMThkOGZjYzY2YjFiNTNjYTBjOCZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/kHmVOy84g8G6my09fu/giphy.gif)

Let's dive into testing real quick!

11 - Go back to your Okta admin pane for your Google app and go to Assignments, and click Assign and then Assign People.

Here, assign your own test admin account to the Google app, so click on Assign next to the user.

![assignpeopletab](/2023-06-13_20_04_08-Window.png)

![assignuser](/2023-06-13_20_06_15-Window.png)

12 - Now this step is important to make SSO work successfully, unless you already have a test account in Google that matches the same email/username in Okta, then use your admin account in your Google Workspace for this SSO test. Take your Admin email account and assign it as the username in Okta for assigning it to your test Okta account. In my case my email in Google Workspace is `chris@christestworkspace.net` so I will input that as the Username for my Okta account assignment. Replace your current username to your new one as shown below, then press the `Save and Go Back` button. Then press Done, and you will see your user assigned to the Google Workspace App

> Like in our analogy before, this is Okta giving you your "nametag" to tell Google who exactly you are when you are trying to SSO into Google.

![changeusername](/2023-06-13_20_09_50-Window.png)

![pressdoneafterusername](/2023-06-13_20_15_09-Window.png)

![userassigned](/2023-06-13_20_16_49-Window.png)

13 - Click on your Okta apps icon on the upper right, and click on the link "My end user dashboard" which will take you to your Okta user Dashboard to see your SSO apps. Here you should see Google apps available for you to test for SSO! 🎉 (You might need to sign into your Okta account)

![ssoapps](/2023-06-13_20_25_24-Window.png)

Click on your Google Workspace Mail app to test SSO, and you should reach your inbox for your assigned account.

![testsso](/2023-06-13_20_28_27-Window.png)

It might ask you verify that it's you so press on Continue

![continue](/2023-06-13_20_55_40-Window.png)

![inbox](/2023-06-13_20_56_53-Window.png)

And just like that, you just setup your SSO connection between Google and Okta, and verified that the setup works! You can now start assigning other users to Google in Okta and having them login via their Okta Dashboard

## Recap

So in this guide, I showed you how to setup some trust between an app like Google and Okta for SSO. I explained some of the basics about SAML 2.0, and we tested logging in to verify that our SSO setup was successful. Hopefully with this you can now take it to your org or company and show of your new SSO skills.

![itadminz](https://i.imgflip.com/7p9plg.jpg)

## Other useful content

- [Setup SSO instructions from Google](https://support.google.com/a/answer/12032922?hl=en)
- [Generic instructions for Google SSO in Okta](https://saml-doc.okta.com/SAML_Docs/How-to-Enable-SAML-2.0-in-Google-Apps.html)
- [Technical SAML SSO Video](https://www.youtube.com/watch?v=SvppXbpv-5k)
