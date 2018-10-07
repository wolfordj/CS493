---
title: "Objects in Good API Design"
description: "This will look at implementing a REST API at a fairly high level. This is a good time to review some object oriented programming practices and see how we can apply them."
categories: ["Exploration"]
weight: 5
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
REST APIs lend themselves well to object oriented design. We are mainly using JavaScript in this class with Node.js, so it may not be quite as clean as it would be in something like C#, but the same principles will sill apply, so lets take a look!

## What are the main Types?

From the last section, we know there are broadly two sorts of things we will be dealing with. Collections as well as resources. The sorts of operations we are going to do on those things will be fairly different. So this might be a good place to look at when making our initial classes.

## Resources

You should consider what sort of operations your resources have in common. In the REST APIs we will be making in this class we may not ever go beyond CRUD operations (Create, Read, Update, Delete). In general, you can expect that pretty much every resource will need to support these operations.

As you start working on more projects professionally you will find that your team probably has a library they use that maps these actions to a database. Using a library that does this might be too much overhead for this class, but the concept behind it is sound.

### Models

A good path to take might be to implement a model class that handles saving and loading properties to a database. This class might have methods that map to the HTTP verbs like `.get()`, `.post()` etc.

JavaScript does not have great support for abstract classes, so there may not be much value in defining this class in code, but understanding conceptually that you want all models to implement those functions is important.

### Controllers

Another piece of the architecture you will want to implement are controllers. The models will load and save data to the database. Maybe you can filter or select groups of items as well. But the controller basically converts the commands the server receives into data you model can deal with, and calls the appropriate method of your model. Then it also can relay the response back to the client in the appropriate format.

## An Example

[This implementation](https://github.com/GoogleCloudPlatform/nodejs-getting-started/tree/8bb3d70596cb0c1851cd587d393faa76bfad8f80/2-structured-data/books) of a Book tracking system implemented by Google to demonstrate storing structured data is a fairly good example. Note that there are two models, one based in the Datastore and on based on SQL that can easily be swapped out. In addition note that there are two controllers, one based on web browser interaction and one based on REST interaction. This level of abstraction makes it easy to make changes to you system because functionality is well encapsulated.

## Review
As you work on the assignments and particularly later in the class when you are working on the final project you may find that there are times you are reusing a lot of code or finding that changing one file makes big impacts to many other files. That is a good indication that you code is not well encapsulated. If that ends up happening come back and review this section and the sample code. You might find some good ways of handling things that will work out better for you.