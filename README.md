
# Poseidon Next  [![Gitter Join the chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/kognifai/Lobby)

Poseidon Next is a subset of the kognifai platform which provides some of the following aspects:

- Quick web applications development through new projects scaffolding
- Reusable components for web applications
- Design system for a uniform look and feel
- Commonly needed APIs for applications and services
- Identity provider (applications, services and users registration and management)
- Commonly used applications
- Quick data adapters development through new projects scaffolding
- Registration tools for applications and data data adapters
- Integration with Galore
- Test pages to showcase usages of the provided services and packages

In this section, we talk about:

[Developers Getting Started page](#Developers-Getting-Started-page)

[Services](#Services)

[Widgets](#Widgets)

[Attributions](#Attributions)

## Developers Getting Started page
[Developers Getting Started page](Developers-Getting-Started.md)  provides information on prerequisites, how to globally install and host posedion dev host from NPM, how to install test modules, how to create a new Poseidon application, and how to use the Kognifai Design System.

## Services

[Services](https://github.com/kognifai/PoseidonNext-Framework/blob/master/Services.md) are library packages intented for specific set of tasks. Poseidon Next offers the following services that can be used in your application.

| Services| Link | Description
|-------------------------|---------------|--------
 App locations Service | [App locations Service](Public-documentation/SDK-reference/App-Locations-Service.md)|The Poseidon ecosystem integrates multiple applications each of whom has one or more locations (URLs) that can be accessed by the users. The App locations service provides hierarchical list of app locations. |
 Authentication Service | [Authentication Service](Public-documentation/SDK-reference/Authentication-Service.md)|This service is used in client applications for authenticating against an OIDC identity server. |
 Authorization Service| [Authorization Service](Public-documentation/SDK-reference/Authorization-Service.md)|This service helps in managing resources and its associated permissions. |
 Configuration Service | [Configuration Service](Public-documentation/SDK-reference/Configuration-Service.md)|This service is used to fetch some basic configurational information for the PoseidonNext.  |
 Cookie Service | [Cookie Service](Public-documentation/SDK-reference/Cookie-Service.md)|The cookie service provides methods to get, set and delete browser cookies.  |
 Data Adapter Service|[Data Adapter Service](Public-documentation/SDK-reference/Data-Adapter-Service.md)|A Data Adapter is an API, which implements a set of standard interfaces defined by Poseidon Next. |
 Data Context Service|[Data Context Service](Public-documentation/SDK-reference/Data-Context-Service.md)|A service for managing application contexts.|
 Date Time Formatter Service|[Date Time Formatter Service](Public-documentation/SDK-reference/Date-Time-Formatter-Service.md)|This service is used to specify the date and time format which is to be displayed to the end user |
  Home and Favorites Service|[Home and Favorites Service](Public-documentation/SDK-reference/Home-and-Favorites-Service.md)|This is the default landing page/view in Poseidon. |
Dropdown directive | [Dropdown Directive](Public-documentation/SDK-reference/Dropdown-directive.md)|The Poseidon dropdown directive toggles the visibility of a dropdown menu. It's used with Design System Dropdown component (kx-dropdown).|
 Logging Service | [Logging Service](Public-documentation/SDK-reference/Logging-Service.md)|This service is used to log messages from client to a centralised repository.  |
  Message Service | [Message Service](Public-documentation/SDK-reference/Message-Service.md)|This service is  used to show users different kinds of messages and toasters  |
 Navigation Service | [Navigation Service](Public-documentation/SDK-reference/Navigation-Service.md) | The Navigation Service holds list of items that are displayed in the left-hand sidebar in Poseidon. It is used by application developers in order to add custom commands in the navigation sidebar. |
 Settings Service | [Settings Service](Public-documentation/SDK-reference/Settings-Service.md)|This service is used to manage various applications and user-specific settings |The primary purpose of this service is to collect information pertinent to various trackable events |
 Sidebar Visibility Service | [Sidebar Visibility Service](Public-documentation/SDK-reference/Sidebar-Visibility-Service.md)|This service is used to make screen opaque and back to normal when showing and hiding menus.|
 Statistics Service |  [Statistics Service](Public-documentation/SDK-reference/Statistics-Service.md)|The primary purpose of this service is to collect information pertinent to various trackable events. |
 Tools Menu Service| [Tools Menu Service](Public-documentation/SDK-reference/Tools-Menu-Service.md)|The Tools menu service holds list of items that are displayed on the right-hand side menu in Poseidon.  |
Unit Of Measurement Service| [Unit Of Measurement Service](Public-documentation/SDK-reference/Unit-Of-Measurement-Service.md)|This service is used to convert units from one to another.   |

## Attributions
Please see the attribution file [Kognifai PoseidonNext-Attribution](KognifaiPoseidonNext-Attribution.pdf)

## License
Read the copyright information and terms and conditions for Usage and Development of the software [here](https://github.com/kognifai/Kognifai/blob/master/License.md#copyright--year-kongsberg-digital-as).
