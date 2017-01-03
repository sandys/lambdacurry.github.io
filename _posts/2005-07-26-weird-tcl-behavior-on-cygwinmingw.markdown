---
author: sandeep
comments: true
date: 2005-07-26 21:37:00+00:00
layout: default
link: http://www.lambdacurry.com/2005/07/weird-tcl-behavior-on-cygwinmingw/
slug: weird-tcl-behavior-on-cygwinmingw
title: Weird TCL behavior on Cygwin/MinGW
wordpress_id: 718
categories:
- software
---

A C++ program compiled with TCL stubs, which performs just fine on Linux, just seems to go out without a sound on Cygwin. TCL_LIBRARY was set properly (also tried the  



<blockquote>"export TCL_LIBRARY=$(cygpath -w /usr/share/tcl8.4)"</blockquote>




hack). But the execution just seems to vanish after a call to Tcl_Init(). Now internally, Tcl_Init parses a whole load of stuff, starting from init.tcl.  

Also tried a weird hack that changes the "tclPreInitScript" variable to help set the $tcl_library variable, et al. But nothing helped.  

On debugging the executable in gdb, the call to Tcl_Init returns a segfault, which is not visible on a normal run.  

The solution to this mystery is a simple call to  



<blockquote>"Tcl_FindExecutable(argv[0])"</blockquote>




, which sets up some internal variables for use by tcl. Now since in cygwin there are two paths (the /usr type path and the /cygdrive/usr path) for all resources, this helps initialise everything correctly. I almost did'nt try this solution.  

But it works!!!




del.icio.us Tags:   [software](http://del.icio.us/sss8ue/software)



