---
author: sandeep
comments: true
date: 2008-06-14 19:56:06+00:00
layout: default
link: http://www.lambdacurry.com/2008/06/of-ls-for-windows-and-good-grep-replacements-for-all-platforms/
slug: of-ls-for-windows-and-good-grep-replacements-for-all-platforms
title: Of "ls" for windows and good Grep replacements (for all platforms)
wordpress_id: 147
categories:
- linux
tags:
- windows productivity
---

Windows Powershell has a very sucky replacement for "ls". It does not support several of the advanced "ls" options. However, it is a wee bit tricky to rerplace the built-in "ls" cmdlet with the [msls](http://utools.com/msls.asp) alternative.

To do that,  you need to unzip msls (viz, ls.exe, grep.exe and dircolors.exe) into _c:windowssystem32 _directory.

Then add the following to your profile.ps1


<blockquote>$env:LS_OPTIONS = "-bhAC --more --color=auto --recent --streams"
set-alias ls "C:WINDOWSsystem32ls.exe" -option allscope</blockquote>


This will take care of setting the required options to get it to work.

In addition, there is a new grep alternative built on perl called [ack](http://petdance.com/ack/). Built on perl, it does 95% of what perl does.

Only problem?

Its not in Python
