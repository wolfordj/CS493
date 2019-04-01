---
title: "Docker Overview"
description: "This exploration will give you a general overview of how Docker works and what it does."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
Docker is an open-source container platform.  It is probably today’s most popular way to containerize software. There are several tools that are part of the Docker platform, but the most essential one is a tool for simply creating and running containers. 

## Files, Images and Containers
As we talk about Docker we are frequently going to be referencing Docker files, images and containers.

Docker Files
: These are written specifications of a Docker image. It is basically a set of instructions of what image to start with and what commands to run on that image. This might download particular versions of software to package into the image and might set up directory structures within the image. In the end it is a very small file that is a list of instructions.

Image
: This contains everything needed to make copies of a particular environment. It is someone analogous to a Class definition in OO programming where it is the thing from which instances (containers) are made. So you can't actually use an image for doing any work, but you can make any number of containers directly using an image. These are significantly larger than Docker files because it actually includes all the data with which to make containers, rather than a description of where to find that data.

Container
: A container is created from an image. It can be in state like running or stopped because it represents an actual environment in which computation can happen. So state can be saved and software can be executed within the container. These are bigger than images because they also include the state of the container.

## So Whats All the Fuss About?
Why is it we care so much about this idea of containers? Think about the work you have been doing on Googles platform. You have probably been working on their PaaS offering. So you had to use their version of software on their choice of operating system.

For simple tasks that might be just fine and keep the cost of development and operations down. But if you need to do more complex operations that a specific operating system would better support and maybe you need to use a specific version of Python or Node.js for performance reasons, then you might want to customize things further.

This is where containers come in. Instead of manually installing your OS and software for every instance you create in the cloud, you can simply provide a Docker File or maybe an image to the cloud provider, they can use that to the create instances of environments that are set up exactly how you want them to be set up with no variation. Every one is set up exactly the same.

This becomes even more important when you have very scalable applications which might scale in size as more people use them. During peak time big services like Netflix or Amazon might have many thousands of servers running, but when the peak passes and people go to bed they release those servers to do other work. The ability do define and load images makes it easy to quickly bring up new servers or change their configuration to do different kinds of work.

{{< kaltura 0_5zargnsk >}}


## Review
This should give you an idea of what the major Docker components are, files, images and containers. In addition you should have an idea of how Docker might be useful and if we were developing projects on a bigger scale, how it might be useful to help deploy them.