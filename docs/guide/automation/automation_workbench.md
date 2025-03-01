# Automation Workbench

The Automation Workbench is a feature that allows users to create, refine, and run scripts that blend both Python code and the capabilities of large language models (LLMs) to automate repeated tasks.

## Concepts

### Scripts

At the most fundamental level, a script in the Automation Workbench is Python code. The script executes within an environment that has built-in access to both the Binary Ninja Python API and a set of Sidekick Python APIs that include the following functionality:

- Perform a task carried out by a large language model
- Read from and write to the Sidekick Analysis Indexes
- Display progress

Since scripts are just Python code, you can do anything with them that you can with Python, provided you import and install the necessasary dependencies into your Python environment. Since scripts have access to the full Binary Ninja Python API, anything you can do within Binary Ninja using the Python API, you can do with a script (including modifying the binary).

### LLM Operators

Scripts support the execution of an object called an `LLM Operator` that performs a given task using an LLM. When executed, the LLM Operator applies the described task to an input Binary Ninja object type and includes any additional context needed based on the type of object passed. For example, if you wanted an LLM to determine if a given function accesses encrypted strings, then you would do the following:

- Define and configure an LLM Operator with the relevant information for that task, including a name for the LLM Operator (e.g.  `does_reference_encrypted_strings`)
- Instantiate an `LLMOperator` object using the name of your defined LLM Operator
- Pass a Binary Ninja Function object when calling the `LLMOperator` object

The following code is an example of how this would look in a script:

```
references_strings = LLMOperator("does_reference_encrypted_strings")

for func in bv.functions:
    result = references_strings(func)
```

### LLM Operator Definitions

LLM Operators must be defined and configured in order to use them within scripts. More precisely, when a script instantiates an `LLMOperator` object with a given LLM Operator name, an LLM Operator definition must exist with that name.

LLM Operator definitions include the following information:

- Name: Unique identifier used to reference the LLM Operator. This value is passed to the `LLMOperator` object during initialization.
- Task Description: Textual high-level description of the task for the LLM Operator
- Model Name: Name of the model (from the [LLM Operator Model Catalog](./llm_operator_model_catalog.md)) used for this LLM Operator
- Prompt Definition:
    - Input Variables: JSON description of variables required by the prompt instructions. Variables can reference pre-defined items from the binary such as code, data, strings, libraries, file info, and memory map. They can also reference user-defined variables passed as keyword arguments when calling the `LLMOperator` object.
    - Instructions: Plain text description of the instructions for the LLM to follow for the task. This description can reference input variables that are replaced with the relevant content when the `LLMOperator` object is called at execution time.
    - Output Schema: JSON description that defines the format of the desired output generated by the LLM.

Each LLM Operator definition for a given script has a separate tab (titled `Operator: <llm_operator_name>`) within the Script Editor, which can be used to view and edit its definition.

### LLM Operator Models

Each LLM Operator can be configured to use a specific LLM model (by name), which must be defined and enabled in the [LLM Operator Model Catalog](./llm_operator_model_catalog.md). To open the LLM Operator Model Catalog, select `Configure LLMs...` from the hamburger menu.

## Scripting Assistant

The Automation Workbench includes an AI-powered Scripting Assistant that provides interactive assistance for creating and refining scripts based on user request. The Scripting Assistant performs the following tasks:

- Interpret the user's requests within the context of the conversation and generate Python code that implements the given request
- Determine what LLM Operators are necessary for the described task and automatically generate the necessary LLM Operator definitions and their uses in the script
- Inspect the script's execution output as part of the conversation context (so that it can refine the script based on the output)


## Scripts Tab

The Automation Workbench contains the `Scripts` tab that has the following modes of operation:

- Search Mode: Allows users to search for existing scripts and run, edit, or delete them; or describe a task to generate a new script
- Edit Mode: Allows users to create, refine, and run scripts with optional support from the Scripting Assistant

### Search Mode

