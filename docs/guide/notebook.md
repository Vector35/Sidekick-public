# Notebook

A Notebook is a per-binary collection of pages that captures interactions with the Sidekick assistant through a simple chat interface. Each page contains a history of interactions with the Sidekick assistant.

Each message in the page contains a link to the location in the binary that was active when the message was added for additional context and quick navigation. Clicking on a message on the page will navigate the current view to the location linked to that message.

As new functions are visited that are associated with messages on the page, the scope of the code that the Sidekick assistant is aware of for that page is expanded. This enables the Sidekick assistant to answer questions pertaining to multiple functions.

Users may add/delete pages to/from the Notebook. Each message on the page can be edited and/or removed.

## Selecting Pages

To select a page from the Notebook, select the desired page from the drop-down list of pages

## Adding Pages

To add a page to the Notebook, select `New Page` from the hamburger drop-down menu in the Sidekick Notebook sidebar

## Renaming Pages

To rename a page in the Notebook, select `Rename Page` from the hamburger drop-down menu in the Sidekick Notebook sidebar

## Deleting Pages

To delete a page from the Notebook, select the desired page from the drop-down list of pages and select `Delete Page` from the hamburger drop-down menu

## Truncating Pages

The message history within a page can be truncated in order to delete all subsequent messages after a selected message. To truncate a page after a selected message, right-click on a message and select `Truncate`

## Sending Messages

Messages are sent to the Sidekick assistant for response. To send a message to the Sidekick assistant for response, enter a message in the chat box and press `Return` or click on the `Send a Message` button

## Recording Private Notes

Notes are items on the page that are not sent to the Sidekick assistant for response. To record a note on the page, enter a message in the chat box and press `Control + Return` (`Command + Return` on MacOS) or select `Record Note` from the hamburger drop-down menu

## Adding New Lines

To add a newline to a Message or Note, press `Shift + Return`
## Editing Messages/Notes

Messages/Notes can be edited. To edit a message/note, right-click the message/note and select `Edit`. In the `Edit Message` window (that pops up), apply edits and click `Accept`

## Deleting Messages/Notes

Messages/Notes can be deleted from the page. To delete a message/note, right-click the message/note and select `Delete`.

## Copying Message Text

To copy a selection of text within a Notebook page message, select the text to copy, right-click the selection, and select `Copy Text`

## Running Python Code

Through the chat interface, Sidekick is able to generate Python code that can be run directly in Binary Ninja's Python Console. To run the Python code that Sidekick generates in the message history, right-click the Python code text box and select `Run Code in Python Console`

## Adding Python Code to Sidekick Index

Through the chat interface, Sidekick is able to generate Python code that can be added to the Sidekick Index as a Sidekick Index Topic script. To add the Python code that Sidekick generates in the message history, right-click the Python code text box and select `Add Code to Sidekick Indexes`

## Search Messages

To search for content in the messages within the current page, enter a search term in the `Search messages...` text box and press `Return`

## Navigating to Message Location

Each message on a Notebook page is linked to the location in the binary that was active when the message was added. In order to navigate that location in the binary, click on the message or right-click on the message and select `Go to Address`

## Append Message to Function Comment

To append a message to the Function Comment for the function associated with the message, right-click and select `Append to Function Comment`

## Append Message to Function Documentation

To append a message to the documentation of the function associated with the message, right-click and select `Append to Documentation`. (Note: The message is appended to the `ADDENDUM` section of the documentation that can be viewed in the `Documentation View` for the associated function.)

## Create Notebook Page for Current Address

To create a new Notebook page for the current address, select `Create Notebook Page for Current Address` from the `Plugins->Sidekick` menu.

Note: This operation creates a new (empty) page named "<function_name\>:<address\>", where <function_name\> is the name of the current function and <address\> is the current address.
