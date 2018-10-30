---
title: "Status Codes and Content Types in Node"
description: "We looked at the concept of status codes and content types in the prior explorations, this looks at implementing them in Node.js"
categories: ["Exploration"]
weight: 15
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
This looks at the tools at your disposal in Node.js to implement the proper use of status codes and content types. We will go through setting response codes, messages and setting and reading response and request headers.

## Setting Status Codes
Using Node.js and Express.js it is very simple to set the response status code. You simply call the response objects `status` method.

```js
res.status(403).end();
```

Would set the status code to 403 and send the response. If you want to include a message you would do so with the `send()` method. For example

```js
res.status(404).send("Not Found");
```

It really is that simple. Just make sure that you don't change the status code without realizing it before sending the response.

## Setting Headers
Setting headers is a touch more prone to error and a little more difficult, but it is still fairly straight forward. The responses `set(header, value)` method will set the specified header to the specified value. For example:
```js
res.set("Content", "application/json");
```
would set the `Content` header to `application/json`. A more complex example:

```js
res.status(405).set("Allow", "GET, DELETE").send("Not Acceptable");
```

might be what you would do if someone tried to `PUT` to a resource that didn't allow edits. This would let the client know the method was not acceptable but they could look at the `Allow` header to see what methods are allowed.

## Sending Different Content Types
There isn't a whole lot to add here. You should be familiar with sending HTML due to your experience in prior classes. You could certainly use a template engine like Handlebars to generate your HTML. Alternatively you could just build an appropriate string and send it using the responses `send` method.

## Node Demo
A demo of this can be seen using [this code](https://gist.github.com/wolfordj/bdc91a059072075ef9a88120fff219b5) and the following video:

{{< kaltura 0_0sdd2lxk >}}

## Review
This particular set of functionality tends to be a little less troublesome than the previous bits because none of it is asynchronous. This is mainly just conditionals to make sure you get to the right status code and content type, then make sure you convert whatever data you need to the format the client want's, set your content type and send that data.