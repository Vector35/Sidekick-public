# Binary Ninja Sidekick

Sidekick is an AI-powered service that takes reverse engineering to the next level. Sidekick augments the [Binary Ninja](https://binary.ninja/) desktop application, providing new capabilities that help users analyze and understand binary programs.

## Features

### Quick Search and Navigation

* [User-Defined Indexes](indexes.md): Use natural language to describe items in the binary you're looking for and automatically find and display them. *(Note: This feature does not fully require Sidekick service access. See [below](#sidekick-service) for details.)*
* [Code Insight Map](code_insight_map.md): View relationships between items in your indexes to help you discover and understand high-level functionality of the program. *(Note: This feature does not fully require Sidekick service access. See [below](#sidekick-service) for details.)*

### Improve Code Clarity

* [Structure Recovery](structures.md): Recover structure definitions for code, rather than just displaying dereferenced pointers. *(Note: This feature does not fully require Sidekick service access. See [below](#sidekick-service) for details.)*
* [Variable Naming](variables.md): Receive suggestions for variable names to help you understand the purpose of parameters and variables in functions.
* [Structure and Field Naming](fields.md): Receive suggestions for structure and field names to improve your understanding of the data structures in your binary.
* [Function Naming](function_naming.md): Receive suggestions for function names that summarize what the code does.
* [Function Comment](briefs.md): Receive suggestions for a comment that briefly summarizes a function to quickly understand and documents its purpose.
* [Function Callee Naming](function_callee_naming.md): Generate names for all functions called by the current function to focus your analysis and get better names.

### Interactive Assistance

* [Notebook](notebook.md): Interact with Sidekick through a chat interface to answer your questions about the binary. *(Note: This feature does not fully require Sidekick service access. See [below](#sidekick-service) for details.)*

### Program Structure Analysis

* [Component Creation](components.md): Identify groups of related functions that correspond to compilation units and arrange them hierarchically, making it easier to understand the binary program's structure.

### Documentation

* [Documentation View](documentation.md): Automatically generate editable, man page-like descriptions of functions to help document your progress. *(Note: This feature does not fully require Sidekick service access. See [below](#sidekick-service) for details.)*
* [Code Comments](code_comment.md): Make sense of cryptic code by inserting a comment that automatically summarizes it


With Sidekick, you have access to these new capabilities that streamline the reverse engineering process, enabling you to do it all more quickly and efficiently!

## Sidekick Service

Most features within the Sidekick plugin require access to the Sidekick service; however, there are some features that do not and are available to all users. The following table lists the features of Sidekick and their dependency on the Sidekick service:

| Feature                       | Sidekick Service Dependency                          |
| -----------                   | ------------------------------------ |
| Indexes                       | Some indexer scripts that we provide require service access to run successfully. However, all users can manually create, add, and run their own indexer scripts without service access. |
| Code Insight Map              | Does *not* require service access |
| Structure Recovery            | Does *not* require service access. However, function components must be manually created for this feature to work without service access. |
| Component Creation            | Requires service access |
| Variable Naming           | Requires service access |
| Structure/Field Naming    | Requires service access |
| Function Naming           | Requires service access |
| Code Selection Comments   | Requires service access |
| Function Comments         | Requires service access |
| Documentation View        | Automatic documentation generation requires service access. Manual generation does *not* require service access. |
| Notebooks                 | Sending messages requires service access. Recording notes does *not* require service access. |