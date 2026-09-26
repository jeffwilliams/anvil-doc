# Version 0.6.3 Release Notes

## Features Added since 0.6

* Upgrade to GIO 0.8.0 to allow compiling with newer Go versions
* Add support for BSD: OpenBSD, NetBSD, FreeBSD
* When acquiring a relative path from the tag, if the position of text being acquired is within the window path, a treat the path as relative to column's or editor's current working directory, rather than the window's path. 
* CTRL+Scrollwheel no longer changes the font size. Instead, a new command [Fontsize](../reference/commands.md#fontsize) was added for this.
* Allow the cursor shape to be defined in style files. See the `CursorProg` setting in the [style.js reference](../reference/config.md#stylejs)
* The cursor in the [Acme](../themes/index.md#acme) theme has been made smaller so as not to overlap text
* Added the commands [Dbg Flame ...](../reference/commands.md#dbg-flame) which can be used to display a flame graph of Anvil's CPU profile
* Added the [Getall](../reference/commands.md#getall) command to execute Get on all windows
* Update the [Only](../reference/commands.md#only) command to accept the optional arguments 'above' (close all windows below the current) or 'below' (close all windows above)
* Improve the performance of text layout
* Make file completion print candidates to directory-specific +Errors window instead of the global +Errors window. That way acquiring them works properly.
* Commands can now be completed using CTRL-H
* The [asm command](../reference/useful-tools.md#asm) was modified to add the `list` subcommand
* Reorganized the source code
* Added support for stackable keymaps. See the [tutorial](../tutorials/keymaps.md) and [reference](../reference/keymaps.md).
* Added support for layers. See the [tutorial](../tutorials/layers.md) and [reference](../reference/layers.md).
* Add extra glyphs from Noto such as runes, arrows, and other symbols to the built-in font

## Defects Fixed since 0.6

* When you close all the columns, don't show a white background
* Clean up SVG icon. The SVG file `editor/misc/icon/anvil-icon.svg` is now just the Anvil icon, and the file `anvil-icon-design.inkscape.svg` contains the design iterations and source material that was in that file previously.
* Fix formatting of error messages in ado and awatch
* Fix crash when the Alias command is run when there is no configuration file created
* Icon was missing from in the windows .exe
* When the Fuzz command was run from the +Errors window it would make many +Live windows
* The New command ignored line numbers at the end of filenames. For example, `New file:20` would open file and leave the cursor at the first line instead of the 20th.
* The Acq command tries plumbing before parsing out the line and column numbers from the filename
* Add the missing right border on scrollbars
* Make HTML syntax highlighting highlight tags
* Prevent scrolling text off the body so that its not visible (thanks user xlii)
* Prevent opening empty file when ALT+Right clicking on empty space at end of file (thanks xlii)
* Sign all MacOS binaries including the extras, not just anvil itself
* Update documentation of Alias command
* Fix possible crash
* Fix crash when executing commands using CTRL+Enter from editor tag
* Cleaned up the Help command 
* If GIO dependencies are not installed, Anvil could silently exit. Added code to print the error that GIO reports in this situation to help troubleshoot why Anvil didn't start.
* Fix scrolling when selecting near the top and bottom of windows
* The awin command will now stream the output from commands to the Anvil window rather than waiting for all the command output to be printed. This makes awin seem more responsive.
* Made CTRL-Left and CTRL-Right more granular
* Added additional logging for SSH interaction


