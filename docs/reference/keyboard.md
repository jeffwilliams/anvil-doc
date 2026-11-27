# Keyboard Reference

This reference documents the default keyboard shortcuts in Anvil. These may be overridden by defining custom [keymaps](keymaps.md).

## Keyboard Shortcuts

| <div style="width:18em">Key Combination</div> | Behaviour |
| --- | --- |
| ++home++ | Go to start of line |
| ++end++ |    Go to end of line |
| ++page-down++ |  Scroll down a page |
| ++page-up++ |  Scroll up a page |
| ++shift+enter++ | Begin new line, like ++enter++, but do not autoindent |
| ++control+enter++ | Execute the entire line as a command |
| ++control+alt+enter++ | Clear the `+Errors` window then execute the entire line as a command |
| ++f1++ - ++f12++ | Go to mark created using ++left-button+f1++ - ++left-button+f12++ |
| ++escape++ | If there are selections present, create a cursor at the beginning of each line the selection intersects. Otherwise, if there are multiple cursors present, reduce the cursors to one. Finally, if there is only one cursor present, select the recently typed text |
| ++control+a++ | Select all text |
| ++control+c++ | Copy |
| ++control+d++ | Replace each selection with a cursor at the beginning and end |
| ++control+e++ | Scroll up a line |
| ++control+f++ | Complete filename |
| ++control+g++ | Get |
| ++control+h++ | Complete command or substitute next completion |
| ++control+k++ | Delete from the current cursor position to the end of the line |
| ++control+l++ | Surround each selection with Lozenge (◊) characters |
| ++control+n++ | Complete word or substitute next completion |
| ++control+p++ | Complete word or substitute previous completion |
| ++control+q++ | Acquire word or selection |
| ++control+r++ | Redo |
| ++control+s++ | Put |
| ++control+t++ | Execute the selected text |
| ++control+alt+t++ | Clear the `+Errors` window then execute the selected text |
| ++control+u++ | Delete each line containing a cursor |
| ++control+v++ | Paste |
| ++control+z++ | Undo |
| ++control+x++ | Cut |
| ++control+y++ | Scroll down a line |
| ++control+arrow-right++ | Move one space-separated word right |
| ++control+arrow-left++ | Move one space-separated word left |
| ++control+home++ | Go to start of file |
| ++control+end++ | Go to end of file |
| ++control+slash++ | Search for word under or preceeding cursor; or selection or lozenge-delimited area under cursor |
| ++control+shift+slash++ | Like ++control+slash++ but search backwards |
| ++arrow-up++ | Move all cursors up one line |
| ++arrow-down++ | Move all cursors down one line |
| ++arrow-left++ | If cursors are present, move each cursor left one character. If selections are present, change the selections to cursors at the beginning of each selection.  |
| ++arrow-right++ | If cursors are present, move each cursor right one character. If selections are present, change the selections to cursors at the end of each selection.  |
| ++alt+arrow-down++ | Make a new cursor on the line below the primary cursor at the same column. Make it the primary cursor |
| ++alt+arrow-up++ | Make a new cursor on the line above the primary cursor at the same column. Make it the primary cursor |

For east-of-use on MacOS, some of the above shortcuts may be executed with the Command key in addition to control:

| <div style="width:18em">Key Combination</div> | Behaviour |
| --- | --- |
| ++command+a++ | Select all text |
| ++command+c++ | Copy |
| ++command+r++ | Redo |
| ++command+s++ | Put |
| ++command+v++ | Paste |
| ++command+x++ | Cut |
| ++command+z++ | Undo |

## Special Behaviours

### Auto Indent

When ++enter++ is pressed and a new line is created, it is automatically indented. The same amount of whitespace at the beginning of the line in which ++enter++ was pressed is prefixed to the new line as well. Use ++shift+enter++ to prevent this behaviour.

### Auto Bracket Matching

If there are an even number of cursors present and you type some form of opening bracket (one of `(`, `<`, `{`, or `[`) then every second cursor will instead type the matching closing bracket. If you immediately undo, it will convert the second brackets back to the originally typed bracket, in case the behaviour was not desired.

