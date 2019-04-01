---
title: "OAuth 2.0 Flow Example"
description: "This example looks at every single request made in an OAuth 2.0 Authentication process."
categories: ["Exploration"]
weight: 1
---
<!--- Make sure to fill out the title and description above, they will be used when generating lists of exploration topics -->
<!--- The weight above determines what order this will be shown among other exploration topics in this same folder, lower numbers are shown first. Start using at least multiples of 5, that way if you need to add a content page between existing ones there are enough open weights to do so. They are integers only -->

{{< title >}}
## Introduction
This module will show in its entirety the requests needed to complete an OAuth 2.0 login. These are the requests specific to Googles OAuth 2.0 Endpoint. They may look a bit different for different providers.

## Getting the Access Code

### Send the End User to the OAuth Provider
The first step is to direct the end user to the server via a GET request with the following parameters.

```http
GET https://accounts.google.com/o/oauth2/v2/auth
response_type:code
client_id:[your-client-id]
redirect_uri:[where-the-client-gets-redirected-to]
scope:[list-of-scopes]
state:[random-secret-string]
```
An example URL would look like this `https://accounts.google.com/o/oauth2/v2/auth?response_type=code&client_id=107461084371-0vr1hjlgafvltftq307ceq0pcjrk2ad4.apps.googleusercontent.com&redirect_uri=https://osu-cs496-demo.appspot.com/oauth&scope=email&state=SuperSecret9000`

### User Accepts at the Server Site
The user will interact with the server to let it know that it authorizes the client to access its protected resource. Upon completing this the server will send back a response that looks like:

```http
/oauth?state=SuperSecret9000&code=4/-NkRHrxqExe43IwSNlTRFExoKxRWUVpJBvOe7ts0G88
```

The client needs to verify the state matches one that was sent previously. The client takes that code and then directly sends it to the server via a POST that looks like this:

```http
POST https://www.googleapis.com/oauth2/v4/token
code:[access-code]
client_id:[your-client-id]
client_secret:[your-client-secret]
redirect_uri:[location-of-redirect-url]
grant_type:authorization_code
```

Actual example data looks like:
```http
code:4/-NkRHrxqExe43IwSNlTRFExoKxRWUVpJBvOe7ts0G88
client_id:107461084371-0vr1hjlgafvltftq307ceq0pcjrk2ad4.apps.googleusercontent.com
client_secret:WAY53N7ZAXTX9UHm_CIgfAhJ
redirect_uri:https://osu-cs496-demo.appspot.com/oauth
grant_type:authorization_code
```

### Server Responds With Access Token
After the server verifies the access code it creates an access token for the end-users protected resource and returns it, along with an expiration. It looks like this:

```json
{
  "access_token": "ya...fK",
  "token_type": "Bearer",
  "expires_in": 3487,
  "id_token": "ey...Vg"
}
```

The `access_token` is the OAuth 2.0 token. The `id_token` is used for authentication rather than authorization. In this case the token expires in 3487 seconds. It is possible to request a token that can be refreshed but that is beyond the scope of this example.

### Making Requests Using the Token
Subsiquent requests to the server need to contain a `Authorization` header set to `Bearer ya..fk`. This is the way of communicating the value of the token to the server so it knows you are authorized to access the protected resource and that is it.

{{< kaltura 0_3ofu0ovj >}}

## Review
As is the way of things when dealing with the web, there are lots and lots of strings, where things like capitalization and character encoding are really important. There are lots of libraries out there to do this stuff. If you ever want to use OAuth 2.0 in production use a library. But there is very little that will replace hand coding a client to build understanding of how the underlying system works. This can make it much easier to learn how to use new libraries and understand things like security risks. Hopefully this gave you an idea as to how OAuth 2.0 works.