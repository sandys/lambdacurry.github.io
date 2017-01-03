---
author: admin
comments: true
date: 2013-12-27 12:14:37+00:00
layout: post
link: http://www.lambdacurry.com/2013/12/aptitude-equivalent-of-apt-get-autoremove/
slug: aptitude-equivalent-of-apt-get-autoremove
title: Aptitude equivalent of "apt-get autoremove"
wordpress_id: 858
---

As I am moving away from Ubuntu towards base debian, I am realigning my workflow to work better in the latter. The biggest being, unsuprisingly, package management.

One of the biggest cons against aptitude was that it does not do "autoremove" as apt-get does. This actually turned out to be false and more of a planned design choice (read more here - http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=683866)

In essence the aptitude equivalent is "sudo aptitude -oAptitude::Delete-Unused=1 install"
