# Pre-Release Version Release Notes 

## Warning

This version modifies the contents of dumpfiles in a way that is not backwards compatible. **Dumpfiles created in older versions of Anvil cannot be loaded in this version.**

## Preview Features

* **aterm: a terminal emulator for Anvil.** The aterm command is similar to awin but with proper terminal emulation for unices and color support. Executing `aterm COMMAND` opens a new window in Anvil that interacts with the command COMMAND. If COMMAND consists of multiple arguments (like `git push`) separate the command using -- (i.e. aterm -- COMMAND).

    Keystrokes are passed through to the command. If you want to use the Anvil keybindings in the window for manipulating the text, first use the Detach command to disconnect keystrokes from the executed program. Use Attach to attach again. When atteched you can copy text using CTRL-Insert, Cut using CTRL-Delete and Paste using SHIFT-Insert. 
    
    The Hist command prints the terminal history to an +Errors window. Executing the Send command writes the text arguments of Send to the command. Sendln does the same except appends a newline.
    
    When the command terminates, executing the Restart command in that window will cause aterm to execute the command in the same window and allow interaction with the new instance. 
    
    You can forceably terminate aterm and the command by executing Del!.

* **Trays: editable popup windows.** Trays are created or made visible by executing text that begins with § and is followed by non-space characters. You can type § in Anvil using CTRL-S. 

    For example, typing §test and executing it using middle-click makes an empty tray visible. Type text in the tray and to close it click outside of the tray or hit Escape.
    
    Trays act similar to the tag in a window, but displayed in an arbitrary place. Executing most commands in a tray act on the window body, like how commands in a tag act.
    
    Trays have different scopes: file, session and global. File scoped trays are unique to the directory of the window in which they are open. That is, if you opened a file-scoped tray §menu in a window for a file `/tmp/file1.txt` and then opened it in a window for a file `/tmp/file2.txt` the same menu would get opened since the files are in the same directory `/tmp`. But if you opened §menu in a window for `/home/user/file1.txt` it would be a different tray. Trays opened from a window body are file-scoped trays by default.
    
    Session scoped trays are unique to the current Anvil session. A session scoped tray with the same name opened anywhere in the current Anvil session (OS window) will open the same content. Trays opened from a window tag are session-scoped trays by default.

    Global scoped trays are the same across all Anvil sessions. A global scoped tray with the same name opened in any Anvil session will open the same content. 
    
    The scope of trays can be changed by adding a prefix to the tray name. Use 'g' to make a tray global-scoped, i.e. §g:commands. Use 's' to make a tray session-scoped, i.e. §s:stuff. Use 'f' to make it file-scoped.

    The Dump command causes the trays to be saved. File scope trays are saved to a subdirectory .anvil in the directory of the file where the tray was created. This allows you to store tray contents along with the files that contain references to them. Session scope trays are saved to the dumpfile. Global scope trays are saved to the directory 'trays' under the Anvil [configuration directory](config.md).

    A handy keybinding to use with trays is the following:
    
    `map C-Space execute-args §s:default`
    
    This allows you to use CTRL-Space to pop up a tray that's shared between all the windows in your Anvil session. It's useful for storing text or commands applicable to what you're currently working on.

* **Offscreen columns.** It's now possible to have columns in the layer that are not visible, and are logically left and right of the visible columns. The visible columns are like a viewport into the sequence of columns. 

    To move a column offscreen, drag the layout box of a column offscreen to the left or right. You can scroll the viewport of visible columns to the left and right (making hidden columns visible and hiding columns at the trailing edge of the viewport) using SHIFT-Scrollwheel or the Left and Right commands.
    
    To increase and reduce the column viewport size (make more or fewer columns visible at once) use CTRL-SHIFT-Scrollwheel or the Narrow and Widen commands. As a special case, if you widen the viewport and there are no hidden columns then a new column is created on the right and the viewport widened to view that new column.

