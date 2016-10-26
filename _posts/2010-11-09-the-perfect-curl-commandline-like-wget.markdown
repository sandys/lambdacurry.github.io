---
author: sandeep
comments: true
date: 2010-11-09 06:16:04+00:00
layout: post
link: http://www.lambdacurry.com/2010/11/the-perfect-curl-commandline-like-wget/
slug: the-perfect-curl-commandline-like-wget
title: The perfect cURL commandline (like wget)
wordpress_id: 465
tags:
- curl
- name
- resume
- wget
---

<blockquote>﻿﻿curl -C - -OLR <URL></blockquote>


What this does is:



	
  1. Resume any broken/failed/paused download (drop the "_-C -" _otherwise)

	
  2. Write the output to a file which is named the same as on the server (you can drop the "_-O" _and instead use "_-o <filename>"_to redirect to a filename of your choosing)

	
  3. Sets the remote file time on the local file (drop the "_-R_" otherwise)




Just as a side note, one of the solutions for resuming a paused download in curl is to use


<blockquote>cat file-that-failed-to-download.zip | curl -C - http://www.somewhere.com/file-I-want-to-download.zip >successfully-downloaded.zip</blockquote>
