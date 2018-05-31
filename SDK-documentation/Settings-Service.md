# Description
The settings service is used to manage various application and user-specific setting. Settings are organized by setting types. The service allows storing single or multiple settings for a setting type, depending on the setting type.

The content (Value) of a setting is not specified, it can be anything (e.g. json, xml, plain text) and the framework is not interested in it. Understanding the value is a responsibility of the application (module) which owns the setting.

![image.png](.attachments/image-bd34a339-adec-41c4-812e-f6b475db0de5.png)

# Using the Settings Service

## Injecting
The setting service can be used by injecting it into a class/component, just like any standard Angular service.
```javascript
export class SettingsServiceTestPageComponent {
   constructor(private settingsService: SettingsService) {
   }

   ...
}
```

## Add a setting type
```javascript
addType(type: ISettingType): Promise<void>
```

Example:
```javascript
this.settingsService.addType({
      id: uuid(),
      isSingular: false,
      moduleId: 'my-module-id',
      name: 'My setting type'    
    })
    .then(() => {  console.log('Added setting type.'); })
    .catch((error) => { console.error('Error: ' + error); });
```

- ```id``` - unique identifier of the settings type
- ```isSingular``` - if ```true```, only allow one setting value to be inserted for the setting type
- ```moduleId``` - the identifier of the owner module (application)
- ```name``` - the name of the setting type

## Get a setting type
```
getType(name: string, moduleId?: string): Promise<ISettingType> 
```

Example:
```javascript
this.settingsService.getType('My setting type', 'my-module-id')
    .then((settingType) => {
        if (settingType) {
            console.log('Got setting type: ' + settingType.name + ' with id: ' + settingType.id);
        } else {
            console.error('No setting type found with name: My setting type');
        }
    })
    .catch((error) => { console.error(('Error: ' + error); });
```
- ```name``` - the name of the setting type
- ```moduleId``` - the identifier of the owner module (application). Optional.

## Set setting values
```javascript
set<T>(settings: Array<ISetting<T>>): Promise<Array<ISetting<T>>>
```

Example:
```javascript
const setting = this.settingsService.create(settingType, 'My setting value here', false);
this.settingsService.set([setting])
.then(() => {
    console.log('Successfully set setting value.');
})
.catch((error) => { console.error('Error: ' + error); });
```

- ```settings``` - array of ```ISetting``` objects, can be created using ```settingsService.create(...)``` or manually.
The ```ISetting``` interface has the following members;
- ```identifier``` - unique identifier of the setting
- ```value``` - the value of the setting
- ```typeId``` - the identifier of the setting type
- ```isUserSpecific``` - if ```true```, the setting is considered specific for the user who creates it, otherwise it is common for all users
- ```created``` - time of creation (no need to supply when writing)
- ```updated``` - time of last update (no need to supply when writing)


## Get setting values
```javascript
get<T>(type: ISettingType): Promise<Array<ISetting<T>>>
```
Example:
```javascript
this.settingsService.get(settingType)
.then((settings) => {
    if (settings && settings.length > 0) {
        console.log('Got ' + settings.length + ' settings for type: ' + settingType.name);
    } else {
        console.error('No settings found for type: ' + settingType.name);
    }
})
.catch((error) => { console.error('Error: ' + error); });
```

## Remove setting values
```javascript
remove<T>(setting: ISetting<T>): Promise<void>
```

Example:
```javascript
const found = _.find(settings, (s: ISetting<any>) => s.identifier === 'my-setting-identifier');
if (found) {     
    this.settingsService.remove(found)
    .then(() => {
        console.log('Setting removed.');
    })
    .catch((error) => { console.error('Error: ' + error); });
}
```
This example demonstrates removing a setting by finding the setting object in an array of previously loaded settings.
Alternatively, you can construct your own ISetting object and pass it to the ```.remove``` method. The only required field is the identifier.

