# How The Web Works

## Learning Goals

1. Define a client and server
2. Explain what an HTTP request is
3. Explain the nature of request and response
4. Define a static site vs. a dynamic site

## Introduction

How many times a day do you use the internet? How many times do you load a
different web page? Think about how many times you do this in a year! As a user,
all you really need to know is the URL to navigate to. You don't need to concern
yourself with what's going on behind the scenes. But if you want to be a web
developer, it's important to have some understanding of how the web works. From
here on out, you are no longer just a user of the internet. You are a creator of
the web.

## Client and Server

So seriously, how does this:

```text
https://www.youtube.com/user/AdeleVEVO
```

Turn into this:

![AdeleVEVO](https://s3.amazonaws.com/learn-verified/request-intro.png)

The internet operates based on conversations between the client (more familiarly
known as the browser) and the server (the code running the web site you're
trying to load). By typing in that URL into your browser, you (the client) are
*requesting* a web page. The server then receives the request, processes it, and
sends a *response*. Your browser receives that response and shows it to you.
These are the fundamentals of the web. Browsers send requests, and servers send
responses. Until today you have always been a client. Moving forward you will be
building the server. This means processing requests, creating responses, and
sending them back to the client.

We will be writing our servers using Ruby and a few different frameworks. But
your browser doesn't know, nor does it care, what server it talks to. How does
that work? How can a server that was written 15 years ago still work with a
browser written 15 months or days ago? 

In addition, you can use multiple clients! You can use Chrome, Safari, Internet
Explorer, Opera, and many others. All of those browsers are able to talk to the
same server. Let's take a closer look at how this occurs.

## HTTP Overview

Being able to switch out both the server and the client happens because the way
browsers and servers talk is controlled by a contract or *protocol*.
Specifically it is a protocol created by Tim Berners-Lee called the **H**yper
**T**ext **T**ransfer **P**rotocol or HTTP. Your server will receive requests
from the browser that follow HTTP. It then responds with an HTTP response that
all browsers are able to parse.

`HTTP` is the language browsers speak. Every time you load a web page, you are
making an `HTTP` request to the site's server, and the server sends back an
`HTTP` response.

In the example above, the client is making an `HTTP GET request` to YouTube's
server. YouTube's server then sends back a response and the client renders the
page in the browser.

![computer server](https://curriculum-content.s3.amazonaws.com/how-the-web-works/Image_17_ComputerServer.png)

## Requests

### URI

When you make a request on the web, how do you know where to send it?  This is
done through **U**niform **R**esource **I**dentifiers or URIs. You've probably
also heard these referred to as URLs. Both are fine. Let's look at the URI we
used up top.

`http://www.youtube.com/user/adelevevo`

This URI is broken into three parts:

+ `http` - the protocol
+ `youtube.com` - the domain
+ `/user/adelevevo` - the resource

The `protocol` is the way we're sending our request. There are several different
types of internet protocols (SMTP for emails, HTTPS for secure requests, FTP for
file transfers). To load a website, we use HTTP.

The `domain name` is a string of characters that identifies the unique location
of the web server that hosts that particular website. This will be things like
`youtube.com` and `google.com`.

The `resource` is the particular part of the website we want to load. YouTube
has millions and millions of channels and videos, so we need to identify the
specific resource we want: `/user/adelevevo` (because we can't get Hello out of
our heads).

An analogy that works well is an apartment building. The domain is the entire
building. Within that building, though, there are hundreds of apartments. We use
the specific resource (also called a path) to indicate that we care about
apartment 4E. The numbering/lettering system is different for every apartment
building, just as the resources are laid out a bit differently for every
website. For example, if we search for "URI" using Google, the path looks like
this: `https://www.google.com/search?q=URI`. If we use Facebook to execute the
same search, it looks like this: `https://www.facebook.com/search/top/?q=uri`.

### HTTP Verbs

When making a web request, in addition to the path, you also need to specify the
action you would like the server to perform. We do this using _HTTP Verbs_. We
can use the same resource for multiple actions, so it is the **combination** of
the path and the HTTP verb that fully describes the request.

`GET` requests are the most common browser requests. This just means "hey
server, please GET me this resource", i.e., load this web page. Other verbs are
used if we want to send some data from the user to the server, or modify or
delete existing data. Below is a list of the available HTTP Verbs and what each
is used for. We will learn about them a bit later:

<table border="1" cellpadding="4" cellspacing="0">
  <tr>
    <th>Verb</th>
    <th>Description</th>
  </tr>
  
  <tr>
    <td>HEAD</td>
    <td>Asks for a response like a GET but without the body</td>
  </tr>
  <tr>
    <td>GET</td>
    <td>Retrieves a representation of a resource</td>
  </tr>
  <tr>
    <td>POST</td>
    <td>Submits data to be processed in the body of the request</td>
  </tr>
  <tr>
    <td>PUT</td>
    <td>Uploads a representation of a resource in the body of the request</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>Deletes a specific resource</td>
  </tr>
  <tr>
    <td>TRACE</td>
    <td>Echoes back the received request</td>
  </tr>
  <tr>
    <td>OPTIONS</td>
    <td>Returns the HTTP methods the server supports</td>
  </tr>
  <tr>
    <td>CONNECT</td>
    <td>Converts the request to a TCP/IP tunnel (generally for SSL)</td>
  </tr>
  <tr>
    <td>PATCH</td>
    <td>Apply a partial modification of a resource</td>
  </tr>
</table>

### Request Format

Our client so far has made a request to YouTube's server. In this case, a
request to `/user/adelevevo`. The server then responds with all the code
associated with that resource (everything between `<!doctype html>` and
`</html>`), including all images, CSS files, JavaScript files, videos, music,
etc.

When the client makes a request, it includes other items besides just the URL in
the "headers." The request header contains all the information the server needs
in order to fulfill the request: the type of request, the resource (path), and
the domain, as well as some other metadata. The request header would look
something like this:

![request header](https://s3.amazonaws.com/learn-verified/request-header.png)

## Responses

Once your server receives the request, it will do some processing (run code you
wrote!) and then send a response back. The server's response is separated into
two sections: the headers and the body.

The server's response headers look something like this:

![response header](https://s3.amazonaws.com/learn-verified/response-headers.png)

The headers contain all of the metadata about the response. This includes things
like content-length (how big is my response) and what type of content it is. The
headers also include the status code of the response.

The *body* of the response is what you see rendered on the page. It is all of
that HTML/CSS that you see! Most of the data of a response is in the body, not
in the headers.

### Status Codes

The primary way that a human user knows that a web request was successful is
that the page loads without any errors. However, you can also tell a request was
successful if you see that the response header's status code is `200`. You've
probably seen another common status code, `404`. This means "file not found."

Status codes are separated into categories based on their first digit. Here are
the different categories:

+ 100's - informational
+ 200's - success
+ 300's - redirect
+ 400's - error
+ 500's - server error

There are a number of other status codes and it's good to get familiar with
them. You can see a full [list of status codes on Wikipedia][codes].

[codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

## Static vs. Dynamic Websites

It's important to note that there are two different types of websites: static
and dynamic. A `static` website is one that doesn't change unless a developer
opens up an HTML file and modifies the content of that file. `Dynamic` websites
are sites where the content changes based on user input (e.g. Facebook, Twitter,
Yelp, etc.). Every time you visit the site, the content you see is most likely
different than the last time you visited because someone else gave a review of
that restaurant, or sent out a new tweet, or commented on that image you liked.

It can be helpful to think of static sites as "websites" and dynamic sites as
"web apps", although there is no official definition of either term or the
difference between them. The terms provide a convenient way to distinguish in a
non-technical way between sites with static vs. dynamic content.

The flow of request and response is slightly different for a static website than
for a dynamic web app. When the client wants to load a static site, the client
makes a request, and the server finds the file on a disk and sends it back. Done
and Done.

It gets a little bit more complex with a web app. The client makes a request, the
server runs application code (think of this as your Ruby code), and returns a
dynamically generated response.
