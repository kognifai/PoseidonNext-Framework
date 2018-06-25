# Description
A widgets package is an Angular module that currently has two main purposes:
 - Declares widget components (so they are visible to other Angular modules)
 - Registers widgets with the Dashboards framework (so they are visible to dashboards creators)

# Prerequisites
The **Kognifai Dashboards**  package is required in order to create widgets packages. It can be installed into the destination project like so:
```
npm install @kognifai/poseidon-dashboards --save
```

# Contracts
There are two main contracts that are necessary for registering a widget into the framework.

**Dashboards widget service** - used to add or remove widgets from the global widgets collection:
```typescript
@Injectable()
export class DashboardsWidgetService {
    /**
     * Registers a widget into a global widgets collection.
     * @param widget The widget to register.
     */
    register(widget: Widget): void { }

    /**
     * Removes a widget from the global widgets collection.
     * @param widget The widget to unregister.
     */
    unregister(widget: Widget): void { }

    /**
     * Removes all widgets from the global widgets collection.
     */
    unregisterAll(): void { }

    /**
     * Retrieves a registered widget object based on its type.
     * @param type The type of the widget to get.
     */
    getWidget(type: string): Widget { }

    /**
     * Retrieves all registered widget objects.
     */
    getAllWidgets(): Widget[] { }

    /**
     * Retrieves the number of all registered wdigets.
     */
    count(): number { }
}
```

**Widget** - contains the widget definition:
```typescript
/**
 * Definition of the widget to register - the object we need to create in order to register it into the dashboards widget service.
 * Should contain all necessary properties to instantiate a widget (components, configuration, etc.).
 */
export interface Widget {
    /**
     * The type of the widget. Should be unique.
     */
    type: string;

    /**
     * Category for widget grouping. Currently not supported.
     */
    category?: string;
    /**
     * Widget description. Currently not displayed.
     */
    description?: string;

    /**
     * The component that represents the widget's view.
     */
    component: Type<WidgetComponent>;
    /**
     * The component that represents the widget's configuration view.
     */
    editComponent: Type<WidgetEditComponent>;

    /**
     * The configuration of the widget.
     */
    configuration: WidgetConfiguration;
}
```

# Implementation
Here is how the project's main module should look like:
```typescript
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';

import { DashboardsWidgetService } from '@kognifai/poseidon-dashboards';

import { DemoWidgetComponent } from './widgets/demowidget/demowidget.component';
import { DemoWidgetEditComponent } from './widgets/demowidget/edit/demowidget.edit.component';

@NgModule({
    declarations: [
        // Widget components must be declared
        DemoWidgetComponent,
        DemoWidgetEditComponent
    ],
    imports: [
        FormsModule,
        CommonModule
    ],
    entryComponents: [
        // Widget components must be exported as 'entry components'
        DemoWidgetComponent,
        DemoWidgetEditComponent
    ]
})
export class BasicWidgetsModule {

    // inject the 'dashboardsWidgetService'
    constructor (private dashboardsWidgetService: DashboardsWidgetService) {

        // register your widget
        this.dashboardsWidgetService.register({
            type: 'Demo',
            configuration: {
                title: 'My Demo Widget 1'
            },
            component: DemoWidgetComponent,
            editComponent: DemoWidgetEditComponent
        });
    }
}
```

# Structure
A widgets package for Dashboards should be implemented as a [Kognifai package](/Poseidon-Next/Developer-documentation/Creating-a-package-and-application-with-Yeoman).

# Usage
To use your newly created widgets package, so the widgets inside it can be available to Dashboards, its **module** should be **imported** into the host application. In this release this is the [Dashboards test page](/Poseidon-Next/Public-documentation/Samples-and-test-pages/Dashboard-Test-Page).