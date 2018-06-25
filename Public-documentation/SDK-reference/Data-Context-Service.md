# Description
Data context is one of the packages from Kognifai application framework.  This aims to be as generic as possible and is domain agnostic.  It also supports simultaneous data context structures and hierarchies from different systems and domains.  The end goal is for a user to specify and for the system to understand: "What you are looking at data in relation to." (e.g. which vessel, well, generator etc.).

Design is focused around the following axioms:

- Data contexts exist in hierarchies
- Selection of data contexts can also be done in a hierarchy

This allows you to have data hierarchies like this for vehicles: "Brand -> Type -> Model" and the possibility to make selections on any level.  A root selection to select brand and type, then a child selection to choose models within that brand.

In the drilling and wells domain, one common data hierarchy structure is: Well -> Wellbore -> Log -> Curve, where the selection is usually done hierarchically from wellbore to curve.  Select a well and a wellbore to inspect. Then selectors dependent on the wellbore selectors are used to select curves.

Data context browsing and selection has been developed purely as a client side utility.  Proxies to the underlying domain specific assets and data structures must be created.  As such structures can be enormous and it is not feasible to load whole hierarchies into the client.  The current implementation is created as a minimum base to fulfil immediate requirements of a non-domain specific selection mechanism that could be extended.

#Terms
The term context has a couple of meanings in relation to Kognifai Data Context.

"**Selection Context**" - It is the context you are selecting a item as active for.
e.g., Setting a item "XXX" as the active "Well".  Setting "Toyota" as the active "car model". (Here "Well" and "Toyota" are selection contexts).

"**Data Context Item**" - An item that can be set active for a selection context.  This exists in hierarchies and has a type, which is likely to relate to the "selection context" it can be set as active for.

#Components
There are two main client side constituents:

**DataContextService** - The data context item repository can contain multiple data context item hierarchies from different domains. The service also facilitates events for hooking onto when the active data context item for a selection context is changed.

**DataContextSelectorComponent** - A client UI control to select the data context for given selection context.  It binds to the data item repository from DataContextService and gives filtering possibilities to only show data context item of a given type.  Selectors can be organized in a parent/child relationship where the selection in one selector will impact what is available on its related selector.

**DataContextPersistenceService** - This service helps in persisting the data context selection state, i.e., which data context item is selected for which selection context, so that it can be retrieved and set at application startup.  This can be useful when storing the state with other settings (like display configuration settings) is not possible.

**DataContextUrlService** - This service helps in transferring the context through Url. This can be useful when sending a particular display url with context, so that it opens the same display and with the context without needing the user to navigate to the context manually. 

# Data Context Items
All interfaces relating to Data Context can be retrieved from '**@kognifai/poseidon-datacontextservice**" package.

```typescript
import { DataContextService } from '@kognifai/poseidon-datacontextservice';
```

We can also use angular service, which extends the above version.

```typescript
import { DataContextNgService} from '@kognifai/poseidon-ng-datacontextservice';
```
Data context hierarchies are defined by data context items.

```typescript
import { IDataContextSource } from './IDataContextSource';

export interface IDataContextItem {
    expanded: boolean;
    identifier: string;
    address?: string;
    type: string;
    label: string;
    source: IDataContextSource;
    children?: IDataContextItem[];
    parent?: IDataContextItem;
}
```
An item has a unique identifier and a type.  The type is used for selector filtering.  It also has a boolean indicator of whether or not this item has been expanded, meaning whether or not the platform has retrieved it's structural children from the item's source.  When data context items are registered into the data context service repository, the source property must reference an instance of **IDataContextSource** that the service can use to retrieve the item's children.  A data context source is domain specific and has one main responsibility, it should know how to expand a **IDataContextItem** that it has sourced.

```typescript
import { IDataContextItem } from './IDataContextItem';

export interface IDataContextSource {
    fallback?: (parent: IDataContextItem, identifier: string) => IDataContextItem;
    expand(item: IDataContextItem): Promise<boolean>;
}
```

The data context source has 2 properties.  "**expand**" fetches and populates the child metadata.  "**fallback**" is used as a lookup logic if the child with specified identifier is not found within the given collection.

#Data Context Service
The data context service keeps track of active data context items for selection contexts. It acts as an event emitter and will raise events when the active item for a context changes.  It is also a repository for storing data context hierarchies of different types.  It gives methods for relating selection contexts. This is used directly by the data context selection component to relate parent/child related instances of the component.

```typescript
export interface IDataContextService {
    /**
     * root items
     */
    items: IDataContextItem[];

    /**
     * notifies when active context changes
     */
    onActiveChange: Subject<IEventDataContext>;

    /**
     * notifies when data context items are repopulated.
     */
    onRefresh: Subject<string>;

    /**
     * register root item
     * @param IDataContextItem item Data Context Item
     */
    register(item: IDataContextItem): void;

    /**
     * register dependency between context identifiers
     * when active on a parent context changes, child contexts will be cleared
     * @param parentContext parent context identifier
     * @param childContext child context identifier
     */
    registerRelationship(parentContext: string, childContext: string): void;

    /**
     * get active data context item for a given context
     * @param contextIdentity Context
     * @returns IDataContextItem active data context, null if no active context is set
     */
    getActive(contextIdentity: string): IDataContextItem;

    /**
     * set active data context item for a context
     * @param contextIdentity Context
     * @param IDataContextItem
     */
    setActive(contextIdentity: string, item: IDataContextItem): void;

    /**
     * clear active data context item for a context
     * @param contextIdentity Context
     */
    clearActive(contextIdentity: string): void;

    /**
     * get a definion of the current state for the supplied contexts
     * @param contexts to get
     * @returns IDataContextState the state for supplied contexts.
     * A hash-map of context name to full path of the active datacontext item for given context.
     */
    getCurrentState(contextIdentity?: string[]): IDataContextState;

    /**
     * based on a definition of active state for a set of data contexts, perform steps to apply that state
     * @param IDataContextState state to use
     * @param number how long to wait until giving up on resolving promise
     */
    setCurrentState(state: IDataContextState, timeout?: number): Promise<void>;

    /**
     * Get an array representing the path of identifier leading to the supplied item.
     * The first entry should contain the identifier of the root item,
     * while the last should contain identifier of supplied item.
     * @param IDataContextItem item to get path for.
     * @returns string[] array of identifiers from root to given data context item
     */
    getPath(item: IDataContextItem): string[];

    /**
     * Refreshes the DataContextSelector with matching context-id
     * @param contextIdentity to refresh
     */
    refresh(contextIdentity: string): void;

    /**
     * Get parent context of a child contexts
     * @param childContext child context identifier
     * @returns parent context identifier
     */
    getParentContext(childContext: string): string;
}
```
The service has methods for getting and setting the current state. This will give the active data context item for all selection contexts that are set. 

