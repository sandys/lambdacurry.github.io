---
author: sandeep
comments: true
date: 2011-12-02 06:05:54+00:00
layout: default
link: http://www.lambdacurry.com/2011/12/timestamp-quickies/
slug: timestamp-quickies
title: Timestamp quickies
wordpress_id: 566
---

To get the current timestamp on your linux machine  (oddly has some problem on my customized zsh shell. works fine on bash)


<blockquote>date +%s</blockquote>


To convert timestamp to date format on your linux machine


<blockquote>date -d @<timestamp></blockquote>


Date to timestamp is


<blockquote>date -d "Dec 21, 2011 22:00:01" +%s</blockquote>


and for heaven's sake when you are using UNIX_TIMESTAMP() function in mysql, please take care about your TZ difference between your OS and mysql.
