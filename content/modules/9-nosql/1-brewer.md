---
title: "Brewer's CAP Theorem"
description: "This goes over the limitations of database engines at a fairly high level. There is a lot more nuance these days with database engines, but these tradeoffs still exist."
categories: ["Exploration"]
weight: 5
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
This entire section can broadly be broken down into the following sentence: consistency, availability and partition fault tolerance, pick two. Eric Brewer proposed the theorem around 2000 and it is still very relevant. Historically relational databases tended to sacrifice availability to ensure data stayed strongly consistent. But many modern database systems to a different approach and that is what we are going to be looking at in this exploration.

{{< kaltura 0_9tyzeaer >}}

## Database Properties
Consider a 2 node example for this section with nodes A and B. These two nodes are where data for a database is stored and they are connected. However the time to communicated between them is non-zero. We will talk about the three properties of the CAP theorem and how they apply to this system.

### Consistency
The first property we will discuss is consistency. This means that if user Alice writes to the database, Bob, if reading from the database after Alice wrote to it, should only see the current state of the data that includes Alice's write.

In principle this seems reasonable, but remember that there are two nodes that can be accessed. And for the sake of argument assume they use some incredibly slow means of communication so that the delay between them is 1 second. If Alice writes data to node A and Bob reads from node B 0.5 seconds after Alice wrote to node A, node B will not have had time to be updated. So, to remain consistent Bob's request needs to be delayed or rejected until the server state can be synced.

Again, for a database to have the property of being consistent a user must <em>never</em> get data that is out of data. So whatever data was most recently submitted to any node must be the data that is returned.

### Availability
Availability is the property that every request must be fulfilled. In our two node example if node A gets some data and moments after someone requests data from node B, node B needs to fulfill that request when it is received. It cannot respond saying that it is waiting for an update from node A.

It should be apparent how this can be problematic for a partitioned system. If we have different nodes that need to communicate, and we want them to always be available we need to accept that sometimes we will get data that is not current.

### Partition Tolerance
Partition tolerance is the property that a system will continue to work even if messages between nodes are lost or delayed. If, when a node in a server becomes slow or off-line we simply shut down the entire service until it is fixed we can have availability and consistency as long as the server is on-line.

In our example, if there is a delay between A and B we simply shut down the whole application until the delay is fixed. If it was unfixable, we would need to simply operate as a one node system. We would have to get rid of the partition.

On the other hand we could accept that there will be a delay and instead sacrifice either availability or consistency.

## MySQL Databases
Previously you may have only worked with databases that did not have partition tolerance. The ONID database database had a single point of access with no redundant data. They make backups, but they are not live. If the server goes down or data is lost, the server cannot be accessed until it is fixed.

This means that you were dealing with data that was both consistent and available.

In general if MySQL databases are scaled to multiple nodes, they lose availability. There are limits imposed on the number of operations per unit of time or some requests are delayed until the database finished processing current requests.

## Review
This should give you at least a toolbox with which to understand the limitations of databases that might exist and to better interpret what you see when reading the specifications and documentation of databases. You should also be able to figure out when this information is omitted and realize that you need to search it out as the behaviors can vary pretty significantly.