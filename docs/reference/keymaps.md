# Keymaps Reference

Keymaps are used to map keypresses on the keyboard to actions. A single keymap consists of a set of these keypress-to-action mappings with a name. Anvil supports what might be called _stackable keymaps_.

Anvil stores a loaded set of keymaps, and also a stack of active keypmaps. Loaded keymaps aren't involved in handling keypresses, but can be pushed onto the stack. When a key is pressed on the keyboard, the keymap at the top of the stack is checked for a matching key mapping, and if a match is found the action from the mapping is executed. If a mapping is not found then the next lower keymap of the stack may be checked, and if the mapping is again not found, then one lower than that and so on, depending on if each keymap allows falling through to these lower maps. Keymaps can dynamically be pushed onto the top of the stack and the top keymap popped from the stack at runtime.

Anvil has a built-in set of loaded keymaps, and the stack begins with one keymap pushed onto the stack named "base". When a keymap is loaded and there is already a keymap with the same name, the existing keymap is either replaced or updated depending on what the loader specifies. If it is updated then if there is a binding in both keymaps for the the same keystoke, then the binding in the newly loaded keymap overwrites the mapping from the old keymap, and bindings that don't exist in the earlier keymap are added.

## Keymap File Format

Keymaps are defined using keymap files, which contain one or more keymap definitions. A keymap definition consists of several lines of directives. Lines beginning with '#' are comments and not executed. 

For reference you can view the default keymap file used by Anvil by looking in the source code at the file `anvil/editor/cmd/anvil/default-keymaps.dat`, or [view the default-keymaps.dat](../../downloads/default-keymaps.dat.html) as of the time of writing.

The directive lines are:

### keymap &lt;name&gt; [flags]

This line declares the beginning of a keymap definition. The lines which follow it all belong to the keymap until the next keymap line or the end of file. Each keymap must have a name, and optionally has one or more space-separated flags. The allowed flags are: 

  * `replace`, which indicates that when the keymap file is loaded if there is already a keymap with this name loaded it is replaced by this keymap. This is the default.
  * `update`, which indicates that when the keymap file is loaded if there is already a keymap with this name then the mappings from this keymap are added to the existing keymap.
  * `fallthrough` which indicates that when this keymap is active at the top of the stack, if a special or modified key is pressed and no mapping is found in this keymap, the next lower keymap can be searched. It in turn may have the `fallthrough` flag set as well. Note that the fallthrough flag has no effect for normal text keys (like letters, numbers and punctuation); they are always typed and no special mapping is required.

For example, this line declares the start of a keymap named "emacs" that when loaded should update any existing keymap already named emacs:

	keymap emacs update

### map &lt;key&gt; &lt;action&gt; [; action...]

