# Description

The Date time formatter service is used to specify the date and time format which is to be displayed to the end user   for application specific use cases. The package is independently developed without having any dependency on angular5 or with any of its sister libraries. The primary dependency for this package is moment.js .

# Using the date time formatter service

## Injecting into a component
The package can be injected into the requiring component in the following manner.
1. First import the package into the component
2. Then inside the constructor function of the component inject it as it is done for any service.

```typescript
constructor(private dateTimeService: DateTimeFormatterService) {}
```

Once the service is injected into the component then we can access various functions inside it by referring to the local placeholder of the service. The below example shows how to invoke a function from inside a component.

```javascript
console.log(this.dateTimeService.getlocale());
```

## Default formats

Below are the default values for various date time formats used in the package.
- **dateFormat** :  "MMMM dd YYYY"
- **timeFormat** : "HH:mm:ss"
- **formatDate-long**  :  "LLLL"
- **formatDate-longForMoment** : "LLLL"
- **formatDate-short** : "l"
- **formatDate-shortForMoment** : "l"
- **formatTime-long** : "LTS"
- **formatTime-short** : "LT"

## API

**formatDateTime()**

This method is used to format the date times . 

```typescript
formatDateTime(dateTime: Date, onlyDate: boolean = false, onlyTime: boolean = false, showMilliseconds: boolean = false)
```

It formats the date time for the date passed as the first parameter to it. The other parameters are boolean values which if passed will give the requested result.  By default all  parameters except the first parameter are given default value as false. So if we pass only the first parameter it will return the formatted value according to momentjs specifications.

**getDateTimeFormatForMoment()** 

This method is used to get the current date time format of the application.

```typescript
getDateTimeFormatForMoment(onlyDate: boolean = false, onlyTime: boolean = false, showMilliseconds: boolean = false);
````
The function can be directly invoked without passing any parameter in which case it will return the entire date and time format as a string. Or by passing specific parameters we can get the only date format or time format.

**formatDateTimeString()**

```typescript
formatDateTimeString(dateTimeString: string, onlyDate: boolean = false, onlyTime: boolean = false, showMilliseconds: boolean = false): string
```

**format()**

It is used to format the date time string to a desired format. The desired format is passed as the second parameter.

```typescript
format(dateTimeString: string, formatString: string): string;
```

**getDateFormat()**

This method returns the Date format as a string.

**getTimeFormat()**

It returns the timeFormat as a string.

**getlocale()**

It returns the locale as a string.

**setDateFormat()**

It sets the date format as passed in the parameter as a string.

```typescript
setDateFormat(format: string);
```

**setTimeFormat()**

It sets the time format as passed in the parameter as a string.

```typescript
setTimeFormat(format: string);
```

**setLocale()**

It sets the Locale as passed in the parameter as a string.

```typescript
setLocale(format: string);
```

**formatShortDate()**

It formats the short date according to the parameter passed to the function.

```typescript
formatShortDate(dateTime: Date): string
```

**formatShortTime()**

It formats the short Time according to the parameter passed to the function.

```typescript
formatShortTime(dateTime: Date): string;
```

**formatShortDateTime()**

It formats the short Date-Time according to the parameter passed to the function.

```typescript
formatShortTime(dateTime: Date): string;
```

**formatLongDate()**

It formats the long date according to the parameter passed to the function.

```typescript
formatLongDate(dateTime: Date): string;
```

**formatLongTime()**

It formats the long time according to the parameter passed to the function.

```typescript
formatLongTime(dateTime: Date): string;
```

**formatLongDateTime()**

It formats the long date-time according to the parameter passed to the function.

```typescript
formatLongDateTime(dateTime: Date): string;
```

**getShortDateFormat()**

It returns the short date format as a string.

**getShortTimeFormat()**

It returns the short time format as a string.

**getLongDateFormat()**

It returns the long date format as a string.

**getLongTimeFormat()**

It returns the long time format as a string.

**getShortDateTimeFormat()**

This function returns short date and time format combined as a string.

**getLongDateTimeFormat()**

This function returns long date and time format combined as a string.

 










