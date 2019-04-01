---
title: "Google App Engine and Python"
description: "This will walk through the basics of setting up the framework for a Python Flask application on Google's App Engine framework."
categories: ["Exploration"]
weight: 20
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
Ther are a lot of similarities between the process for the Python application and the Node.js application.

Once you have the Google Cloud tools installed (which is the same process regardless of Node.js or Python) you might want to go through steps 1-4 of the Python [getting started](https://cloud.google.com/appengine/docs/standard/python3/building-app/) tutorial.

This [guide](https://googleapis.github.io/google-cloud-python/latest/datastore/index.html) will get you the very basics of the datastore set up and give you an API referece. This [site](https://cloud.google.com/datastore/docs/concepts/entities) has more detailed examples on working with the various aspects of the datastore. Just make sure you select the Python option in the code samples.

## Lodging App
This demo app is meant to be the *start* to the lodging/guest app. It will show you how to set up the routes for lodgings, but isn't going to show how to implement guests or how to implement adding guests to rooms.

While not entirely trivial to add those features, they are somewhat intuitive and once you see how CRUD operations work on one entity, it should be apparent how that would be generalized to other entities.

### The Code

[This Gist](https://gist.github.com/wolfordj/a8ea135d6fd012c5929679cf7ce930ad) houses the code required to get this started. `main.py` has the important code that demonstrates the principles. `requirements.txt` is so you can see which libraries were used, in particular note that the Google Cloud Datastore library was used along with Flask. Finally `app.yaml` is included to set up the routes.

### Highlights

#### Keys

Keys in this code come in two flavors, kind only `new_lodging = datastore.entity.Entity(key=client.key(constants.lodgings))` where the key's kind is specified but there is no ID. We do this when we are posting a new lodging and we want the datastore to make an ID for us. When it does, this keys `id` property will be updated to hold the new ID assigned by the datastore.

The other is a key had has an id. `lodging_key = client.key(constants.lodgings, int(id))` here we have a key, still of kind `lodgings` (`constants.lodgings` is defined to be the string `'Lodgings'`) but now it also has an `id` based on the value of the `id` variable passed into `int`. So this key points to a specific lodging and when we pass it to a function like `client.get` or `client.put` it will retrieve or save a specific lodging with the ID we provided.

#### Types
Make sure you keep track of your types. Things passed in as query string parameters will be strings. Things in a request body can be of various types.

## Next Additions
If you were to add guests to this, the main challenge will be to figure out how to keep track of which guests are assigned to which rooms. A good practice would be to keep a list of guest keys as a property of lodgings. Then you could request those keys when you want to list the guests.

A decision you need to make is if you want to store those keys as key objects and convert them to strings when a client requests them or if you want to store them as strings and convert them to keys when you need to use them with the Datastore. You can see that when we return results we have to manually add the `id` to the JSON representation via this code

```python
for e in results:
    e["id"] = e.key.id
```

Without this the id would not be part of the returned JSON.

## Review
This should give you a pretty solid platform with which to work. From here you can change the names or properties of entities. You could work on further abstraction or you could just use this as a basic idea and make your own implementation just borrowing some ideas from this one.