---
title: "REST API Creation"
description: "Having spent some time interacting with a REST API this module will introduce the concept of making a REST API that others can interact with."
categories: ["Module"]
weight: 15
---

{{< title >}}
## Introduction
<!--- Introduce the topic in this section -->
This module is designed to walk you through making a basic rest API. It will show you how to specifically use Node.js and Google App Engine with the Cloud Datastore to make a REST API running on the cloud.

## Key Questions
- What are good URLs to use in a REST API?
- How are routes set up in Google App Engine?
- What are some key differences between accessing items in the Datastore and SQL?


## Assignment Overview
This week you will lay the framework for a basic REST API. You will need to implement a basic two entity API where the two items can be related. Future assignments will build off of this one.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[Node.js Google App Engine Documentation](https://cloud.google.com/appengine/docs/standard/nodejs/)
: The main documentation for Google App Engine with Node.js.

[Google Cloud Datastore Documentation](https://cloud.google.com/datastore/docs/concepts/entities)
: The main documentation for the Google Cloud Datastore. Pay attention to the how-to guides. They contain a lot of helpful info.

[Google Cloud Datastore Node.js Reference](https://cloud.google.com/nodejs/docs/reference/datastore/1.4.x/)
: This specifically looks at the Node.js client library for the Google Cloud Datastore.

## Review
The key for this module is to get a good understanding of the fundamentals of a REST API. You should understand how to do the CRUD operations on a single entity and should have spend some time considering and implementing possible solutions to related entities. In later modules we will talk about some more best practices and advanced functionality. But for now you should have a pretty good understanding of the basic operations.