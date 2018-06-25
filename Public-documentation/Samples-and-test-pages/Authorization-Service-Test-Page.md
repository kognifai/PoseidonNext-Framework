# Sample usage

This component illustrate the usage of authentication service. Below is the sample code for the same.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { AuthorizationTestComponent } from './authorTest.component';
import { AuthorizationService } from '@kognifai/poseidon-ng-authorizationservice';

const routes: Routes = [
  { path: '', component: AuthorizationTestComponent }
];

@NgModule({
  declarations: [
    AuthorizationTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  exports: [AuthorizationTestComponent],
  providers: [AuthorizationService],
  bootstrap: []
})
export class AuthorizationTestModule { }
```
And its component file looks like

```ts
import { Component, OnInit } from '@angular/core';
import { IResource, Permissions } from '@kognifai/poseidon-authorizationservice';
import { AuthorizationService } from '@kognifai/poseidon-ng-authorizationservice';

@Component({
  selector: 'app-authorization-service-test-page',
  templateUrl: './authorTest.component.html',
  styleUrls: ['./authorTest.component.css']
})
export class AuthorizationTestComponent implements OnInit {
  // ideally should be binded to Permission enum
  avaiablePermissions: string[] = ['View', 'Create', 'Edit', 'Remove'];
  hasAccess: string;
  resourceId: string;
  permission: string;
  constructor(private authorizationService: AuthorizationService) {}

  ngOnInit() {
    // by Default binding User.Adminstration Resource Id.
    this.resourceId = 'C1CB8B8C-C1BF-4078-8AE3-05117DEC7678';
    this.permission = this.avaiablePermissions[0];
  }

  hasPermission() {
    const perm = Permissions[this.permission];
    this.authorizationService
      .hasPermission(this.resourceId, perm)
      .then(access => {
        this.hasAccess = access
          ? 'Has permisson'
          : 'Do not have this permssion';
      });
  }
}
```