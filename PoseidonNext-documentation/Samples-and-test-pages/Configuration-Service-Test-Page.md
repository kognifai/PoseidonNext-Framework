# Sample usage

Below is a sample using the configuration service.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { ConfigComponent } from './config.component';
import { ConfigurationService } from '@kognifai/poseidon-configuration';

const routes: Routes = [
  { path: '', component: ConfigComponent }
];

@NgModule({
  declarations: [
    ConfigComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  exports: [ConfigComponent],
  providers: [ConfigurationService],
  bootstrap: []
})
export class ConfigurationModule { }
```

And its component looks like

```ts
import { Component } from '@angular/core';
import { ConfigurationService } from '@kognifai/poseidon-configuration';
import { IConfiguration } from '@kognifai/poseidon-configurationinterface';

@Component({
  selector: 'app-configuration-service-test-page',
  templateUrl: './config.component.html',
  styleUrls: ['./config.component.scss']
})
export class ConfigComponent {
  authenticationEndpoint: string;
  dateFormat: string;
  timeFormat: string;
  logLevel: number;
  logInterval: number;

  constructor(
    private configurationService: ConfigurationService<IConfiguration>
  ) {
    this.dateFormat = this.configurationService.config.formatting.dateFormat;
    this.timeFormat = this.configurationService.config.formatting.timeFormat;
    this.logLevel = this.configurationService.config.logging.logLevel;
    this.logInterval = this.configurationService.config.logging.bufferingTime;
    this.authenticationEndpoint = this.configurationService.config.authenticationEndpoint;
  }
}

```