---
author: sandeep
comments: true
date: 2010-02-26 08:10:26+00:00
layout: post
link: http://www.lambdacurry.com/2010/02/unslowable-linux/
slug: unslowable-linux
title: Unslowable Linux
wordpress_id: 334
categories:
- linux
- ubuntu
tags:
- linux
- overcommit
- RAM
---

For the past week, I have tuned my linux installation to be unslowable - it honors my available RAM and swap and if memory goes low, any new processes terminate rather than thrash (inherently slowing down my system)  There is a bit of tuning involved in this: the key parameters involved are  (in _/etc/sysctl.conf_

)


<blockquote>﻿﻿﻿﻿﻿﻿vm.overcommit_memory and vm.overcommit_ratio</blockquote>


These variables control the behavior of memory allocation and the amount of memory being legally allowed to be requested.  _overcommit_memory _controls the behavior of memory allocation (which, at the end of the day happens through _sbrk_). Setting it to 2, indicates that if the system is out of memory, then _malloc_ should return null.

Surprisingly, this is **not ** the default behavior - it relies on the fact that a program may request 100mb but it is only using 50mb at any given time. Therefore a system has more memory than its swap + RAM.

This does not always play well with heavy loads on a machine - especially 20 tabs browser with flash + Ruby server processes + MySQL. This particular setting means that individual processes may terminate rather than hanging your machine, but you will never have an unresponsive system.

Setting this to 100 gives you exactly RAM + Swap. This is highly pessimistic, since it is true that a lot of processes demand more memory than they need. I have had best results on my machine (with 2GB RAM and 1GB swap) by setting it to 200.

_overcommit_ratio _is the amount of memory that can be requested by your system. With _overcommit_memory _as 2, this turns out to be:


<blockquote>

>     
>     CommitLimit = (RAM * (overcommit_ratio / 100)) + Swap
> 
> 
</blockquote>


Using these settings, I can run a browser with multiple tabs, Ruby servers, MySQL and a few other processes. I will be playing with this number to account for heavy duty VirtualBox, etc. But essentially it tells me the point at which my system will slow down... the better solution is to add more RAM (which I cant in my old laptop... waiting for newer laptops with nVidia and USB 3.0 !) .. but that is a whole different story.
