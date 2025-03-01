# Analysis Console

The Analysis Console is a feature that allows users to interact directly with Sidekick's Analysis Assistant to perform complex analysis tasks. The Analysis Assistant is able to:

- Interpret and analyze both the code and the content within the conversation
- Search for items in the binary using the [Binary Ninja Query Language (BNQL)](bnql.md)
- Store and retrieve analysis data using Sidekick [Analysis Indexes](analysis_indexes.md)
- Search, create, register, and run tools to assist in completing a user’s request
- Edit the binary

The Analysis Console maintains a collection of "sessions" with the Analysis Assistant. Each session contains a history of interactions with the Analysis Assistant. The Analysis Assistant performs best if the scope of a session is limited to a specific topic or set of functions. If you wish to switch topics, you should create a new session for that topic.

In order to complete a user's request, the Analysis Assistant decides what information and [tools](#tools) are needed for the task and may also ask for additional information or clarification from the user. The Assistant may also provide suggestions or ask questions to help the user understand the binary better. During its response, the Analysis Assistant provides a detailed explanation of the steps it took to complete the request. Each action it takes is recorded in the session history and can be expanded to view the details.

## Binary Ninja Query Language (BNQL)

The Analysis Assistant uses the Binary Ninja Query Language (BNQL) to search for items in the binary. BNQL is a powerful query language that allows users to search for items in the binary using a wide range of criteria.  For more information on BNQL, refer to the [BNQL documentation](bnql.md).

Analysis Assistant messages that use BNQL list the query used to search for items in the binary. Users can copy these queries and use them to add its results as entries to an Analysis Index. To do this, refer to the [Analysis Indexes documentation](analysis_indexes.md#adding-entries).

## Analysis Indexes

The Analysis Assistant uses Analysis Indexes to store and retrieve analysis data. It serves as a working "memory" for the Assistant, allowing it to store and retrieve information as needed. Users may also direct the Analysis Assistant to access Analysis Indexes if needed. For more information on Analysis Indexes, refer to the [Analysis Indexes documentation](analysis_indexes.md).

## Tools

The Analysis Assistant maintains a set of active tools that it can use to assist in completing a user's request. Tools are scripts that are registered with the Analysis Assistant and can be run to perform specific tasks. Some tools are included by default and always active:

- `search_binary`: Search for items in the binary
- `edit_binary`: Edit the binary
- `manage_binary_index`: Manage the binary index
- `get_data_dump`: Get a data dump of the binary
- `search_tool_library`: Search the tool library
- `create_scripted_tool`: Create a scripted tool
- `register_tool`: Register a tool
- `search_extended_tool_output`: Search the extended tool output

The Analysis Assistant may create a new scripted tool to assist in completing a request. Users can also direct the Assistant to use a specific tool to complete a task.


## Actions

### Searching Sessions

To search for content in sessions, enter a search term in the `Search all sessions` text box. Results from all sessions are displayed in the Analysis Console.

To navigate to the message in its session for a given search result, hover over the result message and click the `Go to Message` button that appears.

### Selecting Sessions

To select a session, click on the drop-down list of sessions and select the desired session

### Adding Sessions

To add a session, click on the `New Session` button or select `New Session` from the hamburger drop-down menu

### Renaming Session Titles

To rename a session title, select `Rename Session` from the hamburger drop-down menu

!!! note

    New sessions are assigned a default session title. If the session title has not been set by the user, then after the first response to a message request completes, the session title is automatically set to a value relevant to the content of that request and response.

### Deleting Sessions

To delete a session, select the desired session from the drop-down list of sessions and select `Delete Session` from the hamburger drop-down menu

### Sending Messages

Messages are sent to the Analysis Assistant for response. To send a message, enter a message in the message box and perform any of the following actions:

- Press `Return`
- Click on the `Send a Message` button
- Select `Send Message` from the hamburger menu

### Recording Notes

Notes are items on the session that are not sent to the Analysis Assistant for response. To record a note on the session, enter a message in the message box and perform any of the following actions:

- Press `Control + Return` (`Command + Return` on MacOS)
- Select `Record Note` from the hamburger drop-down menu

### Editing User Messages/Notes

Use messages/notes can be edited. To edit a user message/note, hover over the message/note, click the `Edit` button that appears. In the `Edit Message` dialog that pops up, apply edits and click `Accept`.

!!! note

    This action causes the Analysis Assistant to re-evaluate the message history up to and including the edited message and provide a new response. All subsequent messages are removed from the session.

To add new lines to a user message/note, press `Shift + Return`.

!!! note

    Messages are formatted as markdown, so 2 newlines are required to create a new paragraph.

### Viewing Analysis Assistant Message Details

Some messages from the Analysis Assistant (such as tool usage) contain additional details that can be expanded to view. To view/hide these details, hover over the message and click the chevron button that appears.

Details may include additional information for the performed action, output from the tool, or error messages, useful for debugging and troubleshooting.

### Copying Message Text

To copy a selection of text within the message history, select the text to copy and perform any of the following actions:

- Press `Control + C` (`Command + C` on MacOS)
- Right-click the selection and select `Copy`

Additionally, to copy a message from the Analysis Assistant, hover over the message and click the `Copy` button that appears.

### Navigating to Message Locations

Each message (User or Assistant) is linked to the location in the binary that was active when the message was added. In order to navigate to that location in the binary, hover over the message and click on the `Go to address` button that appears.

### Retrying Analysis Assistant Messages

After reviewing a message from the Analysis Assistant, you can retry the message to get a new response. To do this, hover over the Analysis Assistant message and click the `Retry` button that appears.

### Submitting Feedback

To provide feedback on how the Analysis Assistant performed, hover over the message from the Analysis Assistant and click on the `Good response` or `Bad response` button that appears. In the `Send Feedback` dialog that pops up, provide feedback and click `Submit`.

!!! note

    Feedback is only collected for non-commercial plans or commercial-plan users that have opted-in for data collection.

### Viewing/Managing Active Tools

To view or manage the active tools, select `Tools...` from the hamburger drop-down menu. In the `Active Tools` dialog that pops up, you can view the current list of active tools.

To pin/unpin a user tool (i.e. not a system tool), click on the pin icon next to the tool name. Pinned tools are not removed from the list of active tools as the Analysis Assistant manages its limited number of active tool slots.

To remove a user tool, click on the `Remove tool` button next to the tool name.

### View Raw Session

To view the raw session content, select `View Raw Session` from the hamburger drop-down menu. The raw session content is displayed in the `Raw Session Content` dialog that pops up. This content includes the full details of the session, including the message history and other session metadata. This information is useful for debugging and troubleshooting.