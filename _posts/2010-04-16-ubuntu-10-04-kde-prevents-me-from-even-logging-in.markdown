---
author: sandeep
comments: true
date: 2010-04-16 05:38:21+00:00
layout: default
link: http://www.lambdacurry.com/2010/04/ubuntu-10-04-kde-prevents-me-from-even-logging-in/
slug: ubuntu-10-04-kde-prevents-me-from-even-logging-in
title: Ubuntu 10.04 KDE prevents me from even logging in
wordpress_id: 356
---

oh man, these guys really need to get there act together. After yesterday's update, the machine was booting up but I was unable to log in.

Turns out the issue was that /tmp permissions had been changed and I had to do "chmod ug+rwx,o+rwt /tmp" to set it back appropriately.

sucks..
