# Description

The Logging Service is used to log messages from client to a centralised repository. Messages are logged based upon the configuration. In configuration we mention the level of logs that we want to save in sever.  E.g we may want to log only error and fatal messages. Logging service will also log the same message in client console. In server we would see this logs in logs folder. When running dev-host we will see this logs in \content\logSettings.json

# Using the Logging Service

## Injecting
The logging service can be used by injecting it into a class/component, just like any standard Angular service.
```javascript
export class LoggingComponent {
  constructor(private loggingService: LoggingService) {
  }

   ...
}
```

## Logging a message

We can log messages of type trace, debug, info, warn, error, fatal as below.
```typescript
trace(message: string, contextName?: string);
debug(message: string, contextName?: string);
info(message: string, contextName?: string);
warn(message: string, contextName?: string);
error(message: string, contextName?: string);
fatal(message: string, contextName?: string);
```
- ```message``` - the message that we want to log
- ```contextName``` - this can take component name, service name, [the context] which can be later used for grouping messages.


Example:
```javascript
this.loggingService.trace('this is a trace message');
this.loggingService.debug('this is a debug message');
this.loggingService.warn('this is an warning message');
this.loggingService.error('this is an error message');
this.loggingService.fatal('this is a fatal message');
this.loggingService.info('this is an info message');
```

## Configuration
The configuration required to setup logging service.
```javascript
export interface ILoggingConfig {
    logLevel: LogLevel;
    bufferingTime: number;
    endpoint: string;
}
```
- ```logLevel``` - the level after which we want to keep the messages in server. All messages will be logged in console regardless of this level.
- ```bufferingTime``` - how often we would like to keep posting the messages to server.
- ```endpoint``` - the endpoint where server accepts log messages.

Example:
```javascript
logging:{level:"Error",bufferingTime:"300"}
```