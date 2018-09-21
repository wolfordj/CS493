---
title: "Cloud Computing Overview"
description: "This will give you an overview of what we mean when we talk about cloud computing in this course. It is a bit of a fuzzy definition, but we will do our best and then look at some more specific terms."
categories: ["Exploration"]
weight: 5
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
<!--- Introduce the content of this exploration -->
In my personal experience there are not a whole lot of people who like the term "The Cloud" in the programming world. It is a great marketing tool, but it is often found in sentences which are also home to "incubating disruptive synergies" or "impactful value-added transformational e-future proofing". It is fairly inspecific corporate jargon at this point. So lets clarify what thing(s) we might actually be talking about when we use the term "the cloud".

## Distributed Widgets and Gizmos
At the heart of all things "Cloud" is the idea that whatever it is will generally be distributed. This means that it won't live in only one place. When I upload something to a distributed data storage provider the expectation is that it will then be replicated to several different physical pieces of hardware in several different geographic locations.

In general this is a rather good thing. If I keep all my businesses files on a central server in my businesses headquarters and that building is lost in a fire or earthquake, so is all the data. Likewise if that server is compromised all the services hosted on it will be down till it is restored (assuming it even can be restored). In contrast, if a application or data is distributed to many data centers any one (or several) can go down and the service can continue to function and the data can continue to be accessed.

## Types of Cloud Offerings (?aaS)

### Software as a Service (SaaS)

This type of cloud offering is what you might buy as a company that does not specialize in software development or if you need a piece of software that is well outside your area of expertise. The idea is that you buy access to a software application that is run on a 3rd party companies servers and is maintained by that company. For example, OSU uses a number of Google SaaS products like Gmail. The email services are all handled by Google, the data is stored on Google's servers. But there are a bunch of contracts that specify what sort of uptime they guarantee, how they will maintain the data etc.

In general the client of a SaaS product does not have to do any software maintenance or upkeep, but the SaaS is usually relatively expensive and the client gets very little direct control over features.

### Platform as a Service (PaaS)

This is mainly what we will be using in this course. A cloud PaaS offering provides a suite of development tools and environments that allow programmers to write programs so long as they fall within certain constraints.

In our case we will use Google App Engine. This means there are a set of languages we are constrained to if we want to use the standard environment. There are a specific set of libraries that are included and supported. In general you are not going to get access to low level programming interfaces. So calls to the OS are going to be limited. You may not get access to the much of the hard drive that is hosting the machine. So there are a number of limitations, but there are a number of positives.

This is nice because you don't need to worry so much about things like keeping your hardware and operating system up to date in terms of things like security updates. The PaaS provider should handle things like this. Likewise they should handle a lot of the nitty gritty details of actually maintaining correctly configured server settings.

### Infrastructure as a Service (IaaS)

PaaS makes a bit more sense when discussed with the context of IaaS as well. In an IaaS environment you get a hard drive, some sort of network card and a CPU. The rest is up to you. Essentially you are renting hardware at the providers location and that is all they really guarantee. You will get that CPU, network connection and storage, if you muck it up from there that is your fault.

This means you can pick exactly what OS you want to run, you can generally have access to low level hardware, you can pick exactly what software packages are installed and how they are configured.

This also means you **have** to pick exactly what OS you want to run, you have to deal with low level hardware issues and are responsible for any problems that arise with the software you have installed.

{{< kaltura 0_b012ldgq >}}

## Review
This should give you an idea of the major classifications of cloud offerings out there. You probably have used quite a few SaaS offerings, maybe have used a PaaS or two, maybe not, and the same with IaaS. The difference between IaaS and PaaS being the extent to which you want to get involved with the OS and the hardware.

Going forward in this class, try to keep in mind how much is or isn't being done for you by the cloud provider when it comes to things like configuration or networking and think about what the advantages and drawbacks to that are.