The `Scripts` tab of the Automation Workbench opens in `Search Mode` by default. This mode provides the following UI elements:

- Search text box for entering a search term to find existing scripts, or enter a task description for a new script
- List of existing scripts that can be sorted by title, last modified, or last executed
- Hamburger menu for additional actions:
    - New Script: Create a new script
    - Sort by: Sort the list of scripts by title, last modified, or last executed
- `Run` button for executing selected scripts

#### Actions

The `Search Mode` provides the following actions:

| Action | Description | Steps |
| --- | --- | --- |
| Search | Filters existing scripts based on a search term | Enter a search term in the search text box |
| New Task Script | Creates a new script from a task description, switches to Edit Mode, and prompts the Scripting Assistant to generate script code for the task | Enter a new task description in the search text box and press `Enter` |
| Run Script(s) | Executes the selected script(s) | Select script(s) and press `Cmd + Enter` (on MacOS) or `Cntrl + Enter` (on Windows/Linux); or right-click the selected script(s) and select `Run Script` |
| Edit Script | Opens the selected script in Edit Mode | Double-click the script, select the script and press `Enter`, right-click the selected script and select `Edit Script`, or select the script and press `Cmd + ]` (on MacOS) or `Cntrl + ]` (on Windows/Linux) |
| Delete Script(s) | Deletes the selected script(s) | Select script(s), right-click it, and select `Delete Script` |
| New Empty Script | Creates a new empty script | Click the hamburger menu and select `New Script` |
| Sort by | Sorts the list of scripts by title, last modified, or last executed | Click the hamburger menu and select the desired sort option |


!!! note

    When new scripts are added or imported into the script database, the list of scripts may not automatically update. One method for updating them is to enter any search term and then clear the search box.

!!! note

    Scripts are executed sequentially from a queue as they are selected for execution by the user. Consequently, the user can queue up a script for execution while another is currently executing.



### Edit Mode

The `Scripts` tab of the Automation Workbench can be switched to `Edit Mode` by selecting an existing script and performing one of the following actions:

- Double-click the script
- Select the script and press `Enter`
- Right-click the selected script and select `Edit Script`

`Edit Mode` provides the following UI elements:

- Left arrow button for returning to `Search Mode`
- Title text box for setting the title of the script
- `Run` button for executing the script code
- `Cancel` button for canceling the execution of the script code (only while running)
- `Revisions` drop-down combobox for viewing revisions of the script code
- `Main` tab for editing the script code
- `Operator: <llm_operator_name>` tab(s) containing a form for editing the LLM Operator (if included, one for each defined LLM Operator)
    - Name: Unique identifier used to reference the LLM Operator
    - Task Description: Textual high-level description of the task for the LLM Operator
    - Model Name: Name of the model used for this LLM Operator
    - Prompt Definition:
        - Input Variables: JSON description of variables required by the prompt instructions
        - Instructions: Plain text description of the instructions for the LLM to follow for the task
        - Output Schema: JSON description that defines the format of the desired output generated by the LLM
- `Scripting Assistant` chat widget for interactions with the Scripting Assistant:
    - Message box for entering a request to the Scripting Assistant
    - Chat history for viewing the conversation with the Scripting Assistant
    - Context Menu:
        - `Revert script to here`: Reverts the script code to the revision associated with the selected message
- Output widget for displaying separate tabs for `Output` and `Execution Details` for an execution
- Hamburger menu for additional actions:
    - `Show Chat`: Displays/hides the Scripting Assistant chat widget
    - `Show Output`: Displays/hides the output widget
    - `Delete Script`: Deletes the current script
    - `Clone Script`: Makes a copy of the current script
    - `Show Snippet Code`: Displays the code necessary to run the current script from a code snippet
    - `Configure LLMs...`: Opens the LLM Operator Model Catalog
    - `Code Preferences...`: Sets coding preferences for the script (stored in the Binary Ninja setting `sidekick.workbench.code_preferences`)
    - `Submit Feedback...`: Opens a dialog for submitting feedback on the Automation Workbench

