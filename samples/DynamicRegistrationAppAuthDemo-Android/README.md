# Mobile SSO Sample Application For Android

## Overview

This application is an Android native demo application to show you how to achieve mobile single sign-on using the [AppAuth library](https://github.com/openid/AppAuth-Android) with Omnissa Identity Manager as your Authorization Server.
It is based on the [demo application](https://github.com/openid/AppAuth-Android) provided by the OpenID Foundation.

Omnissa Identity Manager supports the OAuth2.0 Authorization Code Grant for mobile apps but requires each application instance to register a unique __Client ID__ and __Client Secret__ for additional security.
This application shows how to set up mobile single sign-on using the AppAuth standard library.

## Building the project

### Prerequisites

- You need a [Omnissa Identity Manager organization](http://www.air-watch.com/omnissa-identity-manager-free-trial), like https://dev.omnissaidentity.asia, where you have __admin__ access.
- The project requires the Android SDK for API level 23 (Marshmallow) to build, though the produced binaries only require API level 16 (Jellybean) to be used.

### Building from Android Studio

* Clone this project.
* Then in AndroidStudio, use File -> New -> Import project. Select the root folder.

### Building from the Command line

DynamicRegistrationAppAuthDemo for Android uses Gradle as its build system. In order to build the library and app binaries, run `./gradlew assemble`
The demo app is output to _app/build/outputs/apk_. In order to run the tests and code analysis, run `./gradlew check`.

### Configure the Demo App

You will need to edit the file `./app/src/main/res/values/idp_configs.xml` and edit the following values:

* the organization URL: this is the full URL of your Omnissa Identity Manager organization:

```xml
    <!-- Your Omnissa Identity Manager organization URL. -->
    <string name="omnissa_url" translatable="false">https://dev.omnissaidentity.asia</string>
```

* the application template and redirection URI: this is the template you defined in the Omnissa Identity Manager admin console under
`Catalog` -> `Settings` -> `Remote App Access`. Click on `Templates` and then `Create Template`.
The `omnissa_auth_redirect_scheme` and `omnissa_auth_redirect_uri` must match what you defined in the previous application template.

```xml
    <!-- The information below must match the template information defined in the admin interface. -->
    <string name="omnissa_template" translatable="false">Omnissa-AppAuth-Samples-Template</string>
    <string name="omnissa_auth_redirect_scheme" translatable="false">com.omnissa.idm.samples.mobilesso</string>
    <string name="omnissa_auth_redirect_uri" translatable="false">com.omnissa.idm.samples.mobilesso://oauth2redirect</string>
```

### Test the application

You can use the default values and log in to the demo Omnissa Identity Manager system using:

* Username: `userN`, where N=1..10
* Password: `omnissa`
