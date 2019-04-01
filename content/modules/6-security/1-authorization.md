---
title: "Authorization"
description: "This looks at authorization, the process of deciding on who can and who cannot access a particular resource and actually limiting that access."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
Authorization, simply put, is the process of determining if the requester of a resource is allowed to access that resource. It is very important to not expand this definition any further than this. Doing so tends to open up a lot of security holes because people believe an authenticated request conveys more meaning or is somehow more complex than this. We will go into some detail on that shortly.

## Authentication vs Authorization
This is probably the most critical distinction to make when discussing the concept of authorization and security. Authentication is the process of determining who is making a request. When you go to the DMV and they ask for various pieces of ID like a birth certificate or utility bill at your current house they are authenticating your identity. They are making sure you are who you say you are.

Now suppose the reason you are at the DMV is to get a drives license after passing your exam. It is 100% possible that you can show up to the DMV, show them ID that convinces them that you are undoubtedly Jack Sparrow. They successfully authenticate you. But when you ask for your drivers license they say "We have no record of you ever taking a drivers exam, we are unable to give a drivers license". Despite successfully authenticating yourself, you were not authorized to access that particular resource.

### Separation of Concepts
In this case, and what may seem like the case as a end user of software, the action of authenticating and authorizing are often very intertwined. It can seem like if something is asking for authorization to do something, it must surely also be asking for authentication as well. And that is where we need to be very careful.

But lets imagine a DMV with much more bureaucracy and distributed systems. Lets say now that Speed Racer is applying for a license, once authenticated, Speed Racer needs to leave a credit card, because it costs $10 to get a license printed. And that instead of being able to check immediately if Mr. Racer passed the test, the DMV needs to contact the Keeper of Driver Test Records and this process takes a day or two.

So some time later the Keeper of Driver Test Records gets a request to find out if one "Speed Racer" passed the drivers test. It turns out that indeed, Speed Racer did pass the exam. At this point Speed Racer has gone home long ago and is nowhere to be seen. However, the Keeper of Driver Test Records has the piece of paper from the DMV saying that the Keeper is authorized to print and mail a license to Speed Racer and charge the credit card on file $10.

The Keeper of Driver Test Records has no idea who Speed Racer is. The Keeper did nothing to verify the identity of Speed Racer, but the Keeper does have authorization to issue the license and bill the credit card because the DMV provided documentation to do exactly that.

{{< kaltura 0_2eeoscdb >}}

### Delegated Authorization
Delegated authorization is one of the more common ways of dealing with authorization between a single end-user and a lot of on-line systems that they use, especially when those on-line systems operate even when the user is away. Consider an on-line message board.

It is fairly common to log into some sort of social media site, say Flittergram, via Facebook. Generally you sign up, you get redirected to Facebook with a prompt that asks if you want to allow Flittergram to access your profile picture, name and contacts. If you say yes, Facebook gives you a token that you can give Flittergram. That token acts as your authorization to allow Flittergram to access your profile information on your behalf. You have delegated access to your Facebook into to Flittergram.

It is critical to note here that you never need to access Flittergram again. But even if you don't Flittergram can continue to make requests to Facebook asking for your current profile picture or an updated list of friends.

Facebook has no idea who is making the requests using the token. It could be you accessing Flittergram and so Flittergam is making requests with you as the end user. It could be someone else browsing your profile or viewing a post you made on a message board.

All Facebook knows is that someone is making a request with a token that you said should have access to your profile information. Heck, it could even be Flittergram's sister company Tweddit that it shared the token with.

It would be a terrible mistake for Facebook to assume that because someone is using that token, that they are you. The token in no way represents that. It also is a mistake to assume that because Facebook issued them a token, that you actually were there to authorize that or even that that token contains information that can identify who authorized it.

The whole point of delegated authorization is that the person who is delegating permissions to access their protected resources need not be around or involved in the process directly.

{{< kaltura 0_canhxrq5 >}}

## Review
This was the non-technical description of authorization and delegated authorization. We discussed authentication as well because it is very, very often confused with authentication and it is important to make the distinction between them. But for this portion of the class we are only going to be focusing on authorization which is important to remember if you ever want to apply this to make a secure system.