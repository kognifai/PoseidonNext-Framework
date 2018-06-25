### Description

Header component uses bunch of services, directives and components. Below is the basic module of that.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { Routes, RouterModule, provideRoutes } from '@angular/router';
import { BreadcrumbModule } from 'kognifai-poseidon-breadcrumb-component';
import { DropdownDirective } from 'kognifai-poseidon-dropdown-directive';
import { HeaderComponent } from './header.component';
import { SidebarsVisibilityService } from 'kognifai-poseidon-sidebar-visibilityservice/dist';
import { AuthenticationService } from 'kognifai-poseidon-authenticationservice';
import { NavigationService } from 'kognifai-poseidon-ng-navigationservice';

@NgModule({
  imports: [
    CommonModule,
    RouterModule,
    BreadcrumbModule
  ],
  declarations: [
    HeaderComponent,
    DropdownDirective
  ],
  exports: [
    HeaderComponent,
    DropdownDirective
  ],
  providers: [
    SidebarsVisibilityService,
    AuthenticationService,
    NavigationService
  ]
})

export class HeaderModule { }
```

And its usage will be something like this

```html
<app-header *ngIf="!initializing" class="kx-page__header kx-flex"></app-header>
```


