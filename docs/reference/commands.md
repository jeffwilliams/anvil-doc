# Command Reference

## About

Print information about the editor, including where some files are expected to be located such as:

- The configuration directory
- The settings file, and if it was loaded on startup
- The style configuration file, and if it was loaded on startup
- The SSH key directory, and a list of cached SSH connections
- The plumbing configuration file
- The API listener port, and a list of active API sessions


## Acq

`Acq` "acquires" its argument. It performs the same function that ++alt+right-button++ performs on a text object.

In Acme and Anvail parlance, "acquire" is defined as the following. First, if the word or selection matches a plumbing rule, execute that plumbing rule. If there is no matching plumbing rule, then if the word or selection is a file or directory path and there is already a window open with that path as the filename portion of its tag, change focus to that window and make it visible. If there is not already a window open for that path, open one. Finally, if a plumbing rule is not executed and the path ends in `:N`, `#C`, or `!X` then go to line N, character C, or regex X of the file.

## Alias

Usage: `Alias [<name> [<command>...]]`

`Alias` creates command aliases. If no arguments are specified it lists currently defined aliases. If `name` is specified, then that alias is removed. If `name` and `command` are specified, an alias for `command` having the name `name` is created.

An alias may contain placeholders of the form `$1` to `$9` which are replaced with the corresponding arguments to the alias when executed. The placeholder `$*` is replaced with all the arguments separated by a space. The placeholder `$$` is replaced with a literal `$`.


## Ansi

Usage: `Ansi [on | off]`

`Ansi` is used to control whether ANSI terminal color escape sequences cause coloring or not. With no argument or `on` specified it enables coloring. With the argument `off` it disables coloring.

## Clr

Clear ("delete") the contents of the window body.

## Cmds

List the most recent external commands executed.

## Cmds*

List the most recent external commands executed along with the directory they were executed in.

## Coldown

Move the current column to the layer below.

## Coldown^

Move the current column to the layer below and make that layer active.

## Cols

`Cols` lists all the columns and layers.

## Cols*

`Cols*` lists all the columns and layers verbosely (including the files in each column).

## Colup

Move the current column to the layer above.

## Colup^

Move the current column to the layer above and make that layer active.

## Cut

`Cut` deletes the last selected text sending it to the clipboard.

## Dbg

Usage: `Dbg <category>`

`Dbg` is used to run commands to help debug the internals of Anvil. Available categories to `Dbg` are:

- `ProfCpu`: Profile CPU usage. See `◊Help Dbg ProfCpu◊`.
- `ProfHeap`: Profile memory usage. See `◊Help Dbg ProfHeap◊`.
- `Goroutines`: Print all goroutines. See `◊Help Dbg Goroutines◊`.
- `Logs`: Print internal debug logs. See `◊Help Dbg Logs◊`.
- `Pid`: Print Anvil's PID. See `◊Help Dbg Pid◊`.
- `Psrv`: Start the Go pprof debug server. See `◊Help Dbg Psrv◊`.
- `Paths`: Print window paths. See `◊Help Dbg Paths◊`.
- `Flame`: Profile CPU and show flame graph. See `◊Help Dbg Flame◊`.

## Del

`Del` closes the current window.

## Del!

`Del!` closes the current window disregarding any unsaved changes.

## Delcol

`Delcol` deletes the column in which it is executed.

## Dellyr

Delete the current layer.

## Do

Usage: `Do <command>...`

`Do` executes its arguments as a command; i.e. as if the arguments were selected and executed alone. This is useful to execute commands from one window in the context of another window.

## Down

Make the layer below this one active.

## Dump

Usage: `Dump [<filename>]`

`Dump` saves the editor's state to disk: the size of the open windows and the current value of their tags. If `filename` is given, the state is written to the file named by the argument.With no argument state is written to the file `anvil.dump`. The state can be loaded using `Load`.

## Elastic

Usage: `Elastic [off]`

When run with no argument, elastic tab stops are enabled for the window body. When run with the argument `off`, elastic tab stops are disabled.

## Exit

`Exit` exits the Anvil.

## Font

Change to the next font defined in the styles.

## Fontsize

Usage: `Fontsize <N | +N | -N>`

Change the font size of the active font. This command accepts one argument. If the argument is a number, then the font size is set to that value in points. If it is `+N` or `-N` then the current font size is increased or decreased by N points respectively.

## Fuzz

Usage: `Fuzz [<terms>...]`

`Fuzz` performs a fuzzy search through the lines in the window body. The terms for the search are the arguments to the Fuzz command. The lines which match the search are written to a new window for the current directory with the suffix `+Live`.

