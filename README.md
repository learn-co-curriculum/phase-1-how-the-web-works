# How The Web Works

## Learning Goals

- Explain what an HTTP request is
- Explain the nature of request and response
- Identify HTTP verbs

## Introduction

How many times a day do you use the internet? How many times do you load a
different web page? Think about how many times you do this in a year!

As a user, all you really need to know is the URL of the website you want to
visit — [www.google.com](www.google.com), for example. You don't need to concern
yourself with what's going on behind the scenes.

Web developers, on the other hand, need to know the fundamentals of how the web
works. From here on out, you are no longer just a user of the internet — you are
a creator of the web!

## Client and Server

So seriously, how does this:

```txt
https://github.com/learn-co-curriculum/phase-1-how-the-web-works
```

Turn into this:

![Github
Readme](https://curriculum-content.s3.amazonaws.com/phase-1/how-the-web-works-readme/github-readme.png)

The internet operates based on conversations between the client and the server.

As we discussed in the previous lesson, clients and servers work together. By
typing a URL into your browser, you (the client) are _requesting_ a web page.
The server then receives the request, processes it, and sends a _response_
containing the client-side code for that webpage — HTML, JavaScript, and CSS
files. Your browser receives that response and uses the client-side code it
contains to display the website.

These are the fundamentals of the web. Browsers send requests and servers send
responses.

Just as we're currently writing _client-side_ code, we can also write
_server-side_ code that tells our server what it's supposed to do — how to
handle specific requests from a client, for example. Writing client-side code is
known as _front end_ development, while writing server-side code is known as
_back end_ development.

We can write server-side code in a wide variety of programming languages.
Python, JavaScript, Ruby, Java, PHP, C#, Go — the list goes on! Your browser
doesn't know, nor does it care, what kind of server it talks to. It can
communicate with servers written in any language!

But, your browser doesn't know, nor does it care, what kind of server it talks
to. It can communicate with servers written in any language! How does that work?
How can a server that was written 15 years ago still work with a browser written
2 years ago?

On top of that, you can use multiple clients! You can use Chrome, Safari,
Firefox, Edge, and many others. All of those browsers are able to talk to the
same servers.

How does all this work? How can all the different browsers and all the different
servers communicate with each other? And how is a server that was written 15
years ago still compatible with a browser written 2 years ago? The answer is
HTTP.

## HTTP Overview

Communication between different clients and different servers is only possible
because communication between browsers and servers is controlled by a
_protocol_.

In computer science, a _protocol_ is simply a set of rules and procedures that
dictates how information is transmitted between different computers. The web
uses a specific type of protocol, originally created by [Tim Berners-Lee][sir
tim]: **Hyper Text Transfer Protocol**, or **HTTP**.

All browsers and all servers are set up to use HTTP - it's what allows clients
and servers of all types to communicate with each other.

Every time you load a web page, you are making an HTTP **request** to the site's
server. The server then sends back an HTTP **response**. Once you start using
`fetch` in JavaScript, you will be writing your own HTTP requests!

In the GitHub example above, the client is making an **HTTP GET request** to
GitHub's server. GitHub's server then sends back a response and the client
renders the page in the browser.

## HTTP Requests

Let's take a look at each of the components that make up a request. The diagram
below shows how clients and servers communicate with each other to complete an
HTTP request.

![computer
server](https://curriculum-content.s3.amazonaws.com/how-the-web-works/Image_17_ComputerServer.png)

### URL

When you make a request on the web, how do you know where to send it? This is
done through **Uniform Resource Locators**, or URLs. You may have also heard
these addresses referred to as URIs (Uniform Resource Identifiers). Both names
are fine.

Let's look at the URL we used up top:

```txt
https://github.com/learn-co-curriculum/phase-1-how-the-web-works
```

This URL is broken into three parts:

- `https` - the protocol
- `github.com` - the domain name
- `/learn-co-curriculum/phase-1-how-the-web-works` — the path

The **protocol** is the format we're using to send our request. There are
actually several different types of internet protocols (SMTP for emails, HTTPS
for secure requests, FTP for file transfers). To load a website, we use HTTP or
HTTPS.

The **domain name** is a string of characters that identifies the unique
location of the web server that hosts that particular website. This could be
something like `youtube.com` or `google.com`.

The **path** is the particular part of the website we want to load. GitHub has
millions and millions of users and repositories, so we need to identify the
specific resource we want using the path:
`/learn-co-curriculum/phase-1-how-the-web-works`.

Let's think about this using a real world example — an apartment building!

The **domain** is the entire building. Within that building, though, there are
hundreds of apartments. We use the specific **path** (also called a resource) to
indicate that we care about apartment 4E.

The numbering/lettering system is different for every apartment building, just
as the resources are laid out a bit differently for every website. For example,
if we search for "URI" using Google, the path looks like this:
`https://www.google.com/search?q=URI`. If we use Facebook to execute the same
search, it looks like this: `https://www.facebook.com/search/top/?q=uri`.

You can learn more about the [anatomy of a URL from MDN][url anatomy].

### HTTP Verbs

When making a web request, in addition to the path, you also need to specify the
action you would like the server to perform. We do this using [**HTTP
Verbs**][verbs], which are also known as **request methods**.

We can use the same path for multiple actions by using different HTTP verbs to
make different types of requests to that same path. It is the **combination** of
the path and the HTTP verb (method) that _fully_ describes the request.

For example, making a **POST** request to
`/learn-co-curriculum/phase-1-how-the-web-works` tells the server something
different than making a **GET** request to
`/learn-co-curriculum/phase-1-how-the-web-works`.

**GET** requests are the most common browser requests. This just means "hey
server, please _GET_ me this resource", i.e., load this web page. Other verbs
are used if we want to send some data from the user to the server, or modify or
delete existing data.

Below is a list of the available HTTP verbs and what each is conventionally used
for. We will learn more about them a bit later.

| Verb    | Description                                                               |
| ------- | ------------------------------------------------------------------------- |
| GET     | Retrieves a representation of a resource                                  |
| POST    | Create a new resource using data in the body of the request               |
| PUT     | Update an existing resource using data in the body of the request         |
| PATCH   | Update part of an existing resource using data in the body of the request |
| DELETE  | Deletes a specific resource                                               |
| HEAD    | Asks for a response (like a GET but without the body)                     |
| TRACE   | Echoes back the received request                                          |
| OPTIONS | Returns the HTTP methods the server supports                              |
| CONNECT | Converts the request to a TCP/IP tunnel (generally for SSL)               |

### Request Format

Our client so far has made a request to GitHub's server. In this case, a GET
request to `/learn-co-curriculum/phase-1-how-the-web-works`. The server then
responds with all the code associated with that resource (everything between
`<!doctype html>` and `</html>`), including all images, CSS files, JavaScript
files, videos, music, etc.

When the client makes a request, it includes additional "metadata" about the
request, besides just the URL, in the **request headers**.

The request headers contain all the information the server needs in order to
fulfill the request: the HTTP verb (method), the resource (path), and the domain
(authority), as well as some other metadata. The request headers look something
like this:

![request
headers](https://curriculum-content.s3.amazonaws.com/phase-1/how-the-web-works-readme/request-headers.png)

You can check out the request/response data for any website in the Network tab
in the browser dev tools: open the Network tab, refresh the page, then click the
top listing to see information about the request and response.

## Responses

Once a server receives the request, it will do some processing using server-side
code and then send a response back. The server's response is separated into two
sections: the **headers** and the **body**.

The server's **response headers** look something like this:

![response
headers](https://curriculum-content.s3.amazonaws.com/phase-1/how-the-web-works-readme/response-headers.png)

The headers contain all of the metadata about the response. This includes things
like `content-length` (how big is my response) and what the `content-type` of
the content is content it is (is it HTML? JSON? an image?). The headers also
include the **status code** of the response.

The **body** of the response is what you see rendered on the page. It is all of
that HTML/CSS that you see! Most of the data of a response is in the body, not
in the headers.

The body of the request can come in many different formats. For a website, the
format will be HTML. For a web API, the format will probably be JSON (JavaScript
Object Notation) or XML (eXtensible Markup Language), which are useful formats
for transmitting structured data.

In all cases, the **body** of the HTTP response is **just a string of text** —
it's up to the client to use that string to build a graphical representation of
the website, or parse the JSON response into another format.

### Status Codes

When human users interact with a website, they generally only pay attention to
whether or not the website loads successfully. If it does, then their web
request was a success. If it doesn't, then something went wrong.

However, the HTTP response header also contains a _status code_ that indicates
whether the request was successful. If the request wasn't successful, the
specific code returned may provide a clue about what went wrong. A status code
of `200` indicates a successful request. Another common status code, `404`,
means "resource not found."

Status codes are separated into categories based on their first digit. Here are
the different categories:

- 100's: informational
- 200's: success
- 300's: redirect
- 400's: error
- 500's: server error

There are a number of other status codes. It's a good idea to familiarize
yourself with them as you continue on your web development journey. You can see
a full [list of status codes on Wikipedia][codes].

## Conclusion

At this point, we're only writing client-side code, but it's still important to
understand the following key concepts: the request-response cycle, URLs, HTTP
verbs and status codes. Together, these components form the foundation of the
internet itself!

When building web applications — whether they're client-side applications in
JavaScript, or server-side applications in Python — it's essential for us to
know and understand these components!

## Resources

- [What is a URL?][url anatomy]
- [HTTP Verbs (Methods)][verbs]
- [HTTP Status Codes][codes]

[sir tim]: https://www.w3.org/People/Berners-Lee/
[url anatomy]:
    https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL
[verbs]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
[codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
