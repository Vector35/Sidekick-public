# Binary Ninja Sidekick

Sidekick is an AI-powered service that takes reverse engineering to the next level. Sidekick augments the [Binary Ninja](https://binary.ninja/) desktop application, providing new capabilities that help users analyze and understand binary programs.

## Features

### Deep Analysis

* [Analysis Console](analysis/analysis_console.md): Interact directly with the Sidekick Analysis Assistant to perform complex analysis tasks.
* [Analysis Indexes](analysis/analysis_indexes.md): Store and display items in the binary to easily reference your analysis results.
* [Code Insight Map](analysis/code_insight_map.md): View relationships between items in your Analysis Indexes to help you discover and understand high-level functionality of the program.

### Smart Automation
* [Automation Workbench](automation/automation_workbench.md): Using interactive assistance, develop and refine scripts that blend both Python code and the capabilities of large language models to automate repeated tasks.

### Improved Decompilation

* [Decompilation Suggestions](decompilation/suggestions.md): Generate suggestions to improve Binary Ninja's decompilation for better code clarity and readability.
* [Structure Recovery](decompilation/structures.md): Recover definitions for structures, rather than just displaying dereferenced pointers.
* [Naming](decompilation/naming.md): Produce meaningful names for functions, variables, structures, and fields.
* [Comments](decompilation/comments.md): Offer explanations of the code to quickly understand and document it

### Artifacts
* [Documentation View](artifacts/documentation.md): Automatically produce editable, man page-like descriptions of functions to help document your progress.

### Management
* [Change Log](management/change_log.md): Track changes made to the binary through the Analysis Assistant, such as renaming functions, adding comments, and more.

## Notable Changes

### Investigations

The Investigations sidebar (from Sidekick 2.0) has been removed and replaced by the more capable Analysis Console. Previously, Investigations explored a fixed number of topics and could only examine a single function. Now, the Analysis Console can perform multi-step investigations of any topic, exploring potentially the entire binary.

## Sidekick Service

Most features within the Sidekick plugin require access to the Sidekick service; however, there are some features that do not and are available to all users. The following table lists the features of Sidekick and their dependency on the Sidekick service:

| Feature                       | Sidekick Service Dependency                          |
| -----------                   | ------------------------------------ |
| Structure Recovery            | Does *not* require service access. However, function components must be manually created for this feature to work without service access. |
| Component Creation            | Requires service access |
| Variable Naming           | Requires service access |
| Structure/Field Naming    | Requires service access |
| Function Naming           | Requires service access |
| Code Selection Comments   | Requires service access |
| Function Comments         | Requires service access |
| Automation Workbench            | Requires service access to create and build scripts automatically. Requires service access to execute scripts that use LLMOperators configured with a Sidekick service model. Requires service access to execute scripts that call Sidekick service APIs (e.g. symbol classifiers used by legacy indexer scripts). All users can manually create scripts that do not use LLMOperators and run them without service access.|
| Analysis Console                 | Sending messages and automatic naming of session titles require service access. Recording notes does *not* require service access. |
| Analysis Indexes                       | Does *not* require service access. Users can manually create and run Analysis Workbench scripts that output content to an index without service access. |
| Code Insight Map              | Does *not* require service access |
| Documentation View        | Automatic documentation generation requires service access. Manual generation does *not* require service access. |
