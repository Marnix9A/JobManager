# Security / Authentication

## Incoming

### User Name & Password

User names and passwords can be used for several endpoints, and can be passed in via several authentication methods. Unfortunattly not all methods allow all types of authentication.

#### Via Cookie

Most calls use cookie authentication, meaning you get the cookie first, and make the actuall calls afterwards.

First request a cookie once, and then make your actuall calls while including the cookie.\
Cookies can be requested like this:

```http
HTTP GET https://raptor.adultimagroup.com/eplatform/api/whitelist/setcookie
?referer=xxx&password=xxx
```

Note: you can also make this call with a HTTP POST, but the parameters still need to be passed in via the query.

#### Via Header

Only for the Kofax and Ephesoft integrations. Customers should never need to setup those routes by themself, so this should not be applicable.

### Raptor Token

Some calls support raptor tokens. If this is the case e-platform will validate the token which is functionally equivalient to using the token on the get user endpoint of the raptor api gateway.

If a user object is returned, then the call will be allowed endpoints linked to the same tenant as the user.

If no user object is returned the call will not be accepted.

## Outgoing

Authentication to other systems are configured per endpoint.&#x20;

Pro: Every endpoint can have it's own independent authentication sheme and user. So if the first endpoint in the route posts data to a D365-FO server, and the second endpoint is used to trigger a power automate flow, then this second endpoint can use a totaly different authentication method.

Con: This means that if you have a route with 5 endpoints to the same target service, you will have to configure the credentials 5 times. And update them 5 times should they ever change.

Possible authentication shemes:

### None

Authentication Type: -1

In case no authentication is required.

### Basic Authentication

Authentication Type: 0

If configured on the output endpoint, will add a http authentication header to the call of type "basic" and including the user name and password.\
Requires 2 parameters:

\[0] user name\
\[1] password

### Azure AD

Authentication Type: 1

If configured on the output endpoint, will add the http authentication header to the call of type "Bearer" with a token generated first.

requires 4 parameters:

\[2] Application ID\
\[3] Authorization URL\
\[4] Resource URL\
\[5] Secret Key

The authorization server will be contacted first to get the authorization token, which will then be included in the http call.

### NTLM

Authentication Type: 2

///

### Raptor

Authentication Type: 3

Can be used for communication with the Raptor API Gateway.\
An "exa-auth-plugin" header will be created, and added to the http call.

requires 3 parameters:

\[9] External System ID\
\[10] Secret\
\[11] User





\
<br>





