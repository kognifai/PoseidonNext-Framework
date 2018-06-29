# Desription

```@kognifai/poseidon-app-registration-cli``` is a command line interface tool (CLI) to register the applications and data adapers you have developed with the Poseidon API. The app registers the metadata information that is automatically generated for you if you have used one of the Poseidon Yeoman generators to scaffold your project.

# Application manifest

Poseidon applications can be scaffolded with the ```@kognifai/generator-poseidon``` Yeoman generators. See the getting started article for more info on how to scaffold a project. A typical application manifest can look like this:

```json
{
    "id": "529cd141-d1a2-4d3b-9e6e-55a14f41a0e7",
    "name": "My App",
    "url": "http://localhost:4200/",
    "oidcClientId": "my-app"
}
```

# Using the tool

_Prerequisite: This app requires Node 8 or greater to be installed._

1. Install the tool as a global npm package by running ```npm install -g @kognifai/poseidon-app-registration-cli```.
2. Restart your command line window
3. You can now run the tool by typing in ```regapp``` form anywhere. This will present you with the options for the tool.

![2018-06-14_08-52-35.png](/Public-documentation/images/2018-06-14_08-52-35-f86cf13e-03a7-4b61-87cd-30f8bb9155c6.png)

# Registering manifests

_The following section assumes that you are a developer using the ```@kognifai/poseidon-dev-host``` API for your local development environment against the default host and port which is localhost:8080. You can specify any username and password below. When using this in a non-developer scenario or against a deployed Poseidon API you need to have a Poseidon user that has permissions to add applications. This will also require some extra configuration as specified below._

## Application

1. Go to the root folder of your application that has been scaffolded with ```@kognifai/generator-poseidon```
2.  Run the following command ```regapp -a app.manifest.json -u username -p password```

## Data adapter

1. Go to the root folder of your data adapter that has been scaffolded with ```@kognifai/generator-poseidon```
2.  Run the following command ```regapp -d adapter.manifest.json -u username -p password```

If the registration was successful you should see the following messages:

![2018-06-14_09-12-32.png](/Public-documentation/images/2018-06-14_09-12-32-8e10e27c-4df5-400f-bd3c-eb35047415e9.png)

# Configuration

If you are using the tool against a hosted Poseidon API other than the ```@kognifai/poseidon-dev-host``` you have to point the app to the API. Change the `host` and `port` properties in the `poseidonAPI` section accordingly. In addition, change the security section to point to the proper endpoints for the OpenID Connect / OAuth2 security service in use.

As per the OpenID Connect specification these endpoints should be available at a known url: ```mySecurityServiceUrl/.well-known/openid-configuration```

For example for the Poseidon Dev Host these endpoints can be found at: [http://localhost:8080/Security/auth/.well-known/openid-configuration](http://localhost:8080/Security/auth/.well-known/openid-configuration)

```json
{
    "poseidonAPI": {
        "host": "localhost",
        "port": 8080,
        "apiBasePath": "/api/v1"
    },
    "security": {
        "issuer": "http://localhost:8080",
        "authentication_endpoint": "http://localhost:8080/Security/auth",
        "authorization_endpoint": "http://localhost:8080/Security/auth",
        "token_endpoint": "http://localhost:8080/Security/auth/token",
        "userinfo_endpoint": "http://localhost:8080/Security/auth/me",
        "jwks_uri": "http://localhost:8080/Security/auth/certs"
    }
}
```
