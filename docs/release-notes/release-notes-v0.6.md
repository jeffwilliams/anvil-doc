# Version 0.6 Release Notes 

## Features Added

* Make the file path of window tags absolute by default. This makes selecting part of a window's path and acquiring it more intuitive
* Column-relative window paths. See the [tutorial](../tutorials/column-rel-paths.md) for more information
* When the Alt key is held while executing a command using either middle-click, CTRL-T, or CTRL-Enter then the +Errors window is cleared before the command output is printed to it.
* Now when a window with unsaved changes is deleted using Del, instead of printing a warning to the +Errors window, the Del in the tag is instead changed to Del!.
* In range statements, allow escapes like \n in the c,i,a, and s commands
* The awatch command now allows the user to edit the command in the +watch window, or add new commands to be run on file changes. Any lines beginning with `%` followed by a space will have the `%` and space stripped off and will be executed as a command.

* When Kill is run with no arg, kill the job started most recently instead of the most old
* Make the Cmds\* command enclose the commands with lozenges
* Disable typing in selections. Now if there are selections present and you hit any key, the selections
    are deleted and replaced with that rune. Backspace and delete simply delete the selections.
* Added the keyboard shortcut CTRL-Q acquire the object under the cursor
* Save the working directory in dumpfiles and change to that directory when they are loaded
* Added the Alias command
* Added support for Elastic Tabstops using the [Elastic](../reference/commands.md#elastic) command
* Added the [Wrap](../reference/commands.md#wrap) command. "Wrap off" can be used to disable line wrapping in a primitive way
* Make double-click at start of line also select trailing newline
* Add the `--version` option.
* Improve awin:
    * Implement more advanced stripping of terminal escape sequences
    * Use websocket api to receive notifications rather than polling over http, so that there is less latency between entering a command in Anvil and it being executed.
    * Add flags to allow disabling or enabling allocation of a pseudo-terminal or on windows, the pseudo-console
    * Make the default on Microsoft Windows to disable pseudo-console allocation. This avoids the problem where Windows uses excessive terminal escape sequences
    * Add check to ensure that we only execute text entered at the end of the body if it ends in a newline
    * Attempt to use non-blocking reads from the process/terminal, and fallback to blocking if the system doesn't support it. This reduces latency when reading from the executed process
    * Add extra debugging logs to help display process output
    * Optimize technique used to append text to window body while taking into account carriage returns embedded in the process output. The new method uses fewer interactions with Anvil over the API and so has improved latency.



## Defects Fixed

* Fixed crash in rune cache
* Fix event handling when app unfocused then focused
    
    This commit fixes an issue where if Anvil was unfocused then focused
    again by left-clicking, it would make a selection from the previous
    location of the cursor to where the new click occurred.
    
    The issue is that Windows when Anvil is refocussed, multiple events are delivered at once to
    Anvil, and one of these is a zero-distance drag event. Zero distance
    drags are normally ignored, but because all events occur quickly they
    are all delivered to Anvil as a queue at once, and in the blockeditable
    code it would loop over each event and process them, but then later
    perform the draw. However the mouse event processing is actually
    performed during the draw as a deferred event because we need to have
    layed out the text to be able to tell what character the mouse click
    occurs on. By deferring the events only the last was processed, and so

* When the text in a tag is changed programatically the cursors and selections are preserved. This change fixes the behaviour of the awin command, where when it repeatedly updates the window while the user is typing in the tag the cursor keeps getting moved to the beginning of the tag. 
* Swap middle and right button actions on win layout box. Now right mouse maximizes the window, and middle mouse minimizes other windows, like how Acme behaves.
* Fix an issue where if the text in a column tag wraps, and you click in the second or later line of the tag, the cursor is moved to a place farther right than where the click occurred 
* Fix a crash in range statements, specifically with the `-` operation.
* Fix an issue where when you scroll up using the mousewheel or scrollbar in a window, the first line of the body might not be displayed
* When Get is performed in a Tag, don't move the cursor to the beginning of the tag
* Make Acq support line/col numbers suffix on filenames
* Range statements: handle multi-byte runes in c,i,a commands properly. Multi-byte runes in the c, i and a statements were counted as multiple runes. If a statement resulted in multiple ranges being changed, later changes were performed later and later in the document than where they should have been performed.
* Allow styling +Errors window text colors
* Use proper os path separator in About
* Fix bug introduced earlier in this pre-release where the flashed errors window tag used the wrong color for the basename
* Fix the coloring of basenames in +Errors tags
* Make CTRL-? work on Windows
* When the layout box of a window was clicked to grow it a few lines, sometimes it would grow many lines at once instead of a few.
* Fix crash when you close all the columns and run awin
* Ensure Get is shown in directory tag instead of Put
