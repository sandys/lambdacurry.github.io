---
author: sandeep
comments: true
date: 2004-12-23 18:52:00+00:00
layout: post
link: http://www.lambdacurry.com/2004/12/python-disassemble-code-lambdas/
slug: python-disassemble-code-lambdas
title: '[Python] Disassemble code, lambdas'
wordpress_id: 13
---

Here's two nice python features:


  
  * Lambda's are unnamed pseudo-functions, which are a functional programming tool
normal functions
```def f (x): return x**2

Lambdas
``f = lambda x: x**2

Usage(for both)
``print g(8)

`

  
  * To disassemble python code and see their bytecode (python can also precompile your code ...somewhat like java)
>>import **dis
****>>dis**.**dis**(f)
             0 LOAD_CONST               1 (1)
             3 LOAD_CONST               2 (2)
             6 BINARY_ADD
             7 RETURN_VALUE
**>>dis**.**dis**(g)
             0 LOAD_CONST               1 (1)
             3 LOAD_CONST               2 (2)
             6 BINARY_ADD
             7 RETURN_VALUE


del.icio.us Tags: [python](http://del.icio.us/sss8ue/python) [lambda](http://del.icio.us/sss8ue/lambda) [software](http://del.icio.us/sss8ue/software)
