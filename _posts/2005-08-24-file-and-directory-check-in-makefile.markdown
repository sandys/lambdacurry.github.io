---
author: sandeep
comments: true
date: 2005-08-24 21:53:00+00:00
layout: default
link: http://www.lambdacurry.com/2005/08/file-and-directory-check-in-makefile/
slug: file-and-directory-check-in-makefile
title: File and directory check in Makefile
wordpress_id: 66
categories:
- software
---

I needed to do some conditional target-based execution via my makefiles. To make them truly generic, I needed to deduce directory structure that I was sitting in.  

One of the things I had to do was to check for existence of a file or directory. Now since Makefiles have a different syntax than ordinary shell, compounded by the problem of interfacing with the *nix shell, it took me some time to figure out/learn how to do this.




The syntax (for GNU make) is




<blockquote>
ifeq (exists, $(shell [ -d directory_name ] ) && echo exists )  

  $(warning hi... I did it)  

endif

> 
> </blockquote>




At first I tried to do




<blockquote>
ifeq (1, $(shell [ -d directory_name ] )  )  

  $(warning hi... I did it)  

endif

> 
> </blockquote>




but this did'nt work, because the shell interface does not return a numeric status (atleast I think so). But in the syntax that works, by the power of logic, the "echo exists" will take place if and only if the "shell" command works.  

Ergo, I can check for directories.




whew!!




del.icio.us Tags:  [software](http://del.icio.us/sss8ue/software)