#### Actions

The `Edit Mode` provides the following actions:

| Action | Description | Steps |
| --- | --- | --- |
| Return to Search Mode | Returns to Search Mode | Click the left arrow button at the front of the title text box, or press `Cmd + [` (on MacOS) or `Cntrl + [` (on Windows/Linux) |
| Set Script Title | Sets the title of the script | Enter the new title in the title text box |
| Edit Script Code | Edits the script code | Enter text in the `Main` code editor |
| Edit LLM Operator | Edits an LLM Operator definition | Select an `Operator: <llm_operator_name>` tab to edit, and apply edits in the form |
| View Revisions | Views the revisions of the script code | Click the `Revisions` drop-down combobox and select a specific revision |
| Save Revisions | Saves revisions of the script code | Revisions are automatically saved when the script is created, the Scripting Assistant updates the code, the `Run` or `Build` action is selected, or the user switches to Search/Edit Mode |
| Run Script | Executes the current script code | Click the `Run` button. During execution of the script code, output will be displayed in the `Output` tab of the Output widget.|
| Cancel Execution | Cancels the execution of the current script code | Click the `Cancel` button (only while running) |
| Send Message | Sends a message containing a request for the Script Assistant to complete based the conversation context | Enter a request in the Message box and press `Enter` or click the `Send a message` button |
| Revert Script to Here | Reverts the script code to the revision associated with the selected message in the chat history | Right-click a message in the chat history and select `Revert script to here` |
| Clone Script | Makes a copy of the current script | Click the hamburger menu and select `Clone Script`. This action copies the current script with a new title and opens the new script in Edit Mode. |
| Delete Script | Deletes the current script | Click the hamburger menu and select `Delete Script`. This action deletes the script and switches to Search Mode. |
| Show Snippet Code | Displays the code necessary to run the current script from a code snippet | Click the hamburger menu and select `Show Snippet Code`. This action opens a dialog window that contains the code necessary to run the current script from a code snippet, which includes the UUID of the script. This allows a user to run the script programmatically using the API. |
| Show Chat | Displays/hides the Scripting Assistant chat widget | Click the hamburger menu and select `Show Chat` |
| Show Output | Displays/hides the output widget | Click the hamburger menu and select `Show Output` |
| Configure LLMs | Opens the LLM Operator Model Catalog | Click the hamburger menu and select `Configure LLMs...` |
| Set Code Preferences | Sets coding preferences for the script | Click the hamburger menu and select `Code Preferences...`. In the `Code Writing Preferences` dialog window that opens, enter instructions that capture the preferences you want and click `Save`.|
| Submit Feedback | Opens a dialog for submitting feedback on the Automation Workbench | Click the hamburger menu and select `Submit Feedback...`. This action opens a Feedback dialog window. Select whether or not the script accomplished your task and provide details on what worked or didn't work. Click `Submit` when finished. |

## Execution Monitor Tab

The Automation Workbench contains the `Execution Monitor` tab that displays the execution history of scripts. This tab includes a table that lists details for each script execution, including the following columns:

- Status: Indicates the current status of the script execution
- Started: Timestamp for when the script execution started
- Finished: Timestamp for when the script execution finished
- Script: Title of the script that was executed
- Binary: Name of the binary that the script was executed on

### Actions

The `Execution Monitor` tab provides the following actions:

| Action | Description | Steps |
| --- | --- | --- |
| Cancel Execution | Cancels the execution of a script that is currently running | Right-click the script execution entry and select `Cancel Execution` |
| Clear History | Clears the execution history table | Right-click the `Execution History` table and select `Clear History` |


## Handling Script Errors

Sometimes scripts will encounter errors during execution, which are displayed in the Output tab within `Edit Mode`. The Scripting Assistant has access to this output to help refine the script and resolve errors, but it needs to be instructed to do something about it. When this happens, send a message to the Scripting Assistant to let it know about the error (e.g. "An error occurred" or "Please fix that error").
