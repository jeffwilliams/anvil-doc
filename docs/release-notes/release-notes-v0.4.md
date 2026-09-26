# Version 0.4 Release Notes 

## Features Added

* The About command now prints a list of which SSH connections have host passwords or keyfile passwords set
* Added the command `Dbg Psrv off` to disable the debugging server
* Added the `l` operation to range statements which is like `x`, but prints the entire line that matches the regular expression. For example, `!l/word/` will match all lines that contain "word".
* Added the table [alias] to the `settings.toml` configuration file that allows the definition of command aliases. See the [Configuration Reference](../reference/config.md#table-alias) for details
* Added API notifications when a file is opened for the first time
* On MacOS, add additional keyboard shortcuts using the Command key:
    * allow Command+C, +X and +V to perform copy, cut and paste respectively
    * allow Command+S to save, Command+Z to undo, Command+R to redo, and Command+A to select all text
* For better support of Apple 2-button mice, allow Left-Click+Command to act as a middle click (execute)
* Make Shift + Left-click on column layout boxes show only basenames in tags. This helps to see what files are open in a column when they have very long names
* Created application bundles for MacOS
* Mac binaries are now codesigned so shouldn't get killed with signal 9 on starting. However they still require unquarantining using `xattr -d com.apple.quarantine anvil`
* The awin command now handles carriage-returns by moving to the beginning of the line. This should make running commands that show progress using carriage-return such as scp more pleasant

## Defects Fixed

* Upgraded GIO to version 0.7.1 to fix a memory leak in keypress events
* The performance of range statements has been improved for statements that select and print matches from a large file
* Improve performance when typing near the end of large files
* Improve the performance when deleting text from large files
* Fixed the help text for the Tint command
* Don't add `Clr` to the tag of `+Errors` windows if they already have it
* Change the ANSI color scheme when a new file is loaded
* Fix crash when a window is created in a non-visible column
* Handle keypresses from Enter on the number pad
* Make triple-clicking on quote characters properly select the quoted text and the quotes themselves
* Fix race condition where clients were sent a notification through the API that a file was Put, but the file was still being written asynchronously and may not have been written to disk yet. This is most visible when using the awatch extras command to compile files.
* Fix issue where pressing Ctrl would execute the last executed command from another window. 
* Compile against unreleased GIO to fix crash when loading GNU unifont




