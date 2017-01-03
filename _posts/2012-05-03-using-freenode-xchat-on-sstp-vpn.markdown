---
author: sandeep
comments: true
date: 2012-05-03 07:40:53+00:00
layout: default
link: http://www.lambdacurry.com/2012/05/using-freenode-xchat-on-sstp-vpn/
slug: using-freenode-xchat-on-sstp-vpn
title: Using freenode xchat on SSTP VPN
wordpress_id: 589
---

it seems that many SSTP VPN providers (like UnblockVPN) screw with port 6667. Freenode being unusually paranoid about Tor/VPN users doesnt let these users to connect.

I have found that using port 7070 with SSL works brilliantly. I'm not sure whether it will work for other IRC servers, but Freenode is what is relevant for me anyways.
