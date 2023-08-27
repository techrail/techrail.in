---
layout: single
title: Starting off with Jekyll
permalink: "/golang/golang-infinite-loop/"
date: "2023-02-03"
future: true
toc: false
published: false
excerpt: "Not everything is obvious when using channels. Using `default` is not always a great idea."
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


## Select keyword
The `select` keyword in Go is used in conjunction with channels to wait on multiple channels simultaneously and receive or send data from the first one that is ready. It allows the program to work with multiple stuff at the same time. The basic syntax of the select statement is:

```go
select {
  case expression1:
    // code to run if expression1 is true
  case expression2:
    // code to run if expression2 is true
  ...
  default:
    // code to run if none of the expressions are true
}
```

Each `case` block usually is a channel receive operation but can also be a channel-send, a timeout or a `default` operation. The `select` blocks until one of the channel operations is ready to proceed, then it will execute the corresponding code block. If none of the operations is ready then it will keep waiting and if a `default` case is present, that gets executed.

## How to use select once
Let's take an example. In this example, we assume we have called a function called `getLatestPosts` and are waiting for the result. The function `getLatestPosts` would look something like this: 

```go
var errChannel chan error
var responseChannel string

func getLatestPosts() {
  // Make an API call to the endpoint that returns blog posts
	response, err := http.Get("https://api.example.com/posts")
	if err != nil {
		errorChannel <- err
	}
	defer response.Body.Close()

	// Read the response body
	body, err := io.ReadAll(response.Body)
	if err != nil {
		errorChannel <- err
	}

  // Normally we would parse the body. However to keep things simple
  // we are sending the body on a channel
  responseChannel <- string(body)
}
```

In this program, we are creating a function that will make a API call and wait for the response. Depending on whether it encounters an error or not, it will send either the response or the error to the corresponding channel. 

Now suppose that we are going to wait for only three seconds for either in response to come or an error to come. In this case, we have to wait for the error channel or the response channel or we have to have a timeout for three seconds.

So we're going to create a select block and wait on three cases. The first case is a input from the response channel. The second case is input from the error channel and the third one is a three second timeout.

The code for that would look like this: 

```go
var err error
var responseText string
select {
  case err <- errChannel:
  fmt.Println("Got error:", err)
  case responseText <- responseChannel:
  fmt.Println("Got Post content:", responseText)
  case <- time.After(3*time.Second):
  fmt.Println("Timeout!!")
}
```

