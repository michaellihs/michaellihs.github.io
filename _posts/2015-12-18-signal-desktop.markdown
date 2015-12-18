---
layout: post
title:  "How to install Whisper Systems Desktop from Github"
summary: "This blog post explains how to install the Whisper Systems Signal Desktop in the Chrome browser from Github"
date:   2015-12-18 13:30:00
categories: tools
tags: ['developer', 'extension', 'chrome', 'signal']
---

[Signal](https://whispersystems.org/) is a messenger currently available as an [Android](https://play.google.com/store/apps/details?id=org.thoughtcrime.securesms&referrer=utm_source%3DOWS%26utm_medium%3DWeb%26utm_campaign%3DMessaging) and [iPhone](https://itunes.apple.com/us/app/signal-private-messenger/id874139669) app. There is a [public beta program for a desktop version](https://whispersystems.org/blog/signal-desktop/) that runs in Google's Chrome browser. The waiting list is rather long so it might take a while to actually get you in. This article describes how you can install the Chrome plugin from sources - i.e. without waiting in line for the public beta.


Disclaimer
----------

The plugin currently only seems to work with Android phones. Since I have an iPhone, I can not verify that the Signal Desktop is actually working after what I explain here.


Getting the sources
-------------------

Go to the [Signal Desktop Github Project](https://github.com/WhisperSystems/Signal-Desktop) and clone the sources to a local repository using the following command:

    git clone https://github.com/WhisperSystems/Signal-Desktop.git

As an alternative you can use the [Download as Zip Button](https://github.com/WhisperSystems/Signal-Desktop/archive/master.zip), download the extension as a Zip file and extract it on your computer.

Now open your Chrome browser and click on the Menu ("the three lines") -> More Tools -> Extensions. Click the "Developer mode" checkbox and then click the button labeled "Load unpacked extension...". Select the folder to which you cloned or extracted the sources. That's it, the extension is loaded.


Acknowledgement
---------------

The Signal messenger is free to use but their developers have expenses, too. Support them by [donating some coins](https://www.coinbase.com/checkouts/51dac699e660a4d773216b5ad94d6a0b) if you like their work!

Thanks to [Matt Cutts](https://www.mattcutts.com/blog/) for sharing the solution of [loading a Chrome extension from sources](https://www.mattcutts.com/blog/how-to-install-a-chrome-extension-from-github/). I did not know that before.
