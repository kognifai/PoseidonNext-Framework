
# Poseidon Next

Create Kognifai applications with the Poseidon Next framework.

To get started please read the [Getting started](https://github.com/kognifai/PoseidonNext-Framework/blob/master/Developers-Getting-Started.md) article on the wiki.

To know more about Poseidon Next services, Widgets, and Dasboards, click any one of the services from the following table:

| Services/Widgets/Dashboards | Description | 
|------|----------|
 [Authentication Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authentication-Service.md) | This service is used in client applications for authenticating against an OIDC identity server. It provides Login and Logout functionality| 
 [Authorization Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Authorization-Service.md)| This Service helps in managing resources and its associated permissions. |
  [Common Data Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Common-Data-Service.md)| This Service is used to fetch data from any time series data provider. |
  [Configuration Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Configuration-Service.md)| This service is used to fetch some basic configurational information for the PoseidonNext. It is registered as one of the providers in app.module.ts in PoseidonNext Core. |
  [Creating a widget](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widget.md)| A widget is an Angular component that can be dynamically added, rearranged, configured, and saved into a view and loaded by Dashboards. |
  [Creating a widgets package](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Dashboards/Creating-a-widgets-package.md)| A widgets package is an Angular module that currently has two main purposes: * Declares widget components (so they are visible to other Angular modules) * Registers widgets with the Dashboards framework (so they are visible to dashboards creators) |
  [Date Time Formatter Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Date-Time-Formatter-Service.md)| This Service is used to specify the date and time format which is to be displayed to the end user for application specific use cases. The package is independently developed without having any dependency on angular5 or with any of its sister libraries. The primary dependency for this package is moment.js . |
  [Home and Favorites Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Home-and-Favorites-Service.md)| This is the default landing page/view in Poseidon. It contains a default icon which enables user to add favourite items on this screen |
  [Logging Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Logging-Service.md)| This service is used to log messages from client to a centralised repository. Messages are logged based upon the configuration. In configuration, we mention the level of logs that we want to save in sever. |
  [Message Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Message-Service.md)| This service is  used to show users different kinds of messages and toasters when there is need for showing information or asking for confirmation. |
 [Settings Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Settings-Service.md)| This service is used to manage various application and user-specific setting |
 [Statistics Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Date-Time-Formatter-Service.md)|  The primary purpose of this service is to collect information pertinent to various trackable events, duration a user spends on a certain page, and other metrices, which is stored in the backend. Backend may choose to post it further to Azure's Application Insights or in its own local repository. |
 [Tools Menu Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Tools-Menu-Service.md)| This service holds list of items that are displayed in the right-hand side menu in Poseidon. It is used by application developers in order to add custom commands in the tools menu. |
[Unit Of Measurement Service](https://github.com/kognifai/PoseidonNext-Framework/blob/master/SDK-documentation/Unit-Of-Measurement-Service.md)| The tools menu service holds list of items that are displayed in the right-hand side menu in Poseidon. It is used by application developers in order to add custom commands in the tools menu. |
           
# Attributions
Please see the attribution file [KognifaiPoseidonNext-Attribution](https://github.com/kognifai/PoseidonNext_Samples/blob/master/KognifaiPoseidonNext-Attribution.pdf)

# License
Read the copyright information and terms and conditions for Usage and Development of the software [here](https://github.com/kognifai/Kognifai/blob/master/License.md#copyright--year-kongsberg-digital-as).
