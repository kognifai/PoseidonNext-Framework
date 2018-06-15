# Description
The authentication service is used in client applications for authenticating against an OIDC identity server. It is simple service to use, provides Login and Logout functionality, and requires minimum configuration and dependencies.


# Using the Authentication Service

## Injecting
The authentication service can be used by injecting it into a class/component, just like any standard Angular service.

```javascript
export class AuthenticationServiceTestPageComponent {
   constructor(private authenticationService: AuthenticationService) {
   }

   ...
}
```

## Configuration
The configuration stage of the service means just passing the client's base URL to the Login method. The URL could be supplied via a configuration file (JavaScript, JSON) or via extracting the protocol, host and path name from the client's browser location.

Example:

```javascript
this.baseUrl = window.location.protocol + '//' + window.location.host + window.location.pathname;
```

## Login
The login function accepts the client's base URL as an argument and returns an ```Observable``` which, when completed, will notify that the user is successfully logged in.

```javascript
this.authenticationService.login(this.baseUrl).subscribe(
       () => {
          // 'next' callback, not supported
       }, error => {
          // error when logging in
       },() => {
          // successfully logged in
       });
```

## Logout
The logout method has a ```void``` return type and no parameters.

Example:
```javascript
this.authenticationService.logout();
```

## Public properties
The service exposes a number of public properties that can be utilized by the client application.

 - ```isAuthenticated``` - returns a ```boolean``` indicating whether the current user is logged in
 - ```profile``` - returns an ```object```, representing the currently logged in user's profile
 - ```accessToken``` - returns a ```string``` that contains the user's access token
 - ```idToken``` - returns a ```string``` that contains the user's identity token

# Prerequisites
There are a couple of things that the client application needs to do before it successfully starts to use the authentication service.

## frame.html
In order for the process of silent token renewal to work, the application needs to periodically navigate to an HTML page that executes a call to the OIDC client library. This page is provided by the authentication service as an HTML file (frame.html) and the client application just needs to copy it to its working directory.

Example (webpack):
```javascript
new CopyWebpackPlugin([
{
   "from": "./node_modules/@kognifai/poseidon-authenticationservice/dist/frame.html",
   "to": ""
}]);
```

## oidc-client.min.js
The frame.html contains a call to the ```oidc-client``` library and thus it needs to know how to load it. This is why the library's script file should also be coppied to the client application's working directory.

Example (webpack):
```javascript
new CopyWebpackPlugin([
{
   "from": "./node_modules/oidc-client/dist/oidc-client.min.js",
   "to": "./node_modules/oidc-client/dist/oidc-client.min.js"
}]);
```
