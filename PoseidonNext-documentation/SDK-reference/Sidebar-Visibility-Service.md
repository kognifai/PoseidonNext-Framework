# Description

This service is used to make screen opaque and back to normal. Here are the fields for the same.

```ts
export class SidebarsVisibilityService {
    pageOverlayActive = false;
    pageOverlayAnimating = false;

    navigationPanelHidden = false;
    navigationPanelActive = false;
    navigationButtonActive = false;

    toolsPanelHidden = false;
    toolsPanelActive = false;
    toolsButtonActive = false;
}

```

Its usage can be found in header.component.ts file like shown below.

```ts
import { Component, OnInit, HostBinding, Input } from '@angular/core';
import { Subscription } from 'rxjs';
import { SidebarsVisibilityService } from './sidebars-visibility.service';
import { INavigationItem } from '@kognifai/poseidon-ng-navigationservice';
import { NavigationService } from '@kognifai/poseidon-ng-navigationservice';
import { AuthenticationService } from '@kognifai/poseidon-authenticationservice';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.scss']
})
export class HeaderComponent implements OnInit {
  subscription: Subscription;
  activeNavigationItems: INavigationItem[];
  constructor(
    private sidebarsVisibilityService: SidebarsVisibilityService,
    private navigationService: NavigationService,
    private authenticationService: AuthenticationService
  ) { }

  ngOnInit() {
    this.navigationService.activeItem.subscribe(item => {
      if (item) {
        this.activeNavigationItems = this.breadcrumbData(item);
      }
    });
  }

  toggleNavigationPanel(): void {
    this.setToolsMenuVisibility(false);
    const isVisible: boolean = !this.sidebarsVisibilityService.navigationPanelActive;
    this.setNavigationPanelVisibility(isVisible);
    this.setPageOverlayVisibility(isVisible);
  }

  private setNavigationPanelVisibility(isVisible: boolean): void {
    if (isVisible) {
      this.sidebarsVisibilityService.navigationButtonActive = true;
      this.sidebarsVisibilityService.navigationPanelHidden = false;
      setTimeout(() => {
        this.sidebarsVisibilityService.navigationPanelActive = true;
      }, 0);
    } else {
      this.sidebarsVisibilityService.navigationButtonActive = false;
      this.sidebarsVisibilityService.navigationPanelActive = false;
      setTimeout(() => {
        this.sidebarsVisibilityService.navigationPanelHidden = true;
      }, 350);
    }
  }

  toggleToolsMenu(): void {
    this.setNavigationPanelVisibility(false);
    const isVisible: boolean = !this.sidebarsVisibilityService.toolsPanelActive;
    this.setToolsMenuVisibility(isVisible);
    this.setPageOverlayVisibility(isVisible);
  }

  private setToolsMenuVisibility(isVisible: boolean): void {
    if (isVisible) {
      this.sidebarsVisibilityService.toolsButtonActive = true;
      this.sidebarsVisibilityService.toolsPanelHidden = false;
      setTimeout(() => {
        this.sidebarsVisibilityService.toolsPanelActive = true;
      }, 0);
    } else {
      this.sidebarsVisibilityService.toolsButtonActive = false;
      this.sidebarsVisibilityService.toolsPanelActive = false;
      setTimeout(() => {
        this.sidebarsVisibilityService.toolsPanelHidden = true;
      }, 350);
    }
  }

  private setPageOverlayVisibility(visible: boolean): void {
    if (visible) {
      this.sidebarsVisibilityService.pageOverlayActive = true;
      setTimeout(() => {
        this.sidebarsVisibilityService.pageOverlayAnimating = true;
      }, 0);
    } else {
      this.sidebarsVisibilityService.pageOverlayAnimating = false;
      setTimeout(() => {
        this.sidebarsVisibilityService.pageOverlayActive = false;
      }, 350);
    }
  }

  logout() {
    this.authenticationService.logout();
  }

  defaultToHome() {
    this.navigationService.setActive(this.navigationService.setActiveByPath('/home'));
  }

  private breadcrumbData(activeItem): INavigationItem[] {
    const items: INavigationItem[] = [];
    let parent = activeItem;
    while (parent) {
      items.push(parent);
      parent = <INavigationItem>parent.parent;
    }
    return items.reverse();
  }

}

```
