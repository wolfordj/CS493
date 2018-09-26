---
title: "HTTP Verbs"
description: "HTTP Verbs are a key concept to understand when working with REST APIs. They let the server know what we want to do with a resource."
categories: ["Exploration"]
weight: 5
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
Verbs are the key to letting us interact with REST APIs. Before we had mentioned that `https://example.com/class/1/student/5` might refer to a student with an ID of `5` enrolled in a class with an id of `1`. Broadly speaking there are 4 major things we could do at this point. We could *create* a new thing and add it to the student, maybe an assignment for example. We could *read* the data about the student or the class in the database. We could *update* the student maybe changing the overall grade in this class. Finally we could *remove* the student. Generally in a REST API these are the 4 things you are going to be doing. Creating, Reading, Updating and Deleting. These are known as the CRUD operations.

## GET
A GET request is an idempotent (meaning calling it multiple times will not make multiple changes to the state of the server) HTTP method. It requests some data from the server. So when the client needs to view data, any sort of data and not change anything a GET request should be used. If you want to change any sort of data on the server then GET is an inappropriate method to be using.

Looking at the Lodgings example:

```http
GET /lodgings/5 HTTP/1.1
Host: exmaple-lodging-service.com
Accept: application/json
```

This might return a response like:

```js
{
    "id":"5",
    "name":"Roach Hotel",
    "description":"Roaches check in but don't check out",
    "price":"5.99"
}
```

Accessing this URL with a `GET` request gets the information for us. You should have done this with quite a bit of frequency in your web development class as it is a really common way to get data with AJAX calls generally, even when not working with REST APIs.

{{< kaltura 0_sntcw94q >}}

## POST
You should have already used `POST` from prior web development classes. However you may have not been using it as the REST requirements specify. `POST` should only be used for the creation of new resources. We will later clarify the different between `POST` and `PUT`, both of which can be used for the creation of resources. But `POST` should be used when the location of the resource to be created is not known. For example, if you wanted to add a new lodging to the database you would `POST` to `/lodgings` with the specifications of a new lodging. The server will then create a new lodging and generally will respond by providing the id or a link to the newly created resource.

This is not idempotent. Multiple requests to the same URL that include the same payload will create different lodgings. That is each request will generate a new resource with a new id, even if all the other attributes are the same.

If we had the following state in our server:

```js
{
"kind": "collection",
"self": "/lodgings",
"contents": [
	{"id": "0",
	"self": "/lodgings/0",
	"kind": "lodging",
	"name":"Pleasant Inn",
	"description": "A pleasant place to stay.",
    "price": "40.99"},
	{"id": "1",
	"self": "/lodgings/1",
	"kind": "lodging",
	"name":"Conformable Inn",
	"description": "Comfortable enough I suppose.",
    "price": "100.00"},
	{"id": "3",
	"self": "/lodgings/3",
	"kind": "lodging",
	"name":"Acceptable Inn",
	"description": "Its OK",
    "price": "117.25"}
]
}
```

and we made the following POST request:

```http
POST /lodgings HTTP/1.1
Host: exmaple-lodging-service.com
Accept: application/json
Content-Type: application/json
```

With the following body:

```js
{
	"kind": "lodging",
	"name":"The Shack Out Back",
	"description": "I am not sure this is legal",
    "price": "9.99"
}
```

we would potentially end up with a new sever state that looked like:

```js
{
"kind": "collection",
"self": "/lodgings",
"contents": [
	{"id": "0",
	"self": "/lodgings/0",
	"kind": "lodging",
	"name":"Pleasant Inn",
	"description": "A pleasant place to stay.",
    "price": "40.99"},
	{"id": "1",
	"self": "/lodgings/1",
	"kind": "lodging",
	"name":"Conformable Inn",
	"description": "Comfortable enough I suppose.",
    "price": "100.00"},
	{"id": "3",
	"self": "/lodgings/3",
	"kind": "lodging",
	"name":"Acceptable Inn",
	"description": "Its OK",
    "price": "117.25"},
    {"id": "4",
    "self": "/lodgings/4",
	"kind": "lodging",
	"name":"The Shack Out Back",
	"description": "I am not sure this is legal",
    "price": "9.99"
    }
]
}
```

The server got our request to make a new lodging entry. We specified the what we wanted the details of the lodging to be, then the server generated a representation of it and assigned it an ID and a URL. In this case the URL and ID were sequential, but it does not need to be. It could be created by some sort of hash function that generated a very long string identifier, for example. The important bit to note is that we didn't specify the location first.

{{< kaltura 0_k172f4t6 >}}

## PUT
`PUT` is an idempotent method to crate or replace data. You must know the resource location where you are wanting to put the resource you are sending.

An example would look like:

```http
PUT /lodgings/4 HTTP/1.1
Host: exmaple-lodging-service.com
Accept: application/json
Content-Type: application/json
```

With a body like:
```js
{
    "kind": "lodging",
    "name":"The Nice Cottage Out Back",
    "description": "Isn't it quaint",
    "price": "99.99"
}
```

This would replace the entire contents of the lodging found at `/lodgings/4`. This is important to note. If you, for example, left out an optional property that previously existed, it would be removed with the operation. It could be thought of as deleting what was there then creating a new item in its place.

{{< kaltura 0_vourefor >}}

## PATCH
`PATCH` is used for partial updates. It should contain a set of instructions to update the resource being patched. This can get quite complex. For this class we are simply going to use it to do partial updates or simple additions or removals. If you send a request like:

```http
PATCH /lodgings/4 HTTP/1.1
Host: exmaple-lodging-service.com
Accept: application/json
Content-Type: application/json
```

With a body like:
```js
{"description": "It is so cozy"}
```

It would replace the contents of the description with "It is so cozy" but change nothing else. This is in contrast to a `PUT` which *would* delete everything else. If you wanted to delete an attribute with a `PATCH` you would need to explicitly set it to an empty string or `null` value in the body.

{{< kaltura 0_uwbroujv >}}

## DELETE
`DELETE` is fairly self explanatory. It is an idempotent method that deletes whatever id is specified in the request. So sending a `DELETE` request to `/lodgings/4` would simply remove the entry for lodging 4. If you had a more complex API that had references between things like lodgings and guests, you would need to make sure to properly handle the situation where a guest potentially had a reservation for that now deleted lodging. That might mean deleting the reservation or potentially rejecting the delete due to it being reserved by a guest.

{{< kaltura 0_qyc1xwhy >}}

## Activity
Head over to the GitHub [REST API](https://developer.github.com/v3/) and look through their documentation in a little more detail. Try to get a sense of how various operations work in their API which is a good model to follow.

It is unlikely you will actually be able to interact with it because getting authentication to work is non-trivial (but is a topic that will be covered eventually in this class!).

## Review
So that is the basic set of REST verbs. The list of HTTP verbs is more numerous than just those provided above but for simplicity the above verbs are all that are used in many REST applications.

Between this set of actions and the previous discussion of routes you should have a good idea of how to, on paper, create a set of routes and describe how you would interact with them using various verbs.