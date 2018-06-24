# Description

**Statistics service** is one of the service provided by **Poseidon Application Framework**.  The primary purpose of this service is to collect information pertinent to various trackable **events**, **duration**. A user spends time on a certain page, and other **metrices** which is stored in backend. Backend may choose to post it further to Azure's Application Insights or in its own local repository.

## Import

```typescript
import { StatisticsService } from '@kognifai/poseidon-ng-statisticsservice';
import { IStatisticRecord, StatisticOperationTypes } from '@kognifai/poseidon-statisticsservice';
```
## Injection
```typescript
constructor(private statisticsService: StatisticsService) { }
```


This service collects data which is  **IStatisticRecord** type.

```typescript
export interface IStatisticRecord {
    operationType: StatisticOperationTypes;
    recordName: string;
    recordValue: string;
}
```
**StatisticOperationTypes** is an **enum**.

```typescript
export enum StatisticOperationTypes {
    TrackEvent = 0,
    TrackDuration = 1,
    TrackMetric = 2
}
```
This service exposes the below method which facilitates the user to store records.

```typescript
export interface IStatisticsCollectionService  {
    addStatisticRecord(record: IStatisticRecord): Promise<void>;
}
``` 
A simple usage of **Statistics Service**.

```typescript
export class ExampleComponent{

  constructor(private statisticsService: StatisticsService) { }

  recordEvent(): void {
    const record: IStatisticRecord = {
      operationType: StatisticOperationTypes.TrackEvent,
      recordName: 'Track Event name',
      recordValue : 'Track record value'
    };
    this.statisticsService.addStatisticRecord(record);
  }

  recordDuration(): void {
    const record: IStatisticRecord = {
      operationType: StatisticOperationTypes.TrackDuration,
      recordName: 'Track record1 name',
      recordValue : 'Track record1 value'
    };
    this.statisticsService.addStatisticRecord(record);
  }
}
```
