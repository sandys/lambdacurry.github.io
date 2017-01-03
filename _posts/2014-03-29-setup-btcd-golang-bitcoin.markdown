---
author: admin
comments: true
date: 2014-03-29 05:11:32+00:00
layout: default
link: http://www.lambdacurry.com/2014/03/setup-btcd-golang-bitcoin/
slug: setup-btcd-golang-bitcoin
title: Setting up btcd + Go build for bitcoin
wordpress_id: 880
---

My last post was about [setting up](http://www.lambdacurry.com/2014/03/compiling-bitcoin-0-9-0-transaction-malleability-fix/) the build system for Bitcoin reference system 0.9.0.

There is an alternative architecture for Bitcoin called _btcd_ which is developed by Conformal Systems. This is claimed to be compatible with the main blockchain (including bugs).

There is a very interesting [thread](https://bitcointa.lk/threads/calling-out-the-bitcoin-foundation-scam.273069/page-10) about how the btcd architecture (especially the split wallet/client and daemon architecture) has been adopted in the reference client at 0.9.0

I find Go very, very pleasant and productive to work and understand and it's package manager is absolutely brilliant.

To setup your machine to work with btcd is absolutely trivial. Remember that this should be the **same **on any platform (Windows, Linux and Mac) since Go is cross platform in general. Only the particular binary of Go would be different.

Download and unpack Go from [http://code.google.com/p/go/downloads/list](http://code.google.com/p/go/downloads/list) . I used [http://code.google.com/p/go/downloads/detail?name=go1.2.1.linux-amd64.tar.gz&can=2&q=](http://code.google.com/p/go/downloads/detail?name=go1.2.1.linux-amd64.tar.gz&can=2&q=) because I'm on Linux-64 bit but go ahead and use the one that you're on.

Assuming you unzip it to /home/sss/Code/go, set the following variable:


<blockquote>export GOROOT=/home/sss/Code/go</blockquote>


Test your Go installation by running _/home/sss/Code/go -v _. Ideally this environment variable should be in your zshrc, bashrc, etc. This never changes.

Now, create a directory called _/home/sss/Code/mybtcd._ This is your **new workspace**. When you are working on a particular workspace, set the following environment variable:


<blockquote>export GOPATH=/home/sss/Code/mybtcd</blockquote>


This tells your Go package manager, the location of your top level workspace directory.

Now, to get btcd and all its dependencies as well as compile it in one shot, run:


<blockquote>/home/sss/Code/go/bin/go get github.com/conformal/btcd/...</blockquote>


After a few minutes, you should have the following directories (which complies with Go's [recommended workspace directory structure](http://golang.org/doc/code.html))


<blockquote>./bin/ -> all your binaries

./pkg/ -> all third party library dependencies

./src/ -> all btcd as well as dependent third party source.</blockquote>


Running your bitcoin daemon is simply _./bin/btcd _(help is at _./bin/btcd --help_)

To hack your code, just write your code in _./src/github.com/conformal/btcd/ _and run


<blockquote>~/Code/go/bin/go install -v -x  github.com/conformal/btcd/</blockquote>


All dependencies and binaries get rebuilt. Simple.
