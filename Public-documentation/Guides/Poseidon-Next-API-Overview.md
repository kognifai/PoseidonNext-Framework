# Kognifai Platform
The kognifai platform is made of many APIs and the Poseidon Next set of APIs is one of them. Many of the services and applications in the kognifai platform come with their own set of APIs, user applications and libraries. 

While all these APIs can run on different endpoints, they can be unified in a uniform way using API gateways.

# Poseidon Next API
The Poseidon Next API aims to support the quick development of front-ent web applications by providing typical services needed by these applications. 

The API is built using ASP.NET Core and is using REST conventions where applicable.

## Interfaces
One major set of the API interfaces are the functional ones where things like settings, logging and units are needed by almost all applications.

The other set is aimed to support the registration and location of applications and data adapters.

## Data Adapters
Data adapters, like the Poseidon Next applications, are intended to be run on different endpoints. Hence, their registration and location is necessary.

Data adapters are meant to give a simplified and unified way of accessing different resources like assets, timeseries and events. A data adapter is an API which implements a set of standard interfaces defined by Poseidon Next.

Not all the API interfaces can be implemented by all resource providers so when registered, data adapters list a set of capabilities which signals which set of the API interfaces have been implemented. All data adapters have to be registered with the Poseidon Next API so that they are made available to the application. A registration tool is included with Poseidon Next.

Poseidon Next provides a generator to scaffold an new ASP.NET Core API Data Adapter project.

## Identity Provider
The last set of Poseidon Next API interfaces are the identity provider interfaces which provide authentication, authorization, user and access management using open standards like OpenID Connect to applications and the other APIs.

# Clients
The API is complemented by a set of client libraries packages which aids the use of the API. The libraries are typically available as normal Javascript modules and as Angular services. More Javascript frameworks might be supported in the next releases.

Client libraries are versioned to reflect which version of the API interfaces they support.

# Versioning
The first version of the API interfaces is built so that is compatible with Poseidon 1.x applications. Next major version will not try to be backwards compatible. For this purpose the API is using the major version number of the interfaces in their URL. If changes are done in a fashion that is backwards compatible (ex: addition, extension) then the major version in the API URL will not change.


