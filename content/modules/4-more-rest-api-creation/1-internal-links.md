---
title: "RESTful Links"
description: "This exploration will look at how we navigate RESTful APIs."
categories: ["Exploration"]
weight: 1
---

{{< title >}}
## Introduction
So far we have not thought too hard about all of the theory behind REST, and we don't really need to. But an important piece we have not talked about and have thus far ignored is using hypermedia to help keep track of the application state.

Hypermedia is basically media which is linked to other media in a network of nodes. When you click on a URL in a webpage you are following a *hyperlink*. This all fits into REST because we want to navigate between various resources in our API and we want to use hypermedia to do that.

For example, if we are looking at a guest list for a room in our lodging app, we should be able to use hyperlinks to navigate to one of those guests and get information about them.

## The Usefulness of Links
Consider these two different entities from two different APIs:

```json
{
  "total_count": 24,
  "entries": [
    {
      "type": "folder",
      "id": "192429928",
      "sequence_id": "1",
      "etag": "1",
      "name": "Stephen Curry Three Pointers"
    },
    {
      "type": "file",
      "id": "818853862",
      "sequence_id": "0",
      "etag": "0",
      "name": "Warriors.jpg"
    }
  ],
  "offset": 0,
  "limit": 2,
  "order": [
    {
      "by": "type",
      "direction": "ASC"
    },
    {
      "by": "name",
      "direction": "ASC"
    }
  ]
}
```
This example is from the Box API. It is looking at a collection of files within a folder. The following example is from GitHub, it is the first in a list of Gists:

```json
[
  {
    "url": "https://api.github.com/gists/aa5a315d61ae9438b18d",
    "forks_url": "https://api.github.com/gists/aa5a315d61ae9438b18d/forks",
    "commits_url": "https://api.github.com/gists/aa5a315d61ae9438b18d/commits",
    "id": "aa5a315d61ae9438b18d",
    "node_id": "MDQ6R2lzdGFhNWEzMTVkNjFhZTk0MzhiMThk",
    "git_pull_url": "https://gist.github.com/aa5a315d61ae9438b18d.git",
    "git_push_url": "https://gist.github.com/aa5a315d61ae9438b18d.git",
    "html_url": "https://gist.github.com/aa5a315d61ae9438b18d",
    "files": {
      "hello_world.rb": {
        "filename": "hello_world.rb",
        "type": "application/x-ruby",
        "language": "Ruby",
        "raw_url": "https://gist.githubusercontent.com/octocat/6cad326836d38bd3a7ae/raw/db9c55113504e46fa076e7df3a04ce592e2e86d8/hello_world.rb",
        "size": 167
      }
    },
    ...
  }
]
```

It is trimmed down to make it fit better. But notice how items are referenced in these two different responses.

The Box simply lists types and IDs of the things within the collection. GitHub lists things first by their URL then by their ID. Now imagine writing a program to interact with these APIs. Which one do you imagine would be easier to navigate?

In the Box API we would need to know what URL one uses to access files. Then we would need to construct a URL using the ID we got from the list and visit it. The GitHub API does not require any of those intermediate steps. The URL is immediately presented to us. We simply make a request to that URL and we will get the data we seek.

## Where Should Links Point?
Recall that when we were talking about accessing things in our lodging apps URL structure there were times where multiple things might have pointed to the same resource. For example `/lodgings/2/guests/5` might return the data for guest `5` if they were staying in lodge `2`, or it might return an `Error 404: Not Found` if that guest is not staying in that room. But it would not be unreasonable for it to return the information for guest `5`. But is that really the most direct and canonical path to that guest? When that guest checks out of that lodging they will still exist in the system. But they will no longer exist at that URL.

The URL we probably want to associate to that guest is something like `/guests/5`. We don't want to pull the lodgings into it at all. So to reiterate, if we were looking at all guests checked into a particular lodging via a url like `/lodgings/3/guests` we could reasonably expect to see an array of guest objects returned and each of those guest objects should have a URL included that would allow us to access it directly.

The terminology for a link that points to its own resource in this class is a **self link**. If an assignment asks you to implement self links for all resources that means that if a resource can be accessed directly somehow, the link to do so should be included in all representations of that resource.

## What Other Links Might We Want?
### Parent or Owner Links
Consider a one-to-many relationship. In our lodging application we could imagine that we might keep multiple credit cards on file for each guest, but that we would not expect a credit card to be shared between different guests.

In a situation like this we might want to add a link to a credit card resource that points to the owner. We might call this an *owner link* in this case. There is not common terminology for this as it will depend on the use case. But having a link to navigate back up a hierarchy is common.

### Pagination
We will talk about this in a lot more detail soon. But we can expect to see lots of links when it comes to navigating large result sets. Sometimes we can navigate only one way, like in a singly linked list, or some times we can navigate both ways. In either case the collection will often contain a link to get the next chunk of results in that result set.

### Kinds
Finally we might want some sort of link to get us back to the parent *category*. This is a little less common than other kinds of links. But if you are going for a very complete REST implementation you might see a link to a parent category like a lodging object might have a `category` URL that simply pointed to `/lodgings`.

## How Much URL
I would always advocate for having a absolute URL. In other words, it should include the protocol, host and path. So we would want to see `https://examplesite.com/lodgings/5` rather than `/lodgings/5` when looking at a URL attached to an object.

This URL should be generated using information gathered from the request. For example, you can set up you sever such that when running locally and getting requests on `http://localhost:8080`, that will always be the thing that prefixes your path. But when deployed you will prefix your path using `https://myapp.appspot.com`. This data can always be pulled out of the request sent by the client and can then be used to dynamically generate URLs.

I have seen arguments to leave it at simply the path, but the whole point of this exercise is to make the programming easier for the client. There is no reason to adhere to an overly strict interpretation of the REST rules at the expense of the ease of use for your users.

## Review
This section should give you a good idea of why we might want to use URLs in addition to simply kinds and IDs in our API. It can make it much easier for users to navigate your API and avoids the need to build URLs and look up or have hard coded paths.