# Description

The Message Service is used to show users different types of messages and toasters when there is  a need for showing information or asking for a confirmation.

## Architecture

The messaging service has mainly two parts.
1. A message component which is used as a directive and placed  at the end of the app.component.html file. 
2. A message service which contains all the methods and configurations 

# Using the Message service


## Injecting

The message  service can be used by injecting it into a class or a ,component, just like any standard Angular service.
```javascript
import { MessageService } from './../service.message';
```
Next, we need to inject the service into the constructor function of the component.

```javascript
constructor(private messageservice: MessageService) { }
```

## Modal functions
The basic syntax of the modal functions are as follows.

`modalType(message: string, title?: string, okCallBack?: any, buttons?: IButtonConfig[])`

- ```message```  It is the content of the modal body. It is a mandatory argument.
- ```title:``` It is the caption of the modal. It is an optional parameter. If this argument is not provided the service will take a default value based on the type of modal.
- ```okCallBack:``` This is an optional parameter. It represents the callback function to be called when the user clicks the default **OK** button. 
- ```buttons:``` This is an optional parameter in the form of  array of type IButtonConfig. Typical structure of the IButtonConfig is as follows.
`IButtonConfig = [...
 {
    caption: string;
    callback: Function;
}
]
`
The buttons are passed to give custom buttons inside the modal body with corresponding callback functions. 

Four modal functions are provided in the package.
1. **info()**
2. **error()**
3. **warning()**
4. **success()**


## Modal Usecases
**Modal with only message :**

`this.messageservice.warning('I am a warning message');`


**Modal with message and a title :**

`this.messageservice.warning('I am a warning message', 'Warning');`

**Modal with message, title and a callback :**

`this.messageservice.warning('I am a warning message', 'Warning', callbackFunction);`

**Modal with message, title, callback and two custom buttons :**

```javascript
 this.messageservice.info('I am an information message', 'Information', '', [{
      caption: 'Yes',
      callback: () => {
        alert('I am a callback function');
      }
    },
    {
      caption: 'No',
      callback: callbackFunction
    }
    ]);
```
**Method call with message, no title, no default callback and custom buttons**

```javascript
 this.messageservice.error('I am an error message', '', '', [{
      caption: 'Yes',
      callback: () => {
        alert('I am a callback');
      }
     },
    ]);
```

## Toaster functions

The basic syntax of the notification/toaster  functions are as follows.

`toastType(message: string, title?: string, timeout?: number)`

- ```message```  It is the content of the toaster body. It is a mandatory argument.
- ```title``` It is the caption of the toaster . It is an optional parameter. If this argument is not provided the service takes a default value based on the type of toaster .
- ```timeout```  It is the timeout for the notification. It is an optional argument.If it is not provided the default timeout is set to 3000 ms.

Four toaster functions are provided in the package.
1. **toastInfo**
2. **toastError**
3. **toastWarning**
4. **toastSuccess**

## Toaster usecases
**Toaster with only message :**

```this.messageservice.toastSuccess('I am a success notification');```

**Toaster with toaster message and title:**

```this.messageservice.toastError('I am an error notification', 'Error');```

 **Toaster with toaster message title and overridden timeout**

```this.messageservice.toastWarning('I am a warning notification', 'Warning', 20000);```