The `Fuzz` command is special in that it can be executed dynamically as you type the search terms. If you add the string `◊Fuzz ` to the tag, then as you type the arguments after the command the search is re-executed and the results updated in the `+Live` window. You can delimit the end of the search arguments using another `◊`.

## Get

`Get` reads the contents of the path that is the leftmost text in the window tag and replaces the window body contents with it.

## Getall

`Getall` executes a `Get` on all open windows, reloading all windows.

## Goto

Usage: `Goto [<markname>]`

`Goto` sets the current cursor position in the window body to the named bookmark, created by `Mark`. If no argument is given it jumps to the bookmark `def`.

## Help

Usage: `Help [<topic>]`

`Help` shows a bit of help for the editor. With no argument it lists the main commands and a brief description. With an argument it displays information about that topic. The argument may be a command, which displays more detail about the command, or it may be another selected topic.

## Hidecol

`Hidecol` hides the current column.

## Hostpass

Usage: `Hostpass <password> <hostname> [<username>] [<port>]`

`Hostpass` is used to specify the password used to log into an SSH server. It takes between two and four arguments. The first argument is the password. The second argument is the hostname or IP address of the server. The third argument is the username for the server; if not specified the current user's name is used. The fourth argument is the TCP port number for the server; if not specified 22 is used.

## Id

`Id` prints the window ID to the `+Errors` window. Useful when using the API.

## Keymap

Usage:

```
Keymap show (def <name> | defs | stack)
Keymap load <file>
Keymap (push <name> | pop)
Keymap win (push <name> | pop | reset)
```

When run with the `show` argument, this command shows keymap information. The argument `defs` shows all defined keymaps. The `def <name>` variant shows the definition of the keymap with name `name`. The argument `stack` shows the current keymap stack, with the top being shown last.

When run with the `load` argument, load a keymap file which contains one or more keymap definitions. When run with the `push` argument, push a keymap onto the global keymap stack. When run with the `pop` argument, pop off the top keymap in the stack. The bottommost keymap is never popped.

If the first argument is `win`, then the keymap for the local window only is modified. If `win push` or `win pop` is executed and the window is using the global keymap stack, then the global keymap stack is copied to the window and a keymap pushed to or popped from that window stack respectively. `win reset` resets the window's keymap stack to be the global keymap stack again.



## Keypass

Usage: `Keypass <keyfile> <password>`

`Keypass` is used to specify the password used to decrypt an SSH private key file. It takes two arguments: the first is the ssh filename and the second is the password. This is needed when an SSH private key file is encrypted and ssh-agent is not being used.

## Kill

Usage: `Kill [<jobname>...]`

`Kill` kills all the jobs that are currently running that have names matching the arguments to the `Kill` command. If no argument is provided the first job is killed.

## Load

Usage: `Load [<filename>]`

`Load` loads the editor's state from disk as written by the `Dump` command. With an argument the state is read from the file named by `filename`. With no argument state is read from the file `anvil.dump`.

## LoadPlumbing

Usage: `LoadPlumbing [<filename>]`

`LoadPlumbing` loads the plumbing rules from a file. With one argument the plumbing is loaded from the file named by `filename`. With no argument it is loaded from [`$ANVIL_CFG_DIR/plumbing`](config.md). When Anvil is started the plumbing file [`$ANVIL_CFG_DIR/plumbing`](config.md) is loaded.

## LoadStyle

Usage: `LoadStyle [<filename>]`

LoadStyle loads the editor style information from a file: the current font and size, colors, etc. With one argument the style is loaded from the file named by `filename`. With no argument it is loaded from [`$ANVIL_CFG_DIR/style.js`](config.md). When Anvil is started the style file [`$ANVIL_CFG_DIR/style.js`](config.md) is loaded.

## Look

Usage: `Look <term>`

`Look` searches for the next string in the window body that matches `term`.

## Lyrname

Usage: `Lyrname <name>`

Set the name of the active layer to `name`.

## Mark

Usage: `Mark [<markname>]`

`Mark` saves the cursor position in the window body with the name specified by the argument. If no argument is given it is saved with the name `def`.

## Marks

`Marks` displays the currently set bookmarks to the `+Errors` window.

## Marks-

`Marks-` clears all the currently set bookmarks.

## New

Usage: `New [<path>]`

`New` makes a new window. If a window for that file is already opened, a new window for that file is not created. Otherwise, the window is opened in the column with the most free space. If `New` is executed with `path` the file or directory with the name of the argument is loaded into the window.

## Newcol

`Newcol` creates a new column.

## Newlyr

Create a new layer and switch to it.

## On

Usage: `On <path> <command>...`

`On` takes two or more arguments. The first is a host and directory (in the format `host:directory`) and the remaining arguments are the command and arguments to run.

## Only

Usage: `Only [above | below]`

