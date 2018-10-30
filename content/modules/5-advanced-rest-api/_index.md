---
title: "Advanced REST API Concepts"
description: "Having made a generally functional REST API this will go into some more complex concepts like paging and caching."
categories: ["Module"]
weight: 25
---

{{< title >}}
## Introduction
<!--- Introduce the topic in this section -->
This module wraps up some final API topics. These are a little more general and apply to more than just REST but they make for a complete API. Some of this stuff is handled under the hood by some server backends, but sometimes you need to tweak it or add functionality the server does not posses.

## Key Questions
- What do status codes in the 200s, 300s and 400s represent?
- What are MIME types?
- What headers are associated with negotiating MIME types?


## Assignment Overview
This week you will make an API that, while very limited in scope, is fully functional in terms of error handling and will for the first time allow the client to request data in more than one format.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
No resources in particular this week. Searching HTTP status codes and MIME types will yield *many* lists of the status codes and APIs. Find one that is organized in a style you like.

## Review
This generally wraps up our coverage of REST APIs. Next we will be moving on to authorization and authentication. These are somewhat related to REST in that all APIs have protected content and there are some special ways we deal with that in a REST API, but it really isn't REST specific in the same way that the status codes in this module were not.

Hopefully at this point it should be very clear what makes a REST API restful and what doesn't. If you still are not clear this is really the last chance to get that clarity before the class moves on from the topic.