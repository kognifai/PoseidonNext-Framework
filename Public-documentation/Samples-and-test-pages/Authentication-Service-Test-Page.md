# Sample usage

This component illustrate the usage of authentication service. Below is the sample code for the same.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';

import { AppComponent } from './app.component';

const routes: Routes = [
  { path: '', component: AppComponent }
];

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  providers: [],
  bootstrap: []
})
export class AuthModule { }

```
and app.component.ts file looks like

```ts
import { Component, OnInit } from '@angular/core';
import { AuthenticationService } from '@kognifai/poseidon-authenticationservice';

@Component({
  selector: 'app-authentication-service-test-page',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  loggedIn: boolean;

  idTokenProperties: { key: string; value: string }[];
  accessTokenProperties: { key: string; value: string }[];

  constructor(private authenticationService: AuthenticationService) {
    this.loggedIn = false;

    this.idTokenProperties = [];
    this.accessTokenProperties = [];
  }

  ngOnInit() {
    if (!this.authenticationService.isAuthenticated) {
      // TODO: implement event emitting or observable
      return;
    }

    this.loggedIn = true;

    const idToken = this.authenticationService.idToken;
    const accessToken = this.authenticationService.accessToken;

    const idTokenObj = this.decodeToken(idToken);
    const accessTokenObj = this.decodeToken(accessToken);

    Object.keys(idTokenObj).forEach((key, index) => {
      this.idTokenProperties.push({
        key: key.toString(),
        value: idTokenObj[key]
      });
    });

    Object.keys(accessTokenObj).forEach((key, index) => {
      this.accessTokenProperties.push({
        key: key.toString(),
        value: accessTokenObj[key]
      });
    });
  }

  private decodeToken(token: string) {
    const base64Url = token.split('.')[1];
    const base64 = base64Url.replace('-', '+').replace('_', '/');
    return JSON.parse(window.atob(base64));
  }
}
```
