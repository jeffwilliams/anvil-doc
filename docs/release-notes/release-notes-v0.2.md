# Version 0.2 Release Notes 

## Features Added

* [Websocket support](../reference/api.md#websocket-notifications) for sending API notifications has been added. This helps clients of the API from having to poll to check for new notifications. 
* API notifications are now sent when a file is put or closed.
* Export the environment variable `ANVIL_DIR` that contains the directory in which Anvil is running.
* Text can now be selected by holding shift and pressing the arrow keys, home, and end. Thanks to Alex Schroeder for implementing this!
* Added a new command 'C' to [Range Statements](../reference/range-statements.md) that copies the ranges to the clipboard.
* Executing with an argument can now also be done by pressing and holding Middle-Mouse then pressing the CTRL key.
* Allow configuring the [SSH TCP connection timeout](../reference/config.md#table-ssh) used for remote editing, with a default of 5 seconds
* Executing OS commands prefixed with '+' force the command to be [run locally](../tutorials/command-execution.md#forcing-local-execution), even if the window is a remote window
* Pressing the Escape key when multiple cursors are present reduces to one cursor
* When CTRL-Enter is used at to execute the current line at the end of a +Errors window, make new line
* Added the Anvil extra command [aedit](../reference/useful-tools.md#aedit), which allows using Anvil in the EDITOR environment variable
* Added the extra command [awatch](../reference/useful-tools.md#awatch), which runs commands when a file in the current directory is Put
* Added the extra command [anvsshd](../reference/useful-tools.md#anvsshd), an SSH server


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

