# Description

The Navigation Service holds list of items that are displayed in the left-hand sidebar in Poseidon. It is used by application developers in order to add custom commands in the navigation sidebar.

## Definitions
- **Navigation item**: Represents a button in the navigation sidebar. It has id, label, icon and associated route to which it leads. Child Navigation items can be assigned.
- **Navigation service**: Angular service provided by the the platform so that applications can register, unregister, and search for navigation items. It also holds a single active Navigation item

# Usage

## Contracts

### Navigation service
```typescript
export interface INavigationService {

navigationItems: INavigationItem[];
activeItem: BehaviorSubject<INavigationItem>;

register(item: INavigationItem, parentId?: string): void;
unregister(id: string): INavigationItem;
findById(id: string): INavigationItem;
notify(): void;
search(query: string): ISearchResult[];
getActive(): INavigationItem;
navigate(item: INavigationItem): void;
getNavigationItems(): INavigationItem[];
setActive(item: INavigationItem): void;
setActiveByPath(path: string): INavigationItem;
```

### Search result
```typescript
export interface ISearchResult extends INavigationItem {
    location: string;
    shortLocation: string;
}
```

## Injecting

As a standard Angular service, the Navigation service can be used by injecting it into your components.
```typescript
@Component( ... )
export class NavigationServiceTestPageComponent {
    constructor(private navigationService: NavigationService) { ... }

```

### Registering Navigation items
The register method accepts a single ```NavigationItem``` and adds it to the navigation sidebar.
```typescript
register(item: NavigationItem, parentId?: string): void {
```

### Unregistering Navigation items
The unregister method accepts a ```string``` value and removes the ```NavigationItem``` with ID equal to that value. In case an item with said ID does not exist, it returns and Error with the message ```'Item not found'```.
```typescript
unregister(id: string): INavigationItem {
```

### Find by ID
Searches for an item with the specified id.
```typescript
findById(id: string): INavigationItem {
```

### Notify
Notifies a component, that items are changed.
```typescript
notify(): void {
```

### Get active item
Returns the current active item.
```typescript
getActive(): INavigationItem {
```
### Set active item (possibly by ID)
Set the current active item by giving the item itself as an argument or its path.
```typescript
setActive(item: INavigationItem) {

setActiveByPath(path: string): INavigationItem {
```
### Searching for Navigation items
The search method accepts a single ```string``` argument and returns an array of ```ISearchResult``` results, matching the string.
```typescript
search(query: string): ISearchResult[] {
```

### Navigate
* Triggers a transition to the specified navigation item.
  - If an onSelected handler is present, it is invoked.
  - If a state is associated with this item, a transition to that state is triggered.
  - Otherwise nothing happens

```typescript
navigate(item: INavigationItem): void {
```

### Get Navigation items
Returns and array of all the ```INavigationItem```
```typescript
getNavigationItems(): INavigationItem[] {
```