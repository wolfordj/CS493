---
title: "Basic Docker Use"
description: "This exploration will look at running a Docker container locally to get an idea of how it should behave."
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
In this exploration we will go through the steps of running a docker container locally. This is a bit easier to work with because if anything goes wrong you will get the error messages on your local machine. If you are trying to directly deploy an image or Docker file to a cloud provider then you very likely will need to rely on things like error logs to debug which can be more time consuming. 

The first think you will want to do is to go pick up the free [Docker Community Edition](https://store.docker.com/search?offering=community&type=edition) for your platform and get that installed.

## Images
Once you get it installed and running you should be able to type `docker images ls` and you should see something like

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

You probably won't see any images listed yet unless you have used Docker in the past. But you should at least see something like this. If not then something has gone wrong installing Docker.

Next lets run `docker run hello-world`. This will look for the `hello-world` image locally and if it can't find it it will pull it from a repository. If all went well you should see some output which includes the following:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

And lets go yet one step further.

```bash
docker run -it ubuntu bash
```

This will run the Ubuntu Docker image and attach it to a terminal (the `i` and `t` flags do this via `-i -t` which can be written as `-it`). If we do that we get dumped into an Ubuntu terminal running bash. Note that this may not work from all command prompts. But it should work from the default Windows command prompt.

We can do things like `echo "hello world" > hello.txt` and create files. But it turns out if we exit the container then all of that gets lost. It isn't stored anywhere.

Lets see if we can fix that

```bash
docker run -it -v D:\tmp\docker:/home/test ubuntu bash
```

This takes the directory on my computer `D:\tmp\docker` and mounts it at the location `/home/test` on the container. Now any files I make in `/home/test` will persist on my computer at `D:\tmp\docker`. Any files I have in `D:\tmp\docker` are visible and editable from `/home/test` in the container.

Be careful doing this. You are giving the container access to the directory. It would be a very bad idea to mount something like `C:\` on  Windows or `/` on Linux because that would give the container access to your main file system. If you instead use an empty directory things are better contained.

### Volumes

Lets talk about the best way to handle persistance, Docker volumes. These are storage spaces managed and persisted by Docker. We can make one like this

```bash
docker volume create hello-volume
```

And we can view them with

```bash
docker volume ls
```

Then we can mount it with

```bash
docker run -it -v hello-volume:/home/test ubuntu bash
```

We replaced the local directory on our machine with the Docker volume. This better compartmentalizes the  data and doesn't give the container access to any of our computers file structure.

We can then delete the volume if we have no further use for it by running

```bash
docker volume rm hello-volume
```

But we need to remove all the containers it is attached to first. We can list all of our containers with

```bash
docker container ls -a
```

And then

```bash
docker container rm [container id or container name]
```

And that should clean everything up.

## Ports

The last thing to talk about are ports. You will probably want to do a lot of work with networking and Docker containers. So it is important that we know how to get access to the network via our Docker container. We can use the `-p host-port:docker-port` flag. So `-p 23456:8080` would mean that connecting to port `23456` on your computer would connect to port `8080` on the Docker container.

```bash
docker run -it -p 23456:8080 node bash
```

This will download and start a container that is configured with Node.js.

If we then run

```bash
apt-get update
apt-get install vim
```

we can use vim to write a simple hello world program in node like

```js
var http = require('http');

var server = http.createServer(function (request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello World\n");
});

server.listen(8080);

console.log("Server running at http://127.0.0.1:8080/");
```

If we run that simple server and then visit `http://localhost:23456` on our machine we will see `Hello World` in the browser and it will be sent from the Docker container. Cool stuff right?

{{< kaltura 0_agpsbsb8 >}}

## Review
Ok, so that is pretty much the extent of what we will look at when it comes to running Docker locally. We have shared filed between a container and our computer, we have accessed it via ports shared to the host computer, we have run different images and installed applications on them. That takes care of all the basic functionality you will probably need at first. The next thing is to figure out how we can get these things working on the cloud!