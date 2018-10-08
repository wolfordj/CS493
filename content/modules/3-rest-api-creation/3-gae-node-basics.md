---
title: "Google App Engine and Node.js"
description: "This will walk through the basics of setting up the framework for a Node.js application on Google's App Engine framework in Node.js."
categories: ["Exploration"]
weight: 15
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
It can be difficult getting a new tool or library up or running. I would encourage you to try this weeks assignment without going through this section. Once you depart school and are working professionally you likely will be tasked with sometimes setting up new projects from scratch. This is often a challenging task as knowing where to start can be hard to figure out. This is a good opportunity to experience that with a language and framework you already have some experience with but a platform and back end that is new.

So see if you can get through it using only 1st party Google documentation and 3rd party guides that are not this one. If, after some time you feel like you are unable to make progress, then head back here and it should get you set on the right track.

As a starter you might want to look at the basic datastore tutorial to make sure everything is configured. Here is a demo of me walking through it

{{< kaltura 1_adi9dnil >}}

## Lodging App
This demo app is meant to be the *start* to the lodging/guest app. It will show you how to set up the routes for lodgings, but isn't going to show how to implement guests or how to implement adding guests to rooms.

While not entirely trivial to add those features, they are somewhat intuitive and once you see how CRUD operations work on one entity, it should be apparent how that would be generalized to other entities.

### The Code

[This Gist](https://gist.github.com/wolfordj/e4aa4c936311110940b62feb54108989) houses the code required to get this started. `server.js` has the important code that demonstrates the principles. `package.json` is so you can see which libraries were used, in particular note that the Google Cloud Datastore library was used. Finally `config.json` is included because I based this off of the Google Books implementation and if you wanted to do something like create multiple backends you would use that config file to do so. It isn't actually used in this particular code sample.

### Video Walkthrough
Most of the information is best expressed in a video walk through of this code seen here.

{{< kaltura 1_04nmatev >}}

{{< kaltura 1_oq71f0rt >}}

### Highlights

#### Keys

Keys in this code come in two flavors, kind only `var key = datastore.key(LODGING);` where the key's kind is specified but there is no ID. We do this when we are posting a new lodging and we want the datastore to make an ID for us. When it does, this keys `id` property will be updated to hold the new ID assigned by the datastore.

The other is a key had has an id. `const key = datastore.key([LODGING, parseInt(id,10)]);` here we have a key, still of kind `Lodging` (`LODGING` is defined to be the string `'Lodging'`) but now it also has an `id` based on the value of the `id` variable passed into `parseInt`. So this key points to a specific lodging and when we pass it to a function like `Datastore.get` or `Datastore.save` it will retrieve or save a specific lodging with the ID we provided.

#### Types
Make sure you keep track of your types. Things passed in as query string parameters will be strings. Things in a request body can be of various types.

## Next Additions
If you were to add guests to this, the main challenge will be to figure out how to keep track of which guests are assigned to which rooms. A good practice would be to keep a list of guest keys as a property of lodgings. Then you could request those keys when you want to list the guests.

A decision you need to make is if you want to store those keys as key objects and convert them to strings when a client requests them or if you want to store them as strings and convert them to keys when you need to use them with the Datastore.

## Review
This should give you a pretty solid platform with which to work. From here you can change the names or properties of entities. You could work on further abstraction or you could just use this as a basic idea and make your own implementation just borrowing some ideas from this one.