`Only` takes effect when executed in a window or its tag. With no argument, close the other windows in this column leaving only this window. With the argument `above`, close windows below this window. With the argument `below`, close windows above this window.

## Paste

`Paste` writes the text from the clipboard to the window.

## Pic

Usage: `Pic <filename> [fit | <N>%]`

`Pic` sets the background picture for the window body. The first argument should be the name of a .png, .gif or .jpeg image. The second argument, if specified, specifies how to scale the image. If the second argument is the word `fit`, without quotes, the image is scaled to the size of the window width. If the second argument is a number followed by the % character (such as `50%`) the image is scaled by that percentage.

## PrintCfg

Usage: `PrintCfg settings.toml`

Print a sample config file to `+Errors`. The argument specifies the type of config file to print. More config file exampless may be added in the future.

## Put

`Put` writes the contents of the window body to the path that is the leftmost text in the window tag.

## Putall

`Putall` executes a `Put` on all open windows, saving all windows.

## Recent

`Recent` writes the list of most recently closed files to the `+Errors` window.

## Redo

Redo the last change.

## Rel

If the column has a column path specified, this command makes all of the paths of the windows in the column relative to that column path.

## Rot

`Rot` rotates the selections when there are multiple selections. The primary selection moves to the next selection, that one to the next and so on, with the last moving to the primary.

## SaveStyle

Usage: `SaveStyle [<filename>]`

`SaveStyle` saves the editor style information to a file: the current font and size, colors, etc. With one argument the style is saved to the file named by `filename`. With no argument it is saved to [$ANVIL_CFG_DIR/style.js](config.md). When Anvil is started the style file [$ANVIL_CFG_DIR/style.js](config.md) is loaded.

## Setlyr

Set which layer index is active.

## Settag

Usage: `Settag [<tag>...]`

`Settag` sets the tag of the current window when executed from a window body or tag, the tag of the current column when executed from a column tag, or the editor when executed from the editor tag. When executed for a window, only the user-editable area is set. This is meant to be used by programs using the API.

The argument may be quoted with single-quotes.

## Showcol

Usage: `Showcol [<column name>]`

`Showcol` makes the column with the name that matches the first argument visible. If no argument is passed, the first hidden column is made visible.

## Shstr

Usage: `Shstr [<string>...]`

When executed with one or more arguments, set the 'Shell String' for the current window: the template string that is used to build the command run on a remote system. It may contain these substitutions:

- `{Dir}`: The window directory
- `{Cmd}`: The name of the command to be executed
- `{Args}`: Arguments to the command

The default Shell String (assuming the current shell is sh) is: `sh -c $'cd "{Dir}" && {Cmd} {Args}'`

When executed with no arguments, set the Shell String for the current window to the default.

## Snarf

`Snarf` copies the last selected text to the clipboard.

## Sort

`Sort` sorts the windows in the column by their file paths.

## Syn

Usage: `Syn [list | off | <language>]`

`Syn` is used to control syntax highlighting for the current window. With the argument `off` it disables syntax highlighting, and with the argument `list` it lists supported languages. With any other argument it enables syntax highlighting and highlights the body using the language named by the argument. With no argument it attempts to analyze the text to autodetect the language.


## Tab

Usage: `Tab [<tabstring>]`

`Tab` sets the string that Anvil inserts when ++tab++ is pressed. With no argument, this sets ++tab++ to insert the tab (`\t`) character. With one argument it sets the value to insert to that argument. The argument may be quoted with single-quotes, and may contain the escapes `\t`, `\n`, `\r`, `\'`, `\"`, or `\\`.

For ++tab++ to insert four spaces, use the following.

```
Tab '    '
```

Use the following to insert a `\t` character:

```
Tab '\t'
```

## Tint

Usage: `Tint [list | <color>]`

`Tint` is used to color selections of text. When executed with the argument `list` it shows the pre-defined tint colors. When executed with one argument that is not `list`, it changes the text in all current selections to that color. The argument must be a hex color code in the form `#rrggbb` or a color name. When executed with no argument and selections present, it removes the coloring for text that overlap the selections. When run with no arguments and no selections it clears all tinting.


## Title

Usage: `Title <title>...`

`Title` sets the title of the editor to its joined arguments. The title is usually displayed by the OS window manager in the title bar.

## Undo

Undo the last change.

## Up

Make the layer above this one active.

## Wins

List the filenames of the open windows.

## Wrap

Usage: `Wrap [off]`

When run with no argument, line wrapping is enabled. When run with the argument `off`, word wrapping is disabled.

## Zerox

`Zerox` opens a second window which is a copy of the current window.

## ◊

If there are no selections, insert a `◊` rune at the cursor. If there are selections, insert a `◊` before and after each selection.


