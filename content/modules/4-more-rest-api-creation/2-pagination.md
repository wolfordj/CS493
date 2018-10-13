---
title: "Pagination in REST"
description: "Sometimes our servers store lots of things. Sometimes clients can't handle that many things. Pagination solve all our problems. Almost."
categories: ["Exploration"]
weight: 5
---

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
There are many databases out there with hundreds of millions of records. It isn't difficult to imagine that sending that many results at once could cause a variety of problems.

Most clients probably don't want that many results. The may just want the first 100, or first 1,000.

Even if they did want that many results, they might not be able to process them all at once. They would take a long time to send, if the connection got interrupted 15 hours in and 95% of the way through you might decide to throw your keyboard out the window in a fit of ISP related anger.

Pagination helps with these issues. We are basically creating pages of results in the same way that a book breaks ups the story in to pages of words. You have certainly seen pagination in action when you search for a term in Google and can move between pages of results.

## Implementation of Pagination
There are two main terms you will hear when talking about pagination. The **offset** and **limit**. The **limit** refers to how many things you can get in a request. So if I limit my results to 5, then even if there are 7 results, I will only get 5 of them. If there are 1,000 results, I will still only get 5.

**Offset** tells us how many results to skip first. So with an offset of 0, I will get results 1-5 (using the previous limit of 5 and assuming 1 indexing). With an offset of 3 I would get results 4-8. An offset of 5 would yield results 6-10.

From here the path to making pages of data should be pretty apparent. Page 1 should start with no offset. Page 2 should have an offset of `1*limit`, page 3 should have an offset of `2*limit`. So with page numbers starting at 1, the offset starting at 0 we get `offset=(page-1)*limit`.

## Database Limitations and Practical Problems
A lot of how you implement pagination will come down to the constraints of your database backend. For example, with MySQL we can simply use `LIMIT x,y` where `x` is the offset and `y` is the limit. So `LIMIT 5,10` will return rows 6-15. This is often handled in URLs as part of the query string. So we might see a URL like `/guests?limit=10&offset=5`, then when that is parsed, the limit and offset supplied by the client will be passed off to the query.

One needs to be carful because you might not want you server to return one hundred million results to a client. So it is reasonable to restrict the maximum limit to some value that makes sense for your application.

### Problems you say?
So what of these problems? Well, consider that it might take a client some time to get a very large result set. And results are typically ordered from newest to oldest, with not many people caring about the oldest results. (This isn't always the case, but generally its the way things are)

So suppose I am downloading page after page of results when someone inserts 50 new records. What happens to my pagination?

Everything is going to get shifted by 50 records. Assuming I had a limit of 10, I am going to end up with 5 duplicate pages. That's not super awesome. Especially if I am doing some sort of analysis on data where duplicate records might throw things off.

*Ahh, I can solve this, just start from the oldest records and work forwards!* Hold on there, that will certainly save us from the insert problem we just described, but what about deletions? If someone deletes 50 records I have already added to the collection that is going to shift the remaining results down by 50. So what was previously the 100th result is now the 50th result. That means that in my pages of data there are going to be 5 pages of data that gets skipped because a different 5 pages of information was deleted.

### Result Sets as Resources
Remember how I mentioned that crazy idea of searches being their own resource? Some database engines let us do the same thing with queries. For example, in Google Datastore you can get a [cursor](https://cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets) as a separate thing from an offset or limit. It will allow you to traverse in one direction through a list of results and not be impacted by changes made to the list that has already been traversed. So instead of remembering a numerical location, it essentially remembers what thing it last returned and what the next thing is to grab, so it is unaffected by inserts or deletes of things it already retrieved.

The tradeoff is that it only works in one direction. You can't go backwards to results you have already seen with a cursor.

If we wanted to implement such a feature, one way to do it would be to have the cursor itself be a resource which could be saved and returned to in subsequent calls.

## Links
While it is possible to have searches be their own resource, we usually don't need to have that advanced of a pagination and result system. Usually clients want a list broken into bits, they want to get all of those pieces one after another till they have the list they were looking for then they call it a day and go home.

An easy way to facilitate this is with links within a result set. We hinted at it when we were talking about links in APIs before but with every collection it is a good idea to return the `offset`, `limit`, `count` and links to the `next` and `prev` pages of results. Those links should have the same limit as the current request did. So if I requested offset 10, and limit 5, I should have a link to `prev` with `offest` 5 and limit 5 and `next` with `offset` 15 and limit 5. In addition a `count` of the total number of results in the set is helpful to know if they client wants to abort getting pages because the result set would be larger than it could handle.

The way to set this up would genenrally be with query parameters named `limit` and `offset`. So `/guests?limit=5&offset=15` might represent the path of the `next` and `/guests?limit=5&offset=5` might represent the path of the `prev` page of results if we are currently on `/guests?limit=5&offset=10`

{{< kaltura 0_6i6a6mrb >}}

## Review
This should give you an idea of how pagination is supposed to function within a REST API. It might not always be so obvious how to implement it, but at least the desired client functionality is pretty clear. A lot of the implementation details are going to depend on which database backend you opt to use.