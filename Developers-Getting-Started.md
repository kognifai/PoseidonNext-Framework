 ```
This is a developer release of Poseidon Next.
```
# Prerequisites [![Gitter Join the chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/kognifai/Lobby)

### 1. Install NodeJs 8 or latest
Download and install the [NodeJs 8 or latest](https://nodejs.org/) version from its official web site.

### 2. Configure NPM to use KDI JFrog

If you are using KDI registry and encountering errors, We recommend you to generate a new API key in JFrog and set it up in npm, see [Configure NPM to use KDI JFrog](https://kognifai.visualstudio.com/Kognifai%20Core/_wiki/wikis/PoseidonNext.wiki?wikiVersion=GBwikiMaster&pagePath=%2FContributors%2FDeveloper%20guides%2FJFrog%3A%20Configure%20NPM%20to%20use%20KDI%20JFrog) on how to generate a new API key in JFrog.

> Note: Run this command ```npm config get registry``` to check the version of npm registry.

### 3. Run commands in Command Prompt or Windows PowerShell
In any version of Windows, open Command Prompt by doing the following steps:

 1. Press **WIN+R** 

 2. In the Run window, type **cmd** and press **Enter** to open the Command Prompt.

In any version of Windows, open [Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/setup/starting-windows-powershell?view=powershell-6) to install the **Poseidon-dev-host** and create your first web application.


# Installing the Poseidon Next

### 1. Install the Poseidon Dev Host ###
Run the following command to globally install the **poseidon-dev-host** from npm.
```powershell
npm install @kognifai/poseidon-dev-host@latest -g
```
>Note: -g indicates that the ```poseidon-dev-host@latest``` is installed globally.

### 2.	Host the Poseidon-dev-host ###
After poseidon-dev-host 2.0 installation, you can host it on your computer ( It may act as a server, a client, or both) by running the following command:

```powershell
poseidon-dev-host
```
This hosts the ioc container such as: 
- Creates ApplicationSettingsRouter files
- Injects router fields
- Loads application manifests

The console displays a message that “Listening at http://localhost:8080.” At this stage, do not copy the URL and open it on any web browser, instead, proceed with the [next installation step](#Create-a-directory). 

> Note: Press **Ctrl+C** and type **Y** to stop the dev-host and proceed with the [next installation step](#Create-a-directory).

###  3.	Create a directory ### 
Once you installed the Poseidon-dev-host, the next step is to create an empty directory (i.e. applications) in your local folder, execute the following command to create the directory:

```powershell
mkdir C:\kognifai\applications
```

Execute the following command to change the directory location to C:\kognifai\applications:

```powershell
cd C:\kognifai\applications
```


###  4.	Install the Poseidon Next applications ### 

You can use **npm** to install the Poseidon Next applications, execute the following commands to load and host these applications:
```powershell
npm install @kognifai/poseidon-home@latest
npm install @kognifai/poseidon-user-profile@latest
npm install @kognifai/poseidon-user-administration@latest
npm install @kognifai/poseidon-test-pages@latest
```
- poseidon-home - This is the home page for the sample applications.
- poseidon-user-profile - This displays the user profile information which can be updated.
- poseidon-user-administration - This is a user management application for the identity provider.
- poseidon-test-page -  - These are the sample pages which showcase different services and integrations in PoseidonNext.

Set the C:\kognifai\applications as a default directory to load your applications.

```powershell
poseidon-dev-host --applications "C:\kognifai\applications"
```
Where the --applications parameter specifies the directory in which poseidon-dev-host must look for applications (including subfolder /node_modules@kognifai). 

A directory contains the following files:

- Content files (html pages, scripts, styles, assets, etc) along with application 
- Manifest file (app.manifest.json). 

When you execute the following command, the host must output a message listing all the manifests of the applications, similar to:

```
Hosting applications from C:\kognifai\applications
Loading application manifests
	Home
	Test Pages
	User Administration
	User Profile
```
Open a browser at http://localhost:8080 in order to view the Poseidon platform. The host comes with a developer-friendly security solution. 

- Type any username and password to log in. 

> Note: You can create your own username and password. 

The following Poseidon platform is displayed on the browser along with the left-hand side navigation.

![image.png](.%20images/Poseidon-Applications.png)

> Note: Remember to stop the **poseidon-dev-host** if it is currently running. Press **Ctrl+C** and type **Y** to stop the dev-host and proceed with Creating new application on Poseidon Next.)



# Creating new application on Poseidon Next



### 1.	Install Yeoman App ###

For the first time users, it is recommended to install Yeoman app (if you’ve not yet installed) by executing the following command:
```powershell
npm install -g yo
```

### 2.	Install the Yeoman generator ###
Yeoman generator can be used in the Kognifai applications. For more information on Yeoman generator, See [Yeoman's Getting Started page](http://yeoman.io/learning/index.html)

To use the Yemoan generator, execute the following command from npm:
  ```powershell
npm install -g @kognifai/generator-poseidon@latest
```
In the Kognifai applications folder, use the following Poseidon generator.
```powershell
cd C:\kognifai\applications
yo @kognifai/poseidon:application
```
For the **Your Application name**, enter the application name which must be same as the folder name (i.e. my-first-app) and press **Enter**.

If you want to use **port 4300** as the **Development port of the application**, press **Enter**.

 After loading all the generator packages, set the default location as your application’s directory location as following:
 ```powershell
cd C:\kognifai\applications\my-first-app
```
Start your application from npm:
 ```powershell
npm start
```
In the Server, to restart **poseidon-dev-host** and reload your first application on your browser, execute the following command:
 ```powershell
poseidon-dev-host --applications "C:\kognifai\applications"
```
Open a browser at http://localhost:8080 in order to view the Poseidon platform which displays your first application.

![image.png](.%20images/my-first-app.jpg)




# Editing the source code in any code editor

You can use VS Code or any one of your favorite IDE/code editor to edit the source code:
```powershell
code .
```
Any code changes you make on application pages, scripts and styles are automatically reflected in the browser (live reload).
You can use the following NPM scripts to start, build, lint, and test:
```powershell
npm start
npm run build
npm run lint
npm run test
```



# Using the Kognifai Design System

Kognifai Design System is a collection of design patterns, components, and guidelines for creating unified and coherent UI in the Kognifai ecosystem.

It contains a set of easy-to-use HTML/CSS components. It does not include JavaScript since we aim to be versatile and technology agnostic. Use it together with any JS framework.

To read the documentation head over to [https://designsystem.kognif.ai/](https://designsystem.kognif.ai/)

# Next Step

Find [Services](Services.md) to consume the available service in your applications.

