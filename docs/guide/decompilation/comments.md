# Comments

Comments is a feature that analyzes the code and automatically generates summary of its behavior that can be applied as a comment.

## Functions

Sidekick can generate and insert a comment that summarizes the behavior of the entire function, which is applied as a function comment at the start of the function.

### How it works

Sidekick submits a representation of the function to the Sidekick service, which uses a language model to generate a summary of the function.

### How to use it

You can request Sidekick to generate a suggestion for a function comment by following [these instructions](./suggestions.md#requesting-suggestions). This allows you to review the suggested function comment before applying it (using [these instructions](./suggestions.md#applying-suggestions)).

Alternatively, you can request Sidekick to automatically generate and insert a function comment by selecting `Add Function Comment` from the `Plugins -> Sidekick` main menu.

## Inline Code

Sidekick can generate and insert comments that summarize or explain a highlighted selection of code. (Currently only High Level IL and Pseudo C are supported.)

To use this feature, highlight a section of code and select `Add Comment for Selected Lines` from the `Plugins -> Sidekick` menu (or alternatively press `Shift + C`).

Comments are applied inline above the code selection.
