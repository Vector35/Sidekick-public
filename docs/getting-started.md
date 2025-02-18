# Getting Started

Welcome to Binary Ninja Sidekick. This document will get you up and running and show you the main features of the Sidekick plugin. For more detailed information, check out the [User's Guide](guide/guide.md).

## Purchase a Sidekick Plan

Most features of the Sidekick plugin are powered by the Sidekick service, which requires an active plan to access. Click [here](https://sidekick.binary.ninja/plans) to purchase a plan that best fits your needs.

!!! note

    When purchasing a plan, you will need to sign in to your Sidekick account. If you do not have a Sidekick account, you will be prompted to create one, or you can create one [here](https://sidekick.binary.ninja/sign_in).

## Sidekick Plugin Installation

The installation process is straightforward and takes only a few minutes.  You can install the Sidekick plugin using the Plugin Manager.

!!! note

    The plugin has been well tested using the version of Python packaged with Binary Ninja, which is currently Python 3.10. By default, Binary Ninja will install the plugin using this version of Python, except for Linux users, which defaults to the latest version available on the system. For Linux users, we recommend configuring Binary Ninja to use Python 3.10. If you decide to configure Binary Ninja to use a separate Python virtual environment, see [Setting Up a Virtual Environment](environment.md).

### Installing the Plugin

Installing the Sidekick plugin is easy.  Launch the Plugin Manager by selecting `Plugins->Manage Plugins` from the main menu. From the Plugin Manager search for "Sidekick" and locate the Sidekick plugin.  Then click the `Install` button.

![Plugin Manager Install Sidekick](images/plugin_manager_install_sidekick.png)

!!! note

    The Sidekick plugin has several package dependencies that may take a few minutes to install. Restart Binary Ninja after installation of the plugin is complete.

### Updating the Plugin

#### Binary Ninja 4.2.5814 and Later

If an update for the installed Sidekick plugin is available, then choose one of the following methods for updating the Sidekick plugin:

* Plugin Manager: Launch the Plugin Manager by selecting `Plugins->Manage Plugins` from the main menu. From the Plugin Manager search for "Sidekick" and locate the Sidekick plugin. If an update is available, then click the `Update` button.

![Plugin Manager Update Sidekick](images/plugin_update_plugin_manager.png)

* Automatic Notification: On plugin startup, Sidekick automatically checks for updates. If one is available, then Sidekick asks you if you want to install it. Click `Yes`. Once the update is complete, then you will need to restart Binary Ninja.

![Auto Update Sidekick](images/plugin_update_auto.png)

#### Before Binary Ninja 4.2.5814

If an update is available, then complete the following steps to update the plugin:

* Launch the Plugin Manager
* Locate the Sidekick plugin
* Click `Uninstall`
* Restart Binary Ninja
* Launch the Plugin Manager
* Locate the Sidekick plugin
* Click `Install`

### Configuring the Plugin

#### Set the API Key

To set your Sidekick API Key:

* Open the Settings tab within Binary Ninja from the `Binary Ninja->Preferences->Settings` menu
* Search for `sidekick.api_key`
* Copy one of your API keys from your Sidekick account to the `Sidekick API Key` setting

!!! note
    You can find the API keys in your Sidekick account [here](https://sidekick.binary.ninja/account#api-keys)

Alternatively, the first time you launch the Sidekick plugin, you will be prompted to enter your Sidekick API key. If you provide an API key at this point, then it will get saved to your Settings.

## Quick Start

### Connecting to the Sidekick Service

The plugin will connect to the Sidekick service using the API key value in the `sidekick.api_key` setting.  If an API key is not provided, then you will not be able to access the Sidekick service.

!!! note
    All Sidekick features that do not rely on access to the Sidekick service are available to use for free. Refer [here](guide/guide.md#sidekick-service) for more information on which features require access to the Sidekick service.

### Sidekick Service Connection

You can configure the Sidekick plugin to connect to/disconnect from the Sidekick service. To switch the Sidekick plugin between the connected (online) and disconnected (offline) status, click the Sidekick status in the status bar at the bottom of the Binary Ninja window and select Connect/Disconnect.

![Sidekick Status](images/status_bar.png)

### Basic Usage

#### **Sidekick Analysis Workbench Sidebar**

The Sidekick Analysis Workbench Sidebar provides an interface for creating, modifying, and running scripts that blend both the capabilities of Python code and large language models to perform a wide variety of program analysis tasks.

![Analysis Workbench](images/analysis_workbench.png)

Try running the existing example script named "High-Level Functions" and click `Run`. This particular script outputs results to an Index named "High-Level Functions", which can be viewed in the Sidekick Indexes Sidebar.

![Run Analysis Workbench Script](images/analysis_workbench_run_script.png)

Try describing a new analysis task and pressing `Enter`, which will open a new script editor. Sidekick will generate an initial version of the script based on your analysis task description.

![Run Analysis Workbench Script](images/analysis_workbench_describe_task.png)
![Run Analysis Workbench Script](images/analysis_workbench_script_editor.png)

(Note: In this example, the script uses the `LLMOperator` class to request a large language model to perform a given task based on an initial prompt and an input Binary Ninja object (e.g. `Function`).)

The script editor also comes with the Sidekick Coding Assistant to provide you a chat-like interface to incrementally revise the script to do what you want.

![Run Analysis Workbench Script](images/analysis_workbench_coding_assistant.png)

Once you are satisfied with the script, try running it by clicking `Run`. Since this script outputs results to an index named "CSV Processing Functions", open the "CSV Processing Functions" index within the Sidekick Indexes Sidebar to view them.

![Run Analysis Workbench Script](images/analysis_workbench_run_script_in_editor.png)

Provide us with feedback on how things went by selecting `Submit Feedback...` from the hamburger menu.

![Run Analysis Workbench Script](images/analysis_workbench_submit_feedback.png)
![Run Analysis Workbench Script](images/analysis_workbench_feedback_dialog.png)


!!! note

    Feedback is only collected for non-commercial plans or commercial-plan users that have opted-in for data collection.

#### **Sidekick Indexes Sidebar**

The Sidekick Indexes Sidebar manages a set of indexes for the current binary. Each index contains a table of items in the binary (e.g., functions, instructions, strings, etc.) that are added by scripts from the Analysis Workbench. By default, when opening a binary for the first time, the Indexes Sidebar does not contain any indexes.

![Default Indexes](images/indexes_default.png)

Try adding an index by running one of the example scripts from the Analysis Workbench (e.g. High-Level Functions). To do this, open the Analysis Workbench Sidebar, enter "High" in the search box, select the "High-Level Functions" script, and click `Run`. Once the script completes, open the Sidekick Indexes Sidebar, select "High-Level Functions" from the indexes drop-down combobox, and view the entries in the table.

![High-Level Functions Index](images/indexes_high_level_functions.png)

!!! note

    Sidekick legacy indexer scripts (from Sidekick 1.x) can been converted to scripts in the Analysis Workbench. Any legacy indexer scripts stored in a user's Binary Ninja Database (BNDB) or User Directory can be converted by selecting the appropriate `Import Indexer Scripts` action from the Sidekick Plugin main menu.

![Import Indexers](images/import_indexers.png)

#### **Sidekick Suggestions Sidebar**

Once you have selected a function to investigate, use the `Sidekick Suggestions` sidebar to get suggestions for improving the clarity of the current function.

Request Sidekick to make suggestions for you, or choose specific suggestions types yourself

![Suggestions](images/suggestions_make.png)

Review suggestions and accept the ones you want to apply

![Suggestions](images/suggestions_results.png)

Sit back and watch Sidekick apply them

![Suggestions](images/suggestions_apply_all.png)

#### **Code Insight Map View**

The `Code Insight Map View` is a call-graph oriented view centered on a selected function and includes items only from the index topics.  This view allows you to quickly visualize the calling relationships between functions and their index topics to aid program comprehension.

Select the Code Insight Map view from the View drop-down menu

![Code Insight Map](images/code_insight_map.png)

Enable/disable displayed topics

Adjust Call Depth sliders to expand/collapse the call graph context of the given function
#### **Sidekick Assistant Sidebar**

The Sidekick Assistant Sidebar provides a chat interface to interact with the Sidekick Assistant for a given scope of functions. These conversations are stored for easy reference.

![Sidekick Assistant](images/notebook.png)

Ask a question about the current function

![Sidekick Assistant Ask Question](images/notebook_ask_question.png)

Navigate to another function and ask a question about that function

![Sidekick Assistant Add Second Function](images/notebook_add_second_function.png)

Add a private note to the page that does not get sent to the Sidekick Assistant

![Sidekick Assistant Add Note](images/notebook_add_note.png)

#### **Sidekick Investigations Sidebar**

The Sidekick Investigations Sidebar provides an interface for launching topic-specific investigations and documenting those findings for a given function. Currently, Sidekick offers a set of pre-defined investigations such as manpage-like information, instances of use-after-free, SQL injections, NULL pointer dereferences, and more.

![Sidekick Investigations](images/investigations.png)

Launch an investigation

![Sidekick Manpage Investigation](images/launch_investigation.png)

Edit findings

![Sidekick Edit Investigation](images/investigations_edit.png)

For a complete description of Sidekick's features, see the [User's Guide](guide/guide.md).

#### **Documentation View**

!!! note
    This feature will be deprecated in a future release.

The `Documentation View` provides a description of the current function very much in the style of a traditional man page. Sidekick will automatically generate documentation based on the function code; however, you are able to edit and/or extend this content as you wish.

Select the Documentation View from the View drop-down menu

![Selecting Documentation View](images/doc_view_default.png)

Generate documentation

![Generating Documentation](images/doc_view_results.png)
