---
title: "More Authorization and Authentication"
description: "This week goes into a bit more detail on the topics of authorization and authentication as well as giving a broad look at security."
categories: ["Module"]
weight: 35
---

{{< title >}}
## Introduction
We have covered the major aspects of working with setting up an API and working with other cloud providers. The topics covered in this section are going to look at some broader concepts related to cloud computing along with a couple specific technical topics that we didn't have time to cover earlier.

## Key Questions
- How does Open ID Connect work in conjunction with OAuth 2.0?
- What is the CIA Triad of security?
- Of the concepts in the triad, which is the hardest to guarantee?
- What are steps that can be taken to help ensure security of data?


## Assignment Overview
This week you will implement a simple account system where you store protected content that only particular users are allowed to access.

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[jwt.io](https://jwt.io/)
: This website has a lot of useful information about JWTs including a JWT debugger you can use to inspect the contents of your JWT.

[Auth0](https://auth0.com)
: This is a good provider of free authentication services. Overall it is a bit simpler than Google to use for very basic authentication like in this week's demo but the documentation is a little lacking.


## Review
Hopefully this gives you a bit more information about authentication after mainly focusing on authorization last week. In addition it pulls together the two in the demo to show how we can authenticate a user at a 3rd party website then use the JWT provided by that website to authorize them to access resources on our server.