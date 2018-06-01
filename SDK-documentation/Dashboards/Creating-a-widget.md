
# Description
A widget is an Angular component that can be dynamically added to a view, rearranged and configured, saved into a view and loaded by Dashboards. In its essence, it is a configurable piece of logic with its corresponding UI presentation.

# Prerequisites
The **Kognifai Dashboards**  package is required in order to create widgets. It can be installed into the destination project like so:
```
npm install @kognifai/poseidon-dashboards --save
```

# Views
A widget consists of two UI parts/views:

## Presentation part
This is the main view of the widget. This is the presentation that the user sees when they insert the widget into a dashboard.
An example of a widget view is:

![widget.png](https://github.com/kognifai/PoseidonNext-Framework/blob/master/.attachments/widget-6b5c116c-dcc0-47ed-bddf-c1838a36610e.png)

*Note the buttons in the top right corner. They are utility buttons which bring up the configuration view of the widget and remove it from the dashboard correspondingly. They are provided by the Dashboards framework and are not part of the widget view itself.

## Configuration part
A widget also must have a view/means to interact with its configuration.
An example of a widget configuration view is:

![widget_config.png](https://github.com/kognifai/PoseidonNext-Framework/blob/master/.attachments/widget_config-896a4f67-799c-4634-b91a-734e1c48b71e.png)

*Note the buttons in the bottom right corner. They are utility buttons which persist or discard the changes made to the widget configuration. They are provided by the Dashboards framework and are not part of the widget configuration view itself.

# Implementation
A widget is implemented as a pair of Angular components (main and edit).
Each of them should have the typical elements in place: 
 - A **.ts** file for component logic
 - A **.html** file that contains the UI definition
 - A **.css** file that holds its styles

An example of a widget component declaration is no different than any other Angular component:

```typescript
import { Component, Input } from '@angular/core';

@Component({
    templateUrl: './demowidget.component.html',
    styleUrls: ['./demowidget.component.css']
})
export class DemoWidgetComponent ...
```

## Contracts
**WidgetComponent**
```typescript
/**
 * Base interface for the widget view component to implement.
 */
export interface WidgetComponent {
    /**
     * The configuration object of the widget for the component to work with.
     */
    configuration: WidgetConfiguration;

    /**
     * Initialization function, called when widget is created or when the configuraiton object changes.
     */
    init(): void;
    /**
     * Update function, called based on a timer, that is started when the dashboard loads.
     */
    update(): void;
    /**
     * Utility function used to collect all series addresses, associated with the widget.
     */
    collectAddresses(): string[];
    /**
     * Utility function used to collect all data subscriptions that the widget started.
     */
    collectSubscriptions(): Subscription[];
}
```

**WidgetEditComponent**
```typescript
/**
 * Base interface for the widget configuration editing view component to implement.
 */
export interface WidgetEditComponent {
    /**
     * The configuration object of the widget for the component to work with.
     */
    configuration: WidgetConfiguration;
}
```

**WidgetConfiguration**
```typescript
/**
 * Configuration of the widget.
 * This is a base configuration interface that has to be implemented/extended by widgets' own configuration types.
*/
export interface WidgetConfiguration {
    /**
     * Title of the widget.
     */
    title: string;
}
```

## Components
In order for the paired components to be a valid Dashboards widget, they must inherit certain interfaces.

### Main component
The main widget component should inherit from the ```WidgetComponent``` interface, like so:

```typescript
import { WidgetComponent } from '@kognifai/poseidon-dashboards';

...

export class DemoWidgetComponent implements WidgetComponent { }
```

Implementation of this interface means that the component class will have to define some members:
- **configuration** - a property of the **WidgetConfiguration** interface type. Any widget must have  **configuration** property that will provide the definition of what the user can edit for the widget via the configuration component
- **init()** - executed when:
  - the widget is first added to the dashboard
  - the widget is loaded initially when the dashboard is loaded
  - the configuration of the widget is changed
- **update()** - executed each second. A suitable place for refreshing/pulling data from a service
- **collectAddresses()** - necessary for the framework to be able to collect all configured timeseries addresses from the widget.
Currently **NOT** implemented in framework.
- **collectSubscriptions()** - necessary for the framework to be able to collect all data subscriptions objects and dispose of them.
Currently **NOT** implemented in framework.

Here is an example of a full widget component definition:
```typescript
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';
import { WidgetComponent, WidgetConfiguration } from '@kognifai/poseidon-dashboards';

@Component({
    templateUrl: './demowidget.component.html',
    styleUrls: ['./demowidget.component.css']
})
export class DemoWidgetComponent implements WidgetComponent, OnChanges {

    @Input() configuration: WidgetConfiguration;

    private value: number;

    init() {
        console.log('Widget initialized.');
    }

    update() {
        this.value = Math.random() * 1000;
    }

    collectAddressed() {
        return [];
    }

    collectSubscriptions() {
        return [];
    }

    ngOnChanges(changes: SimpleChanges) {
        console.log('Widget configuration changed.');
    }
}
```

For the sake of completeness, here are the .html and .css files contents for this widget:

```html
<div class="demo-widget-content">
    My title is: {{configuration.title}}
    <br/>
    <br/>
    My current value is: {{value}}
</div>
```

```css
.demo-widget-content {
    position: absolute;
    width: 100%;
    top: calc(50% - 40px);
}
```

*Note that these interface definitions may be subject to breaking changes in future releases.

### Edit component
The component that will represent the UI for the **configuration** object of the widget should implement the **WidgetEditComponent** interface. Currently the only member it defines is the configuration object itself.

Here is a full example of a widget's **edit component**:

```typescript
import { Component } from '@angular/core';
import { WidgetEditComponent, WidgetConfiguration } from '@kognifai/poseidon-dashboards';

@Component({
    templateUrl: './demowidget.edit.component.html',
    styleUrls: ['./demowidget.edit.component.css']
})
export class DemoWidgetEditComponent implements WidgetEditComponent {
    configuration: WidgetConfiguration;
}
```

```html
<div class="kx-form__element">
    <input class="kx-field kx-field--size-base" id="title" type="text" [(ngModel)]="configuration.title" placeholder="Title"/>
    <label class="kx-label" for="title">
        Title: 
    </label>
</div>
```

## Registration
For information on how to register a widget, so it can be available to Dashboards, please see the [Create a widgets package](https://github.com/kognifai/PoseidonNext-Framework/wiki/Creating-a-widgets-package) article.
