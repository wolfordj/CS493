---
title: "Docker on the Cloud"
description: "This will look at deploying Docker images on the cloud."
categories: ["Exploration"]
weight: 20
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
So now we have worked with some Docker containers locally and have made some docker images ourselves. Now we need to look at how we can go beyond using these things locally on our computer and instead figure out how to deploy them onto some variety of cloud service.

## Google Container Registry
Many cloud providers provide a place to store containers, images or Dockerfiles. Getting the file to the Google Container Store should be pretty easy. In the location where you Dockerfile is you run:

```bash
gcloud builds submit --tag gcr.io/[your-project]/[image-tag-name] .
```
You need to specify your project and also give the container a name.

Once that runs successfully we have gotten our container uploaded to the Google Container Registry. At this point we can access it via Compute Engine to deploy it on individual VMs or we can use something like Kubernetes to deploy it to a cluster of VMs. We will look at the former as it is easier to wrap you head around.

## Google Compute Engine
Google Compute Engine is a tool for running virtual machines in the cloud. While Google App Engine was PaaS, Google Compute Engine is IaaS. You can specify pretty much everything about your virtual machine.

In addition there is a very convenient field you can use when making a VM that will let you choose a container. If you fill that out with a path to a container in the GCR then it will by default pick a VM that is optimized to run containers and it will download and launch the container you specify when you start the VM.'

## Networking
It is almost that simple. But nothing is every actually that simple. Remember when we made a container we exposed ports? Well, they are mapped directly to the host VMs ports. So if we `EXPOSE 8000` then we access that port via port 8000 on the host. That seems simple enough. But by default the VMs are pretty locked down in terms of the firewall. So we need to go to the VPC network configuration and add an exception for whatever ports we need. In this case I want to add a rule that allows connections from all other IP address to port 8000. So I allow TCP on 8000 and have it apply to connections from `0.0.0.0/0`. Once I add that rule then I can connect to the public IP of my VM and see my hello world message being sent by my Node container.

{{< kaltura 0_t5l20vn9 >}}

## Review
So we have done everything from running Docker containers locally, all the way up through making our own custom docker container and deploying it to a live cloud server. This is something, if you go work in this field, you will be doing quite a bit of. You may be managing just a few VMs in the cloud or you might end up managing clusters of 100s of VMs all running containers that are part of a larger application.