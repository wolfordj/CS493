---
title: "Security Overview"
description: "This looks at some higher level security topics that relate to cloud computing."
categories: ["Exploration"]
weight: 5
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
Security is a topic that is relevant to really all software, but I would argue it is exceptionally relevant to cloud software for a couple reasons. First is that often times other software providers will be using or relying on your software, so not only do you have to worry about your customers, but also the customers of other developers who might be using your software. The other aspect is that the whole point of the cloud is to have an application that is accessible from anywhere. That means malicious users from anywhere can try to do bad things to your software. With desktop applications the barrier to attempt to be malicious is set higher.

## The CIA's Definition
The CIA has defined a triad of security attributes that has become a popular standard by which to discuss security. It is certainly not the only definition but it is a clear, simple definition that we will use in this class and that covers the major aspects of security. The three parts of the triad are Confidentiality, Integrity and Availability

Confidentiality
: Keeping secret data secret. Only authorized users should be able to view this data. An example of a failure of security would be a hacker accessing credit card information from customers of a on-line store.
Integrity

: Changing data only when authorized to do so. Only people who own/have access to data should be allowed to modify it. An example of a lapse in integrity would be if a flood destroyed a database that was not backed up or if a hacker deleted encrypted files.

Availability
: Keeping data available for users who are authorized to view or modify it. And example of a lapse in availability would be if servers were under DDoS attack and that prevented users from logging into or using the website.

## Confidentiality
### Common Attacks
Breaches in confidentiality are some of the most widely reported security failures. Whenever you hear of passwords being hacked, names being released or otherwise private data no longer being private, these are failures in confidentiality.

In general they start with a failure to properly secure a server. A malicious user gains access to a protected server which is the step. From there they are able to find and read protected data.

### Prevention
Confidentiality can generally be maintained if either of these steps are prevented. Keeping malicious users from getting access in the first place is often a matter of making sure that recent security updates to all software on the server are installed correctly and that users with access to the server understand best practices in keeping their accounts secure. These are common practices that should be used in any software environment.

The next step is once a malicious user gains access, they need to be prevented from actually reading confidential data. The way to do this is via encryption. Anything that is potentially sensitive should be encrypted from end to end. That means that it should be sent over TLS when being transmitted to and from the server and it should be in an encrypted database on the server.

That is not to say that all data should be encrypted. There is a hit to speed when data needs to be encrypted and decrypted so very frequently accessed non-confidential data should probably not be encrypted.

In addition to this, extra care should be taken with passwords. Because if a malicious user gets access to account credentials it can potentially compromise both confidentiality and integrity of the users data on your server and on any other server where they used the same credentials.

To prevent this you should either rely on a reliable 3rd party to securely handle authentication or use practices beyond simple encryption, like salting and hashing passwords. The process of doing this is beyond the scope of this class presently but if you ever do need to handle account credentials you should use a library that does this and make sure to follow the best practices of that library to salt and hash passwords.

## Integrity
Integrity might at first seems redundant with confidentiality. If no one bad can read the data, then how can anyone bad muck around with it? More often than not this comes in the form of destroying data rather than changing it and using it for some nefarious purpose.

### Common Attacks
Breaches in integrity need not always be 3rd party attackers. A physical disaster like a fire or flood that damages servers that do not have backups would be a breach of data integrity. But there are also malicious attacks that can damage integrity. Examples would be users who gain access to a server and reformat a drive or selectively delete or change files. Another common issue is SQL injection attacks (which could also cause breaches in confidentiality). A user could inject malicious SQL code that would delete tables or rows in a database. Recently there have been attacks where an attacker encrypts the data on a hard drive and holds it ransom. The data isn't permanently changed but because it was changed to be encrypted and the original owner does not have they key to encrypt it, it can be effectively destroyed unless the victim pays the attacker to unencrypt it.

### Prevention
The answer to almost every problem dealing with integrity is a good backup system. There should be many backups, as the backups get older they can be weeded out. You might have hourly backups, then when they get to a day old you might only keep one per day. Then as they age to a month you might only have one per week and so on.

You also need to have a process to regularly restore from backup. If you have not checked and confirmed that you can restore from a backup in the last month that is often considered no better than not having a backup. Many times backups are made that are not actually complete or are missing critical configuration details to actually use them.

In addition to this, making sure your site and forms are not vulnerable to injection attacks is important along with making sure protected resources are actually protected.

It is good practice to be secure by default. In other words, if a resource is not explicitly public, it should not be publicly accessible. In general, without any additional steps the opposite is often true. Resources are public unless there is specific logic in place to secure it, but this is prone to missing something and causing data to be insecure because of that.

## Availability
### Common Attacks
This is almost exclusively a Distributed Denial of Service attack (DDoS). A massive number of computers make requests to a server at the same time simply overwhelming it. This causes the server to simply be unable to process requests and it appears to go off-line.

### Prevention
There is not a great deal that the developer of an application can do to mitigate malicious users launching a DDoS attack on the developer's application. By using a distributed platform some mitigation is afforded because there are multiple servers that must be attacked at once to bring the service down. But often times there is still a few bottlenecks which can still get overwhelmed. Things that make a fast service will tend to mitigate DDoS attacks as well. For example having a good load balancing system with several servers that can both handle and distribute load is a good tool to make DDoS attacks more difficult.

But often times this is going to be something that your cloud provider has more ability to mitigate than you do as the user of a cloud platform. On the other hand, if you are using IaaS then it really may fall entirely on you to mitigate these things. Another reason why using IaaS should not be taken lightly.

{{< kaltura 0_4fuk6a3p >}}

## Review
This is obviously a non-comprehensive coverage of security. But hopefully it gives you a frame in which to consider security issues as they relate to cloud computer and helped you consider some potential attacks and issues that you may not have previously considered. The best advice for most security issues is to use software that is mature, widely used and well supported. It is much more likely that software like this will be more secure than implementations you create yourself.

At the same time there is quite a bit of value in implementing for practice, not production, these systems by hand so that you understand the likely points of failure and you are able to better understand how the software you are using might be working and how it should be configured.