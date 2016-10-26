---
author: sandeep
comments: true
date: 2012-04-05 09:43:04+00:00
layout: post
link: http://www.lambdacurry.com/2012/04/getting-hp-network-scanning-working-with-linux-12-04/
slug: getting-hp-network-scanning-working-with-linux-12-04
title: Getting HP network scanning working with Linux 12.04
wordpress_id: 584
tags:
- '12.04'
- hplip
- linux
- scanner
- ubuntu
---

Even after I configure my printer/scanner and _**scanimage**_** -L** being able to successfully identify it, I was not getting any remote scanning to work.

Simple-scan used to complain about unable to locate scanners and scanimage complained about "_unable to load restricted library /usr/share/hplip/scan/plugins/bb_soapht.so_"

What fixed it was reinstalling hplip and running _**sudo hp-plugin -i**_ (and saying Y to everything)
