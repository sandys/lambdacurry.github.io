---
author: sandeep
comments: true
date: 2007-07-30 17:59:21+00:00
layout: post
link: http://www.lambdacurry.com/2007/07/ubergeek-alsa-sound-on-intel-82801g-sound-cards/
slug: ubergeek-alsa-sound-on-intel-82801g-sound-cards
title: Ubergeek - Alsa sound on Intel 82801G sound cards
wordpress_id: 124
categories:
- linux
---

First compile and build the latest alsa-driver, alsa-lib and alsa-utils (ver 1.0.14). After they are installed:


<blockquote> sudo modprobe -r snd_hda_intel

sudo modprobe snd_hda_intel model=3stack</blockquote>


Well that took a while to figure out!!
