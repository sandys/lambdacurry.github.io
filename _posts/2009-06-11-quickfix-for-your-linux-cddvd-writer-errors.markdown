---
author: sandeep
comments: true
date: 2009-06-11 07:32:52+00:00
layout: default
link: http://www.lambdacurry.com/2009/06/quickfix-for-your-linux-cddvd-writer-errors/
slug: quickfix-for-your-linux-cddvd-writer-errors
title: Quickfix for your linux CD/DVD writer errors
wordpress_id: 261
tags:
- linux
- ubuntu
---

Are you getting


<blockquote>Buffer I/O error on device sr0</blockquote>


Change your [grub boot options](https://help.ubuntu.com/community/BootOptions#Change%20Boot%20Options%20Temporarily%20For%20An%20Existing%20Installation) to add


<blockquote>all_generic_ide=1</blockquote>
