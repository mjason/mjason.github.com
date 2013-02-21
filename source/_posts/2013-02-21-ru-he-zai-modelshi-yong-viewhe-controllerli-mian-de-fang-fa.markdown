---
layout: post
title: "如何在model使用view和controller里面的方法"
date: 2013-02-21 12:02
comments: true
categories: ruby rails Thread
---

当在些model的时候我们很多时候需要使用一些在hepler方法或者其他，model是使用不了这些的，一般是通过传变量来解决，可是这样的话，总是感觉怪怪的

这个时候可以使用线程来达到我们需要的东西

下面以在model使用devise的current_user为例说明如何使用

在ApplicationController里面写入一个方法

```ruby
before_filter :set_request_environment

  private
  def set_request_environment
    Thread.current[:current_user] = current_user if current_user
  end
```

在model里面就可以访问到这个线程的内容

```ruby
def is_teacher?
    if Thread.current[:current_user] == teacher
      return true
    else
      return false
    end
end
```

