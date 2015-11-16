# How The Web Works

<img src="https://s3.amazonaws.com/learn-verified/welcome-to-internet.jpg" width="300" hspace="10" align="right">

## Objectives 
+ Define a client and server
+ Explain what an HTTP request is
+ Explain the nature of request and response
+ Define a static site vs. a dynamic site


## Intro
How many times a day do you use the internet? How many times do you load a different web page? I bet you can't even begin to guess how many times in a year! In order to be a developer, and especially a web developer, it's incredibly important to understand how the web works.


## Client and Server

You'll read the words "client and server" thrown around a lot throughout this reading. 

The internet operates based on conversations between the client (more familiarly known as the browser) and the server (the code running the web site you're trying to load). In very simple terms, the client makes a request to the server, and the server responds to that request by sending back all the code that the client can interpret and loads as a web page for your viewing/reading pleasure.

So seriously, how does this:

```
https://www.youtube.com/user/AdeleVEVO
```

Turn into this:

<img src="https://s3.amazonaws.com/learn-verified/request-intro.png">

## Overview

`HTTP` is the language browsers speak. Every time you load a web page, you are making an `HTTP request` to the site's server, and the server sends back an `HTTP response`.

In the example above, the client is making an `HTTP GET request` to YouTube's server, YouTube's server sends back a response, and the client renders the page in the browser.

<img src="https://s3.amazonaws.com/learn-verified/requests.png">

## URI

`http://www.youtube.com/adelevevo`

+ `http` - the protocol
+ `youtube.com` - the domain
+ `/adelevevo` - the resource

The full URI allows gives us specific information. The `protocol` is the way we're sending our request. There are several different types of internet protocols (SMTP for emails, HTTPS for secure requests, FTP for file transfers). To load a website, it's always and HTTP request.

The `domain name` is a string of characters that identifies the unique location of the web server that hosts that particular website.


The `resource` is the particular part of the website we want to load. YouTube has millions and millions of channels and videos, so the specific resource we want is `/adelevevo` (becuase we can't get Hello out of our heads).

## Requests

So the client makes a request to YouTube's server. In this case, a `GET` request to `/adelevevo`. And the server responds with all the code associated with that resource `<!doctype html> .....</html>`, including all images, CSS files, JavaScript files, videos, music, etc. 

When the client makes a request, the `request header` would look something like this. The request header contains all the information the server needs in order to fulfill the request: the type of request, the resource (path), the domain:


<img src="https://s3.amazonaws.com/learn-verified/request-header.png">

And the server's response looks something like this:

<img src="https://s3.amazonaws.com/learn-verified/response-headers.png">

The response contains information like the status code (200 for successful response), the content type, the content length, the date, the body of the request will contain all the code to load Adele's Vevo page.


## HTTP Verbs

So far, we've walked through `GET requests`, but there are many more type's of HTTP requests that communicate what kind of interaction we'd like to have with the server. You'll hear these refered to as HTTP `methods` or `verbs`.

| VERB  | Description |
| ------------- | ------------- |
| HEAD  | Asks for a response like a GET but without the body  |
| GET  | Retrieves a representation of a resource  |
| POST | Submits data to be processed in the body of the request|
| PUT | Uploads a representation of a resource in the body of the request |
| DELETE | Deletes a specific resource| 
| TRACE | Echoes back the received request | 
| OPTIONS | Returns the HTTP methods the server supports | 
| CONNECT | Converts the request to a TCP/IP tunnel (generally for SSL)|
| PATCH | Apply a partial modification of a resource | 

## HTTP Responses

The most important part of the response header is the `status`. Every time there is a successful response (you'll know it's successful because the page will load without any erros), it's a status code of `200`, but there are other status codes and it's good to get familiar with them.

+ 100's - informational
+ 200's - success
+ 300's - redirect
+ 400's - error
+ 500's - server error

## Server

It's important to note that there are two different types of webapps: static and dynamic. A `static` webapp is one that doesn't change. The content doesn't change unless a developer opens up and HTML file and modifies the content of that file. A `dynamic` webapp are sites where the content changes based on user input (i.e. Facebook, Twitter, Yelp, etc.). Every time you visit the site, the content is most likely different because someone else gave a review of that restaurant, or sent out a new tweet, or commented on that image you liked.

The flow of request and response changes slightly based on a static of a dynamic webapp. 

When the client wants to load a static site, the client makes a request, the server finds the file on a disk, and sends it back. Done and Done.

It gets a little bit more complex with a webapp. The client makes a request, the server runs application code (think of this as your Ruby code), and returns a dynamically generated response. 

## Summary

We'll dive further into each of the these topics in the following readings, and especially into writing server-side code that handles different requests, but it's important to get a good overview.
