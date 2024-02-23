# Introduction

The Suggestions sidebar enables users to request suggestions from Sidekick that are focused on improving the clarity of the current function. The types of suggestions that Sidekick offers include:

* [Recover Structures](./structures.md)
* Eliminate Dead Stores
* [Name Variables](./variables.md)
* [Name Structures and Fields](./fields.md)
* [Name Functions](./function_naming.md)
* [Describe Function](./briefs.md)
* [Name Function Callees](./function_naming.md#name-callee-functions)

As Sidekick generates suggestions, users are able to review and accept or reject them.

The following sections detail the actions that users can take within the Suggestions sidebar. To get the most use out of the Suggestions features, read [Tips on Using Suggestions](./suggestions.md#tips-on-using-suggestions)

## Requesting Suggestions

Users have two primary methods for requesting suggestions: general and specific. Suggestions returned by Sidekick are added to the suggestions tree and organized by function within the Sidekick Suggestions sidebar. Suggestions will accumulate within the tree until applied or cleared by the user.

### General Suggestions

When requesting general suggestions, Sidekick will determine what suggestions to make based on the current state of the function. Sidekick makes suggestions in stages according to the following order of categories:

1. Code Suggestions - These are suggestions that impact IL generation (e.g., structure recovery, dead store elimination, variable types, and parameter counts)
2. Name Suggestions - These are suggestions that impact names of things (e.g. variable names, type names, subroutine names, etc)
3. Metadata Suggestions - These are suggestions that add information about things (e.g., comments, documentation)

As users iteratively request general suggestions, Sidekick will generate other suggestion types during its progression through each suggestion stage.

To request general suggestions for the current function, perform any of the following actions:
- Click the `Make suggestions for: <current_function>` button
- Select `Make suggestions for: <current_function>` from the hamburger menu

### Specific Suggestions

Users can also request Sidekick to generate suggestions of a specific type. To request suggestions of a specific type for the current function, select from the following items in the hamburger menu:

- `Suggest Function Name`
- `Suggest Function Comment`
- `Suggest Variable Names`
- `Suggest Struct/Field Names`

These actions are also available from the `Plugins->Sidekick` menu.

(Note: Structure and field name suggestions will not be generated if [Structure Recovery](./structures.md) has not been performed first.)

## Applying Suggestions

Suggestions returned by Sidekick in the suggestions tree can be applied in the following ways:

- To apply all suggestions in the tree (for all functions), perform any of the following actions:
    - Select `Apply All` from the hamburger menu in the Sidekick Suggestion sidebar
    - Select `Apply All Suggestions` from the `Plugins->Sidekick` menu
- To apply a selection of suggestions, select each suggestion you want to apply (using `Cntrl + Click` or `Shift + Click` depending on the desired selection scope) and perform any of the following actions:
    - Click on the `Accept selected suggestions` button
    - Right-click and select `Apply`
- To apply all suggestions for the current function, perform any of the following actions:
    - Select `Apply and Suggest for: <current_function>` from the hamburger menu in the Sidekick Suggestions sidebar. (Note: If auto-suggestions are disabled, then Sidekick will not make suggestions after applying suggestions for the current function.)
    - Select `Apply Suggestions for Current Function` from the `Plugins->Sidekick` menu
    - Press `F12`

## Clearing Suggestions

Suggestions returned by Sidekick in the suggestions tree can be cleared in the following ways:

- To clear all suggestions in the tree (for all functions), perform any of the following actions:
    - Select `Clear All` from the hamburger menu in the Sidekick Suggestions sidebar
    - Select `Clear All Suggestions` from the `Plugins->Sidekick` menu
- To clear a selection of suggestions, select each suggestion you want to clear (using `Cntrl + Click` or `Shift + Click` depending on the desired selection scope), right-click, and select `Clear`
- To clear all suggestions for the current function, select `Clear and Suggest for: <current_function>` from the hamburger menu. (Note: If auto-suggestions are disabled, then Sidekick will not make suggestions after clearing suggestions for the current function.)

## Auto-Suggestions

Sidekick supports the ability to generate suggestions automatically when a user dwells at a given location for a period of time (configurable in Settings). When enabled, the user simply clicks on a location in a function, stays there for the configured time, and then Sidekick starts to generate suggestions for that function. After a user applies all of the suggestions for the current function, then Sidekick will generate another set of suggestions based on the updated function. This iterative process repeats until no more suggestions can be made.

The `sidekick.suggestions.auto_suggest_dwell_time` setting controls the dwell time (in seonds) for auto-suggestions. Set to 0 to disable auto-suggestions.

## Saving Suggestions

When saving a BNDB, all suggestions currently in the suggestions tree are stored in the BNDB.  When re-opening a saved BNDB, suggestions stored in the BNDB are reloaded in the suggetions tree.

## Tips on Using Suggestions

The following lists several ways to use Suggestions more easily and effectively:

1. Tired of all the clicking to just accept what Sidekick has suggested for the current function? Then simply press `F12`.
2. Speaking of `F12`, when combined with the auto-suggestion feature, the sequence of visiting a function, automatically receiving suggestions, and quickly applying them via `F12` is an effective workflow to quickly reverse engineer a function.
3. Sidekick tends to suggest better names for things in the function after all of the callees in the function have been named. Sometimes Sidekick will make this suggestion for you, but if not, then just select `Name Callee Functions` from the `Plugins->Sidekick` menu. (Note: This operation can take a while to complete based on the number of unnamed callee functions.)
4. Not getting a specific type of suggestion from Sidekick? Manually request the specific suggestion type from the hamburger menu in the Suggestions sidebar.
5. If you clear a suggestion, then Sidekick will no longer make a suggestion of that type automatically (using any of the `Make Suggestions for: <current_function>` actions). This is one reason why you may not be getting a specific type of suggestion from Sidekick. You must manually request it for that function after that point.
6. Not getting suggestions for structure and field names? Make sure that you've run structure recovery first by selecting `Recover Structures` from the `Plugins->Sidekick` menu.