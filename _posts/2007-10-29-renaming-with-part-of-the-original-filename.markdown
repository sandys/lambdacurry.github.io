---
author: sandeep
comments: true
date: 2007-10-29 14:29:44+00:00
layout: post
link: http://www.lambdacurry.com/2007/10/renaming-with-part-of-the-original-filename/
slug: renaming-with-part-of-the-original-filename
title: Renaming with part of the original filename
wordpress_id: 131
categories:
- linux
- software
---

quirky ... but necessary. Unless you want to spend hours renaming everything by hand

in short it is:


<blockquote> find . -name *Wac* | awk '{print "mv", """ $0 """ " " $1 "_" $3 "_" $5}' | sh</blockquote>


That came after a lot of trime trying quirky things like:


<blockquote> find . -name *Wac* | xargs -J X `awk '{print $1,"_",$3,"_",$5}'`
find . -name *Wac* | xargs -J X awk '{print $1,"_",$3,"_",$5}'
find . -name *Wac* | xargs -J X `awk '{print $1,"_",$3,"_",$5}'`
find . -name *Wac* | awk '{print $1,"_",$3,"_",$5}'
find . -name *Wac* | awk '{print $0, $1,"_",$3,"_",$5}'
find . -name *Wac* | awk '{print "mv",$0, $1,"_",$3,"_",$5}'
find . -name *Wac* | awk '{print "cp",$0, $1,"_",$3,"_",$5}'</blockquote>


In all honesty, I must also mention [this link](http://www.linuxfocus.org/English/September1999/article103.html), which did point me to the right direction.
