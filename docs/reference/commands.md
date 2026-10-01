# Command Reference

## About

Print information about the editor, including where some files are expected to be located such as:

  *  The configuration directory
  *  The settings file, and if it was loaded on startup
  *  The style configuration file, and if it was loaded on startup
  *  The SSH key directory, and a list of cached SSH connections
  *  The plumbing configuration file
  *  The API listener port, and a list of active API sessions


## Acq

Acq 'acquires' its argument. It performs the same function as ALT+Right Click performs on a text object.

Acquire means the following. First, if the word or selection matches a plumbing rule, execute that plumbing rule. If there is no matching plumbing rule, then if the word or selection is a file or directory path and there is already a window open with that path as the filename portion of it's tag, change focus to that window and make it visible. If there is not already a window open for that path, open one. Finally, if a plumbing rule is not executed and the path ends in :N, #C or !X then go to line N, character C or regex X in the file.	
	

## Alias

Usage: Alias [name] [command...]
	
Alias creates command aliases. If no arguments are specified it lists the current aliases. If one argument is specified, then that alias is removed. If two arguments are specified, then the first is the name of the alias, and the rest is the aliased command.

An alias may contain placeholders of the form $1 to $9 which are replaced with the corresponding arguments to the alias when it is executed. The placeholder $* is replaced with all the arguments separated by a space. The placeholder $$ is replaced with a literal $.
	

## Ansi

Usage: Ansi [on|off]

Ansi is used to control whether Ansi terminal color escape sequences cause coloring or not. With no argument or the 'on' it enables coloring. With the argument 'off' it disables coloring.

## Clr

Clear (delete) the contents of the window body

## Cmds

List the most recent external commands executed

## Cmds*

List the most recent external commands executed along with the directory they were executed in

## Coldown

Move the current column to the layer below

## Coldown^

Move the current column to the layer below and make that layer active

## Cols

Cols lists all the columns and layers

## Cols*

Cols* lists all the columns and layers verbosely (including the files in each column)

## Colup

Move the current column to the layer above

## Colup^

Move the current column to the layer above and make that layer active

## Cut

Cut deletes the last selected text and it to the clipboard.

## Dbg

Dbg is used to run commands to help debug the internals of Anvil. The available commands are:

ProfCpu  (◊Help Dbg ProfCpu◊)  
	Profile CPU usage  
ProfHeap  (◊Help Dbg ProfHeap◊)  
	Profile memory usage  
Goroutines  (◊Help Dbg Goroutines◊)  
	Print all goroutines  
Logs  (◊Help Dbg Logs◊)  
	Print internal debug logs  
Pid  (◊Help Dbg Pid◊)  
	Print Anvil's PID  
Psrv  (◊Help Dbg Psrv◊)  
	Start the Go pprof debug server  
Paths  (◊Help Dbg Paths◊)  
	Print window paths  
Flame  (◊Help Dbg Flame◊)  
	Profile CPU and show flame graph  


## Del

Del closes the current window.

## Del!

Del! closes the current window. If there are unsaved changes, the user is not prompted to save them.

## Delcol

Delcol deletes the column in which it is executed.

## Dellyr

Delete the current layer

## Do

Usage: Do <command...>

Do executes it's arguments as a command; i.e. as if the arguments were selceted and executed alone. This is useful to execute commands from one window in the context of another window.

## Down

Make the layer below this one active

## Dump

Usage: Dump [filename]

Dump saves the editor's state to disk: the size of the open windows and the current value of their tags. With an argument the state is written to the file named by the argument. With no argument state is written to the file anvil.dump. The state can be loaded using Load

## Elastic

Usage: Elastic  
Elastic off

When run with no argument, elastic tab stops are enabled for the window body. When run with the argument 'off', elastic tab stops are disabled.

## Exit

Exit exits the editor.

## Font

Change to the next font defined in the styles

## Fontsize

Change the font size of the current active font. This command accepts one argument. If the argument is a number, then the font size is set to that value in points. If it is +NUM or -NUM then the current font size is increased or decreased by NUM points respectively

## Fuzz

Usage: Fuzz [terms...]

Fuzz performs a fuzzy search through the lines in the window body. The terms for the search are the arguments to the Fuzz command. The lines which match the search are written to a new window for the current directory with the suffix '+Live'.

The Fuzz command is special in that it can be executed dynamically as you type the search terms. If you add the string '◊Fuzz ' to the tag, then as you type the arguments after the command the search is re-executed and the results updated in the +Live window. You can delimit the end of the search arguments using another ◊