* **Compound commands.** This change allows you to execute a compound command in Anvil that consists of intermixed OS and Anvil commands separated by semicolons (;). Commands are split into internal and external (OS) commands such that a series of external commands separated by ';' are executed as one contiguous command. The commands are forced to be executed synchronously; the previous completes before the next starts. 

* **Override syntax highlighting using configuration files.** Files added to the syntax subdirectory under the Anvil configuration directory are loaded as if they were [Syn lexer files](https://github.com/jeffwilliams/syn/tree/master/lexers/embedded). This allows you to do things like add extra keywords to an existing supported filetype by copying the existing lexer and adding new keyword handling.

* **Pinned windows.** The Pin and Unpin commands can be used to pin a window to a specific layer. When a window is pinned, if output is added to the window autonomously (say, from a long running command sending output to a +Errors window) and a different layer is active, the window is not moved to the current layer. Pinned windows show a dot in the center of the layout box.

* Added the Unsel command to unselect all selections.
* Add the "Dbg Mouse" command to enable logging mouse events to the debug logs.
* Allow $$ in substitutions (like aliases). $$ is replaced with a literal $.
* Added the arenum extra program. arenum is a program to which you pass a simple lisp-style program on the command line that renumbers the values in Anvil selections based on your expression.
* Added the adiffplumb extra program. This is meant to be executed from a plumbing rule of the form: 

    ```
    match @@ -\d+,\d+ \+\d+,\d+ @@
    do adiffplumb
    ```

    When you have a diff open in Anvil and plumb the part of a line in a diff that begins and ends with '@@' it will Acquire the file and line affected by that chunk of the diff.
    
* anvsshd: the log timestamps now include microseconds
* Added the command `Ssh clear` to close all cached open SSH connections. This is useful if you changed shell initialization files on the remote host and want to reconnect such that the settings are applied.
* Make remote commands faster by setting environment variables asynchronously.
* Added APIs for managing tinted text regions and added support for setting the background color of tinted text via API.
* Added Mvlyr command to move a layer in the layer stack.
* Added the Expr command to execute a raw range statement. This is useful in compound commands.
* Rename aclangd to alsp and add support for gopls.

## Defects Fixed

* Fix typed characters not appearing on Mac.
* Upgraded to GIO v0.10.1 to fix copy-paste issue on Windows. See [GIO issue 682](https://todo.sr.ht/~eliasnaur/gio/682)
* Make the regions created by the Tint command handle overlapping better
* Change SHIFT-RightMouse for execute to CTRL-RightMouse
* Improve performance of range expressions
* Fix bug where lowest window in column can be rendered below screen when stacked
* When executing a remote command using the On command and also holding shift, the remote +Errors window is now cleared like when a command is executed similarly without using On.
* Properly calculate the pixel coordinates of text index when index is after last rune in file
* When the text in the Tag is changed by Anvil the selections in the Tag are unselected. This fixes a bug where if you have a modified file (so Put is shown in the tag) and select some text to the right of Put, and then save the file using CTRL-S, the text in the tag shifts but the selection is not shifted.
* Fix possible crash when scrolling
* Dump and load the tab string: the string inserted by the tab key which was set using the Tab command.
* Make more commands find files relative to window path, such as Dump, SaveStyle, LoadStyle, LoadPlumbing, and Keymap Load.
* Improve memory usage by better sharing text shapers
* Fix possible goroutine leak in file handling
* Fix the filename shown in the range statement P command
* Preserve user-added text at the bottom of directory windows when the window size changes or the window is refreshed using Get. Any text that is added at the bottom of a directory window that is separated from the directory contents lines by at least one empty line is preserved.
* Fix bug in the Go API where GET errors were not handled
* When build.sh is run and the local repo has been converted to a go workspace, preserve the go workspace
* Refactor command execution to avoid race conditions with the help system
* Fix typo in Keymap command help ('Keymap load' was listed as 'Keymap add')
* aad: throttle requests to Anvil's API latency to avoid locking Anvil when it recovers from being swapped out