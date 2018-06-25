# Sample usage

Below is a sample using the date time formatting service.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { DatetimeformattingservicetestComponent } from './Datetimeformattingservicetest.component';
import { DatetimeFormattingService } from '@kognifai/poseidon-ng-datetimeformattingservice';

const routes: Routes = [
  { path: '', component: DatetimeformattingservicetestComponent }
];

@NgModule({
  declarations: [
    DatetimeformattingservicetestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  providers: [DatetimeFormattingService],
  exports: [DatetimeformattingservicetestComponent],
  bootstrap: []
})
export class DatetimeFormattingServiceTestModule { }
```
And its component looks like this

```ts
import { Component } from '@angular/core';
import { DatetimeFormattingService } from '@kognifai/poseidon-ng-datetimeformattingservice';

@Component({
  selector: 'app-datetimeformatting-service-test-page',
  templateUrl: './Datetimeformattingservicetest.component.html'
})
export class DatetimeformattingservicetestComponent {
  locale: string;
  dateFormat: string;
  dateTimeFormat: string;
  currentFormatedDate: string;

  constructor(private dateTimeFormatingService: DatetimeFormattingService) {
  }

  getDateFormat() {
      this.dateFormat = this.dateTimeFormatingService.getDateFormat();
  }

  getDateTimeFormat() {
      this.dateTimeFormat = this.dateTimeFormatingService.getDateTimeFormat();
  }

  getCurrentFormatedDate() {
      const now = new Date();
      this.currentFormatedDate = this.dateTimeFormatingService.formatDateTime(now);
  }

  getLocale() {
      this.locale = this.dateTimeFormatingService.getlocale();
  }

  setLocale() {
      this.dateTimeFormatingService.setLocale('bg');
      this.locale = '';
      this.dateFormat = '';
      this.dateTimeFormat = '';
      this.currentFormatedDate = '';
  }
}
```