## Get

Get reads the contents of the path that is the leftmost text in the window tag and replaces the window body contents with it.

## Getall

Getall executes a Get on all open windows, reloading all windows.

## Goto

Usage: Goto [markname]

Goto sets the current cursor position in the window body to the named bookmark, created by Mark. If no argument is given it jumps to the bookmark 'def'.

## Help

Usage: Help [topic]

Help shows a bit of help for the editor. With no argument it lists the main commands and a brief description. With an argument displays information about that topic. The argument may be a command, which displays more detail about the command, or it may be another selected topic.

## Hidecol

Hidecol hides the current column.

## Hostpass

Usage: Hostpass <password> <hostname> [username] [port]

Hostpass is used to specify the password used to log into an ssh server. It takes between two and four arguments. The first argument is the password. The second argument is the hostname or IP address of the server. The third argument is the username for the server; if not specified the current user's name is used. The fourth argument is the TCP port number for the server; if not specified 22 is used.

## Id

Id prints the window ID to the +Errors window. Useful when using the API.

## Keymap

Usage: Keymap load <file>  
Keymap show def <name> | defs | stack  
Keymap push <name>  
Keymap pop  
Keymap win push <name>  
Keymap win pop  
Keymap win reset

When run with the 'show' argument, this command shows keymap information. The argument 'defs' shows all defined keymaps. The 'def <name>' shows the definition of the keymap with name <name>. The argument 'stack' shows the current keymap stack, with the top being shown last.

When run with the 'add' argument, load a keymap file which contains one or more keymap definitions. When run with the 'push' argument, push a keymap onto the global keymap stack. When run with the 'pop' argument, pop off the top keymap in the stack. The bottommost keymap is never popped.

If the first argument is win, then the keymap for the local window only is modified. If 'win push' or 'win pop' is executed and the window is using the global keymap stack, then the global keymap stack is copied to the window and a keymap pushed to or popped from that window stack respectively. 'win reset' resets the window's keymap stack to be the global keymap stack again.



## Keypass

Usage: Keypass <keyfile> <password>

Keypass is used to specify the password used to decrypt an ssh private key file. It takes two arguments: the first is the ssh filename and the second is the password. This is needed when an ssh private key file is encrypted and ssh-agent is not being used.

## Kill

Usage: Kill [jobname...]

Kill kills all the jobs that are currently running that have names matching the arguments to the Kill command. If no argument is provided the first job is killed

## Load

Usage: Load [filename]

Load loads the editor's state from disk as written by the Dump command. With an argument the state is read from the file named by the argument. With no argument state is read from the file anvil.dump

## LoadPlumbing

Usage: LoadPlumbing [filename]

LoadPlumbing loads the plumbing rules from a file. With one argument the plumbing is loaded from the file named by the argument. With no argument it is loaded from [&lt;config-dir&gt;](config.md)/plumbing. When the editor is started the plumbing file [&lt;config-dir&gt;](config.md)/plumbing is loaded

## LoadStyle

Usage: LoadStyle [filename]

LoadStyle loads the editor style information from a file: the current font and size, colors, etc. With one argument the style is loaded from the file named by the argument. With no argument it is loaded from [&lt;config-dir&gt;](config.md)/style.js. When the editor is started the style file [&lt;config-dir&gt;](config.md)/style.js is loaded

## Look

Usage: Look <term>

Look searches for the next string in the window body that exactly matches the argument to Look.

## Lyrname

Set the name of the active  layer to the concatenation of the arguments separated by spaces

## Mark

Usage: Mark [markname]

Mark saves the current cursor position in the window body with the name specified by the argument. If no argument is given it is saved with the name 'def'.

## Marks

Marks displays the currently set bookmarks to the Errors window.

## Marks-

Marks- clears all the currently set bookmarks.

## New

Usage: New [path]

New makes a new window or with an argument opens a path. If a window for that file is already opened, a new window for that file is not created. Otherwise, the window is opened in the column with the most free space. If new is executed with an argument the file or directory with the name of the argument is loaded into the window.

## Newcol

Newcol creates a new column.

## Newlyr

Create a new layer and switch to it

## On

Usage: On <path> <command...>

Run takes two or more arguments. The first is a host and directory (in the format host:directory) and the remaining arguments are the command and arguments to run.

## Only

