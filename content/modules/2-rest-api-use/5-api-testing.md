---
title: "API Testing"
description: "The goal of this module is to demystify the process of using Postman. This should allow you to use more of your time focusing on the assignments and not struggling with your tools."
categories: ["Exploration"]
weight: 20
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
This module will look at the more practical aspects of writing API tests with the Postman testing too.

### Good Practices
When creating a testing suite there are some things to consider to make your work more streamlined and thorough.

#### Assume nothing

When testing an API it is best to approach developing a testing suite without any preconceived notions. This means a few things: 
  
* You cannot assume anything about the API works correctly so you must test even the most basic functionality
* Your testing suite should be data/state _agnostic_, meaning it runs no matter the current state of data on the server
   
#### Start small

As mentioned above, you must begin by testing the most basic functionalities of an API. This means having tests to verify simple GET and POST statements work before you move onto more complex API functionality.
   
#### Build off of proven test

Only once you have proven that the simple stuff works you can then "safely" use that same functionality in later tests. For example, after verifying that a GET request for a record works, you can then use that same GET request when testing to see if an UPDATE request was successful.
   
#### Status codes can lie

When testing an API you cannot simply rely on status codes. To do so would go against the _assume nothing_ mantra. While it may seem like extra work to test more than status codes it is important to remember the goal of this course. You will eventually be creating your own API with status code responses that you yourself write. The only way to verify you wrote the code correctly is to test it, so get in the habit now.
   
#### Check before and after

Just as it is not enough to test just the status codes, it is also not enough to simply test the response body. Everything could appear correct with the response, but in fact no changes have been made to the data. Therefore if you want to test to see if the number of records increases by 1 with each create request you will need to know the number of records **before** _and_ **after**.
   
#### Clean up after yourself

It is a good idea to undo any changes your testing suite has made to the server data. This will help prevent your tests from making any assumptions about the current state of the data. With this in mind, it wouldn't be a bad idea to have a few requests in the testing suite to delete all the records it created.

## Anatomy of a Request

Once you have created a _collection_ in Postman you will need to start adding **requests**. Each request is made up of multiple parts.

#### Type

This is where you specifically the kind of request you will be sending. The most common types of requests are:

* **GET**
* **POST**
* **PUT**
* **PATCH**
* **DELETE**

#### URL

This is the _target_ of the request and will depend on thee desired functionality you are looking to examine.

#### Params

Here is where you can specify any particular parameters you wish to add to your request. This is most commonly done with GET requests. If you type parameters into Postman they will be added to the URL automatically.

