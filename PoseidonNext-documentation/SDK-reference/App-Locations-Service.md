# Description
The Poseidon ecosystem integrates multiple applications each of whom has one or more locations (URLs) that can be accessed by the users. The **App locations service** provides hierarchical list of **app locations**.
# Usage
## Contracts
### App locations service
```typescript
export class AppLocationsService {
    public get(): Promise<IAppLocation[]> { ... }
}
```
### App location
```typescript
export interface IAppLocation {
    id: string;
    name: string;
    path: string;
    appLocations: IAppLocation[];
}
```
## Injecting
App locations service is standard Angular service provided by Poseidon and can be used by injecting it into application services and components.
- package.json
```json
{
  "dependencies": {
    "kognifai-poseidon-applocationsservice": "^2.0.0",
    "kognifai-poseidon-ng-applocationsservice": "^2.0.0"
  }
}
```
- app.module.ts
```typescript
import { AppLocationsService } from '@kognifai/poseidon-ng-applocationsservice';
@NgModule({
  providers: [
    AppLocationsService
  ]
})
export class AppModule {
```
- my.component.ts
```typescript
import { AppLocationsService } from '@kognifai/poseidon-ng-applocationsservice';
@Component( ... )
export class MyComponent {
  constructor(private appLocationsService: AppLocationsService) {
    this.appLocationsService.get().then((appLocations: IAppLocation[]) => {
      // app locations loaded
    }
  }
}
```
# Sample response
This is example response returned by the `get()` method:
```json
[{
  id: "329cd141-d1a2-4d3b-9e6e-55a14f41a0e7",
  name: "Home",
  path: "http://localhost:4200/"
}, {
  id: "9de61b14-6d65-430e-8b61-928a8fd9c95c",
  name: "User Administration",
  appLocations: [{
    id: "58846c3f-a426-4a82-a6f8-b8d264f4a8b7",
    name: "Roles",
    path: "http://localhost:4202/#/roles"
  }, {
    id: "e21f0da3-fa11-4b31-951f-0a754f026596",
    name: "Users",
    path: "http://localhost:4202/#/users"
  }]
}, {
  id: "6ed28824-f09e-4837-997d-42b2d7a81c06",
  name: "User Profile",
  path: "http://localhost:4201/"
}]
```