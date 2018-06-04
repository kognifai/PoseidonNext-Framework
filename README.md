
# Poseidon Next

Create Kognifai applications with the Poseidon Next Framework.

To get started please read the [Getting started](https://github.com/kognifai/PoseidonNext-Framework/blob/master/Developers-Getting-Started.md) article.

Poseidon Next Services, Widgets, and Dashboards information are available in the following table. Click the link associated to a particular Service, Widget, or Dashboard for more description and sample codes.

| Services/Widgets/Dashboards | Description | Link | 
|------|----------|----------|
 Authentication Service | This service is used in client applications for authenticating against an OIDC identity server. It provides Login and Logout functionality| [Authentication Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authentication-Service.md)|
 Authorization Service| This service helps in managing resources and its associated permissions. |[Authorization Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authorization-Service.md)|
  Common Data Service | This service is used to fetch data from any time series data provider. |[Common Data Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Common-Data-Service.md)|
 Configuration Service | This service is used to fetch some basic configurational information for the PoseidonNext. It is registered as one of the providers in app.module.ts in PoseidonNext Core. |[Configuration Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Configuration-Service.md)|
  Creating a widget | A widget is an Angular component that can be dynamically added, rearranged, configured, and saved into a view and loaded by Dashboards. |[Creating a widget](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widget.md)|
  Creating a widgets package | A widgets package is an Angular module that currently has two main purposes: 1. Declares widget components (so they are visible to other Angular modules) 2. Registers widgets with the Dashboards framework (so they are visible to dashboards creators) |[Creating a widgets package](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widgets-package.md)|
 Date Time Formatter Service | This service is used to specify the date and time format which is to be displayed to the end user for application specific use cases. The package is independently developed without having any dependency on angular5 or with any of its sister libraries. The primary dependency for this package is moment.js . | [Date Time Formatter Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Date-Time-Formatter-Service.md)|
 Developers Getting Started page | A developer must start reading from this page to have a holistic view of Poseidon Next features | [Developers Getting Started page](https://github.com/kognifai/PoseidonNext-Framework/blob/master/Developers-Getting-Started.md)|
  Home and Favorites Service | This is the default landing page/view in Poseidon. It contains a default icon which enables user to add favourite items on this screen |[Home and Favorites Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Home-and-Favorites-Service.md)|
 Logging Service | This service is used to log messages from client to a centralised repository. Messages are logged based upon the configuration. In configuration, we mention the level of logs that we want to save in the server. |[Logging Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Logging-Service.md)|
  Message Service | This service is  used to show users different kinds of messages and toasters when there is a need for showing information or asking for confirmation. |[Message Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Message-Service.md)|
 Settings Service | This service is used to manage various applications and user-specific settings |[Settings Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Settings-Service.md)|
 Statistics Service |  The primary purpose of this service is to collect information pertinent to various trackable events, duration a user spends on a particular page, and other metrics, which is stored in the backend. Backend may choose to post them further to Azure's Application Insights or in their own local repository. |[Statistics Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Date-Time-Formatter-Service.md)|
 Tools Menu Service| The Tools menu service holds list of items that are displayed in the right-hand side menu in Poseidon. It is used by application developers in order to add custom commands in the Tools menu. |[Tools Menu Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Tools-Menu-Service.md)|
Unit Of Measurement Service| This service (UOM) is used to convert units from one to another. This service is the single source of truth for any units and dimensions specific operations.  |[Unit Of Measurement Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Unit-Of-Measurement-Service.md)|
           
# Attributions
Please see the attribution file [KognifaiPoseidonNext-Attribution](https://github.com/kognifai/PoseidonNext_Samples/blob/master/KognifaiPoseidonNext-Attribution.pdf)

# License
Read the copyright information and terms and conditions for Usage and Development of the software [here](https://github.com/kognifai/Kognifai/blob/master/License.md#copyright--year-kongsberg-digital-as).
