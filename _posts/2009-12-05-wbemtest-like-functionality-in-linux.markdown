---
author: sandeep
comments: true
date: 2009-12-05 18:01:42+00:00
layout: default
link: http://www.lambdacurry.com/2009/12/wbemtest-like-functionality-in-linux/
slug: wbemtest-like-functionality-in-linux
title: wbemtest like functionality in Linux
wordpress_id: 312
categories:
- linux
- win32
- windows
tags:
- linux
- systeminfo
- wbemtest
- wmi
---

when I was working on the Windows Management Instrumentation (WMI), we got to use _wbemtest _quite a lot. Especially the _root/cimv2 _namspace was good to get information about system hardware.

These days if someone asks me (on a windows machine about how many RAM slots it has, etc., I can look it up in _wbemtest _quick enough.

Call me stupid, but I never knew what the Linux equivalent was - considering Linux addresses everything as a file it was exceedingly straightforward


<blockquote>read bv < /sys/class/sound/card0/device/modalias

echo $bv</blockquote>


or


<blockquote>read bv < /sys/class/dmi/id/bios_version

echo $bv</blockquote>
