---
title: "Introduction to REST"
description: "This looks at what it is that defines the REpresentational State Transfer model of an API. It is a specific set of requirements that can help make APIs easier to use."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
Representational State Transfer, much more commonly called REST is a very specific way of designing an API. The core concept of a REST Web API is that all the URLs identify resources, we will talk about this in some depth. Another important aspect of REST Web APIs is that they are stateless. The server does not store any information about the current state of a client. There are several other constraints, but these are the main ones we will focus on in this class. That said we will discuss all of them.

## Resources
This is really at the heart of a REST implementation. It is also at the heart of philosophical programming arguments that turn violent during lunch. Every single URL in a REST API represent a resource. A resource is a thing, a noun: dog, student, class, spaceship, report, item, inventory. These are all things, they are resources. When I talk about a URL identifying a resource, I mean everything that comes before the query string. For example `http://this.is.part.com/of/the/url?this=is+not`, everything before the ? is what the URL is identifying. What comes after the ? is the query string.

As a trivial example `https://example.com/game` might represent a single game people can access on a server. A more realistic URL like `https://example.com/class/1/student/5` would represent a resource at every level (except the domain name). class represent a collection of classes. 1 represents the class with an id of 1, student represents a collection of students and 5 represents the specific student with an id of 5.

There are some things that are very tempting to do with a web API and they are not ‘wrong’, but they are very much not RESTful. In this class we are explicitly dealing with REST APIs so, unless an explicit exception is made you should never make a URL like I am about to describe.

`https://example.com/addStudent` or `http://example.com/addStudent.html` or any variation of a URL that has the letters addStudent in it. As mentioned before a URL must point to a representation of a resource. addStudent is not a resource, it is not a thing, it isn’t just a noun, it has a verb in it. And verbs within a URL is what REST seeks to banish from this world and the next. If you make a URL, and it has a verb in it is very likely that what you are doing is not RESTful. Again, in some contexts this is OK, but not in this class. We will cover resources in yet more detail in another section.

## Stateless
A stateless API in a REST architecture must store no data about the current state of a client. The client must send all the information needed to process that client’s request within the request itself. The server cannot rely on any data previously sent by the client.

The most common way you will see this violated is with websites that use server side sessions. You may have implemented yourself or seen implemented a login system where a user logs in once and then the state of their login is stored on the server, this is RESTless (I didn’t make up that term). In a RESTful implementation of a login system whatever is used to authorize the user is sent with every single request. A client is never ‘logged in’. Every single request is treated as its own wholly separate interaction.

Another common place you might see this violated is with a history. Suppose when a user uses a web service they are uniquely identified and the server keeps a log of which pages they have viewed. And further suppose there is a way to navigate back to the previously viewed page. This is very likely be RESTless because the server is keeping track of the state of the client. The ‘go back’ interaction only works if the server maintains state information about the client.

But have caution, it is easy to over generalize here. Cookies are almost always a part of sessions. But cookies are not, by themselves RESTless. They are a tool that is used to store data that is sent to the server with every request. This is fine. The client can store state information and send it to the server with every request. It can be confusing though because the way a server that uses server side sessions tracks its clients is by using cookies with unique identifiers. And that is RESTless because the server is tracking information about that particular cookie.

### Ok, Thats Great, Why do we Care?
Well, let me tell you! Because state is incredibly messy and needs to be meticulously tracked. When one is working on a single server with a small number of clients tracking state can make things simple and easy. But consider a provider like Google. They literally have thousands upon thousands of servers across the world.

One great feature of distributed computing is the ability to balance load across numerous servers. If the west coast is getting a lot of traffic but people are asleep on the east coast, it might make a lot of sense to route requests to the east coast to lighten the load on west coast servers. But this becomes problematic if state is kept on servers. Now, instead of just having to read from a single server, every time the client’s state changes it needs to be sent to every single server that they could possibly use next. Alternatively they may be locked into accessing only a single sever for the duration of the session which could become problematic if it becomes congested or goes down. The better, more scalable solution is to not maintain state.

## Review
These are the big two. We are not really going to talk about statelessness any more. This concept is important, but also fairly straight forward. You may need to think a bit about how to handle situations where you used to use server side sessions to handle things, but overall it should make some sense and be somewhat intuitive when you are or are not storing client specific state on the server. URLs representing resources are so important and such a critical part of REST that we will have another entire section talking about them. In addition to these two parts of rest there are a few more constraints that we will also talk about in a different section. But when the topic of REST comes up, these are the major two issues that are almost always at the heart of it.