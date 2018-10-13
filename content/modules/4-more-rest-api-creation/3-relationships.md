---
title: "RESTful Relationships"
description: "Relationships in REST APIs"
categories: ["Exploration"]
weight: 15
---

{{< title >}}
## Introduction
In principle, relationships are not that new or exciting when dealing with a REST API. The same sorts of relationships still exist like they do in a standard relational database. We have one-to-one, one-to-many and many-to-many relationships.

That said, there are some interesting choices we need to make when returning results.

## Basic Relationships
Lets return to our lodging API. `/lodgings/:id/guests` could very reasonably be expected to return the lists of guests for a particular lodging. This could be a one-to-many or a many-to-many relationship depending on how we set things up. If a guest can only reserve one room, but a room can have several guests, it is one-to-many, if a guest can reserve multiple rooms it is many-to-many.

But from the perspective of the this URL it does not mater, either way, we are getting back a list of guests here. If this is a supernaturally large room, that is maybe bigger on the inside, we might need to paginate the list of guests.

This isn't too exciting.

### Other Representations
But what about the URL `/lodgings` or `/lodgings/:id`. Now we need to start making some decisions based on expected use cases.

Lets say this is a family resort and rooms have on average 4 guests staying in them. We need to decide when to display that guest information and how much to display.

Consider the following set of lodgings that might be returned by `GET /lodgings`.

```json
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

It makes no mention at all of guests. But it is somewhat compact. Now imagine that a guest had about as many properties. We could nest guests within lodgings like so:

```json
{"id": "0",
	"self": "/lodgings/0",
	"kind": "lodging",
	"name":"Pleasant Inn",
	"description": "A pleasant place to stay.",
  "price": "40.99",
  "guests":[
    {"self":"/guests/2",
    "f_name":"John",
    "l_name":"Doe",
    "rewards_member":false,
    "is_minor":false},
    ...
  ]},
```

this is perfectly workable and correct, but it could potentially double the size of our result response because every room would have a fully populated list of guests. And if we had a ton of guests in a room there is no good way to deal with nested pagination so this can end up being problematic.

However, it *might* be a good approach for the url `/lodgings/:id` where we are only looking at a *single* lodging. If we know the list of guests will never be too long it would present all of the data at once.

There are two other viable options here. One is to make the guest listing less verbose in the lodging representation. So we might include only a link, or only a link and a name. So a guest list, in the context of a lodge object might just look like

```json
"guests":{
  "self":"/lodgings/5/guests",
  "count":2,
  "elements": [
    {"name":"John Doe",
    "self":"/guests/5"},
    {"name":"Jane Doe",
    "self":"/guests/8"},
  ]
}
```

Finally we could provide just a count and link to the list of guests

```json
"guests":{
  "self":"/lodgings/5/guests",
  "count":2,
}
```

The correct choice here depends on your implementation.

## Many-to-Many Sides
Another place we need to be a little careful is with very asymmetric many-to-many relationships, but this isn't unique to REST APIs. If we had a photo site that had 50 million photos and 500 tags, we need to be a bit cautious setting this up.

Consider the potential contents of something like `GET /tags/cat`. One could imagine this would return some sort of information about the cat tag. Maybe some info on how many photos use the tag, maybe a list of related tag (kittens, pets, cute), maybe the most popular photo with the tag etc.

What it probably should not include is a list of all the photos that have the `cat` tag. This could be in the many thousands of results. We would want to be sure to have nothing more than a link to `/tags/cat/photos` and maybe a count, like in the last example. Anything else would make a totally unreasonable monster of an object to deal with.

But consider the flip side. If we have `GET /photos/my_cat` it would probably be pretty reasonable to return all of the tags associated with the photo in the photo object. It probably has no more than a couple tags, so returning them along with their self links would be no big deal and many applications would want that data so it would save additional requests.

## Internal Storage
This is where things get really different depending on your backend. With MySQL you know how you handle all these things with relationship tables and the like. 

In general, to avoid inconsistency issues you often want to store keys to other objects and load them as needed. Like doing a JOIN in MySQL. But that may not always be the best option.

Take the photo example, it is unlikely that the tag `cat` is going to change its name any time soon. We could, because it is very small, store a copy of the relevant data (eg. the name of the tag and a link to it) with the photo and not need to make a query to the database.

On the other hand, information about a room a guest is staying in might update frequently so it would be important to query the database when the guest is loaded to make sure we have the most up to date information about the room the guest is staying in.

## Review
Hopefully this gives you a good idea of what it looks like to deal with relationships in a REST API and has helped you make the transition from MySQL to thinking about some other less normalized options where appropraite.