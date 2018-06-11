
# Poseidon Next

Poseidon Next is a framework for developers to easily create web applications on the Kognifai ecosystem.

Developer's Getting Stated page is the home page for you to get started with. Access Developer's Getting Started page from the following table.

| Services| Link | Description  
|-------------------------|---------------|----------------
 Developers Getting Started page | [Developers Getting Started page](https://github.com/kognifai/PoseidonNext-Framework/blob/master/Developers-Getting-Started.md)      | A developer must start reading from this page to have a holistic view of Poseidon Next features |


Services are Library packages intented for specific set of tasks. Poseidon Next offers the following services that cab be used in your application.

| Services| Link       | Description  
|-------------------------|---------------|--------
 Authentication Service | [Authentication Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authentication-Service.md)|This service is used in client applications for authenticating against an OIDC identity server. It provides Login and Logout functionality|
 Authorization Service| [Authorization Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authorization-Service.md)|This service helps in managing resources and its associated permissions. |
  Common Data Service | [Common Data Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Common-Data-Service.md)|This service is used to fetch data from any time series data provider. |
 Configuration Service | [Configuration Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Configuration-Service.md)|This service is used to fetch some basic configurational information for the PoseidonNext. It is registered as one of the providers in app.module.ts in PoseidonNext Core. |
 Date Time Formatter Service |  [Date Time Formatter Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Date-Time-Formatter-Service.md)|This service is used to specify the date and time format which is to be displayed to the end user for application specific use cases. The package is independently developed without having any dependency on angular5 or with any of its sister libraries. The primary dependency for this package is moment.js . |
  Home and Favorites Service | [Home and Favorites Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Home-and-Favorites-Service.md)|This is the default landing page/view in Poseidon. It contains a default icon which enables user to add favourite items on this screen |
 Logging Service | [Logging Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Logging-Service.md)|This service is used to log messages from client to a centralised repository. Messages are logged based upon the configuration. In configuration, we mention the level of logs that we want to save in the server. |
  Message Service | [Message Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Message-Service.md)|This service is  used to show users different kinds of messages and toasters when there is a need for showing information or asking for confirmation. |
 Settings Service | [Settings Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Settings-Service.md)|This service is used to manage various applications and user-specific settings |The primary purpose of this service is to collect information pertinent to various trackable events, duration a user spends on a particular page, and other metrics, which is stored in the backend. Backend may choose to post them further to Azure's Application Insights or in their own local repository. |
 Statistics Service |  [Statistics Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Statistics-Service.md)|The primary purpose of this service is to collect information pertinent to various trackable events, duration a user spends on a particular page, and other metrics, which is stored in the backend. Backend may choose to post them further to Azure's Application Insights or in their own local repository.|
 Tools Menu Service| [Tools Menu Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Tools-Menu-Service.md)|The Tools menu service holds list of items that are displayed in the right-hand side menu in Poseidon. It is used by application developers in order to add custom commands in the Tools menu. |
Unit Of Measurement Service| [Unit Of Measurement Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Unit-Of-Measurement-Service.md)|This service (UOM) is used to convert units from one to another. This service is the single source of truth for any units and dimensions specific operations.  |

To create your Widgets and Widget packages, explore their description and sample codes from the following table.

| Widgets/Dashboards | Link | Description | 
|-------------------------|---------------|---------------|
  Creating a widget | [Creating a widget](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widget.md)|A widget is an Angular component that can be dynamically added, rearranged, configured, and saved into a view and loaded by Dashboards. |
  Creating a widgets package | [Creating a widgets package](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widgets-package.md)|A widgets package is an Angular module that currently has two main purposes: 1. Declares widget components (so they are visible to other Angular modules) 2. Registers widgets with the Dashboards framework (so they are visible to dashboards creators) |
  
# Attributions
Please see the attribution file [KognifaiPoseidonNext-Attribution](https://github.com/kognifai/PoseidonNext_Samples/blob/master/KognifaiPoseidonNext-Attribution.pdf)

# License
Read the copyright information and terms and conditions for Usage and Development of the software [here](https://github.com/kognifai/Kognifai/blob/master/License.md#copyright--year-kongsberg-digital-as).
