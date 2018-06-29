# Kognifai Platform
The kognifai platform is made of many web applications and Poseidon Next provides some of the commonly needed applications in the platform. Additionally it aims to ease and accelerate the development of web based front-end applications.

Web based applications in the kognifai platform are unified through the use of the same APIs, design, components and libraries.

Technological diversity is embraced and as such there are no restriction on the technologies used to build web application which run on the kognifai platform.

# Development
Poseidon Next offers a generator which scaffolds a new Angular application that pulls together all the necessary components for a typical application. The generator will be able to scaffold projects based on other frameworks (ex: React, Vue, etc.) in the next releases.

A typical  application is composed of a sidebar menu, a tools menu, a header, a footer and the main application surface. The sidebar menu provides navigation to other applications and routes within the same application. The tools menu provides access to functionality related to the current application or route.

![appstructure.PNG](.%20images/appstructure-8c7c0cfe-dd86-4179-ad09-4c38e1012cbd.PNG)

Poseidon Next publishes many component as Angular components and as web components in next releases. Libraries are typically available as normal Javascript modules and as Angular services. More Javascript frameworks might be supported in the next releases.

# Deployment
Web applications can be deployed in any way and anywhere as long as they can be accessed by the users and they can access the Poseidon Next API and other APIs that they need to function. Applications need to register themselves against the Poseidon Next API in order to be made available to the users of the kognifai platform. A registration tool is included with Poseidon Next.

# Migration
There are many degrees of integration:
1. Host your web application as before and register it with the Poseidon Next API so that it show up in the list of available applications. Register sub-routes if your application has any.
2. Provide a mechanism to navigate from your application to the other Poseidon Next applications.
3. Use the libraries provided by Poseidon Next to use the available services
4. Use of the design system so that the application has the same look and feel as the other Poseidon Next applications.
5. Use the components eventually provided by Poseidon Next. Angular components if you have an Angular application and if not then the eventually released webcomponents provided by Poseidon Next.

##Poseidon 1.x
A recommended migration path for Poseidon 1.x applications will be made available with the next releases. Poseidon 1.x applications can still integrate like any other applications as mentioned above.