The map directive defines one keypress in the mapping. The &lt;key&gt; specification must be a name of one of the keys on the keyboard as defined by GIO, optionally preceeded by one or more modifier letters and a hyphen. The keynames for letters, digits, and punctuation are simply the letter in uppercase, the number or punctuation. The function keys (F1-F12) are named as expected. Other keys may use symbolic names from unicode; see the [reference](https://pkg.go.dev/gioui.org/io/key#Name) for the type Name in the package gioui.org/io/key for a list.

Modifiers letters consist of 'S' for shift, 'A' for alt, 'C' for Ctrl and 'K' for Command. When Anvil loads a keymap from a file for each mapping containing the 'C' modifier Anvil makes a duplicate mapping with 'C' substituted with 'K', so it is sufficient to only define the mapping for Ctrl.

Following the key specification is a semi-colon-separated list of action names. The action names may not contain spaces. Each action in the list is executed when the key is pressed.

Here are some examples. To map the tab key to the action named tab, you would use this line:

	map Tab tab

To map the newline key to the action named "newline", you would use this line:

	map ⏎ newline

To map the keypress Ctrl+C to the action copy, you would use:

	map C-C copy

To map the keypress Ctrl+Alt+T to perform the action named clear-errors then the action named execute, you would use:

	map CA-T clear-errors; execute

### default &lt;action&gt;

If this line is specified, then when a key is pressed and no other mapping in the keymap matches the keypress then this action will be performed. This default action also applies to normal text keys (like letters, numbers and punctuation), so can be used to override their behaviour. 

For example, you can cause keypresses that have no mapping in this keymap to be ignored by Anvil by doing:

	default noop

## Actions

The following actions can be used in key mappings.

| Name | Arguments | Description |
| ----- | --- |--------- |
| backspace |  | Delete the rune before each cursor and move the cursors backwards one rune |
| clear-errors |  | Clear the errors window associated with the current window |
| execute-line |  | Execute the line with the cursor as a command |
| move-to-sol |  | Reduce cursors to one and move it to the start of the file |
| delete |  | Delete the rune after each cursor |
| move-left-rune |  | Move each cursor left one rune |
| move-right-chunk |  | Move each cursor right one chunk |
| move-left-chunk |  | Move each cursor left one chunk |
| move-up |  | Move each cursor up one line |
| move-right-word |  | Move each cursor right one space-separated word |
| move-left-word |  | Move each cursor left one space-separated word |
| new-cursor-below-last |  | Create a new cursor below the lowest cursor |
| move-down |  | Move each cursor down one line |
| move-to-eof |  | Reduce cursors to one and move it to the end of the file |
| add-lozenge |  | Insert a lozenge character at each cursor, or surround each selection with a lozenge |
| newline | no-indent | Insert a newline at the current cursor position. |
| move-right-rune |  | Move each cursor right one rune |
| complete-file |  | Reduce cursors to one and complete the file path ending at the cursor |
| complete-word |  | Reduce cursors to one and complete the word ending at the cursor |
| get |  | Get the current file |
| complete-command |  | Reduce cursors to one and complete the command ending at the cursor |
| move-page-up |  | Move the viewport up one page of text |
| copy |  | Copy the selected text to the clipboard |
| acquire | location | Acquire the word under the cursor, the lozenge-delimited text surrounding the cursor, or the current selection. If the first argument is set to 'same-window' then the item is acquired in the same window instead of creating a new window |
| move-page-down |  | Move the viewport down one page of text |
| cut |  | Copy the selected text to the clipboard then delete the selected text |
| move-to-sof |  | Reduce cursors to one and move it to the start of the file |
| move-to-eol |  | Move each cursor to the end of the line |
| move-to-layer-below |  | Make the layer below the current one active |
| delete-layer |  | Delete the current layer |
| move-to-window-below |  | Move the keyboard focus to the window below the current one |
| new-layer |  | Make a new layer and switch to it |
| move-to-window-body |  | Move the keyboard focus to the window body |
| move-to-window-tag |  | Move the keyboard focus to the window tag |
| move-to-highest-layer |  | Make the highest layer active |
| move-to-window-above |  | Move the keyboard focus to the window above the current one |
| move-to-layer-above |  | Make the layer above the current one active |
| move-to-editor-tag |  | Move the keyboard focus to the editor tag |
| move-to-column-tag |  | Move the keyboard focus to the column tag |
| cursor-at-selections-lines |  | Make a cursor at the start of each selection and remove the selections |
| delete-to-eol |  | Delete from each cursor to the end of the line |
| delete-line |  | Delete the line containing each cursor |
| execute-args | command... | Execute the arguments of the action as a command |
| halt-if-handled |  | Some actions such as reduce-cursors-to-one specifically indicate whether or not they handled an action (i.e. if they actually performed some action). This action will halt if the previous action executed in the mapping indicated they handled an action. |
| delimit-with-cursors |  | Selimit each selection with cursors |
| move-to-window-on-left |  | Move the keyboard focus to the window left of the current one |
| move-to-window-on-right |  | Move the keyboard focus to the window right of the current one |
| execute |  | Execute the word under the cursor, the lozenge-delimited text surrounding the cursor, or the current selection |
| new-cursor-above-first |  | Create a new cursor above the highest cursor |
| scroll-line-down |  | Move the viewport down one line |
| tab |  | Insert the current tab string at each cursor position |
| previous-completion |  | If the last action was a completion, move to the previous completion in the list |
| put |  | Put the current file |
| scroll-line-up |  | Move the viewport up one line |
| pointer-paste |  | If the left pointer button is held down, paste at that position |
| undo |  | Undo the last change |
| select-up |  | Extend each selection up one line |
| select-all |  | Select all the text in the window body |
| select-down |  | Extend each selection down one line |
| select-to-eol |  | Extend each selection to the end of the line |
| redo |  | Redo the last undone change |
| select-to-eof |  | Reduce cursors to one and select to the end of the file |
| select-to-sol |  | Extend each selection to the start of the line |
| noop |  | Do nothing |
| select-to-sof |  | Reduce cursors to one and select to the start of the file |
| pointer-cut-or-exec-with-arg |  | If the right pointer button is currently held down after making a selection, cut that selection. If the middle pointer button is currently held down after making a selection, execute that selection with the last selected text as an argument |
| select-right-chunk |  | Extend each selection to the right one chunk |
| select-left-chunk |  | Extend each selection to the left one chunk |
| select-right-rune |  | Extend each selection to the right one rune |
| select-left-word |  | Extend each selection to the left one word |
| select-left-rune |  | Extend each selection to the left one rune |
| search | direction | Search for the word under the cursor, the lozenge-delimited text surrounding the cursor, or the current selection. If the first argument is set to 'reverse' then the search is performed backwards |
| select-right-word |  | Extend each selection to the right one word |
| push | keymap-name | Push the loaded keymap with the specified name onto the top of the stack |
| pop |  | Pop the keymap stack: remove the top active keymap from the stack |
| reduce-cursors-to-one |  | If there are multiple cursors, reduce to one cursor |
| select-recently-typed |  | Select the recently typed text |
| paste |  | Insert the text from the clipboard at each cursor position or selection |
| pointer-save-or-goto-mark |  | If the left pointer button is held down, save a mark named after the current key. Otherwise, goto to the mark named after the current key |
| set-layer | index | Set the current active layer to the argument |

## Manipulating Keymaps

Anvil loads a built-in set of keymaps when started, then it will load the keymaps defined in the `keymaps` file from the [configuration directory](config.md) if it exists.

There is also a command named [Keymap](commands.md#keymap) to manipulate keymaps at runtime.