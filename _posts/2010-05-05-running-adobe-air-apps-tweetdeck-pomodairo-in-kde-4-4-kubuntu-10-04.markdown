---
author: sandeep
comments: true
date: 2010-05-05 09:25:58+00:00
layout: post
link: http://www.lambdacurry.com/2010/05/running-adobe-air-apps-tweetdeck-pomodairo-in-kde-4-4-kubuntu-10-04/
slug: running-adobe-air-apps-tweetdeck-pomodairo-in-kde-4-4-kubuntu-10-04
title: Running Adobe Air apps (Tweetdeck, Pomodairo) in Kde 4.4 (Kubuntu 10.04)
wordpress_id: 365
tags:
- adobeair
- kde
- tweetdeck
---

So, I wanted to run [Pomodairo](http://code.google.com/p/pomodairo/) and [Tweetdeck](http://tweetdeck.com/go/download/tweetdeck) in my KDE 4.4.2 installation, over Kubuntu 10.04. Adobe gave nice clear directions on what to do and how to install them. I downloaded the .bin file, duly installed it.

It was all crap.

The only way to run Air apps in KDE is using their SDK (not the Air installation file). Download the tar file from [here](http://www.adobe.com/cfusion/entitlement/index.cfm?e=airsdk).  Oh and that tar file needs to be unzipped in a sub-directory and only using _sudo _(asinine, I know). _chown _it back to you.

Then download any _.air _file (for the app of your choice). Unzip it using


<blockquote>unzip <something>.air</blockquote>


Run the whole thing using


<blockquote>﻿<AIR SDK Dir>/bin/adl -nodebug  <air application dir>/META-INF/AIR/application.xml  <air application dir></blockquote>


**P.S. **You may need _python-gtk2 _and _python-gconf_

**P.P.S **The best and viable _[pomodoro timer](http://www.pomodorotechnique.com/) _for KDE4 (or Kubuntu) is [RSIBreak](www.rsibreak.org/). Gnome has its stuff, but somehow RSIBreak doesnt crop up for any pomodoro related searches. It is already in the Ubuntu repositories, so a simple _apt-get_ will install it for you
