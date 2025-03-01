# Structure Recovery

Structure recovery is a feature that automatically creates structure definitions for code, rather than just displaying dereferenced pointers. This helps identify the data structures in your binary.

## How it works

Sidekick first [creates a component](components.md) for the current function if one does not already exist, which is a necessary pre-requisite for structure recovery. Next, Sidekick performs an interprocedural points-to analysis within the component to identify the data structures that are used by the functions in the component.
It then uses the data structures to create structure definitions for the functions in the component.

Sidekick tries to infer more refined types for the fields.
For example, if a field takes on a small number of integer values (e.g., 0, 1, 2, 3), it will be inferred as an enum.
Or, if the only values are 0 and 1, it will be inferred as a boolean.

By default, the structs and fields are named using a simple prefix scheme (i.e., `struct_` and `field_`).
You can choose to prefix the structs and fields with the component name to make them more meaningful.
Even better, you can ask Sidekick to suggest more meaningful names using the [Structure and Field Naming](naming.md#structures-and-fields) feature.

## How to use it

To recover structures for the current component, click on the `Recover Structures` item from the `Plugins->Sidekick` menu. If a component does not exist for the current function, then Sidekick automatically creates a component for the current function.
The structure recovery operation is generally rather fast, but it could take a few moments to complete, depending on the size of the component.

When it's done, you'll see the IL updated with new structs and fields, and the types will appear in the Types sidebar.

Alternatively, when using the Sidekick Suggestions sidebar, Sidekick may suggest that you recover structures for a component.
Accepting the suggestion is equivalent to clicking on the `Recover Structures` menu item.

## How to customize it

You can customize the naming convention for structures and field names by following [these instructions](naming.md#naming-convention).

## Common questions

### What about structures that are used by multiple components?

Sidekick creates structures for each component independently.
If a structure is used by multiple components, it may be created multiple times under a different name.
This is a limitation of the current implementation, which we plan to address it in the future.
However, if you use the Structure Recovery feature one component at a time, Binary Ninja's type propagation should prevent the creation of duplicate structures most of the time.
