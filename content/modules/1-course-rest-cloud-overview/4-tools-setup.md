---
title: "Tools and Software Setup"
description: "This will help you get oriented with the tools that we will be using throughout the class. It is important to get these set up early and see if there are any roadblocks that might keep you from being successful in the future portions of this class."
categories: ["Exploration"]
weight: 15
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
There are a few tools and providers we will need to work with throughout this class. In this section we are going to get them set up and working so we know, down the road, that we don't need to worry about getting any of this configured and we can focus on the topics at hand.

## Postman
Setting this one up is pretty straight forward. Go to [https://www.getpostman.com/](https://www.getpostman.com/), download Postman for your OS and you are good to go. Strictly speaking you don't *need* it for this class, however it will make it a lot easier to work with APIs which lack a UI (which are most of the ones we are dealing with in this class). As an alternative you could use something like cURL or Python to make calls, but it will take some more time to learn than Postman will.

## Google App Engine
This course will use Google App Engine as a cloud provider on which to run your servers code. You should go through a quick start tutorial which should be linked in this weeks assignment in order to get started.

### The Local Environment vs The Cloud Shell
You will see some references to setting up your local environment or setting up using the cloud shell. You need to make a bit of a choice here. Everything generally should be available on the cloud shell. The downside to using the cloud shell is that it will be a little bit more difficult to edit files.

### The Local Environment
This means that you do all your development on your local computer and that all the tools you need to develop and test are installed on your computer. The upside is that you can use whatever editor you want with ease and that connecting to your local webserver will always be fast and easy. The drawback is that some of these tools can be a little tricky to install and configure with the most complexity arising when trying to install them on Windows.

I have done development like this so it is certainly doable, and once everything is installed and configured to your liking it is quite nice. However, there were some challenges with getting the correct PATH variable set up and with getting the right versions of tools to be found.

### The Cloud Shell
On the opposite end is doing development primarily on the cloud shell. You will mostly be using a text editor like Vi or Emacs. This can be difficult to use if you are not used to it and might slow down testing but is significantly easier to configure because it is more or less all installed and configured for you in advance.

### A Middle Ground
No matter what you will be using the `gcloud` tools. These are a suite of tools installed locally and accessed via the command line. You can use them to transfer files from your local computer to the cloud computer. If you wanted you could use `gcloud` to edit source files locally, transfer them to the cloud and test them there. The benefit is that you can use your editor of choice without needing to install much locally. The drawback is that it adds time for every change you make because you need to add a step to upload it to the server then head over to the cloud shell to run it.

In the end they all should work and it is a matter of personal preference as to which option best suits you.

### Testing vs Deployment
The Google App Engine tutorial will walk you through getting a Hello World website set up. It is important to note there are **two** stages to this. The first is getting it set up on the testing server. This will be a server that is accessed via an address that has a port number in it. Something like `:8080`. This is the testing server.

There is another step to deploy it so that others may access it. To do that you need to run a deploy command and it will be accessed at a URL that looks like `your-project-name.appspot.com`. You need to get to this step to show that you have gotten all the way through the process and that your selection of options is able to produce a fully deployed website.

### Don't Short Change Yourself
Be aware, there are some really clear tutorials on Googles site that will, with the click of a few buttons and copying some code, get this site up and running. If you follow only those directions and never try to expand on them and figure out how to run it on your desired setup (eg. on your local machine) you may find that you run into some problems later.

Now is the time to get everything set up the way *you* want it set up. That is the purpose of this week so make sure to that you like and understand the method of creating code and deployment that you use.
