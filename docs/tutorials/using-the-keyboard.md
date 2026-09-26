# Using the Keyboard

Using the keyboard in Anvil is similar to most editors. This section will demonstrate the parts where Anvil diverges from the norm with a short video to demonstrate the usage. 

A complete list of the keyboard shortcuts can be found in the [Keyboard Reference](../reference/keyboard.md).

## Undo and Redo

To undo the last change, use CTRL-Z. To redo an undone change use CTRL-R.

![type:video](../../img/anvil-tut-using-the-keyboard-1-undo.mp4)

## Put and Get

You can use the shortcut CTRL-S to save the file in the current window, and CTRL-G to load the contents from disk.

![type:video](../../img/anvil-tut-using-the-keyboard-2-put-get.mp4)

## Autoindent

When you press the Enter key at the end of a line of text, the next line is automatically indented by the same amount of whitespace as the previous line. However, if you use SHIFT-Enter at the end of a line, the next line is not indented.

![type:video](../../img/anvil-tut-using-the-keyboard-3-autoindent.mp4)

## Executing Text

Anvil has two separate shortcuts for executing text. The shortcut CTRL-T executes the text contained in the primary selection. The shortcut CTRL-Enter executes the entire current line.

![type:video](../../img/anvil-tut-using-the-keyboard-4-exec.mp4)

## Delimiting Text

A common text-editing operation is to surround a portion of text with some character. For example, adding double-quotes at the beginning or ending of a string, adding opening and closing parenthesis around an expression, adding a blank line before and after some text to add vertical whitespace, and so on.

Anvil has a shortcut that helps make this easier. The shortcut CTRL-D (for delimit) replaces each selection with a cursor at the beginning and end of each selection. Thus if you selected some text and hit CTRL-D, you could  then type a string that would be added to the beginning and end of the selection.

As a special case, if you created cursors this way and then typed an opening bracket then each second cursor is instead replaced with the matching closing bracket. Put another way, if you created an even number of cursors and then typed a bracket in the general sense (one of '(', '[', or '{') then matching bracket pairs are inserted instead. This is a convenient way of surrounding text with brackets. In case your intent was only to add opening brackets instead, then performing an Undo immediately after the bracket is typed acts specially to instead replace the matching brackets with the opening brackets instead.

Since commands that contain spaces are common in Anvil usage, there is also a shortcut CTRL-L that performs the same action as the lozenge (◊) command; it delimits each selection with lozenge characters.

![type:video](../../img/anvil-tut-using-the-keyboard-5-delimit.mp4)

## Completion

Anvil has two separate shortcuts for completion. CTRL-F attempts to complete the current word as if it is a file. This is similar to how Tab works in bash. CTRL-N attempts to complete the current word by finding candidate words from the currently open files. This is similar to CTRL-N in VIM.

With either type of completion the word preceeding the cursor is replaced with the first candidate completion, and if there is more than one candidate they are listed in the +Errors window. If CTRL-N is pressed again then the word is replaced instead with the next completion candidate, and so on. If CTRL-P is pressed then the word is replaced with the previous candidate completion.

The following video demonstrates file completion for a couple of files in the current directory, and one under another directory:

![type:video](../../img/anvil-tut-using-the-keyboard-6-complete-part1-file.mp4)

The following video demonstrates word completion using words from the system dictionary file:

![type:video](../../img/anvil-tut-using-the-keyboard-6-complete-part2-word.mp4)

## Quick Marks

Anvil uses the function keys to perform quick and simple bookmarking. Clicking with the left mouse button and pressing a function key (F1 through F12) while the left mouse button is held creates a bookmark: the current cursor position is remembered. Pressing a the same function key without the mouse moves the cursor back to the remembered cursor position.

![type:video](../../img/anvil-tut-using-the-keyboard-7-marks.mp4)

## Line Kill

Anvil implements two keyboard shortcuts inspired by the shell. CTRL-K deletes the text from each cursor position to the end of the line containing that cursor, and CTRL-U deletes each entire line containing a cursor.


