---
title: "OpenID Connect"
description: "OpenID Connect is a authentication protocol that sits on top of the OAuth 2.0 Authorization protocol."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
OpenID Connect is a authentication protocol that sits on top of the OAuth 2.0 Authorization protocol. There were multiple attempts to get OpenID to become an authentication standard but they generally failed as they tended to be more complex than standards like OAuth. So people started misusing OAuth to do authentication. In response OpenID Connect was created to give people an option to easily add authentication to the OAuth login flow.

## Authentication Flow
The OpenID Connect authentication flow is very similar to the OAuth 2.0 flow. (Hence, why it is said to sit on top of the OAuth 2.0 standard).

Recall in OAuth 2.0 the first step of the server side flow is to redirect the user to the Server's login page and ask for permission to access their protected resource. Upon doing so the Server issued a access code that the client could exchange for a token.

In OpenID Connect in addition to issuing an access code, a JSON Web Token is also issued. This token is not used for authorization of requests. Instead it is used to authenticate the user. It has information about who the user is. It also guarantees that the user authenticated with the OpenID Provider (OP).

At this point the Client (known as the Relying Party (RP)) needs to validate the JWT. It does this by either sending the token directly to the OP or using the OPs public RSA key to check the signature of the JWT. Once the JWT has been verified it can be used to authenticate the user.

## Authentication Use Cases
"Great, so why do we care about all this. I thought we had our problems solved with OAuth."

Well, I am sure you probably don't go more than a month before you hear about some company that just had all of its users credentials leaked and a little later you get an email saying that "you should change all the passwords you, your kids and your pets ever used and we are super super sorry we let you info get hacked".

OpenID can help mitigate that. It lets you authenticate a user without ever having to store their user-name and password. So they can still have an account at your website that contains whatever information you need. But you don't need to handle storing their authentication details or handling the authentication process. You can hand that off to some 3rd party that should theoretically have better resources to handle security than you might.

For example, because I use GMail for almost all of my work and accounts, I have essentially every possible security feature enabled. I need to enter in a code on my phone if I want to log into GMail on a new computer. Having this sort of two factor authentication set up is not easy but it is very robust. It is exceptionally unlikely that someone would manage to brute force their way into my account.

Now suppose I want to have an account with a hypothetical on-line video game, say Continent of Conflictcraft for example. These are often targets of hacking attempts. I could create an account with the makers of the game, Snow Storm Interactive. However, if they use OpenID Connect with Google as a OP then I could also use that Google system I know to be secure and not have to worry about someone hacking my user-name and password from Snow Storm Interactive.

In an ideal world I might only ever have to log into one OP that had really good security. All the other sites I use would simply get my authentication details from that provider when I need to log into their sites. The only way for someone to impersonate me would be to access my credentials for that one OP. None of the other sites that rely on it actually handle the authentication themselves.

## What This Doesn't Solve
So that's great, the authentication problem is solved! But that is only one of many privacy and security issues. Even if Google handles your authentication, sites may still store you address, your phone number or your credit card information. All of those things can still be compromised if someone hacks their database. OpenID does not help with any of that.

What it does help with is limiting the damage to only one site. Because no authentication information is stored on the RP servers a hacker can not use that information to try to log into other sites. Whereas if you happen to reuse the same password in multiple places that is a real risk.

{{< kaltura 0_c7ys66m6 >}}

## Review
OpenID Connect is a layer that sits on top of OAuth 2.0. It makes it so that a user does not need to share or store any credentials with a Relying Parties servers. Instead an OpenID Provider stores and checks credentials and sends a token to a RP indicating if a user authenticated successfully and if they did, gives details about who they were.

This means that user have to remember and deal with fewer login credentials and that sites which are more trusted by the user can be used to authenticate them at less trusted sites.