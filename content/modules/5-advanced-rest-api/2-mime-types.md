---
title: "MIME Types"
description: "We are going to look at MIME types in HTTP and how it applies to REST"
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
This exploration looks at MIME (Multipurpose Internet Mail Extensions) types, also known as media types. You should have a vague understanding of these maybe from CS290. At least you have probably seen them in a request or response here and there. They typically look something like `text/html` or `application/json`.

These MIME types help the client and server negotiate what data is going to be sent and received.

## Using MIME Types
Up till now we have likely been sending some improper requests or at the very least, not known that our testing tool was fixing requests on our behalf. There are two headers we are going to be concerned with `Content-type` and `Accept`. The former, `Content-type` is used by any party sending data. So if the client is sending a payload via a `POST` or `PUT` the `Content-type` header lets the server know what format it is in. Likewise if the server is sending back a response to the client it used the `Content-type` header to let the client know what format it is in.

`Accept` is used exclusively by the client to let the server know what kinds of response it would find acceptable. So it can ask for `text/html`. If the server supports it, it will send back an `html` version of the resource and specify that in the `Content-type` header. If it does not support sending back an `html` version of the page, it would reply with status `406 Not Acceptable`. It is possible to for the client to specify a range that the server can pick form, for example: `Accept: text/html, application/xhtml+xml, application/xml`.

That is really all there is to it. The actual negotiation of MIME type is straight forward. The challenge can come with trying to get the server to parse one kind of database record into different formats. But there are a number of libraries and built in functions that can often assist with this.

## MIME Types
The interesting part is discussing how to make MIME types work. [Here is a list](https://www.iana.org/assignments/media-types/media-types.xhtml) of probably around 1,000 different MIME types. Just look up the one for the kind of thing you are dealing with. Some good ones to know offhand are `text/html` for HTML documents, `application/json` for JSON, `text/css` for CSS. As a general rule that probably has more exceptions than things that follow it, MIME types that are prefaced by `application` are opened by an application whereas ones that are prefaced by `text` are supposed to be human readable. I would argue JSON is pretty human readable, but the regulatory body decided that it was used by applications to exchange data rather than by humans. HTML is usually parsed by applications to. But I digress.

I always look up a MIME type when I need it and you should too.

{{< kaltura 0_whtwns7n >}}

## Review
This isn't particularly interested stuff. Your clients and use cases will determine what data formats you need to support. There are not a whole lot of interesting design decisions to make here.  But it is important you know how to ask for and return particular content types as it is a pretty common need to support multiple content types.