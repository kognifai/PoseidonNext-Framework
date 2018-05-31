# Description

Configuration service is used to fetch some basic configurational information for the PoseidonNext.  It is registered as one of the providers in **app.module.ts** in **PoseidonNext Core**.  Some of the information that can fetched through this service are **authenticationEndpoint**, **logging**, **date and time formatting**, etc.,  We can even customize and add new properties, which we would like to have as configurable.


## Injection

To use the configuration service it has to be imported as follows

```typescript
import { ConfigurationService } from '@kognifai/poseidon-configuration';
```

Injection is as below:

```typescript
constructor(private configurationService: ConfigurationService<IConfiguration>) {}
```

This service exposes the following methods
```typescript
export class ConfigurationService<T> {
    public load(): Promise<void> { }
    public get config(): T {}
}
```
The **load** method is used to read the configuration information, which reads the **"config.json"** present in **PosiedonNext Core**.  

```typescript
public load(): Promise<void> { }
```
The configuration information can be accessed through the **config** method.
```typescript
public get config(): T {}
```
Currently, configuration service revolves around **IConfiguration** interface.  This interface can be modified to suit our application's needs.
```typescript
export interface IConfiguration {
    authenticationEndpoint?: string;
    logging?: ILoggingConfig;
    formatting?: IDateTimeFormatterConfig;
}
```
The above **IConfiguration** interface in itself is a package and has to be imported:
```typescript
import { IConfiguration } from '@kognifai/poseidon-configurationinterface';
```

### Example Usage of Configuration Service:

```typescript
import { ConfigurationService } from '@kognifai/poseidon-configuration';
import { IConfiguration } from '@kognifai/poseidon-configurationinterface';

@Injectable()
export class ExampleComponent  {
    constructor(private configurationService: ConfigurationService<IConfiguration>) { }

    loadConfiguration(): void {
        this.configurationService.load().then(() => {
            console.log("Configuration successfully loaded");
        }).catch((error) => {
            console.log("Unable to load configuration: " + error);
        });
    }

    fetchConfiguration(): void {
        const configuration = this.configurationService.config();
        console.log("Authentication Endpoint: " + configuration.authenticationEndpoint);
        console.log("Logging: " + configuration.logging);
        console.log("Formatting: " + configuration.formatting);
    }

}
```

## Customizing

In order to customize the configuration, we need to add our custom properties to **config.json**.  This file is located at the root level of ```PoseidenNext's Core``` folder.  The default **config.json** is as below.

```json
{
    "authenticationEndpoint": "http://localhost:8080/Security/auth",
    "logging": { 
        "logLevel" : 4,
        "bufferingTime" : 5000,
        "endpoint": "bulkEntry"
    },
    "formatting": {
        "dateFormat": "MMMM dd YYYY",
        "timeFormat": "HH:mm:ss",
        "formatDate": {
            "format": "dd/MM/yyyy",
            "long" : "dddd, d MMMM yyyy",
            "longForMoment" : "dddd, D MMMM YYYY",
            "short" : "dd/MM/yyyy",
            "shortForMoment" : "DD/MM/YYYY" 
        },
        "formatTime": { 
            "format": "HH:mm:ss",
            "long": "HH:mm:ss", 
            "short": "HH:mm" 
        },
        "formatNumber": { 
            "decimalSeparator": ".", 
            "groupSeparator": " ", 
            "decimalDigits": 2, 
            "decimalGorup": 3, 
            "leadingZeros": 1 
        },
        "culture": "en"
    }
}
```
To demonstrate customization, we add **"apiEndpoint"** as one of the new property to the above **config.json**. 

```json
{
    "authenticationEndpoint": "http://localhost:8080/Security/auth",
    "apiEndpoint": "http://localhost:8080/",
    "logging": { 
        "logLevel" : 4,
        "bufferingTime" : 5000,
        "endpoint": "bulkEntry"
    },
    "formatting": {
        "dateFormat": "MMMM dd YYYY",
        "timeFormat": "HH:mm:ss",
        "formatDate": {
            "format": "dd/MM/yyyy",
            "long" : "dddd, d MMMM yyyy",
            "longForMoment" : "dddd, D MMMM YYYY",
            "short" : "dd/MM/yyyy",
            "shortForMoment" : "DD/MM/YYYY" 
        },
        "formatTime": { 
            "format": "HH:mm:ss",
            "long": "HH:mm:ss", 
            "short": "HH:mm" 
        },
        "formatNumber": { 
            "decimalSeparator": ".", 
            "groupSeparator": " ", 
            "decimalDigits": 2, 
            "decimalGorup": 3, 
            "leadingZeros": 1 
        },
        "culture": "en"
    }
}
```
We extend the **IConfiguration** Interface.
```typescript
import { IConfiguration } from '@kognifai/poseidon-configurationinterface';

export interface IExtendedConfiguration extends IConfiguration {
  apiEndpoint: string;
}
```
The above extended interface can now be used with **ConfigurationService**.   The code snippet below demonstrates it.

```typescript
import { ConfigurationService } from '@kognifai/poseidon-configuration';

@Injectable()
export class ModifiedExampleComponent  {
    constructor(private configurationService: ConfigurationService<IExtendedConfiguration>) { }

    loadConfiguration(): void {
        this.configurationService.load().then(() => {
            console.log("Configuration successfully loaded");
        }).catch((error) => {
            console.log("Unable to load configuration: " + error);
        });
    }

    fetchConfiguration(): void {
        const configuration = this.configurationService.config();
        console.log("Authentication Endpoint: " + configuration.authenticationEndpoint);
        console.log("Logging: " + configuration.logging);
        console.log("Formatting: " + configuration.formatting);
        
        //The newly added apiEndpoint property.
        console.log("API Endpoint:  " + configuration.apiEndpoint);

    }
}
```
