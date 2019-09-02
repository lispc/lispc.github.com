---
layout: post
title: "Y Combinator"
description: ""
category: 
tags: []
---
{% include JB/setup %}
{% highlight python %}
#! /usr/bin/env python3
Y=lambda F:(\
        (lambda x: (\
            F(lambda y:((x(x))(y)))\
            ))\
        (lambda x: (\
            F(lambda y:((x(x))(y)))\
            ))\
        )
FactGen=lambda fact:(\
        (lambda n:(\
            (1 if n==0 else n*fact(n - 1))\
            )\
        ))
print(list(map(Y(FactGen),(range(1,10)))))
{% endhighlight %}
