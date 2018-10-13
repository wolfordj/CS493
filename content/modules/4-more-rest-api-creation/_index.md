---
title: "Yet More REST API Creation"
description: "Making REST APIs can be a bit tricky. So this module expands upon the prior giving you some more time to get this built."
categories: ["Module"]
weight: 20
---

{{< title >}}
## Introduction
This week moves on from the basics to cover some topics that will make your REST API actually usable by clients. We will look at making it easier to navigate a REST API, dealing with large sets of results and setting up relationships between different entities in the API.

## Key Questions
- Why might we want to set up links as parts of objects?
- How can we deal with large sets of results?
- What are some of the pitfalls we can encounter when working with large result sets?
- What are some special considerations when working with relationships in REST APIs?


## Assignment Overview
This weeks assignment will be similar to last weeks in that you will implement an API according to a specification we provide. The changes being that internal links will be required, we will want to paginate result sets and there will be some additional emphasis placed on relationships between entities.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[Web API Design Book](https://pages.apigee.com/rs/apigee/images/api-design-ebook-2012-03.pdf)
: This book addresses REST API design at a good level for this class. It talks about many of the topics we will look at in this week. It isn't required, but is good if you are struggling with any of the REST concepts.

[Cloud Datastore Cursors](https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets)
: This goes over the use of cursors in the Google Cloud Datastore. Remember that the code sample all have a link at the top to get to a GitHub repository that has full working code samples.


## Review
This is the second of three weeks covering REST API design. We have covered most of the fundamentals of REST at this point. From here we will look at stuff that ends up being a bit more application specific and we can look at some exceptions to the usual rules and practices that will make APIs easier to use.