![Postman Params Example](https://oregonstate.box.com/shared/static/xzq8v8b8gsap8hhuabovhl8q8eaibn8a)
   
#### Authorization

This is a very powerful tab. It allows you to easily handle multiple types of authorization protocols. You can specify a _Bearer Token_ or even allow for OAuth2.0 (covered in a later section). This is important as most public APIs require some sort of authentication to prevent spamming or abuse.

#### Headers

HTTP Requests can have any number of headers attached to them. These are things that can be read by the API to modify its behavior. Technically _authorization_ and the _body_ (described below) are parts of the header, but Postman separates them out. In this class you are going to use the header most often to request the type of response you want: HTML or JSON.

#### Body

This is where you will place the _payload_ for your POST requests. When interacting with RESTful APIs this will generally be in JSON format.

#### Pre-request Script

When crafting a testing suite with Postman pre-request scripts will allow you to set up any environmental variables that will be required for your tests. This can even include initiating separate requests before the main request. This is useful for determining the state of the data before the main request so you can compare it to the response. These scripts are implemented using vanilla JavaScript and the Postman framework.

#### Tests

This is the main focus of using Postman for this class: testing. This is where you will include the tests you wish to run on the given request. It is perfectly reasonable to have multiple tests per request. Just as with the pre-request scripts, the tests are written using JavaScript.

## Let's Make a Request

So you can practice making requests before jumping into actual testing, please follow the provide steps below. We will be using OpeanWeatherMap's API for this exercise.

1. Go to https://home.openweathermap.org/users/sign_up and sign up for a free account. You may already have an account if you did CS 290 recently
2. Once registered and logged in go to https://home.openweathermap.org/api_keys where you will see an API Key and copy it to your clipboard
3. Create a new collection in Postman and create a new request

   ![Create New Collection](https://oregonstate.box.com/shared/static/kch1rn9rg0gekiel5s6jnp47o6oixkos)
   
   ![New Request - Step 1](https://oregonstate.box.com/shared/static/hui6ex8vjhviicqhpnsu00kruhoqbvif)
   
   ![New Request - Step 2](https://oregonstate.box.com/shared/static/cezrdcjy599bc7vpe360c5dcnwsc8mfs)

4. When prompted, give the request a name: e.g. "Get My Weather"
5. Set a _target_ URL to `api.openweathermap.org/data/2.5/weather`
6. Under the _Params_ tab, create a new **key** called `zip` and give it a value of `<your_zipcode>,us`. For example, to get the weather for Corvallis, Oregon you would use `97330,us`. You should see the URL update as you enter these values
7. This API does not utilize _Bearer Tokens_ and instead uses an API Key in the header. Under the _Headers_ tab, create a new **key-value** pair using the copied API Key: `appidd:<your_key>`. Your Request should look similar to this:

   ![Complete Request](https://oregonstate.box.com/shared/static/9eugk08jn5gjifasrke5sdayr7bigd6f)
   
8. Since this request doesn't require any _Headers_ or _Body_ we can click **Send**
9. Your response should look similar to the following:
   ```json
   {
    "coord": {
        "lon": -123.26,
        "lat": 44.56
    },
    "weather": [
        {
            "id": 500,
 0           "main": "Rain",
            "description": "light rain",
            "icon": "10d"
        }
    ],
    "base": "stations",
    "main": {
        "temp": 279.2,
        "pressure": 1022,
        "humidity": 41,
        "temp_min": 277.04,
        "temp_max": 281.48
    },
    "visibility": 16093,
    "wind": {
        "speed": 5.1,
        "deg": 10
    },
    "rain": {
        "1h": 0.25
    },
    "clouds": {
        "all": 1
    },
    "dt": 1551646157,
    "sys": {
        "type": 1,
        "id": 3727,
        "message": 0.0089,
        "country": "US",
        "sunrise": 1551624338,
        "sunset": 1551665075
    },
    "id": 420029177,
    "name": "Salem",
    "cod": 200
   }
   ```
.10 Congratulations, you have made your first Postman request!

## Anatomy of a Test

As mentioned above the _Tests_ tab uses JavaScript and Postman's Framework. Everything discussed here can be used in the _Pre-request Script_ tab excluding actual tests.

#### Environmental Variables
Postman allows you to create **environmental variables** to store data between or during requests. It is important to use environmental variables and **not** global variables as this can lead to your test suite creating errors for others. 

The simplest way of creating and initializing an environmental variable is to use `pm.environment.set(<key>,<value>)`. This will create a new variable with the name `key` and set the value to `value`.

You can then access this variable using `pm.environment.get(<key>)`.

#### Sending Requests

Sometimes it will be necessary to send additional requests either in the _Pre-request Script_ or in _Tests_. This is accomplished using `pm.sendRequest()`. 

This function takes two arguments: the _target url_ and a function that handles the response from the request. Below is a _sendRequest_ that manually creates the previous call to the OpenWeatherMap API that logs the response to the console.

```javascript
var url = "api.openweathermap.org/data/2.5/weather";
var zip = "97330,us";
var appid = "43352e4c665493330fc986402cd71862";
pm.sendRequest(url + '?zip=' + zip + '&appid=' + appid, function(err, res) {
	if(err) {
		console.log(err);
	} else {
		console.log(res.json);
	}
});
```

You can decide how to use the response however you wish, including running tests. This is useful when verifying UPDATE requests as you send a _sendRequest_ to verify that the changes did in fact occur.

#### Initiating a Test

The simplest way of creating a test in Postman is to use `pm.test()`. This function takes two arguments: the test name and a function for how to run the test. Inside of this function you will often utilize `pm.expect()` to specify what you want to verify. In Postman, `pm.expect()` is very similar to an _assert_ and will evaluate to either true or false.

For the sake of example, suppose you wanted to verify the number of records increased by 1 after a create request. In your _pre-request script_ you may already have determined the current number of records with the following:

```javascript
pm.sendReqeust(target_url, function(err, res) {
	if (err) {
		console.log(err);
	} else {
		pm.environment.set("prevRecords", res.json().length);
	}
});
```

In the _Tests_ tab you would then create a test that checks the new number of records:

```javascript
pm.sendReqeust(target_url, function(err, res) {
	if (err) {
		console.log(err);
	} else {
		var newRecords = res.json().length;
		pm.test("Number of records increased by 1", function() {
			pm.expect(newRecords).to.equal(pm.environment.get("prevRecords") + 1);
		});
	}
});

```

Note how `expect` is followed by `.to.equal()`. This syntax is from the _Chai Assertion Library_ and allows for some very complex comparisons. Most of your tests will use `to.equal()` there are many other options (https://www.chaijs.com/api/bdd/). 

Another common thing you will be checking is _status codes_. You can check this using `pm.response.to.have.status(<status_number>)`. Please note that `pm.response` refers to the response to the Postman request, not any `sendRequest` you may have. 

For more examples about how to create Postman tests, please visit https://learning.getpostman.com/docs/postman/scripts/test_scripts/. 


## Let's Make a Test

To practice writing tests let's add one to the request you created above. Under the _Tests_ tab add code to test to see if the request returns a 200 Status Code.  This will require you to use `pm.expect()` and `pm.response` as well as the _Chai Assertion Library_ syntax. Please try your hand at creating the request before viewing the solution.

<details>
  <summary>Click for solution</summary>
  
  ```javascript
	pm.test("Status Code is 200", function() {
	  pm.expect(pm.response.to.have.status(200)) ;
	});
  ```
</details>