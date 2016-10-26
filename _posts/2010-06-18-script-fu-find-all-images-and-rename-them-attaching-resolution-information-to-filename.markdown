---
author: sandeep
comments: true
date: 2010-06-18 15:02:09+00:00
layout: post
link: http://www.lambdacurry.com/2010/06/script-fu-find-all-images-and-rename-them-attaching-resolution-information-to-filename/
slug: script-fu-find-all-images-and-rename-them-attaching-resolution-information-to-filename
title: 'script-fu: find all images and rename them, attaching resolution information
  to filename'
wordpress_id: 393
categories:
- linux
---

dont ask  

  

[sourcecode lang="bash"]
 find   .  -name *image* -exec sh -vc ' cp {}  `echo {} |xargs  basename| sed "s@(.*).jpg|png|bmp@1@"`__`identify -verbose {}  | grep Geometry | sed -e "s@^.*Geometry: ([0-9]*)([x]*)([0-9]*).*@__1_3@"`.`echo {} | sed "s@(.*).(jpg|png|bmp)@2@"` ' ;
[/sourcecode]
