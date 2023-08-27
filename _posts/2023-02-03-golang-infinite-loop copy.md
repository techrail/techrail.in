---
layout: single
title: Infinite loop in golang using for-select
permalink: "/posts/golang-infinite-loop/"
date: "2023-02-03"
future: true
toc: false
published: true
excerpt: "Not everything is obvious when using channels. Using 'default' is not always a great idea."
header:
  overlay_image: /assets/images/posts/golang-infinite-loop/tangerine-newt--XJHtyhIVmo-unsplash.jpg
  overlay_filter: rgba(0, 0, 0, 0.4)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com/photos/-XJHtyhIVmo)"
tags:
  - golang
  - development
  - backend
---

One of the things about golang is that it allows you to build highly concurrent programs. While working on golang, you would come across the language construct called `select`.

`select` allows you to wait on multiple channels and execute the block that is ready or execute. Or, if there is a default block, then that gets executed. For example: 

```go
select {
  case err <- errorChannel:
    fmt.Println("Error:", err)
  case response <- responseChannel:
    fmt.Println("Response:", response)
  default:
    fmt.Println("Neither error nor response is ready")
}
```

In the above block if there is an input available on the errorChannel then the error is printed or if a response is available on the responseChannel then that is printed and if neither of them is available then the message "Neither error nor response is ready" is printed.

One of the many ways in which the select block is used is to constantly wait on one of the channels using a for loop like this.

```go
for {
  select {
    case err <- errorChannel:
      fmt.Println("Error:", err)
    case response <- responseChannel:
      fmt.Println("Response:", response)
    default:
      fmt.Println("Neither error nor response is ready")
  }
}
```

In the above case, the for loop will run infinitely and keep waiting on response for either the error channel or the response channel or it will print the default message. The catch here is though that the loop does not end and for every time the loop executes, if there is no response available in either of the channels then the default message will always be printed.

This is how your colon code can get into an infinite loop using the select block. It is a common mistake to ignore a construct like this and cause 100% CPU usage.

