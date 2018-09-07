---
title: "REST API Usage"
description: "This module should introduce you to the concept of using a REST API which will likely be different from the APIs you may have made or interacted with in the past."
categories: ["Module"]
weight: 10
---

{{< title >}}
## Introduction
This module is going to discuss the concept of APIs and more specifically, RESTful APIs. An API is an Application Programming Interface. No one calls them that. If you do you will sound silly. It is basically the way for a programmer to access the functionality of a piece of software, library or hardware. REST is a particular style of making an API to make things a bit more standard on the web.

## Key Questions
- What is an API and what is it used for?
- What are the requirements for an API to be RESTful?
- How does one map a data model to a RESTful API?
- What is the relationship between REST APIs and the HTTP verbs?

## Assignment Overview
This week you will practice using an existing REST API by writing a series of tests to prove that it works. This should give you some insight into how APIs work before you jump into building one yourself.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[Web API Design](http://classes.engr.oregonstate.edu/eecs/winter2017/cs496/resources/Web-design-the-missing-link-ebook-2016-11.pdf)
: this is an eBook that goes into detail on REST at what I believe is an appropriate level of detail for this class and for the extent that many people will interact with REST APIs. It focuses much more on the URL structure and not so much on the use of verbs, but is nonetheless a good resource.

[Dan Fielding's Rest Dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
: the original, official, it all started here, dissertation by Dan Fielding. Chapters 5 and 6 are where the real meat of the content is. Consider the reading optional, but if you ever need to win an argument about REST, this is the document you should use to do so.

## Review
There is yet more to come on REST. But this is a good overview of the practical parts of REST that we will care about in this class. There are additional components to REST that we will not implement and there is quite a bit to be done in the area of proper HTTP status code usage which is also beyond the scope of this class. But for now, this should give you everything you need to design in the abstract, a REST API along with defining how one would interact with that API.