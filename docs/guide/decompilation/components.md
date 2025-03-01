# Component Creation

The Component Creation feature of Sidekick automatically identifies groups of related functions (think compilation units) and arranges them hierarchically, making it easier to understand the binary program's structure.

## How it works

Sidekick uses features derived from BinaryNinja's static analysis and consolidates them into a single graph that captures the relationships between functions. The graph is uploaded to the Sidekick service where it is partitioned into components, arranged hierarchically to form a tree. The tree is then displayed in the `Symbols` sidebar.

Sidekick attempts to name the components based on function names and other symbols it finds. If these features are not present in the binary, the components will be named based on their location in the binary.

## How to use it

The following methods can be used to create a component:

- To create a component for the current function, click on the `Create Component` item in the `Plugins/Sidekick` menu.
- To create a component for the set of functions displayed within a Code Insight Map, follow [these instructions](../analysis/code_insight_map.md#create-a-component-from-the-current-functions).

The operation can take a few minutes to complete, depending on the number of functions selected. When it's done, you will see the components in the `Symbols` sidebar.

## How to customize it

The component creation algorithm has several parameters that you can adjust to customize its behavior. To adjust these parameters, go to the Settings tab and locate the `Sidekick.components` section. The following options are available:

| Option | Description |
| --- | --- |
| Minimum Component Size | The minimum number of functions that a component must contain.<br>The default is 2.
| Maximum Component Size | The maximum number of functions that a component must contain.<br>The default is 50.
| Component Depth | The maximum depth of the component tree.<br>The default is 3.
| Maximum Tier Width | The maximum number of components in a tier.<br>The default is 7.
| Maximum Adjacent Distance | The maximum distance between adjacent functions in a leaf component.<br>The default is 1.

!!! note

    The default values for the component clustering options are based on our experience with the most common types of binaries. You can experiment with other values, but the results may vary depending on your binary.

You can customize the naming convention used for components by following [these instructions](naming.md#naming-convention).

## How to interpret it

The component creation process depends on the features that are available in the binary. Some binaries will have more indicators than others.  In general, the components will correspond to logical units of the program and roughly correspond to its compilation units, libraries, or subsystems.
