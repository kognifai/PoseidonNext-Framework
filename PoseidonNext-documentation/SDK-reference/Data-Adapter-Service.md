## Description

**Data Adapter** is an API, which implements a set of standard interfaces defined by **Poseidon Next**.  The data adapters are meant to give a simplified and unified way of accessing different resources like assets, timeseries and events.  Not all the API interfaces can be implemented by all resource providers, so when registered data adapters lists a set of capabilities, which signals which set of the API interfaces have been implemented.  All data adapters have to be registered with the **Poseidon Next API,** so that they are made available to the application.

**Data adapters**, like the Poseidon Next applications, are intended to be run on different endpoints. Hence, their registration and location is necessary.  A registration tool is included with Poseidon Next.  Poseidon Next provides a generator to scaffold an new ASP.NET Core API Data Adapter project.

## Install
```typescript
// Angular wrapper
npm install @kognifai/poseidon-ng-dataadaptersservice
npm install @kognifai/poseidon-ng-dataadapterslocationsservice

// dependencies include the below packages 
npm install @kognifai/poseidon-dataadaptersservice
npm install @kognifai/poseidon-dataadapterslocationsservice
```

## Usage
**Poseidon Next** gives us 2 services relating to Data Adapter.
1) DataAdaptersLocationsService - Fetches all the registered data adapters. 
2) DataAdaptersFactoryService - Service which includes the standard API interfaces. 

```typescript
import { DataAdaptersFactoryService, HttpClientHelperService } from '@kognifai/poseidon-ng-dataadaptersservice';
import { DataAdaptersLocationsService } from '@kognifai/poseidon-ng-dataadapterslocationsservice';
```
## Injection
```typescript
constructor(private dataAdaptersFactoryService: DataAdaptersFactoryService, 
            private dataAdaptersLocationService: DataAdaptersLocationsService) { }
```
## Below is a simple usage example

