# Description
The Navigation Sidebar is a visual component, that visualises a list of Navigation items listed in the left-hand side menu in Poseidon. It provides developers with access to visual components ```NavigationItemComponent``` and ```SidebarComponent```.
[Navigation Service](/Poseidon-Next/Public-documentation/SDK-reference/Navigation-Service) a required dependency for the component to be used.

## Definitions
- **Navigation Item Component**: Visualises a single ```NavigationItem``` as a clickable part of the Navigation menu wtih label and icon. If the ```NavigationItem``` has children, it has a caret icon, indicating the item can be expanded
- **Navigation Sidebar Component**: The left-aligned sidebar in Poseidon. It shows a list of ordered items, provided by the [Navigation Service](/Poseidon-Next/Public-documentation/SDK-reference/Navigation-Service)

# Usage

## Visualising

### Navigation Item Component
This component visualises the object as a clickable part of the Sidebar; It uses an icon defined by the ```NavigationItem``` iteself or uses a default one.
If the ```NavigationItem``` has children items, it gets a caret icon, representing the user's ability to expand it.
This component uses ```NavigationService``` as a dependency, in order to mark a single ```NavigationItem``` as active and visually separate it from the rest. If no active item is selected, the **Home** application will be the default active item.

### Sidebar Component
Visualises the collection of ```NavigationItem``` objects, which it gets from ```NavigationFilterPipe```.
