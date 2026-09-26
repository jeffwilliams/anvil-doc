# Version 0.3 Release Notes 

## Features Added

* Fonts sizes now take into account the display DPI. This makes the default font sizes more readable on high-DPI displays.
* Binary packages for MacOS 64-bit are now built. Thanks to Orcus for providing a development system to test the x86-64 version. The binaries are not yet codesigned, so some MacOS versions may have problems running the binaries.
* CTRL-Scrollwheel now adjusts the font size.
* The new command Fuzz has been added. Fuzz performs a case-insensitive fuzzy search in the body of the window for lines that match the arguments to the command. As the arguments to the Fuzz command are typed, the search is executed and the results are shown on the fly in a separate +Live window. To terminate the list of arguments to Fuzz, surround the command in lozenges, like: ◊Fuzz TERM◊.
* After typing with one cursor, pressing the Escape key selects the recently typed text.
* Allow the `/execute` API to optionally execute in the context of a specific window, rather than the editor.
* Add the Pic command to set the background picture of a window body. See the help for more details (execute ◊[Help Pic](../reference/commands.md#pic)◊).
* High-level client APIs have been added to the Go API package.
* A new extras command `adiff` has been added that can diff the contents of the bodies two windows. Mark the two windows by typing `&&1` and `&&2` in the windows to diff, then run `adiff`. It will open a new +Diff window with the diff. You can run `adiff clr` to remove the marks.

## Defects Fixed

* Don't consider a path remote unless it contains a colon. Some paths that contained '@', for example, were considered remote paths and Anvil would try to connect to them over SSH when they were acquired.
* When programs that were run remotely over SSH by Anvil and that connected to the Anvil API and requested a websocket, the request could hang because of a deadlock between the Go SSH and HTTP packages. This fix applies the proposed patch in review by Nicola Murino from [https://go-review.googlesource.com/c/crypto/+/562756](https://go-review.googlesource.com/c/crypto/+/562756). Anvil now relies on a version of go-x-crypto with this fix applied found here: github.com/jeffwilliams/go-x-crypto. Once the official fix is released we can change the dependency back to the official go-x-crypto again.
* Fix the handling of opening local files. When a local file that doesn't exist is opened, don't complain. Fix how the absolute path to local files are created relative to the window path.
* The `ssh.env` table in the settings.toml file which lists additional user-defined environment variables has been renamed to `env` and is now also applied to locally run programs.
* Stop printing syntax highlighting lexer errors to standard output on startup.
* Fixed issue where performing Del on a maximized window makes the column appear empty and the other windows in the column that were hidden when the maximized window was present are not shown.
* After a command was run with input piped to it (the command was prefixed with |) then the window was not redrawn.
* GIO was updated to version 0.6.0
* Behave more gracefully when killing a remote process
* Fix issue where when opening a second remote file for a host where there is already an ssh connection being opened but not yet established can hang the UI
* Handle overlapping selections better
* Make CTRL-T determine the text to be executed like middle-click, rather than just accepting a selection
* Fix crash in expression handling
* Allow compiling on mac


