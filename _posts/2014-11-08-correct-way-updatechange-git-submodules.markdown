---
author: admin
comments: true
date: 2014-11-08 04:57:23+00:00
layout: post
link: http://www.lambdacurry.com/2014/11/correct-way-updatechange-git-submodules/
slug: correct-way-updatechange-git-submodules
title: The correct way to update/change git submodules
wordpress_id: 911
---


	
  * rm -rf .git/modules/interesting_modules

	
  * delete the lines containing "[submodule "interesting_modules"] url="http://something/"

	
  * update .gitmodules

	
  * run "git submodule sync"

	
  * run "git submodule init"

	
  * run "git submodule update" - at this point, a new checkout should happen.

	
  * new checkout will fail about a version mismatch. This is expected - the version of the submodule stored in the super-project is mismatched. "git status" should also show you "modified" in the submodule directory.

	
  * "cd interesting_submodule"

	
  * "git reset --hard HEAD"

	
  * enjoy !


