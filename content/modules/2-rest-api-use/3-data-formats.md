---
title: "Common Data Formats"
description: "This looks at the common data types you are likely to encounter when working with REST APIs."
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
When working with APIs you might encounter several formats of data. Most commonly you will see JSON, XML and potentially some sort of format made for humans, like HTML or plain text. In this class the only data format you will need to work with is JSON so this will primarily serve as a quick refresher on JSON format. may

## JavaScript Object Notation
This notation is more or less the same notation used to describe JavaScript Objects but it somewhat more strict. At the highest level there are two sorts of things that can be the root of a piece of JSON data. It can be an `object` or an `array`.

### JSON Objects
JSON objects are the most common format you will see when it comes to the data returned from an API (though you will see lots of arrays within these objects). Objects are of the format:

```json
{
    string1 : value1,
    string2 : value2,
    ...
    stringN : valueN
}
```
Strings are always enclosed in `"`. Some languages or JSON libraries will allow you to have object keys which are not strings. So if things are not working properly, make sure you are putting quotes around your strings. And if you are returning JSON objects to clients make sure you are returning them with the `"`s included.

The values in an object can be any JSON value, including another object or array. So you can nest JSON several layers deep.

### JSON Arrays
Arrays in JSON are pretty straight forward. They do not need to contain all of the same type of item. In practice however it would be very difficult to practically use an array if it did not contain a collection of like types. The format is like you have seen elsewhere

```json
[value1, value2, ... valueN]
```

### Further Reference
For further reference I suggest you look at [JSON.org](https://json.org/) it has a list of all the possible data types and some neat flow diagrams that show valid combinations of characters.

## XML
XML is the other major data format you are likely to encounter. While JSON can be summed up in a single page with some flow charts, XML requires a multi-part [tutorial](http://www.xmlmaster.org/en/article/d01/) to learn.

Often times you will encounter a couple pieces to an XML document. A schema which defines how the data can appear and what the various data types are within an XML document along with the data itself that contains instances of the data types specified in the schema.

XML data can be significantly more complex and in some circumstances (eg. when created instances of complex classes) it can be useful to have that level of specificity and complexity available.

However, in this class, we will be sticking with the simpler to use and understand JSON. If you were to want to use or experiment with an API that uses XML make sure to find a good library for XML tree navigation and parsing.

## HTML
Finally, you may on occasion see an API that provides HTML or some other human readable format. Imagine a weather API that returned JSON formatted weather data that any program could use to display weather. But it might also be nice to simply embed todays weather in a website directly. That is the sort of use you might have for returning HTML data.

Typically you will simply be viewing the data in this form and not interacting with it, though more complex options could be imagined, we won't get into them in this class.

## Review
At this point you should be fairly confident in your ability to both write and reason JSON objects. If this is something you were struggling with in prior classes, make sure to brush up on it now because we will be working with them extensively (almost exclusively) in the rest of this class.