#DataContextPersistenceService

This service helps in data context selection state persistence i.e., which data context item is selected for which selection context, so that it can be retrieved and set at application startup.  This service has the below methods that can be to used in our application.

##Import
```typescript
import { DataContextPersistenceNgService } from '@kognifai/poseidon-ng-datacontextservice';
``` 
This service's interface is shown below:

```typescript
export interface IDataContextPersistenceService {
    /**
     * tells if there is any saved context.
     */
    isPinned: boolean;

    /**
     * tells if there is any saved context.
     */
    onPinChange: Subject<boolean>;

    /**
     * The method fetches saved data context state.
     */
    getSavedContext(): Promise<IDataContextState>;

    /**
     * Save active data context item for a context
     * @param {string} contextIdentity Context
     * @param {IDataContextItem}
     */
    pin(contextIdentity: string, item?: IDataContextItem): Promise<void>;

    /**
     * clears stored data context state
     * @param {string} contextIdentity Context
     */
    unpin(contextIdentity: string): Promise<void>;
}

```

#DataContextUrlService
This service helps in transferring the context through URL. This can be useful when sending a particular display URL with context, so that it opens the same display and with the context without needing the user to navigate to the context manually.

##Import
```typescript
import { DataContextUrlNgService } from '@kognifai/poseidon-ng-datacontextservice';

```
 This service's interface is shown below:

```typescript
export interface IDataContextUrlService {
    /**
     * apply datacontext from url
     */
    applyUrlValues(): Promise<void>;

    /**
     * gets url string for the datacontext
     * @param contextIdentity Context
     * @returns string url for active data context, null if no active context is set
     */
    getUrlValue(contextIdentity: string): string;

    /**
     * gets datacontextstate from url
     * @returns IDataContextItem active data context, null if no active context is set
     */
    getCurrentUrlDataContextState(): IDataContextState;
}

```

#DataContextSelectorComponent
The data context selector UI component is implemented as an angular component, giving a new html tag to use in templates where data context should be possible to select.

##Import
```typescript
import { DataContextSelectorComponent } from '@kognifai/poseidon-datacontextselectorcomponent';
``` 
##Usage
```typescript
<app-data-context-selector
      id="id"
      depth="depth"
      maxDepth="maxDepth"
      type="type"
      labels="labels"
      parent="">
</app-data-context-selector>
```

It has these attributes:

**id** - Identifier for this selector. It will be the context used when the active item for the selector is set against the data context service.  It's also the reference to use in the "parent" property of related selectors.
**depth** - How many levels of the hierarchy should the control initially show.
**maxDepth** - The max number of hierarchical levels should be possible to drill down.  An active item for a selector context is set when,
-  no more children exists, 
-  selection depth equals current depth

**type** - This will filter the data context items bound to the selection component. If no parent is specified it will be populated with root elements of this type. If parent context is specified it will display data context elements of given type that exists of children of the active data context item set for the parent context.
**labels** - Labels for the different hierarchy levels. Comma seperated. Will be run through translator.
**parent** - The parent context (if any). If the active item in the parent context changes the selection of a child selector will be invalidated.

##Usage and Examples

```typescript
import { Component, EventEmitter, ChangeDetectorRef } from '@angular/core';
import { IExampleContextItem } from './model';
import { ExampleDataContextSource } from './example-data-context.source';
import { DataContextNgService } from '@kognifai/poseidon-ng-datacontextservice';
import { IEventDataContext } from '@kognifai/poseidon-datacontextservice';

@Component({
  selector: 'app-comp',
  templateUrl: `<div>
                <app-data-context-selector id="selectorId" depth="2" maxDepth="2" type="server"></app-data-context-selector>
                </div>`,
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  showRoot: boolean;
  constructor(private dataContextService: DataContextNgService,
    private exampleSource: ExampleDataContextSource, private router: Router) {
    this.exampleSource.getData().then((items: IExampleContextItem[]) => {
      for (const item of items) { this.dataContextService.register(item); }
    });
  }
}

```


```typescript
@Injectable()
export class ExampleDataContextSource implements IExampleDataContextSource {
    private getExampleRequest: Promise<IExampleContextItem[]>;
    getData(): Promise<IExampleContextItem[]> {
        this.getExampleRequest = new Promise((resolve, reject) => {
              resolve(data);
        });
        return this.getExampleRequest ;
    }
}
```
Above is the basic component, where we use "**ExampleDataContextSource**" (a service which implements **IDataContextSource** methods) to fetch and register the root items for the data context selector.


