---
title: "Authentication in Node"
description: "This looks at how we would actually implement authentication in Node.js using Auth0"
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
This program demonstrates how one could go about implementing a simple authorization system in Node.js relying on a 3rd party to store usernames and passwords.

This particular flow is not as secure as it could be because the client needs to provide the username and password to my API for it to be relayed on to the Auth0 server. In a more robust flow they would be redirected to Auth0 via a browser. However, I did not want to add the complexity of all of those requests and you should have seen how that would work in a previous module.

This real purpose of this is to demonstrate relying on JWTs for authorization.

{{< kaltura 0_prbvrv6m >}}

<script src="https://gist.github.com/wolfordj/adfdfe420daa32278ec1005bd74c83ef.js"></script>
