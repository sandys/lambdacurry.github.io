---
author: sandeep
comments: true
date: 2012-01-13 12:15:07+00:00
layout: post
link: http://www.lambdacurry.com/2012/01/apt-get-through-a-http-proxy/
slug: apt-get-through-a-http-proxy
title: apt-get through a http proxy
wordpress_id: 575
---

God - this bugged me no end at my workplace. Especially the interplay of sudo, loading environment variables, etc. with http proxy.

Rule of thumb is - sudo (if present) should be the first command, http_proxy (if present) should be the second and then the rest of the actual command

Effectively, it is something like


<blockquote>sudo http_proxy=http://1.1.1.1:80 apt-get update</blockquote>





