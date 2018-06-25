# Sample usage

Below is a sample using the logging service.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { LoggingTestComponent } from './loggingTest.component';
import { LoggingService } from '@kognifai/poseidon-ng-loggingservice';
import { LogLevel } from '@kognifai/poseidon-loggingservice';
import { HttpClientModule } from '@angular/common/http';
import { ConfigurationService } from '@kognifai/poseidon-ng-configurationservice';

const routes: Routes = [
  { path: '', component: LoggingTestComponent }
];

@NgModule({
  declarations: [
    LoggingTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    HttpClientModule,
    RouterModule.forChild(routes)
  ],
  exports: [LoggingTestComponent],
  providers: [LoggingService, ConfigurationService]
})
export class LoggingTestModule { }

```

And, its component follows like as shown below.

```ts
import { Component, OnInit, Input } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { IHttpProxy, ILoggingService, Logger, ILoggingConfig, LogLevel } from '@kognifai/poseidon-loggingservice';
import { LoggingService } from '@kognifai/poseidon-ng-loggingservice';

@Component({
  selector: 'app-logging-service-test-page',
  templateUrl: './loggingTest.component.html'
})
export class LoggingTestComponent {
   levelInfo: LogLevel = LogLevel.Info;
  constructor(private loggingService: LoggingService) { }

  logTrace() {
    this.loggingService.trace('this is a trace message');
  }

  logDebug() {
    this.loggingService.debug('this is a debug message');
  }

  logWarn() {
    this.loggingService.warn('this is an info message');
  }

  logError() {
    this.loggingService.error('this is an error message');
  }

  logFatal() {
    this.loggingService.fatal('this is a fatal message');
  }

  logInfo(level: LogLevel) {
    this.loggingService.info('this is an info message');
  }
}

```