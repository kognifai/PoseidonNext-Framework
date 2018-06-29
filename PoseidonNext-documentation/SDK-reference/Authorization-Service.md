# Description

**Authorization Service** is one of the services in **Application Framework**, which helps in managing resources and its associated permissions.  

##Import

```typescript
import { IResource, Permissions } from '@kognifai/poseidon-authorizationservice';
import { AuthorizationService } from '@kognifai/poseidon-ng-authorizationservice';
```

##Injection

```typescript
constructor(private authorizationService: AuthorizationService) {}
```
This service has the below interface:

```typescript
export interface IAuthorizationService {
    hasPermission(resourceId: string, permissionId: string): Promise<boolean>;
}
```
The **hasPermission** method can be used to check the access for a given **resourceId** against a specific permission.  This specific permission can be **'View', 'Create', 'Edit',** or **'Remove'** .  These permissions do have a pre-defined **permissionId** associated with it.

```typescript
export enum Permissions {
    Create = "12506856-5B28-4621-8A4F-3120C10167B9",
    Edit = "6E1BAF33-DD83-4367-85E3-B544A6F810EC",
    Remove = "ABBEE0A9-FB01-40A7-8986-517F2C9BA1B7",
    View = "4B6695BE-2730-4F9E-A5C6-E2B8F51314CD",
}
```

## Example usage of the authorization service is shown below:

```typescript
import { IResource, Permissions } from '@kognifai/poseidon-authorizationservice';
import { AuthorizationService } from '@kognifai/poseidon-ng-authorizationservice';

export class AppComponent implements OnInit {
  constructor(private authorizationService: AuthorizationService) {}

  ngOnInit() {
    this.resourceId = 'C1CB8B8C-C1BF-4078-8AE3-05117DEC7678';
  }

  hasPermission() {
    this.authorizationService
      .hasPermission(this.resourceId, Permissions.View)
      .then(access => {
        this.hasAccess = access ? 'Has permisson' : 'Do not have this permssion';
      });
  }
}
```



   