Only takes effect when executed in a window or its tag. With no argument, close the other windows in this column leaving only this window. With the argument 'above', close windows below this window. With the argument 'below', close windows above this window.

## Paste

Paste writes the text from the clipboard to the window.

## Pic

Usage: Pic <filename> [scaling]

Pic sets the background picture for the window body. The first argument should be the name of a .png, .gif or .jpeg image. The second argument, if specified, specifies how to scale the image. If the second argument is the word 'fit', without quotes, the image is scaled to the size of the window width. If the second argument is a number followed by the % character (such as 50%) the image is scaled by that percentage.

## PrintCfg

Usage: PrintCfg <default settings file name>

Print a sample config file to +Errors. The argument specifies the type of config file to print:
  ◊PrintCfg settings.toml◊ generates a settings file


## Put

Put writes the contents of the window body to the path that is the leftmost text in the window tag.

## Putall

Putall executes a Put on all open windows, saving all windows.

## Recent

Recent writes the list of most recently closed files to the Errors window.

## Redo

Redo the last change

## Rel

If the column has a column path specified, this command makes all of the paths of the windows in the column relative to that column path.

## Rot

Rot rotates the selections when there are multiple selections. The primary selection moves to the next selection, that one to the next and so on, with the last moving to the primary.

## SaveStyle

Usage: SaveStyle [filename]

SaveStyle saves the editor style information to a file: the current font and size, colors, etc. With one argument the style is saved to the file named by the argument. With no argument it is saved to [&lt;config-dir&gt;](config.md)/style.js. When the editor is started the style file [&lt;config-dir&gt;](config.md)/style.js is loaded

## Setlyr

Set which layer index is active

## Settag

Usage: Settag [tag...]

Settag sets the tag of the current window when executed from a window body or tag, the tag of the current column when executed from a column tag, or the editor when executed from the editor tag. When executed for a window, only the user-editable area is set. This is meant to be used by programs using the API.

The argument may be quoted with single-quotes.

## Showcol

Usage: Showcol [column name]

Showcol makes the column with the name that matches the first argument visible. If no argument is passed, the first hidden column is made visible

## Shstr

Usage: Shstr [string...]

When executed with one or more arguments, set the 'Shell String' for the current window: the template string that is used to build the command run on a remote system. It may contain these substitutions within braces:

  Dir: The window directory
  Cmd: The name of the command to be executed
  Args: Arguments to the command

The default Shell String (assuming the current shell is sh) is: sh -c $'cd "{Dir}" && {Cmd} {Args}'

When executed with no arguments, set the Shell String for the current window to the default.


## Snarf

Snarf copies the last selected text to the clipboard.

## Sort

Sort sorts the windows in the column by their file paths

## Syn

Usage: Syn <language>  
Syn off  
Syn list

Syn is used to control syntax highlighting for the current window. With the argument 'off' it disables syntax highlighting, and with the argument 'list' it lists the valid supported languages. With any other argument it enables syntax highlighting and highlights the body using the language named by the argument. With no argument it attempts to analyze the text to autodetect the language.


## Tab

Usage: Tab <tabstring>

Tab sets the string that Anvil inserts when the tab key is pressed. With no argument, sets the tab key to insert the tab character. With one argument it sets the value to insert to that argument. The argument may be quoted with single-quotes, and may contain the escapes \t, \n, \r, \', \", or \\.

For example, to cause the tab insert four spaces, use: Tab '    '. To insert a tab use: Tab '\t'.

## Tint

Usage: Tint list  
Tint <color>  
Tint

Tint is used to color selections of text. When executed with the argument 'list' it shows the pre-defined tint colors. When executed with one argument that is not 'list', it changes the text in all current selections to that color. The argument must be a hex color code in the form #rrggbb or a color name. When executed with no argument and selections present, it removes the coloring for text that overlap the selections. When run with no arguments and no selections it clears all tinting.


## Title

Usage: Title <title...>

Title sets the title of the editor to it's joined arguments. The title is usually displayed by the OS window manager in the title bar.

## Undo

Undo the last change

## Up

Make the layer above this one active

## Wins

List the filenames of the open windows

## Wrap

When run with no argument, line wrapping is enabled. When run with the argument 'off', word wrapping is disabled.

## Zerox

Zerox opens a second window which is a copy of the current window

## ◊

If there are no selections, insert a ◊ rune at the cursor. If there are selections, insert a ◊ before and after each selection.


