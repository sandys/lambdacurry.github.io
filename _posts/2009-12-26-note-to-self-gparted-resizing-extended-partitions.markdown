---
author: sandeep
comments: true
date: 2009-12-26 07:40:27+00:00
layout: default
link: http://www.lambdacurry.com/2009/12/note-to-self-gparted-resizing-extended-partitions/
slug: note-to-self-gparted-resizing-extended-partitions
title: 'Note to self: gparted resizing extended partitions'
wordpress_id: 327
---

When resizing extended partitions with gparted - and your extended partition contains your swap partition - make sure you turn off your swap (right click and "swapoff"). Otherwise you will NOT be able to resize your extended partition.

I had a duhh moment, until I realized that the swap partition showed a key/lock symbol next to it - meaning it was in use.