```typescript
import { Component, AfterViewInit } from '@angular/core';
import { DataAdaptersFactoryService } from '@kognifai/poseidon-ng-dataadaptersservice';
import { DataAdaptersLocationsService } from '@kognifai/poseidon-ng-dataadapterslocationsservice';
import { IDataAdaptersLocations } from '@kognifai/poseidon-dataadapterslocationsservice';

import { VerticesReadResponse, SeriesReadResponse, EdgesReadResponse, SeriesMetadataResponse } from '@kognifai/poseidon-dataadaptersservice';
import { forEach } from '@angular/router/src/utils/collection';

@Component({
  selector: 'app-dataadapter-comp',
  templateUrl: './dataadaptertest.component.html',
  styleUrls: ['./dataadaptertest.component.css']
})
export class DataAdapterTestComponent implements AfterViewInit {
  adapterName = 'Registered Adapters';
  registeredAdapters: Adapter[];
  selectedAdapter: Adapter;
  assetInput: string;
  seriesInput: string;

  assetsResponse: VerticesReadResponse | EdgesReadResponse;
  seriesResponse: SeriesReadResponse | SeriesMetadataResponse;
  notificationText = '';
  notificationClass = 'kx-notification--success';

  private notifyError(text: string) {
    this.notificationClass = 'kx-notification--danger';
    this.notificationText = text;
  }

  constructor(private dataAdaptersFactoryService: DataAdaptersFactoryService,
              private dataAdaptersLocationService: DataAdaptersLocationsService) {

  }

  ngAfterViewInit(): void {
    // Fetches all the registered data adapters.
    this.dataAdaptersLocationService.get().then((data: IDataAdaptersLocations[]) => {
      this.registeredAdapters = data;
    }).catch((error) => {
      this.notifyError(error.message);
    });
  }

  didSelectAdapter(adapter: Adapter, event: Event) {
    this.notificationText = '';
    this.selectedAdapter = adapter;
    this.adapterName = this.selectedAdapter.name;
  }

  getVertices() {
    try {
      this.notificationText = '';
      this.assetsResponse = '';
      const adapterValues = JSON.parse(this.assetInput);
      /** Retrieve assets vertices using AssetsRead */
      this.dataAdaptersFactoryService.CreateAssetsQuery(this.selectedAdapter.endpointUrl)
      .GetVertices(adapterValues.rootVerticesIds, adapterValues.traverseOptions, adapterValues.matchOptions,
        adapterValues.loadOptions).then((data: VerticesReadResponse) => {
        this.assetsResponse = JSON.stringify(data);
      }).catch((error) => {
        this.notifyError(error.message);
      });
    } catch (error) {
      if (this.selectedAdapter === undefined) {
        this.notifyError('Please select a registered data adapter.');
      } else {
        this.notifyError(error.message);
      }
    }
  }

  getEdges() {
    try {
      this.notificationText = '';
      this.assetsResponse = '';
      const adapterValues = JSON.parse(this.assetInput);
      /** Retrieve assets edges using AssetsRead */
      this.dataAdaptersFactoryService.CreateAssetsRead(this.selectedAdapter.endpointUrl)
      .GetEdges(adapterValues.rootVerticesIds, adapterValues.traverseOptions,
        adapterValues.matchOptions, adapterValues.loadOptions).then((data: EdgesReadResponse) => {
        this.assetsResponse = JSON.stringify(data);
      }).catch((error) => {
        this.notifyError(error.message);
      });
    } catch (error) {
      if (this.selectedAdapter === undefined) {
        this.notifyError('Please select a registered data adapter.');
      } else {
        this.notifyError(error.message);
      }
    }
  }


  getSeries() {
    try {
      this.notificationText = '';
      this.seriesResponse = '';
      const adapterValues = JSON.parse(this.seriesInput);
     /** Retrieve series using SeriesRead*/
      this.dataAdaptersFactoryService.CreateSeriesRead(this.selectedAdapter.endpointUrl)
      .GetSeries(adapterValues.seriesIds, adapterValues.rangeOptions,
        adapterValues.aggregationOptions, adapterValues.readOptions).then((data: SeriesReadResponse) => {
        this.seriesResponse = JSON.stringify(data);
      }).catch((error) => {
        this.notifyError(error.message);
      });
    } catch (error) {
      if (this.selectedAdapter === undefined) {
        this.notifyError('Please select a registered data adapter.');
      } else {
        this.notifyError(error.message);
      }
    }
  }

  getSeriesMetaData() {
    try {
      this.notificationText = '';
      this.seriesResponse = '';
      const sIds = Array.from(JSON.parse(this.seriesInput)) as string[];
      /** Retrieve series meta data using SeriesRead */
      this.dataAdaptersFactoryService.CreateSeriesRead(this.selectedAdapter.endpointUrl)
      .GetSeriesMetadata(sIds).then((data: EdgesReadResponse) => {
        this.seriesResponse = JSON.stringify(data);
      }).catch((error) => {
        this.notifyError(error.message);
      });
    } catch (error) {
      if (this.selectedAdapter === undefined) {
        this.notifyError('Please select a registered data adapter.');
      } else {
        this.notifyError(error.message);
      }
    }
  }

}

```
#Scaffolding a .NET Core API Data Adapter project
Poseidon Next provides a generator to scaffold an new ASP DOTNET Core API Data Adapter project.  
For more information [Scaffold ASP DOTNET Core API Data Adapter project](Poseidon%20Next%2FPublic%20documentation%2FGuides%2FCreating%20Poseidon%20Data%20Adapter%20project%20using%20Yeoman)

#Registering our custom data adapter
We need a registration tool for registration.
```powershell
npm install -g @kognifai/poseidon-app-registration-cli@">=2.0.0-beta.1 <3.0.0" 
```
Once we have the above tool installed, we can do the registration.
```powershell
poseidon-app-registration-cli --dataadaptermanifest mydataadapter\dataadapter.manifest.json --username  xyz --password xyz
```
Parameter **--dataadaptermanifest** - it is the path to **dataadapter.manifest.json** file, which can be found in ASP.Net Data Adapter project scaffolded above.








