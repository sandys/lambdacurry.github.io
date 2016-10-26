---
author: sandeep
comments: true
date: 2009-05-06 04:49:44+00:00
layout: post
link: http://www.lambdacurry.com/2009/05/a-clean-install-of-ruby-191-ruby-on-rails-232-on-ubuntu-904/
slug: a-clean-install-of-ruby-191-ruby-on-rails-232-on-ubuntu-904
title: A clean install of Ruby 1.9.1 + Ruby-on-Rails 2.3.2 on Ubuntu 9.04
wordpress_id: 232
categories:
- linux
- software
- startup
- ubuntu
tags:
- rails
- ruby
---

I think the best way to go about this is to build everything from source. There are a few caveats of course, but I hope to clear them up.

**Prerequisites:**


<blockquote>sudo apt-get install libncurses5-dev libreadline5-dev mysql-server libmysqlclient15-dev mysql-client libssl-dev sqlite3 libsqlite3-dev</blockquote>


Download the sources for ruby, [rubygems](http://rubyforge.org/frs/?group_id=126), [mysql-ruby](http://rubyforge.org/frs/?group_id=4550)

**OPTIONAL: **Add [this](http://timetobleed.com/fix-a-bug-in-rubys-configurein-and-get-a-30-performance-boost/) [patch](http://github.com/ice799/matzruby/commit/0b9b69f9653782a33aee2b8937d405eae245b60c.diff) to ruby for a 30% boost with _pthreads._


<blockquote>patch -p1 < patch.diff

autoconf

./configure --prefix=<release>`--disable-ucontext --enable-pthread`

make; make install</blockquote>


Set ruby(<release>/bin) onto your path.

**Edit: **remember to set


<blockquote>RUBYLIB to <release>/lib:$RUBYLIB</blockquote>


Now here's the interesting step, install readline by


<blockquote>cd <src dir>/ext/readline

ruby extconf.rb

make;make install

cd <src dir>/ext/openssl

ruby extconf.rb

make;make install</blockquote>




<blockquote>cd rubygems

ruby setup.rb

make;make install</blockquote>


gems will automatically come onto your path, since it installs to the same directory as ruby (<release>/bin) above.

Time to install gems. But first create a directory, say "~/GEMS" and set **both **GEM_HOME and GEM_PATH to it. Also add $GEM_HOME/bin to your $PATH


<blockquote>gem install rubygems-update rails sqlite3-ruby</blockquote>


this should again place rails on your ruby install path

Do a


<blockquote>gem update</blockquote>


to update your gems periodically.

**Important Note: **if you are using a pre-2.3 Rails app in your 2.3 rails, make sure you rename


<blockquote>app/controllers/application.rb app/controllers/application_controller.rb</blockquote>
