---
author: sandeep
comments: true
date: 2008-01-03 12:28:02+00:00
layout: default
link: http://www.lambdacurry.com/2008/01/subversion-build-errors-gss_delete_sec_context/
slug: subversion-build-errors-gss_delete_sec_context
title: 'Subversion build errors: gss_delete_sec_context'
wordpress_id: 132
categories:
- linux
- software
---

Gah... have a better Autoconf/configure.

When building Subversion with "_./configure --without-berkeley-db_" , it builds fine but the Python bindings croak out.

You have to do a lot of arcane debugging (by setting **PYTHONVERBOSE** to 2 or greater) and then you see that it fails in "_import svn.core_" .  What might be the problem?


<blockquote> gss_delete_sec_context undefined</blockquote>


To fix this, you need to modify the Makefile in the top level subversion directory from:


<blockquote> <  _SVN_APR_LIBS =  /home/ssriniva/s2/subversion-1.4.4/apr/libapr-1.la -luuid -lrt -lcrypt  -lpthread -ldl_</blockquote>




<blockquote>to</blockquote>




<blockquote> >_ SVN_APR_LIBS =  /home/ssriniva/s2/subversion-1.4.4/apr/libapr-1.la -luuid -lrt -lcrypt  -lpthread -ldl -L/usr/lib/sasl -lgssapiv2_</blockquote>


The location of libgssapiv2 may vary from system to system.

This fixes the problem.
