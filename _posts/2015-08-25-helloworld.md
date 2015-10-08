---
layout: post
published: false
title: "HelloWorld"
author: "cfool"
description: ""
category: 
tags: [test, tag1]
---

``` language-ruby
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
```