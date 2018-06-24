# Description

A widgets package is an Angular module that currently has two main purposes:
 - Declares widget components (so they are visible to other Angular modules)
 - Registers widgets with the Dashboards framework (so they are visible to dashboards creators)

# Prerequisites
The **Kognifai Dashboards**  package is required in order to create widget packages. It can be installed into the destination project in this manner:
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
     * Retrieves the number of all registered widgets.
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
Here is how the project's main module must look like:
```typescript
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';

import { DashboardsModule, DashboardsWidgetService } from '@kognifai/poseidon-dashboards';

import { DemoWidgetComponent } from './demowidget/demowidget.component';
import { DemoWidgetEditComponent } from './demowidget/edit/demowidget.edit.component';

@NgModule({
    declarations: [
        // Widget components must be declared
        DemoWidgetComponent,
        DemoWidgetEditComponent
    ],
    imports: [
        DashboardsModule,
        FormsModule,
        CommonModule
        // and any other module imports your widgets might need
    ],
    entryComponents: [
        // Widget components must be exported as 'entry components'
        DemoWidgetComponent,
        DemoWidgetEditComponent
    ]
})
export class DashboardsModule {

    // inject the 'dashboardsWidgetService'
    constructor (private dashboardsWidgetService: DashboardsWidgetService) {

        // register your widget
        this.dashboardsWidgetService.register({
            type: 'DemoWidget',
            configuration: {
                title: 'My Demo Widget 1'
            },
            component: DemoWidgetComponent,
            editComponent: DemoWidgetEditComponent
        });
    }
}
```
