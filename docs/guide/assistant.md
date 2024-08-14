# Assistant

The Sidekick Assistant provides a simple chat interface to capture interactions with the Sidekick AI Assistant in a per-binary collection of pages.

Each message in the page contains a link to the location in the binary that was active when the message was added for additional context and quick navigation. Clicking on a message on the page will navigate the current view to the location linked to that message.

As new functions are visited that are associated with messages on the page, the scope of the code that the Sidekick Assistant is aware of for that page is expanded. This enables the Sidekick Assistant to answer questions pertaining to multiple functions. The Sidekick Assistant automatically requests the amount and level (e.g. disassembly, IL) of code necessary to complete a request.

Users may add/delete pages to/from the Notebook. Each message on the page can be edited and/or removed.

## Selecting Pages

To select a page, click on the drop-down list of pages and select the desired page

## Adding Pages

To add a page, click on the `New Page` button or select `New Page` from the hamburger drop-down menu

## Renaming Page Titles

To rename a page title, select `Rename Page` from the hamburger drop-down menu

!!! note

    New pages are assigned a default page title. If the page title has not been set by the user, then after the first response to a message request completes, the page title is automatically set to a value relevant to the content of that request and response.

## Deleting Pages

To delete a page, select the desired page from the drop-down list of pages and select `Delete Page` from the hamburger drop-down menu

## Truncating Pages

The message history within a page can be truncated in order to delete all subsequent messages after a selected message. To truncate a page after a selected message, right-click on a message and select `Truncate`

## Sending Messages

Messages are sent to the Assistant for response. To send a message to the Assistant for response, enter a message in the message box and perform any of the following actions:

- Press `Return`
- Click on the `Send a Message` button
- Select `Send Message` from the hamburger menu

## Recording Private Notes

Notes are items on the page that are not sent to the Assistant for response. To record a note on the page, enter a message in the message box and perform any of the following actions:

- Press `Control + Return` (`Command + Return` on MacOS)
- Select `Record Note` from the hamburger drop-down menu

## Adding New Lines

To add a newline to a Message or Note, press `Shift + Return`

## Editing Messages/Notes

Messages/Notes can be edited. To edit a message/note, right-click the message/note and select `Edit`. In the `Edit Message` window (that pops up), apply edits and click `Accept`

## Deleting Messages/Notes

Messages/Notes can be deleted from the page. To delete a message/note, right-click the message/note and select `Delete`.

## Copying Message Text

To copy a selection of text within the message history, select the text to copy and perform any of the following actions:

- Press `Control + C` (`Command + C` on MacOS)
- Right-click the selection and select `Copy Text`

To copy an entire message within the history, right-click the message and select `Copy Text`

## Running Python Code

The Assistant is able to generate Python code that can be run directly in Binary Ninja's Python Console. To run the Python code that the Assistant generates in the message history, right-click the Python code text box and select `Run Code in Python Console`

## Search Messages

To search for content within messages of the current page, enter a search term in the `Search messages...` text box

## Navigating to Message Location

Each message is linked to the location in the binary that was active when the message was added. In order to navigate to that location in the binary, click on the message or right-click on the message and select `Go to Address`

## Append Message to Function Comment

To append a message to the Function Comment for the function associated with the message, right-click and select `Append to Function Comment`

## Append Message to Function Documentation

To append a message to the documentation of the function associated with the message, right-click and select `Append to Documentation`.

!!! note
    The message is appended to the `ADDENDUM` section of the documentation that can be viewed in the `Documentation View` or `Investigations Sidebar` for the associated function.

## Create Assistant Page for Current Address

To create a new page for the current address, select `Create Assistant Page for Current Address` from the `Plugins->Sidekick` menu.

!!! note

    This operation creates a new (empty) page named "<function_name\>:<address\>", where <function_name\> is the name of the current function and <address\> is the current address.
