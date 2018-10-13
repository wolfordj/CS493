---
title: "Demo of Intermediate REST API Features"
description: "This gives an overview of intermediate REST features implemented in Google App Engine using Node.js"
categories: ["Exploration"]
weight: 15
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
This video looks at the lodging application as it is being updated to include more intermediate features. The Gist with the code sample can be found [here](https://gist.github.com/wolfordj/3080eeec83bdc3bcc916c3c8fcd3b383). This isn't a complete and functioning API, it is only built to showcase some important features and show how to do some specific tasks using Node.js and Google App Engine.

## The Box API Demo
{{< kaltura 0_lcd8eos6 >}}


## Review
<!--- Encourage students to reflect on what they should have learned from this exploration. -->
Between the complete examples in the Google App Engine documentation and this walkthrough that addresses some of the points that are not really hit on in the Google documentation you should be in a position where you can set up simple relationships, implement one-way paging using a cursor and implement links within an API.

I know as I was working on this code I was very close to needing to implement some further abstraction to keep things reasonable. My next steps, which you might want to take now, would be to implement modules for my entities that facilitate loading them into a JSON string and saving them back to the datastore. I know that I will need to update the PUT method for lodgings to accommodate the guest lists now, for example, and that would be much easier done if the load and save functions were encapsulated.