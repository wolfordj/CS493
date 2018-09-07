---
title: "API Introduction"
description: "This is designed to get you familiar with the idea of an API which is basically a software service without a UI that other programmers can use."
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
An Application Programming Interface or API is the mechanism by which a programmer might interface with an application. APIs exists at almost all levels of the software stack. Operating systems expose systems calls as an API that allows access to the lower levels of the operating system. C++ libraries expose APIs that allow you to access various data structures or features in the language. The standard template library is a good example of this.

## Programs vs APIs
It can be a bit confusing at first to figure out what actually makes an API different from a typical program or functions in that program. Node.JS makes this fairly easy to see. For example, in the linked `string_decoder.js` only 4 or 5 functions are exported in the StringDecoder object. However, there are many many functions that follow which are needed for those functions to work. The programmer does not have access to, know about or need to know about the inner workings of the `string_decoder` module. They only need to access a specific set of function calls to use it. Those exported functions would be considered part of the Node.JS API. They are what the programmer uses to interface with Node.JS. There is a lot of stuff that goes into making Node.JS work, but the stuff that is actually exposed to the programmer using it is what is considered an API.

You may have seen similar things when you created data-structures or other libraries and then provided a header file that had function prototypes a user of that data structure could call to use it.

In summary there are lots and lots of functions, classes and variables that are part of a library or program. But only the ones that an external programmer has access to are part of the API.

## Web APIs
So you may be wondering, at this point how exactly APIs are going to fit in to a cloud and mobile class. As it turns out web APIs are how almost all applications in the Internet communicate with each other. I am going to show you a couple examples here but I want to make it very clear this is not how you should make an API in this class but Remote Procedure Calls (RPCs) are a little easier to understand than a REST API at first so we are going to show a couple examples.

`http://exampleschool.edu/admin/addStudent?name=Jack%2BSparrow%26status=Freshman`
This would be a pretty typical RPC to add a student to a school database. The browser would make a request to the addStudent URL and pass it some parameters. The server would get these parameters and pass them on to a function (aka a Procedure) which would then run on the server and add the student to the database. So someone at a remote location called a procedure on the server, passed it the required parameters and it was run on the server.

Likewise you might delete a student via a call like:

`http://exampleschool.edu/admin/deleteStudent?id=1141204`
This would call a function to delete a student and you would be passing the id of the student to delete.

### Web API Responses
In general a web API is going to respond using a notation like JSON or XML. Sometimes they may give you just plain text or HTML, but more commonly you will get back JSON or XML because those are easier for programs consuming the data to parse.

## HTTP Specific Features
In addition to the URLs that are used to make calls can often make use of a lot of data that is 'hidden' in the request that is sent to it. Things like the request type (GET, POST, PUT etc), the accept type, authentication headers and so on.

Arguments can also be passed in the body of the request, which is a bit further from a standard looking function call where arguments are passed in the URL, but the idea is still the same, you are calling some function and passing it some data and then it is being executed on the server.

{{< kaltura 0_nt0478h8 >}}

## Review
This is just some background on APIs more broadly. You probably even implemented the basics of an RPC based API in your web development or database class when you had URLs to modify the contents of a database.