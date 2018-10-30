---
title: "Some Bits of Security"
description: "Security in the cloud is a HUGE topic. This will cover authorization and OAuth 2.0, a tiny sliver of security, but an important sliver to be able to play well with others."
categories: ["Module"]
weight: 30
---

{{< title >}}
## Introduction
This module discusses the concept and technical implementation of authorization. It will go over what it means to authorize an entity (and what it does not mean). It will also discuss how one of the most common authorization protocols currently in use, OAuth 2.0 is used.

## Key Questions
- Why is authorization needed?
- What is the difference between authorization and authentication?
- What is delegated authorization?
- What does authorization tell us about the user?
- What are the stages in a typical server side OAuth 2.0 authentication flow?
- Why do each of those stages exist?


## Assignment Overview
For this week you will implement an OAuth 2.0 client "by hand". In general this would be bad practice. There are lots of people that have done a lot work making secure libraries. In production of a non-learning piece of software, use a library. But to learn how OAuth 2.0 works hand coding it is the way to go.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[Google's OAuth 2.0 Information](https://developers.google.com/identity/protocols/OAuth2)
: This is one of the better descriptions of OAuth and includes several samples in several languages of how the authorization flow is handled for a wide variety of devices.

The rest of the Internet
: I know I didn't immediately get OAuth 2.0. I had to try site after site until one explained it in a way that made sense. I also didn't learn it in a class, so you will have the added opportunity to ask questions when something does not make sense. But do explore different sites descriptions of OAuth 2.0. And do an image search on Google for OAuth 2.0 flow diagrams, there might be one there that really makes sense to you specifically.

## Review
So there you have the overview of OAuth 2.0. The major way to authorize web services to access end-user data on a 3rd party site. This is currently used all over the place. How long it remains the flavor of the week remains to be seen. Authentication and authorization on the web are rapidly evolving topics but this represents the current state of the art.