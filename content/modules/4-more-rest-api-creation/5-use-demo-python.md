---
title: "Demo of Intermediate REST API Features in Python"
description: "This gives an overview of intermediate REST features implemented in Google App Engine using Python"
categories: ["Exploration"]
weight: 25
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
This exploration looks at the lodging application as it is being updated to include more intermediate features. The Gist with the code sample can be found [here](https://gist.github.com/wolfordj/b72a813f0d809a7d7f849a9689a18f5f). This isn't a complete and functioning API, it is only built to showcase some important features and show how to do some specific tasks using Python and Google App Engine.

## Points of Interest

### Use of Blueprints

```python
...
import lodging
import guest

app = Flask(__name__)
app.register_blueprint(lodging.bp)
app.register_blueprint(guest.bp)
```

The app has been broken up into modules that separate out the guest and lodging functionality. This is an optional step, but is good practice for application design to help separate concerns into different files. Generally the blueprint functions the same as an app.


```python
from flask import Blueprint, request

...

bp = Blueprint('lodging', __name__, url_prefix='/lodgings')

....

@bp.route('/', methods=['POST','GET'])
def lodgings_get_post():
    if request.method == 'POST':
        content = request.get_json()
```

Before where we might use `app.route` to define a route we now use `bp.route` We also specify the `url_prefix` of the blueprint, and that is essentially the point where the URLs are all relative to. So the above blueprint is mounted at `/lodgings` so the route of `/` actually points to `/lodgings` in this blueprint. And later you see a route of `/<id>` which maps to `/lodgings/<id>`. Again, these are optional if you decide that you don't want to have to deal with the added feature, but it will make your project better organized.

### Handling Relationships

#### Adding Guests
We now have routes like

```python
@bp.route('/<lid>/guests/<gid>', methods=['PUT','DELETE'])
def add_delete_reservation(lid,gid):
```

This lets us associate a guest with a lodge. The code for that operation is as follows:

```python
    if request.method == 'PUT':
        lodging_key = client.key(constants.lodgings, int(lid))
        lodging = client.get(key=lodging_key)
        guest_key = client.key(constants.guests, int(gid))
        guest = client.get(key=guest_key)
        if 'guests' in lodging.keys():
            lodging['guests'].append(guest.id)
        else:
            lodging['guests'] = [guest.id]
        client.put(lodging)
        return('',200)
```

In this case we are getting the lodging key and loading the lodging, then we are also getting the guest key and loading the guest. If a guest list doesn't exist already, we make one, then we add the guest. You might wonder why we even bother loading the guest, as we are just saving the `id` that was passed into the URL. The reason I am doing that in this case is basic error checking. If the user passes in a URL that has an invalid id, then at least the program will error when it tries to load the guest. Without this step it would be possible to associate guest ids to lodgings where the guest id didn't exist. That would cause some major problems when we try to load the guest.

#### Viewing Reservations

The other piece of the puzzle is viewing guests. That function is below:

```python
@bp.route('/<id>/guests', methods=['GET'])
def get_reservations(id):
    lodging_key = client.key(constants.lodgings, int(id))
    lodging = client.get(key=lodging_key)
    guest_list  = []
    if 'guests' in lodging.keys():
        for gid in lodging['guests']:
            guest_key = client.key(constants.guests, int(gid))
            guest_list.append(guest_key)
        return json.dumps(client.get_multi(guest_list))
    else:
        return json.dumps([])
```

This is again part of the lodging blueprint, so the URL to access this will end with `/lodging/<id>/guests`. We look up the lodging like usual, then we loop through the ids of the guests in the `for in` loop making keys for each one and appending them to the list of keys. Then we use a function called `get_multi` to load all of the guests at once from the list of keys. Then we just dump the list of guests as JSON. Depending on your desired functionality, you may want to append guest ids to the guests in this list before dumping them via JSON. You would do that in the same way that the `GET` function for lodgings did by appending the `key.id` as the `id` property of each element in the list.


#### Deleting Guests

The code for deleting reservations is fairly straight forward.

```python
if request.method == 'DELETE':
        lodging_key = client.key(constants.lodgings, int(lid))
        lodging = client.get(key=lodging_key)
        if 'guests' in lodging.keys():
            lodging['guests'].remove(int(gid))
            client.put(lodging)
        return('',200)
```

We don't actually delete the guest in this case, they might have other reservations! Instead what we do is we load the lodging and remove the id from the list of guests associated to that lodging. Then we need to remember to save the lodging again. It is very similar to when we `PUT` to `/lodgings` except that instead of being able to edit the whole thing, we are only editing the guest list of the lodging.

## Review
<!--- Encourage students to reflect on what they should have learned from this exploration. -->
This should hopefully give you some insight into the changes we made to add this relationship management between these two entities. The main thing we had to do was figure out a way to keep track of the relationship in the datastore. The option we took is similar to a relational database where one entity keeps a foreign key reference to another and loads that other entity when needed.

Now where might we go from here? We will have some problems right now if a current guest who has a reservation is deleted. Our datastore doesn't do anything to 'clean up' after a deletion. So we might want to add additional logic that will, when a guest is deleted, look through all the lodgings and delete all references to that guest.