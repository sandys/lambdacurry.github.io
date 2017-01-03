---
author: sandeep
comments: true
date: 2011-07-02 12:21:51+00:00
layout: default
link: http://www.lambdacurry.com/2011/07/this-is-why-i-love-my-android-phone/
slug: this-is-why-i-love-my-android-phone
title: How to reset your Android bluetooth settings without factory reset
wordpress_id: 544
---

so my bluetooth was acting all wonky - and I really, really did not want to do a factory reset of my phone. My android was not pairing, or pairing and not connecting, etc. etc.

So what do I do ?

I fire up my good ole terminal on my android handset and do


<blockquote>"rm -rf /data/misc/bluetoothd/*"</blockquote>


Reboot and all bluetooth settings are reset.

Awesome!
