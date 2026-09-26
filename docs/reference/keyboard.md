# Keyboard Reference

This reference documents the default keyboard shortcuts in Anvil. These may be overridden by defining custom [keymaps](keymaps.md).

## Keyboard Shortcuts

| Key Combination | Behaviour |
| --------------- | --------- |
| HOME            | Go to start of line |
| END |    Go to end of line |
| PG DN |  Scroll down a page |
| PG UP |  Scroll up a page |
| SHIFT-Enter | Begin new line, like enter, but do not autoindent |
| CTRL-Enter | Execute the entire line as a command |
| CTRL-ALT-Enter | Clear the +Errors window then execute the entire line as a command |
| F1-F12 | Go to mark created using Left Button + function key |
| ESC | If there are selections present, create a cursor at the beginning of each line the selection intersects. Otherwise, if there are multiple cursors present, reduce the cursors to one. Finally, if there is only one cursor present, select the recently typed text |
| CTRL-A | Select all text |
| CTRL-C | Copy |
| CTRL-D | Delimit selections with cursors | replace each selection with a cursor at the beginning and end |
| CTRL-E | Scroll up a line |
| CTRL-F | Complete filename |
| CTRL-G | Get |
| CTRL-H | Complete command or substitute next completion |
| CTRL-K | Delete from the current cursor position to the end of the line |
| CTRL-L | Surround each selection with Lozenge (◊) characters |
| CTRL-N | Complete word or substitute next completion |
| CTRL-P | Complete word or substitute previous completion |
| CTRL-Q | Acquire word or selection |
| CTRL-R | Redo |
| CTRL-S | Put |
| CTRL-T | Execute the selected text |
| CTRL-ALT-T | Clear the +Errors window then execute the selected text |
| CTRL-U | Delete each line containing a cursor |
| CTRL-V | Paste |
| CTRL-Z | Undo |
| CTRL-X | Cut |
| CTRL-Y | Scroll down a line |
| CTRL-Right | Move one space-separated word right |
| CTRL-Left | Move one space-separated word left |
| CTRL-Home | Go to start of file |
| CTRL-End | Go to end of file |
| CTRL-/ | Search for word under or preceeding cursor; or selection or lozenge-delimited area under cursor |
| CTRL-? | Like CTRL-/ but search backwards |
| Up Arrow, Down Arrow | Move all cursors up or down one line respectively |
| Left Arrow | If cursors are present, move each cursor left one character. If selections are present, change the selections to cursors at the beginning of each selection.  |
| Right Arrow | If cursors are present, move each cursor right one character. If selections are present, change the selections to cursors at the end of each selection.  |
| ALT-Down | Make a new cursor on the line below the primary cursor at the same column. Make it the primary cursor |
| ALT-Up | Make a new cursor on the line above the primary cursor at the same column. Make it the primary cursor |

For east-of-use on MacOS, some of the above shortcuts may be executed with the Command key in addition to control:

| Key Combination | Behaviour |
| --------------- | --------- |
| Command-A | Select all text |
| Command-C | Copy |
| Command-R | Redo |
| Command-S | Put |
| Command-V | Paste |
| Command-X | Cut |
| Command-Z | Undo |

## Special Behaviours

**Auto Indent.** When the Enter key is pressed and a new line is created, it is automatically indented. The same amount of whitespace at the beginning of the line in which Enter was pressed is prefixed to the new line as well. Use Shift-Enter to prevent this behaviour.

**Auto Bracket Matching.** If there are an even number of cursors present and you type some form of opening bracket (one of '(', '<', '{', or '\[') then every second cursor will instead type the matching closing bracket. If you immediately undo, it will convert the second brackets back to the originally typed bracket, in case the behaviour was not desired.

