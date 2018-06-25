# Description

The home screen is the default landing page/view in Poseidon.   It would contain a default icon which enables user to add favourite items on this screen.  The initial screen would be looking like as below:

 ![image.png](/Public-documentation/images/image-86f8e543-b5af-44e3-be89-20d94b8c8a71.png)

Adding favourite item onto the home screen is facilitated by **FavoritesService**.

## **Usage**

**FavoritesService** exposes the following methods.

```typescript
export class FavoritesService {
    load(): Promise<IFavorite> { ... }
    pin(item: IFavorite): Promise<boolean> { ... }
    unpin(item: IFavorite): Promise<boolean> { ... }
    search(query: string): Promise<IFavorite> { ... }
    isPinned(id: string): boolean { ... }
}
```

A **IFavorite** object has the following properties.

```typescript
export interface IFavorite {
    id: string;
    name: string;
    displayName: string;
    tooltip: string;
    route: string;
    icon?: string;
    iconUrl?: string;
    isPinned?: boolean;
    location?: string;
    shortLocation?: string;
}
```

## **Injecting**

We need to import the **FavoritesService** as below:

```typescript
import { FavoritesService } from '../../services/favorites.service';
```
It is injected as below:

```typescript
export class FavoitesTestPageComponent {
    constructor(private favoritesService: FavoritesService) { ... }
}
```

When the user clicks/presses the **Add Favorite** button, it opens an interface where user can search/filter items, which they would like to add/remove as a favourite item.  The search interface by default is prepopulated with all navigation items.  The navigation items are fetched using the below method.

```typescript
load(): Promise<IFavorite> { ... }
```

The user can click anywhere on the screen to dismiss the search interface.

When the user does a search, it returns a list that matches the queried string and below is the method which is invoked.

```typescript
search(query: string): Promise<IFavorite> { ... }
```
The items which are already a favourite would be listed in yellow colour.  To check if a navigation item is already a favourite or not, we use the below method.  The **id** parameter used here is **INavigationItem's id** property.

```typescript
isPinned(id: string): boolean { ... }
```

The user can either pin or unpin an result item.  If the item is pinned (made as favourite), it would get added to the home screen.  The user can also unpin an item from either the search list and it would be removed from the home screen or use the option **'X'** as in the below image to delete the item.

When the user wants to **add** a navigation item as favourite item, below method is called.

```typescript
pin(item: IFavorite): Promise<boolean> { ... }
```

When the user wants to **remove** a navigation item as favourite, below method is invoked.

```typescript
unpin(item: IFavorite): Promise<boolean> { ... }
```

 ![image.png](/Public-documentation/images/image-1e9ab818-c985-4085-91e5-7c4ac11496df.png)

If the user does a **long press** on the favourite item,  they would get the option **'X'** on the icon.  Upon clicking the **'X'** on the favourite item, it would be removed from the home screen.  To remove the **'X'** symbol, the user can click anywhere on the screen and the icon would return to normalcy.

 ![image.png](/Public-documentation/images/image-89a1beaa-b9aa-4837-b4a1-319ac91a0e6f.png)

A simple sample component using **FavoritesService** is as below:

```typescript
import { FavoritesService } from '../../services/favorites.service';

export class ExampleComponent {

    const resultItem: IFavorite;

    constructor(private favoritesService: FavoritesService) { }

    loading(): void {
        this.favoritesService.load().then((favorites: IFavorite[]) => {
            console.log('Did load items and the count is ', favorites.length);
        }).catch((error) => {
            console.log('Error occurred ', error);
        });
    }

    searching(searchString: string): void {
        this.favoritesService.search(searchString).then(results: IFavorite[]) => {
            console.log('Did fetch items for searched string and the count is ', results.length);
        }).catch((error) => {
            console.log('Error occurred ', error);
        });
    }

    pinning(resultItem: IFavorite): void {
        this.favoritesService.pin(resultItem).then(() => {
            console.log('Successfully added as favorite'):
        }).catch((error) => {
            console.log('Error occurred ', error);
        });
    }

    unpinning(resultitem: IFavorite): void {
        this.favoritesService.unpin(resultItem).then(() => {
            console.log('Successfully removed as favorite'):
        }).catch((error) => {
            console.log('Error occurred ', error);
        });
    }

    isFavorite(navigationItem: INavigationItem): boolean {
        return this.favoritesService.isPinned(navigationItem.id);
    }

}
```

