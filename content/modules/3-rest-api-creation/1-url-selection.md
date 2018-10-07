---
title: "Deciding on URLs"
description: "This exploration will look at URLs in REST APIs."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
In this section we return to the concept of resources representing URLs. We are going to talk in some more detail about what this means and how it is applied to a web application. Everything in this section will assume the data is stored as a simple JSON representation. For our example we are going to to use a lodging provider that has provides lodgings to guests. These will be the two kinds of entities that we will keep track of in our application. We will look at what a REST URL structure for this might look like.

## URLs Identifying Resources
<!--- Main topic headings are at ## -->
Again, because it cannot really be overstated, every URL should point to a thing. By convention I am going to start all URLs with a `/`. The implication is that the appropriate domain name would be prefixed onto the URL (e.g. `https://mysite.com/` would begin the URL). So lets start with the simple case of an incredibly small lodge that has one room and no guests. It might look like when we issue a `GET` request with `Accept: application/json`:

```json
{
  "id": "1",
  "name": "The one lodge",
  "description": "It will rule them all",
  "price": 100.00
}
```
But keep in mind, we could use `Accept: text/html` and get back a web page that displays this same information. Whatever URL we are sending this `GET` request to represent the resource. And the resource is the lodging. The resource *is not* the JSON representation of it or the HTML representation of it. That is the difference between a resource and its representation. If we alter the resource by using a `PUT` to replace it, and we use XML in the payload, it doesn't replace it with XML. It just changes the underlying data and then we can request it again using JSON, XML, HTML or whatever else the server might support.

This is somewhat similar to when you make a website that is backed by a SQL database. There can be multiple pages that show the same data in different ways, and modifying that data in any particular page will make it persist to other pages.

I spend some time on this because while we *could* implement a server that can return several kinds of data, we may only do that once or twice. For the vast majority of this course we will be sending and receiving JSON data for the sake of simplicity. But we need to be aware that that isn't the only way to do it.

## Things, Not Actions

It bears repeating. Our URLs should always contain *things* or identifiers of things. The URL `/robots/wall-e` would be an appropriate URL in a REST API. The URL `/getRobot?name=wall-e` would not be an appropriate URL because it is an action. The URL does not represent a resource, it represents an action that can get us a resource.

This can get a little tricky with things like *search*. It may be that you implement a search using filtering of a collection. For example `/robots?contains=wall` might return a list of all robots that have the word *wall* in them. That would be fine, the URL terminates at the `?`. Everything past that is the query string.

You could also implement it as `/robots/search` but it gets a little dicey and you are likely to start workplace arguments. If this is a search that you can save then it is certainly a resource. For example, I can save a Google News search and be notified when additional news stories matching that search show up. I can go back to that search and edit parameters. On the other hand if I just type 'Kittens' into Google and run a search it is a little harder to defend the results as being a resource.

There are not always black and white answers, but it is important to consider the implications of your choice and to be consistent.

## URL Pattern Rules of Thumb

As we look at URLs there is a fairly common pattern that often emerges. You will see URLs that usually conform to `/collection_1/id_1/collection_2/id_2...`. An example might be `/classes/CS493/students/Peter-Ian-Staker` or `/lodging/5/guests/`. It is difficult to come up with some other pattern. You generally need to start with a collection, you can then return that collection, or access an item in that collection. At that point you can return the item, or access a collection associated to the item. Then the process repeats with the items collection. You can return the collection or an item from it.

This makes sense, a collection typically has nothing associated with it other than perhaps some properties like the length or type of item in the collection. So the URL `/classes/students` would not have any reasonable meaning. We don't know which students we would be looking at. But `/classes/CS493/students` makes it clear we are looking at the students in CS493.

Likewise when we are looking at individual items if something is a property we can just pull it directly from the item `/students/Peter-Ian-Staker` might contain the GPA for that student along with other properties like year enrolled, library balance etc. There would be no need to access `/students/Peter-Ian-Staker/GPA` because that is simply a numeric property. But we *might* want to access a collection, like grades for all classes. In that case `/students/Peter-Ian-Staker/grades` might return a collection of classes and associated grades for Mr. Staker.

## Final URL Thoughts

We will talk more about some specifics of how we handle some special cases. But looking at the big picture is should be fairly clear that we use URLs to access collections and then specific items within those collections. But it isn't quite so simple. We do, at some point, need to decide what collections stand on their own and what collections only exist as a part of a different resource and many might exist in both places.

For example, in our lodging system we definitely want a collection of lodgings `/lodgings`. We also probably want a list of guests who are in/have reserved a lodging `/lodging/:id/guests`. But we also might want a guest list of all guests who are at or have reservations at our lodge `/guests`. And further, we might want a list of all lodging reservations a guest has made `/guests/:id/lodgings`. So in this case lodgings can stand on their own or as a collection owned by a guest. And guests can stand on their own or as a collection owned by a lodging.

But suppose we had a list of credit cards on file for each guest `/guest/:id/credit-cards`. We might not have any need for a master list of all credit cards on file. Instead it might be fine to only be able to access the cards on file for a guest via the guest's URL.

There are not any really clear rules for these sorts of decisions and it depends largely on use case.

## Review

Hopefully it is becoming clear how we might go about structuring a REST API. There are some pretty good rules we can follow when it comes to figuring out if our URL pattern is valid. If we have to collection types adjacent in a URL or if we have two specific resources adjacent in a URL something has probably gone wrong because we are not following the collection/item pattern.