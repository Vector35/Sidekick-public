# Code Insight Map

The Code Insight Map is a call-graph oriented view focused on a selected function. The graph is comprised of nodes that represent the selected function and its calling ancestor and descendant functions.

Each node in the Code Insight Map contains only items pertaining to the index selected for display from the set of indexes for the current binary. This allows the user to quickly obtain a top-level understanding of a function's behavior by visualizing both the calling relationships between displayed functions and also their selected indexes.

## Opening the Code Insight Map

The Code Insight Map is a separate view within Binary Ninja. To open the Code Insight Map, select `View -> Code Insight Map` from the main menu at the top of the window or click on the view drop-down menu in the current view frame and select `Code Insight Map`.

## Adding/Removing Nodex (Indexes)

From the `Nodes` drop-down combo-box, click on an available index to select/deselect it for display.

(Note: Indexes available for display in this combo-box are populated from the Sidekick Indexes. To add/remove indexes from the Sidekick Indexes, refer to [indexes](indexes.md).)

## Adding/Removing Edges

From the `Edges` drop-down combo-box, click on an available index to select/deselect it for display.

(Note: Indexes available for display in this combo-box are populated from the Sidekick Indexes. Sidekick will use the edge information contained in the selected indexes to create edges between nodes in the Code Insight Map. To add/remove indexes from the Sidekick Index, refer to [indexes](indexes.md).)

## Adjusting the Call Depth

The size of the Code Insight Map can be configured by adjusting the call depth of the ancestor/descendent nodes of the selected function using the the Up/Down arrow controls. This allows the user to better manage the amount of information displayed.

## Navigation

When using the default navigation settings, double-clicking on an item within a node will navigate the view to focus on the function containing the item clicked. (Note: If the Code Insight Map view is in a sync group with another view, then all other views in that sync group will also navigate to the selected item.)

When using the pinned navigation setting (by selecting the Pin icon at the top of the Code Insight Map view), double-clicking on an item within a node will not navigate the Code Insight Map view away from the currently pinned function. However, if the Code Insight Map view is in a sync group with another view, then all other views in that sync group will navigate to the double-clicked item. This behavior allows the user to navigate to locations in other views while keeping the Code Insight Map view pinned on a selected function. This is particularly helpful when wanting to examine the details of an item within the Code Insight Map without having to navigate away from the context displayed in the Code Insight Map.

(Note: If the Code Insight Map pin is deselected and the Code Insight Map view is part of a sync group, then the Code Insight Map view will navigate to the function containing the location currently selected for that sync group.)

## Create a Component from the Current Functions

To create a component from the set of functions currently displayed in the Code Insight Map, right-click on the map and select `Create Component`
