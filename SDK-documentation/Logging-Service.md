# Description

Logging Service is used to log messages from client to a centralised repository. Messages are logged based upon the configuration. In the configuration, we mention the level of logs that we want to save in the server.  For example, we may want to log only errors and fatal messages. Logging service also logs the same message in the client console. In the server, we would see this logs in the logs folder. When running dev-host we see this logs in \content\logSettings.json

# Using the Logging Service

## Injecting

The logging service can be used by injecting it into a class or a component, just like any standard Angular service.
```javascript
export class LoggingComponent {
  constructor(private loggingService: LoggingService) {
  }

   ...
}
```

## Logging a message

We can log the following message types of: trace, debug, info, warn, error, and fatal:

```typescript
trace(message: string, contextName?: string);
debug(message: string, contextName?: string);
info(message: string, contextName?: string);
warn(message: string, contextName?: string);
error(message: string, contextName?: string);
fatal(message: string, contextName?: string);
```
- ```message``` - message that we want to log
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

The configuration require to setup logging service.

```javascript
export interface ILoggingConfig {
    logLevel: LogLevel;
    bufferingTime: number;
    endpoint: string;
}
```
- ```logLevel``` - the level after which we want to keep the messages in the server. All messages will be logged in console regardless of this level.
- ```bufferingTime``` - how often we would like to keep posting the messages to server.
- ```endpoint``` - the endpoint where the server accepts the log messages.

Example:
```javascript
logging:{level:"Error",bufferingTime:"300"}
```
