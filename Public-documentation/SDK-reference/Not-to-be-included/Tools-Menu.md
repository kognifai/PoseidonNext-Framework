# Description
The Tools Menu is an Angular component. It is the right-hand side menu in Poseidon. It imports items from [```ToolsMenuService```](https://kognifai.visualstudio.com/Kognifai%20Core/_wiki/wikis/PoseidonNext.wiki?wikiVersion=GBwikiMaster&pagePath=%2FPoseidon%20Next%2FSDK%20documentation%2FTools%20Menu%20Service&_a=edit), displays them, and lets them be expanded or collapsed.


## Definitions
- **Tools menu**: the right-aligned sidebar in Poseidon, toggled by the following button - ![image.png](.attachments/image-72f21012-8af3-45f4-8574-67e4f8cd36ea.png) . It shows list of items (buttons) provided by the tools menu service.
- **Tools menu item:** represents button in the tools menu with label, associated action and possibly list of child items that are displayed nested under the parent. 
- [Tools Menu Service](/Poseidon-Next/Public-documentation/SDK-reference/Tools-Menu-Service): Angular service provided by the platform so that applications can register tools menu items. 

# Usage

## Visualising

### Tools Menu Item component:
This component receives an array of ```ToolsMenuItem``` objects and visualises them in a list of html buttons with label, icon. If an item has child items attached to it, there is a functionality for expanding and collapsing. An example of this component can be seen on [Tools Menu Service](/Poseidon-Next/Public-documentation/SDK-reference/Tools-Menu-Service)

**Collapse method:**
```typescript
itemClicked(item: ToolsMenuItem, event: any): void
```
### Tools Menu component:
This component is a wrap around the list of Tools Menu Items.
It adds a header, and makes sure the user is aware when there are no Tool Menu Items available.