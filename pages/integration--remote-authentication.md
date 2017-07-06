---
title: Remote Authentication
permalink: /integration/remote-authentication
redirect_from: "/display/DOC/Remote+Authentication"
---

Using the Remote Authentication module it's possible to completely secure a Flipbook, while maintaining full control of access validation on the clients' own systems.

{% include important.html content='Please note that iPaper does not support any 3rd party protocols such as OAuth or Facebook. If you're looking to integrate a SSO solution into your flipbook, you'll need you create a custom solution using Token Based Authentication' %}

## Authentication Types

There are two overall mechanisms that allows the user to be granted access to the flipbook.

### Credential Based Authentication

In this scenario, when the user tries to open a secured Flipbook, he/she is automatically redirected to our standard login page. On the login page, the user can enter his/her username & password. Once "Login" is clicked, the iPaper system contacts the clients' system. Depending on the response from the clients' system, the user is either denied or granted access.

### Token Based Authentication

In this scenario, the user is browsing on the clients' secured website. Instead of having to login again to see the catalog, token based authentication can be used. When linking to the desired catalog, an arbitrary string (token) is sent along in the querystring. Once the catalog opens, iPaper will contact the clients' system and provide the token back - at this point the clients' system can verify that the user stems from there originally and hence grant or deny access.

## Implementing Credential Based Authentication

For credential based authentication, the client system must expose a public url that the iPaper system will call to authenticate users. While not a requirement, we recommend that it's exposed through HTTPS for optimal security. The url itself is specified through the "Authentication url" setting under the "Remote Authentication" module for either a Flipbook or a folder.

Once a user logs in, we will send a POST request to the specified url, containing the following POST fields:

| POST Field         | Description
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------
| CatalogUrl         | This is the url of the catalog - in case logins need to be verified according to the requested catalog. Example: /Company/Catalogs/Week13/
| UserIP             | This is the IP of the user trying to authenticate. Example: 212.242.193.110
| AuthenticationMode | For credential based authentication this will always be Credentials
| Username           | This is the username provided by the user
| Password           | This is the password provided by the user

The response should be in the following format:

```xml
<RemoteAuthentication>
    <AccessAllowed>true</AccessAllowed>
</RemoteAuthentication>
```

AccessAllowed being a boolean specifying whether the user is granted or denied access to the requested catalog.

## Implementing Token Based Authentication

For token based authentication the client system must expose a public url that the iPaper system will call to authenticate tokens. While not a requirement, we recommend that it's exposed through HTTPS for optimal security. The url itself is specified through the "Authentication url" setting under the "Remote Authentication" module for either a Flipbook or a folder.

For token based authentication to be invoked, a catalog must be opened with a "RemoteAuthenticationToken" parameter in the querystring. Once a protected catalog is opened and a remote authentication token is present in the querystring, we will send a POST request to specified url, containing the following POST fields:

| POST Field         | Description
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------
| CatalogUrl         | This is the url of the catalog - in case logins need to be verified according to the requested catalog. Example: /Company/Catalogs/Week13/
| UserIP             | This is the IP of the user trying to authenticate. Example: 212.242.193.110
| AuthenticationMode | For credential based authentication this will always be Credentials
| Token              | This is the token as specified by the RemoteAuthenticationToken querystring parameter

The response should be in the following format:

```xml
<RemoteAuthentication>
    <AccessAllowed>true</AccessAllowed>
</RemoteAuthentication>
```

AccessAllowed being a boolean specifying whether the user is granted or denied access to the requested catalog.

## Remote Authenticaition Settings

These are set on the Flipbooks(s) to be protected, just as the actual remote authentication service URL.

### Alternate External Login URL

When using token based authentication and the user visits a catalog directly, it might be desirable to redirect the user to the clients' own website for logging in. If the "External login url" setting is set, the user will automatically be redirected here, instead of being shown the standard login page. At this point, the client site may perform a login, create a token and redirect the user back to the catalog.
The original catalog url will be provided in the "CatalogUrl" querystring parameter.

### Alternate External Login Failure URL

In case of a login failure, it may be desirable to send the user to a custom login failure page. If the "External login failure url" setting is specified, the user will be sent here on login failures, instead of being shown the standard login failure page.

## Extra Response Options

Besides the AccessAllowed (true/false) response, there's a number of extra results that may be returned.

### RedirectTo

In the authentication response, a RedirectTo parameter may be specified like so:

```xml
<RemoteAuthentication>
    <AccessAllowed>true</AccessAllowed>
    <RedirectTo>http://www.client.com/ExpiredLogin.aspx</RedirectTo>
</RemoteAuthentication>
```

If the RedirectTo parameter is set, the iPaper system will automatically redirect the user to the specified url. This may be useful to provide a user with user specific feedback in case of login failures, promotions etc.
Note that the RedirectTo parameter will be utilized no matter if a positive or negative AccessAllowed response is returned. If a positive AccessAllowed response is returned, the user is granted access to the catalog before being sent on to the RedirectTo url. Thus the user can be sent back to the catalog without going through the authentication procedure again.
The original catalog url will be provided in the ```CatalogUrl``` querystring parameter.

### GrantAccessToDescendants

In the authentication response, a GrantAccessToDescendants parameter may be specified like so:

```xml
<RemoteAuthentication>
    <AccessAllowed>true</AccessAllowed>
    <GrantAccessToDescendants>true/false</GrantAccessToDescendants>
</RemoteAuthentication>
```

If the GrantAccessToDescendants element is set to true, iPaper will automatically validate the user for any Flipbook that are either direct children or descendants of the current address.

Imagine the following structure:

* /MyFolder/
  * /MyFolder/A/
  * /MyFolder/B/
  * /MyFolder/C/

If you access A/B/C directly and validate, you will only be granted access to that specific catalog, even with the GrantAccessToDescendants parameter set to true. If you setup one of the A/B/C Flipbooks as the default Flipbook of /MyFolder/ and validate, the user will automatically be validated for any Flipbooks starting with /MyFolder/ - in effect, A/B/C. As such, visiting just the default Flipbook, can be used to validate the user for a whole structure of Flipbooks.

## Sample ASP.NET Implementation

The [RemoteAuthentication.zip](/files/RemoteAuthentication.zip) file contains two pages: Login.aspx and Authenticate.ashx

Authenticate.ashx contains functionality for validating both credential and token based authentication requests, using a simple switch on the AuthenticationMode parameter. The credentials and token are hardcoded in the files, so it can be used as a template for performing a real validation.

Login.aspx is used for testing out token based authentication with a remote login page. The following workflow shows the functionality:
1. User attempts to open a protected catalog.
2. User is sent to the remote login url (Login.aspx).
3. Once user validates, Login.aspx redirects the user back to the original catalog, alongside a RemoteAuthenticationToken in querystring.
4. iPaper contacts the authentication page and attempts to validate the provided token.
5. Given a positive result, the user now has access to the catalog.
