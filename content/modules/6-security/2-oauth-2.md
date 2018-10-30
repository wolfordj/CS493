---
title: "OAuth 2.0"
description: "OAuth 2.0 is a delegated authorization standard. This looks at how one goes about using it as a client."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
OAuth 2.0 is an authorization protocol that is widely adapted among web services. If you want to access a users resources on differently platforms it is very, very likely that OAuth 2.0 will be the authentication protocol that is used to do so.

## OAuth 2.0
[This answer](https://stackoverflow.com/questions/4727226/on-a-high-level-how-does-oauth-2-work/32534239#32534239) on StackOverflow is my favorite high-level description of OAuth 2.0.

<iframe width="560" height="315" src="https://www.youtube.com/embed/byZQ9KT7wWA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


## Flow Types
#### Definitions
Definitions
End-User
: This is typically the actual human involved in using an application.

Client
: The program that needs to access the end-users protected information.

Server
: The program that allows access to the end-users protected resource.

Protected Resource
: The thing that is trying to get accessed.

The most important thing to notice here is that the client and the end user are not the same person. Often times when talking about the client and the server in the context of web based applications one assumes the client is a human (or

### Server Side Flow
For cloud applications this is what we are most interested in and it is the flow that is described in the metaphor with Olaf the baker.

1. The end user requests that the client access a protected resource on the server.
1. The client sends the end user's browser to the server along with a list of permissions the client is asking for and a secret phrase that the client just made up.
1. The server asks the end-user if they are OK with giving the client the things it is asking for.
1. The end-user is redirected back to the client with an authorization code and the secret phrase that the client made up moments ago.
1. The client gets the authorization code from the end-user.
1. The client sends the authorization code along with a secret phrase to the server. (The secret phrase is agreed upon ahead of time)
1. The server makes sure that the secret phrase is associate to that client and that the authorization code is the one it gave out.
1. The server sends back an access token.
1. The client saves the access token and sends it along with all requests for the end-users information.

We will talk about the technical implementation of this is a bit, but there are a few common questions that come up when dealing with OAuth 2.0.

### How is this Secure?
You will notice there is, at no point, the mention of encrypting anything or securing anything. That is entirely up to the client and server to negotiation on their own. In general this would use TLS for all requests. Failure to do so would be a huge security risk. So without adding encryption to this, you are asking for trouble.

### Whats up with the Access Code?
Obviously the token is sort of like a normal username and password sort of deal. It is what proves the client was given access to the resource. But what about the access code? Why not just return the token immediately?

Well, in the first 5 steps of the above flow the client has no contact with the server. But the server only has agreements with certain clients. So the server knows who the end-user is, and the server knows the end-user is OK giving its information to the client, but the server isn't yet confident that the client is actually the one sending the end-user to the server.

So when the client sends the access code to the server, it also sends a code that only the server and the client know. This makes sure that only authorized clients get tokens. Otherwise clients could be impersonated which would be a big security risk.

### Whats up with the First Secret Phrase?
When the client sends the end-user to the server it gives them a random secret phrase. This is to prevent XSRF attacks. Discussing these is beyond the scope of this class. But the basic idea is that this proves the end-user started at the client's site and not from some other malicious site.

{{< kaltura 0_pkg8jisa >}}

### Implicit Flow
The implicit flow, also known as the client side flow is a bit different. It is used for purely client side (in this case client side meaning controlled by the end user) applications. This is what the implicit flow looks like:

1. End-user requests that the client application access a protected resource.
2. Client application redirects the user to the server with a list of permissions and a random phrase.
3. The server asks the client if it is OK with the client app accessing the things in the list provided by the client app.
4. The server redirects the end-user to the client app with a URL fragment (the thing after the # in a URL) containing an access token along with the random phrase.
5. The client app sends the token to the server to ask if the server indeed issued that token.
6. The server says that it did.
7. The client app makes requests on the end-users behalf with the token.

So this looks pretty similar but there is a major difference. The client does not need to register with the server. This would be the case when everything is done client side via JavaScript for example. The requests would be coming from the users of the JavaScript app, not a central server, so there is no way to verify who the client is. Without being able to validate the client, there is no need to issue the access code and the token is issued directly.

Also worth noting is that the client app is not required to verify the token with the server. That is, the server will not reject requests if the token is not verified. But it is a major security risk to not verify the token first and it is entirely the client application's responsibility to do so.

In general we won't worry about the implicit flow in this class but it is good to know about.

{{< kaltura 0_bytxu7au >}}

### Mobile Apps
Finally lets talk about mobile and desktop apps. If you were really considering things carefully you might be noticing a potential problem if you want to use the server side flow with a mobile or desktop app. The issue is that the client secret will never be able to be kept secret if the desktop or mobile app is acting as the client.

The answer is not to use the implicit flow. Instead it is to use the server-side flow, with the mobile or desktop app acting as the client, but simply not use a client secret.

**What the Heck? Is this Client Secret Just to Make Life Harder?**

If we can just 'not use' the client secret, why did we spend all that time talking about it?! Well the reason is, is that it is fairly easy to pretend to be a website. BadGuy can buy a domain like `oregonst.edu` and load up all the HTML and CSS from `oregonstate.edu` and do a pretty convincing job pretending to be Oregon State. The client prevents that because it isn't public, so BadGuy won't be able to send that to a server when he has a client pretending to be Oregon State.

On the other hand it is a lot harder to pretend to be Microsoft Word or World of Warcraft. You would need to get someone to download and install a product that looked and acted just like the legitimate counterpart. So the reason things still work without a client secret with installed apps is because of the difficulty in spoofing one.

## Activity
I know that is a lot to take in. I have tried one way of explaining this. But there are literally hundreds of other explanations, pictures and metaphors out there. Go find three other descriptions of OAuth 2.0 server side flow and make sure they make sense to you. Once you have a good grasp of it you should be able to understand most descriptions.

## Review
So that is the medium level look at how OAuth 2.0 works. You should understand conceptually what all the steps are and why they are used. At this point it would still be a stretch to implement it, but you should be able to look at an implementation and identify the various pieces. Soon we will be looking at actually implementing this.