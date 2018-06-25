# Sample usage

Below are the usages of Settings service test page.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';

import { SettingsTestComponent } from './settingsTest.component';
import { SettingsService } from '@kognifai/poseidon-ng-settingsservice';
import { ConfigurationService } from '@kognifai/poseidon-ng-configurationservice';

const routes: Routes = [
  { path: '', component: SettingsTestComponent }
];

@NgModule({
  declarations: [
    SettingsTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  providers: [ConfigurationService, SettingsService],
  exports: [SettingsTestComponent]
})
export class SettingsTestModule { }
```
And its associated component looks like

```ts
import { Component } from '@angular/core';

import * as _ from 'lodash';
import { v1 as uuid } from 'uuid';

import { SettingsService } from '@kognifai/poseidon-ng-settingsservice';
import { ISettingType, ISetting } from '@kognifai/poseidon-settingsservice';

@Component({
    selector: 'app-settings-service-test-page',
    templateUrl: './settingsTest.component.html',
    styleUrls: ['./settingsTest.component.css']
})
export class SettingsTestComponent {
    settingTypeName = 'my-type';
    setType = 'my-type';
    setValue = 'my-value';
    setIsUserSpecific = false;
    getTypeName = 'my-type';
    getSettingsResult: ISetting<any>[] = [];
    removeId = '';
    removeTypeName = 'my-type';

    notificationText = '';
    notificationClass = 'kx-notification--success';

    constructor(
        private settingsService: SettingsService
    ) { }

    private notifyOk(text: string) {
        this.notificationClass = 'kx-notification--success';
        this.notificationText = text;
    }

    private notifyError(text: string) {
        this.notificationClass = 'kx-notification--danger';
        this.notificationText = text;
    }

    private notifyWarning(text: string) {
        this.notificationClass = 'kx-notification--warning ';
        this.notificationText = text;
    }

    addSettingType() {
        if (this.settingTypeName) {
            this.settingsService.getType(this.settingTypeName).then((settingType) => {
                if (settingType) {
                    this.notifyWarning('Setting type already exists.');
                } else {
                    this.settingsService.addType({
                        id: uuid(),
                        isSingular: false,
                        moduleId: uuid(),
                        name: this.settingTypeName
                    }).then(() => { this.notifyOk('Added setting type: ' + this.settingTypeName); })
                        .catch((error) => { this.notifyError('Error: ' + error); });
                }
            }).catch((error) => { this.notifyError('Error: ' + error); });
        }
    }

    getSettingType() {
        if (this.settingTypeName) {
            this.settingsService.getType(this.settingTypeName)
                .then((settingType) => {
                    if (settingType) {
                        this.notifyOk('Got setting type: ' + settingType.name + ' with id: ' + settingType.id);
                    } else {
                        this.notifyWarning('No setting type found with name: ' + this.settingTypeName);
                    }
                }).catch((error) => { this.notifyError('Error: ' + error); });
        }
    }

    setSetting() {
        if (this.setType && this.setValue) {
            this.settingsService.getType(this.setType).then((settingType) => {
                if (!settingType) { this.notifyWarning('Setting type not found.'); return; }
                const setting = this.settingsService.create(settingType, this.setValue, this.setIsUserSpecific);
                this.settingsService.set([setting]).then(() => {
                    this.notifyOk('Successfully set setting value.');
                }).catch((error) => { this.notifyError('Error: ' + error); });
            }).catch((error) => { this.notifyError('Error: ' + error); });
        }
    }

    getSettings() {
        this.getSettingsResult = [];
        if (this.getTypeName) {
            this.settingsService.getType(this.getTypeName).then((settingType) => {
                if (!settingType) { this.notifyWarning('Setting type not found.'); return; }
                this.settingsService.get(settingType).then((settings) => {
                    this.getSettingsResult = settings;
                    if (settings && settings.length > 0) {
                        this.notifyOk('Got settings for type: ' + settingType.name);
                    } else {
                        this.notifyWarning('No settings found for type: ' + settingType.name);
                    }
                }).catch((error) => { this.notifyError('Error: ' + error); });
            }).catch((error) => { this.notifyError('Error: ' + error); });
        }
    }

    removeSetting() {
        if (this.removeId && this.removeTypeName) {
            this.settingsService.getType(this.removeTypeName).then((settingType) => {
                if (!settingType) { this.notifyWarning('Setting type not found.'); return; }
                this.settingsService.get(settingType).then((settings) => {
                    const found = _.find(settings, (s: ISetting<any>) => s.identifier === this.removeId);
                    if (!found) { this.notifyWarning('Setting not found.'); return; }
                    this.settingsService.remove(found).then(() => {
                        this.notifyOk('Setting removed.');
                    }).catch((error) => { this.notifyError('Error: ' + error); });
                }).catch((error) => { this.notifyError('Error: ' + error); });
            }).catch((error) => { this.notifyError('Error: ' + error); });
        }
    }
}
```