# Sample usage

Below you can see a sample using the statistics service.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { StatisticsService } from '@kognifai/poseidon-ng-statisticsservice';


import { StatisticsComponent } from './statistics.component';
import { HttpClientModule } from '@angular/common/http';
import { ConfigurationService } from '@kognifai/poseidon-ng-configurationservice';

const routes: Routes = [
  { path: '', component: StatisticsComponent }
];

@NgModule({
  declarations: [
    StatisticsComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    HttpClientModule,
    RouterModule.forChild(routes)
  ],
  providers: [StatisticsService, ConfigurationService],
  exports: [StatisticsComponent],
  bootstrap: []
})
export class StatisticsModule { }
```

And, its component follows like as shown below.

```ts
import { Component, OnInit } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { StatisticsService } from '@kognifai/poseidon-ng-statisticsservice';
import { IStatisticRecord, StatisticOperationTypes } from '@kognifai/poseidon-statisticsservice';

@Component({
    selector: 'app-statistics-service-test-page',
    templateUrl: './statistics.component.html'
})
export class StatisticsComponent {

  constructor(private statisticsService: StatisticsService) { }

  clickMe() {
    const record: IStatisticRecord = {
      operationType: StatisticOperationTypes.TrackEvent,
      recordName: 'Track Event name',
      recordValue : 'Track record value'
    };
    this.statisticsService.addStatisticRecord(record);
  }

  clickMe1() {
    const record: IStatisticRecord = {
      operationType: StatisticOperationTypes.TrackDuration,
      recordName: 'Track record1 name',
      recordValue : 'Track record1 value'
    };
    this.statisticsService.addStatisticRecord(record);
  }
}
```
