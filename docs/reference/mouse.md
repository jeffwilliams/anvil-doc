# Mouse Reference

## Mouse Usage in a Column Layout Box

| Button | Event | Behaviour |
| -----| -------- | -------------------- |
| Left | Drag horizontally | Resize or reorder column |
| Left | Shift+Click and hold | While held, display only the basenames of files in window tags |
| Left | Ctrl+Click | Evenly space the windows in the column |

## Mouse Usage in a Window Layout Box

| Button | Event | Behaviour |
| -----| -------- | -------------------- |
| Left | Single click | Make the window slightly larger |
| Left | Drag vertically | Change the height of the window if there are other windows in the column |
| Left | Drag horizontally | Move the window to another column |
| Right | Single click | Minimize other windows  |
| Middle | Single click | Hide other windows   |

## Mouse Usage in a Scrollbar

| Button | Event | Behaviour |
| -----| -------- | -------------------- |
| Left | Single click | Scroll upwards. The amount scrolled is relative to the vertical position of the click within the scrollbar. Near the bottom scrolls an entire page, while near the top scolls a line. |
| Right | Single click | Scroll downwards  |
| Middle | Drag vertically | Scroll to that relative position in the file  |

## Mouse usage in a Window Body or Tag

### Unchorded

| Button | Event | Behaviour |
| -----| -------- | -------------------- |
| Left | Single click | Set cursor position and remove other cursors and selections |
| Left | Alt + Single click | Create an additional cursor |
| Left | Double click | Select the string of alphanumeric characters under the mouse |
| Left | Triple click | Select the space-separated word under the mouse |
| Left | Quad click |   Select the current line |
| Left | Double click on the first character of a line | Select current line |
| Left | Double click on a delimiting character¹ | select text enclosed by the brackets, excluding the brackets² |
| Left | Triple click on a delimiting character¹ | select text enclosed by the brackets, including the brackets² |
| Left | Drag | Select text and remove other selections |
| Left | Alt + Drag | Create an additional selection |
| Left | Press + Command | Simulate a middle-button press when a user presses and holds the left mouse button then hits the Command key. Useful for MacOS users with two-button mice |
| Right | Single click | Search for word or selection under cursor and make a new selection. If word or selection is surrounded by / then it is treated as a regular expression. |
| Right | Alt + Single click | Acquire the word or selection under the cursor³ |
| Right | Alt + Ctrl + Single click | Like Alt + Single click, but if a new window would be opened for a path, instead load the path in the current window |
| Middle | Single click | Execute the word or selection under the mouse. This can be an Anvil command (New, Del, Paste, etc) or a shell command |
| Middle | Alt + Single click | Clear the +Errors window then execute the word or selection |
| Middle | Select and release | Execute the selected command |
| Middle | Alt + Select and release | Clear the +Errors window then execute the selected command |
| Scroll | Ctrl + Scroll | Increase or reduce font size |

[1] A delimiting character refers to an opening or closing bracket, or an opening or closing quote character. Explicitly, one of `{`, `[`, `(`, `<` or its matching closer, or one of `"`, ```, ``` or `◊`. 

[2] For quotes, if it is ambiguous where the matching quote character would be because there is a candidate match both to the left and the right, then Anvil matches to the right.

[3] Acquire means the following. First, if the word or selection matches a plumbing rule, execute that plumbing rule. If there is no matching plumbing rule, then if the word or selection is a file or directory path and there is already a window open with that path as the filename portion of it's tag, change focus to that window and make it visible. If there is not already a window open for that path, open one. Finally, if a plumbing rule is not executed and the path ends in :N, #C or !X then go to line N, character C or regex X in the file.

### Chorded

Chorded mouse usage refers to clicking and holding one mouse button, and then while that button is held, clicking and releasing another button or keyboard key. In the table below, "Primary Button" refers to the first button that must be pressed and held, and "Secondary Button / Key" refers to the next button or keyboard key that must be pressed and released.

| Primary Button | Secondary Button / Key | Behaviour |
| -----| -------- | -------------------- |
| Left | Middle | Cut selected text to clipboard |
| Left | Right | Paste text from clipboard |
| Middle | Left | Execute command with the text of the last created selection in a window body as the first argument |
| Middle | Ctrl | Execute command with the text of the last created selection in a window body as the first argument |
| Left | F1-F12 | Create a mark at primary cursor position who's name is the function key. |





