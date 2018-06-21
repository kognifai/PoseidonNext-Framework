# Description

Home page is the default landing page/view in Poseidon.   It contains a default icon that enables you to add your favourite items on this page.  The following is the initial page:

 ![image.png](https://github.com/kognifai/PoseidonNext-Framework/blob/master/.attachments/image-86f8e543-b5af-44e3-be89-20d94b8c8a71.png)

Adding favourite item on the home page is facilitated by **FavoritesService**.

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

We need to import the **FavoritesService** as following:

```typescript
import { FavoritesService } from '../../services/favorites.service';
```
It is injected as below:

```typescript
export class FavoitesTestPageComponent {
    constructor(private favoritesService: FavoritesService) { ... }
}
```

When you click/press the **Add Favorite** button, it opens an interface where you can search/filter items that you want to add/remove as a favourite item.  By default the search interface is prepopulated with all navigation items.  The navigation items are fetched using the following method. 

```typescript
load(): Promise<IFavorite> { ... }
```

The user can click anywhere on the screen to dismiss the search interface.

When you search, it returns a list  of matching queried string and below is the method which is invoked.

```typescript
search(query: string): Promise<IFavorite> { ... }
```
The items which are already favourites are listed in yellow colour.  To check if a navigation item is already a favourite or not, we use the below method.  The **id** parameter used here is **INavigationItem's id** property.

```typescript
isPinned(id: string): boolean { ... }
```

The user can either pin or unpin a result item.  If the item is pinned (made as favourite), it gets added to the home page.  The user can also unpin an item from the search list and it is removed from the home page or use the option **'X'** as in the following image to delete the item.

When the user wants to **add** a navigation item as a favourite item, the following method is called.

```typescript
pin(item: IFavorite): Promise<boolean> { ... }
```

When the user wants to **remove** a navigation item, the following method is invoked.

```typescript
unpin(item: IFavorite): Promise<boolean> { ... }
```

 ![image.png](https://github.com/kognifai/PoseidonNext-Framework/blob/master/.attachments/image-1e9ab818-c985-4085-91e5-7c4ac11496df.png)

If the user does a **long press** on the favourite item,  you get the option **'X'** on the icon.  Upon clicking the **'X'** on the favourite item, it is removed from the home page.  To remove the **'X'** symbol, you can click anywhere on the screen and the icon  returns to normal.

 ![image.png](https://github.com/kognifai/PoseidonNext-Framework/blob/master/.attachments/image-89a1beaa-b9aa-4837-b4a1-319ac91a0e6f.png)

A simple sample component using **FavoritesService** is as following:

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

