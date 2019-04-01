---
title: "CAP Examples"
description: "This exploration looks at a few different database systems in terms of the CAP theorem."
categories: ["Exploration"]
weight: 10
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
In this exploration we are going to look at a couple real world examples of databases and discuss how they handle the constraints put forward in the CAP theorem. It would be a fair amount of work to configure these things to simply see them not work or to get the inconsistent results yourself, but you are welcome to give them a shot!

{{< kaltura 0_eok0noa8 >}}

## MySQL
We are going to talk about two different MySQL configurations. A single node server and a multi-node server.

### Single Node
The single node MySQL server is the classic CA situation. The server is consistent and available, but cannot be partitioned. One could argue the CAP theorem does not even apply to it because it isn't multi-node, but that is a technicality we don't really care about.

So what happens when Alice writes to the database and Bob reads from it?

It is a little complicated if you are doing anything other than single writes and reads and can depend on the database setup. If Alice is doing a single write and Bob is doing a single read it is pretty straight forward. Once the write is committed to the database, Bob will see that result if his read started after the commit. Otherwise he will see the previous result.

There is also the concept of transactions, where you might run several operations in a sequence and they all *must* operate on the same set of unchanged data. This gets a little tricky and is beyond the scope of CAP. CAP only applies to single reads and writes.

### Multi-node
A multinode MySQL setup gives up consistency in the sense of Brewer's theorem. Two requests sent at the same time to different nodes might see a different state of data. Managing consistency can become quite tricky depending on the type of errors that you are willing to accept and if you can keep related tables together on single nodes.

It would best be described as a AP model but it is a little fuzzy.

## PostgreSQL
Single node, it is basically the same as MySQL but when moved into a multi-node situation it has a controller that more carefully tracks the state of the database. It can guarantee consistency and is a good example of a database that is CP. It is probably the only example of such a database we will talk about.

{{< kaltura 0_02dt7th0 >}}

### BigTable
Google's [BigTable](https://cloud.google.com/bigtable/) is their very scalable, fast access data offering. It can scale up to many nodes, but at a rather steep cost of around $0.60/hr/node. It advertises itself as a NoSQL database that can be used to operate on very large datasets.

While writes are very fast, this is again designed for larger transactions but it makes no claims of being consistent. Writes are fast but it is designed for jobs that take minutes, so dealing with data that changes over the course of a job is simply expected.

It is a good example of a database where relationships are completely forgone in the pursuit of being able to rapidly access and store massive amounts of data.

### Cloud Datastore
This is an interesting beast. It is a blend and shows why CAP is really not enough to capture the complexity of modern data storage options. It stores objects. Those objects are grouped into entity groups. Transactions that span only one entity group are strongly consistent, that is they are generally CP. However, transactions across groups are AP, you might get some data that hasn't synced yet. So you can structure portions of data to be consistent. For example a user might be the top of an entity group and all that users content is within the group. So any queries involving a single user and their content are CP. But if were to query across multiple users it would be AP.

It uses a concept called eventual consistency. This is actually a little tricker than simply looking at an old version of the database like you might see with MySQL. With eventually consistent data you might end up in states where one entity is committed to the database and the thing it references isn't. This sort of this does not happen with many things that still are available and partition tolerant. Those tools will still show data that is valid in that references all exist, but it might be outdated.

Eventual consistency is a step down from that, it does not even guarantee that the current snapshot will be valid.

{{< kaltura 0_ztrfe5f1 >}}

## Review
These are just a few examples of the sorts of compromises that current products make when it come to CAP. You probably have some experience working in MySQL and have been working with the Datastore, but in all likelihood you have not developed applications or tested them in such a way to actually the the consequences of these factors. One needs to fairly carefully and intentionally design tests that exploit the specific limitations of these databases to see the results, but when you run into a bug that affects 0.1% of transactions and you have hundreds of thousands of transactions a day, that can be a problem.