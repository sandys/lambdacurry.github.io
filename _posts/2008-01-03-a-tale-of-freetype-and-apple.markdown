---
author: sandeep
comments: true
date: 2008-01-03 14:26:02+00:00
layout: post
link: http://www.lambdacurry.com/2008/01/a-tale-of-freetype-and-apple/
slug: a-tale-of-freetype-and-apple
title: A tale of Freetype and Apple
wordpress_id: 133
categories:
- freedom
- linux
- software
---

Some time back I was trying to get [Fvwm ](http://www.fvwm.org/) on my Ubuntu laptop. One of the prereqs was the open source font-rendering engine [Freetype ](http://freetype.sourceforge.net/index2.html) .

But no matter how hard I tried, I couldnt get the fonts to look pretty ( I even got the [Open Source Liberation Fonts](http://en.wikipedia.org/wiki/Liberation_fonts)  ).

And then I discovered about the Microsoft and Apple patents.

It seems that they own a few patents in font rendering, which meant that unless I turned them on by hand and compiled them in FreeType, these obviously superior engines would not be used for rendering.

The way to switch them on is:


<blockquote> in include/freetype/config/ftoption.h , uncomment lines:</blockquote>




<blockquote> /* #define TT_CONFIG_OPTION_BYTECODE_INTERPRETER */  (Apple Patent)</blockquote>




<blockquote>/* #define FT_CONFIG_OPTION_SUBPIXEL_RENDERING */ (Microsoft Patent)</blockquote>


Voila. Ze beautiful fonts are heerre.
