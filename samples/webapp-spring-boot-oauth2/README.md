Log in with Omnissa Identity Manager
=========================================

This demo application shows the use of Spring Boot and its built-in OAuth2 capabilities to
let a user authenticate with Omnissa Identity Manager™ and then use the access token to
 access Omnissa Identity Manager resources (like the user information).

This application is based on the [Spring Demo application](https://spring.io/guides/tutorials/spring-boot-oauth2/#_social_login_github)
and has been modified to integrate Omnissa Identity Manager as an authorization server.

## Building the project

### Prerequisites

- You need a [Omnissa Identity Manager organization](http://www.air-watch.com/omnissa-identity-manager-free-trial), like https://dev.omnissaidentity.asia, where you have __admin__ access.
- The project requires JDK 8

### Building from IDE

* Clone this project.
* Then import the root folder. You can run the main class `SocialApplication`.

### Building from the Command line

You can run the app by using:
`$ mvn spring-boot:run`

or by building the jar file and running it with `mvn package` and `java -jar target/*.jar` (per the Spring Boot docs and other available documentation).

### Configure the Demo App

* Create an OAuth2.0 client in the Omnissa Identity Manager admin console.
Go to `Catalog` -> `Settings` -> `Remote App Access`. Click on `Create Client`.
The _redirect URI_ must be set to `http://localhost:8080/login/omnissa`

* Edit the file `./src/main/resources/application.yml` to set your own Omnissa Identity Manager organization URL in the defined endpoints,
and the OAuth2 client id and client secret as they were defined in the previous step:

```yaml
omnissa:
  client:
    accessTokenUri: <your organization URL>/SAAS/auth/oauthtoken
    userAuthorizationUri: <your organization URL>/SAAS/auth/oauth2/authorize
    clientId: <client id>
    clientSecret: <client secret>
  resource:
    userInfoUri: <your organization URL>/SAAS/jersey/manager/api/userinfo
```

### Test the application

The web application will be available on `http://localhost:8080`. Click on "Login with WorkspaceONE" to start the OAuth2 flow.
You can use the default values and log in to the demo Omnissa Identity Manager system using:

* Username: `userN`, where N=1..10
* Password: `omnissa`

### What is happening?

Your web application is a client application that authenticates the users using Omnissa Identity Manager
through the OAuth2 authorization code grant and obtains an access token that is used to fetch some more information
about the user. In that case, Omnissa Identity Manager is the authorization and resource server and check the access token before returning
the user's information.
