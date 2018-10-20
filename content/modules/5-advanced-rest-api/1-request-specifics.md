---
title: "This module will look at some more advanced features of requests that might be overlooked when looking at REST for the first time."
description: "1"
categories: ["Exploration"]
weight: 5
---

{{< title >}}
## Introduction
At the point we should have a pretty good idea of how to generate the bulk of a typical request that is well formatted. But a lot of APIs go beyond this in terms of what they implement. Any good REST API should use status codes to communicate what is going on. In addition we will start paying attention to the Accept header and returning different sorts of data.

This exploration will look at status codes and some of the request header and how we deal with them.

## Status Codes
<!--- Main topic headings are at ## -->
It is easy to get wrapped up in the body of the response. That is where all of the interesting stuff happens right? If we want to request a lodging, the lodging is represented in the body of after all. But that assumes all goes well and that there is actually a reason to send a body.

What do we do when we PUT a guest into a lodge? We don't really need to return anything. How do we notify the client that it worked (or didnt)? And how about when things go wrong? What do we do when the sever does everything right, but the client sends bad data? Or what if something goes wrong and we don't know why?

Stats codes help communicate all of these things. You may have a pretty good idea of how these work from prior classes but here we will look at them in the context of REST APIs.

### 2xx Awesome!
The status codes in the 200 range are the codes where everything worked well.

200 OK
: Everything worked and there is no better code to send. Generally you would use this when returning data from a `GET` request.

201 Created
: The server made something new. This is the code sent out *after* the server has successfully created a resource. This is typically going to come when you make a new resource with a `POST`. You could also see it when adding content via a `PUT`. You would not use it when simply updating content. When you create a new resource it is bet practice to include the URL to access that new resource in the response `Content-Location` header field so that a client knows where to find it.

202 Accepted
: We are not super like to use `202` in this class. It is used to signify that a proper request was received, but that the results are not ready yet. Imagine sending an update that affected a million records. It might take some time to process. This is a situation where the sever would return `202 Accepted` to indicate to the client the request was accepted, but it will take a bit for it to get done.

204 No Content
: This is the status code we will use for requests which merit a response but are quick to accomplish. For example, if we wanted to delete a resource we don't really have anything to send back to the client, but we want to let the client know it worked and that they should not expect content. That is what a `204 No Content` response is for. It should be used when a request is done, but there is nothing to send back.

### 3xx Don't Get Lost
The codes in the 300s are for things which might have moved and the client needs to look elsewhere for them.

301 Moved Permanently
: This is used when you redesign an API structure and what used to be found at location A is now found at location B. You should, in the response's `Location` header include the new URL. I have never needed to use this response code.

302 Found
: This is an old way to redirect a client from one resource to another. The industry didn't follow the spec with browsers to it is kind of a mess I would probably stay clear of this in favor of 303 and 307.

303 See Other
: This is a bit of an interesting one. It tells the client the request was handled and if you want to see the resource make a GET request to the location specified in the `Location` header of the response. You might use this if the client created a very large object or maybe uploaded a file. The server does not want to send back the result every time, but it wants to tell the client how to find it.

307 Temporary Redirect
: This tells the client that the resource is found at a different location and that it needs to repeat the same request at that location. So maybe you want to edit a guest via the URL `/loding/:lodgingid/guest/:guestid` with a `PUT`. Your server might use `307 Temporary Redirect` with `/guest/:guestid` to let the client know that is the URL to send the `PUT` to to update the guest. It is not too common to go to this much work and instead your API docs should probably just say to make the `PUT` to the guest root URL to begin with.

### 4xx Its the Clients Fault!
The 400s are used when there was an error with the request sent by the client and it is the clients responsibility to fix it.

400 Bad Request
: This is used when no better explanation of the issue can be figured out. For example, the request headers are not properly formatted so it can't even be parsed.

401 Unauthorized
: This is used when the client needs to provide credentials for authorization but failed to do so or provided bad credentials. So if you needed to include an OAuth token, but didn't, this would be the error to return. Likewise, if a username and password were provided but didn't actually correspond to any user, this would be the error to return.

403 Forbidden
: It can be a little tricky to understand the difference between 401 and 403 at first. A `403` status should be returned if the client provided good authentication info BUT that user does not have permission to access the resource. For example, if I successfully provided Mallory's credentials but tried to access Alice's email I should get a `403` because only Alice should be allowed to get her email.

404 Not Found
: This one is pretty easy. It should be returned when the client asks for a URL that does not exist. If they asked for `/airplanes` in our lodging app, they are not going to find it. Likewise if they ask for `lodgings/42` but no lodging with an ID of 42 exists they should get back the 404 response.

405 Method Not Allowed
: If a particular URL only lets the client `GET` or `PUT` but they try to `POST` then the server should return `405 Method Not Allowed` the response headers should include the `Allow` header with a list of allowed methods eg. `Allow: GET, PUT`.

406 Not Acceptable
: This should be returned if the client wants a media type the server can't offer. If you the client sends `Accept: application/xml` but the server can only return `text/json` then the server should return `406 Not Acceptable`.

415 Unsupported Media Type
: This is a lot like `406` but going the other way. If the **client** sends an unsupported media type to the server the server will respond with this to let the client know it is not acceptable. For example if you tried to `POST` a new lodging but provided YAML instead of JSON in the payload of the `POST`, but the server only accepts new data in JSON format, it would reply with `415 Unsupported Media Type`

### SUBTOPIC HERE!
<!--- Subtopic headings are at ### -->

<!--- Embed kaltura videos like this {{< kaltura video_identifier >}} where video_identifier is replaced with the id of the video found in the kaltura video URL -->

## Activity
<!--- Where possible include one or more activities for students to do to further cement their understanding of the topic. They will learn more from doing than reading -->

## Review
<!--- Encourage students to reflect on what they should have learned from this exploration. -->