---
title: "Docker Files"
description: "This exploration will look at how we can make custom images using Docker files."
categories: ["Exploration"]
weight: 15
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
We have so far taken a good look at how to get images and how to make containers from them. What we haven't really looked at is how we can make our own images. To do that we need to use Docker files. These files specify the steps required to create an image. It will include things like picking a base image, copying files into the image and running commands within the image. We will make a simple image that will start a web server and display a custom message.

## Docker Files
We are going to go through this step by step.

First we make a new directory that we will work from. We will call it `/mydocker`.

In that directory I make a simple node server like so named `index.js`

```js
var express = require('express');
var app = express();
const port = process.env.PORT || 8000;

app.get('/', function(req, res){
  res.send('hello world');
});

app.listen(port);
```

I want to use express it it so I need to install it via `npm install express` and I add a start script to the package.json file:

```js
  "scripts": {
    "start": "node index.js",
    ...
```

At this point if I run `npm start` in this directory it should start a node server and everything is dandy. Nothing so far should be new or exciting.

But, we want to do this with Docker. So we are going to make a file called `Dockerfile` in this directory and we put the following content into it line by line:

```bash
FROM node:8
```

This starts us from the Node Docker image running version 8 of node. So it will begin with this image.

```bash
WORKDIR /usr/src/app
```

This will set the Docker image to use `/usr/src/app` as the working directory. All the commands we run from here on out will use this directory if they need a directory.

```bash
COPY package*.json ./
```

This copies the package files into the image's working directory. So we will have the `package.json` and `package-lock.json` files copied in. That will allow us to have the next command get all the modules we need

```bash
RUN npm install
```

Because we got the package files in place this will install all the node packages we need, just Express.js in this case.

```bash
COPY . .
```

Now we copy in the server code. This would actually copy in a bunch of other stuff but we will stop that with a `.dockerignore` file that we will look at in a moment.

```bash
ENV PORT=8000
```

This sets an environmental variable, we will use it in the next command and the Node.js server will use it as well.

```bash
EXPOSE ${PORT}
```

This will let people know that port 8000 is the one to use and it will expose it from our image.

```bash
CMD [ "npm", "start" ]
```

Finally we list the command we want to run by default, in this case it is `npm start`. Note that the command is split up with each token being a string in an array. Keep in mind this will be executed from within the working directory we created earlier.

Finally lets look at that `.dockerignore` file. We make it in our current directory and we will add to it just one line `node_modules`.

This will stop the image from copying in all the stuff in `node_modules` instead this will be pulled in via the `npm install` command we ran as part of the Dockerfile.

## Creating the Image

Now we run the following command in the directory

```bash
docker build -t hello-dockerfile .
```

This will build a new image tagged `hello-dockerfile`. You will see it if you run `docker image ls`. You can make a container with it using 

```bash
docker run -d --name df -P hello-dockerfile
```

This will run a detached container (due to the `-d` flag). `-P` will bind all exposed ports. If we run `docker container ls` we should see this container running along with a listing of which port it bound to our exposed port. We can see what it looks like on my machine here

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
2234e3031371        hello-dockerfile    "npm start"         5 seconds ago       Up 3 seconds        0.0.0.0:32776->8000/tcp   df
```

So in my case it bound 32776 to 8000. So I can see the output if I visit `localhost:32776`.

If you need to remove a image to rebuild it you can use `docker image rm [imagename]`. You need to remove any containers made with it first and you can see all the containers you made with `docker container ls -a`. You can also use `docker system prune` to get rid of all unused images and containers.

{{< kaltura 0_liosfv6u >}}

## Review
So there you have it, you have a Docker file created that will run your server whenever you start it. Next we will look at getting this running on the cloud!