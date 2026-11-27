# Mouse Reference

## Mouse Usage in a Column Layout Box

| <div style="width:12em">Button</div> | <div style="width:12em">Event</div> | Behaviour |
| --- | --- | --- |
| ++left-button++ | Drag horizontally | Resize or reorder column. |
| ++left-button++ | ++shift++ + Click and hold | While held, display only the basenames of files in window tags. |
| ++left-button++ | ++control++ + Click | Evenly space the windows in the column. |

## Mouse Usage in a Window Layout Box

| <div style="width:12em">Button</div> | <div style="width:12em">Event</div> | Behaviour |
| --- | --- | --- |
| ++left-button++ | Single click | Make the window slightly larger. |
| ++left-button++ | Drag vertically | Change the height of the window if there are other windows in the column. |
| ++left-button++ | Drag horizontally | Move the window to another column. |
| ++right-button++ | Single click | Minimize other windows.  |
| ++middle-button++ | Single click | Hide other windows.   |

## Mouse Usage in a Scrollbar

| <div style="width:12em">Button</div> | <div style="width:12em">Event</div> | Behaviour |
| --- | --- | --- |
| ++left-button++ | Single click | Scroll upwards. The amount scrolled is relative to the vertical position of the click within the scrollbar. Near the bottom scrolls an entire page, while near the top scolls a line. |
| ++right-button++ | Single click | Scroll downwards.  |
| ++middle-button++ | Drag vertically | Scroll to that relative position in the file.  |

## Mouse usage in a Window Body or Tag

### Unchorded

| <div style="width:12em">Button</div> | <div style="width:12em">Event</div> | Behaviour |
| --- | --- | --- |
| ++left-button++ | Single click | Set cursor position and remove other cursors and selections. |
| ++left-button++ | ++alt++ + Single click | Create an additional cursor. |
| ++left-button++ | Double click | Select the string of alphanumeric characters under the mouse. |
| ++left-button++ | Triple click | Select the space-separated word under the mouse. |
| ++left-button++ | Quad click |   Select the current line. |
| ++left-button++ | Double click on the first character of a line | Select current line. |
| ++left-button++ | Double click on a delimiting character[^1] | Select text enclosed by the brackets, excluding the brackets[^2]. |
| ++left-button++ | Triple click on a delimiting character[^1] | Select text enclosed by the brackets, including the brackets[^2]. |
| ++left-button++ | Drag | Select text and remove other selections. |
| ++left-button++ | ++alt++ + Drag | Create an additional selection. |
| ++left-button++ | Click and hold, then ++command++ | Simulate a ++middle-button++ press when a user presses and holds ++left-button++ then hits ++command++. Useful for MacOS users with two-button mice. |
| ++right-button++ | Single click | Search for word or selection under cursor and make a new selection. If word or selection is surrounded by `/` then it is treated as a regular expression. |
| ++right-button++ | ++alt++ + Single click | Acquire the word or selection under the cursor[^3]. |
| ++right-button++ | ++control+alt++ + Single click | Like ++alt++ + Single click, but if a new window would be opened for a path, instead load the path in the current window. |
| ++middle-button++ | Single click | Execute the word or selection under the mouse. This can be an Anvil command (`New`, `Del`, `Paste`, etc) or a shell command. |
| ++middle-button++ | ++alt++ + Single click | Clear the `+Errors` window then execute the word or selection. |
| ++middle-button++ | Select and release | Execute the selected command. |
| ++middle-button++ | ++alt++ + Select and release | Clear the `+Errors` window then execute the selected command. |
| ++scroll-wheel++ | ++control++ + Scroll | Change the active layer by moving up and down the layer stack. |

[^1]: A delimiting character refers to an opening or closing bracket, or an opening or closing quote character. Explicitly, one of `{`, `[`, `(`, `<` or its matching closer, or one of `"`, `` ` ``, or `◊`.

[^2]: For quotes, if it is ambiguous where the matching quote character would be because there is a candidate match both to the left and the right, Anvil matches to the right.

[^3]: Acquire means the following. First, if the word or selection matches a plumbing rule, execute that plumbing rule. If there is no matching plumbing rule, then if the word or selection is a file or directory path and there is already a window open with that path as the filename portion of it's tag, change focus to that window and make it visible. If there is not already a window open for that path, open one. Finally, if a plumbing rule is not executed and the path ends in `:N`, `#C` or `!X` then go to line N, character C or regex X in the file.

### Chorded

Chorded mouse usage refers to clicking and holding one mouse button, and then while that button is held, clicking and releasing another button or keyboard key. In the table below, "Primary Button" refers to the first button that must be pressed and held, and "Secondary Button / Key" refers to the next button or keyboard key that must be pressed and released.

| <div style="width:12em">Primary Button</div> | <div style="width:12em">Secondary Button / Key</div> | Behaviour |
| -----| -------- | -------------------- |
| ++left-button++ | ++middle-button++ | Cut selected text to clipboard. |
| ++left-button++ | ++right-button++ | Paste text from clipboard. |
| ++middle-button++ | ++left-button++ | Execute command with the text of the last created selection in a window body as the first argument. |
| ++middle-button++ | ++control++ | Execute command with the text of the last created selection in a window body as the first argument. |
| ++left-button++ | ++f1++ - ++f12++ | Create a mark at primary cursor position who's name is the function key. |





