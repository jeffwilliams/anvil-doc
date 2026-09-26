# Range Statement Reference

Executing text of the form `!...` executes a statement that selects and manipulates text in the body of a window. The statement consists of a series of basic operations that are executed in series. Some operations select text, and some perform a command on the selected text. Those that select text perform their selection relative to the previous selections in the expression. The first selection in the expression operates relative to each of the current selections in the window body, and if there are no previous selection the entire text of the window body is used.

The simple expressions are:

| Expression | Behaviour |
| --------------- | --------- |
| N | If N is a number, select that line within the ranges. Example: !40 |
| #N |  If N is a number, select and go to that character. Example: !#40 |
| /RE/ | Select the first regular expression RE in the ranges |
| 0 | The beginning of the file |
| $ | The end of the file |
| . | The position of the primary cursor |

Expressions may be combined using four operators:

| Operator | Behaviour |
| --------------- | --------- |
| EXPR1+EXPR2 | Execute EXPR2 starting from the end of EXPR1 |
| EXPR1,EXPR2 | Select from the beginning of EXPR1 to the end of EXPR2 |
| EXPR1-EXPR2 | Execute EXPR2 looking in the reverse direction starting at the beginning of EXPR1 |
| EXPR1;EXPR2 | Select from the beginning of EXPR1 to the end of EXPR2, but evaluating EXPR2 at the end of EXPR1 |

There are five looping and filtering expressions:

| Expression | Behaviour |
| --------------- | --------- |
| x/RE/ | For each matching regular expression RE in the ranges create a new range |
| l/RE/ | Like x//, but match entire line containing RE. Matches the regex `^.*RE.*$` |
| y/RE/ | For each section of text between the matching regular expression RE create a new range |
| z/RE/ | For each match of RE, create a new range from the start of the match to the start of the next match of the RE |
| g/RE/ | For each range, only keep those that contain RE |
| v/RE/ | For each range, only keep those that do not contain RE |

Commands may be grouped by enclosing them in braces:

	{ EXPR1 [EXPR2] [EXPR3]... }
	
This has the effect that each expression in the group is executed in the ranges that were input to the group, rather than the output of the preceeding expression. For example, EXPR2 in the above expression will operate on the same input ranges as EXPR1 does, instead of operating on the ranges that EXPR1 outputs. Likewise EXPR3 operates on the original input range, rather than the output of EXPR2. Another way to think of it is that where normally expressions written sequentially are executed sequentially, the expressions in a group are logically executed concurrently.

The commands that operate on the previous selections defined by the selections are:

| Expression | Behaviour |
| --------------- | --------- |
| d | Delete the text |
| p/sep/ | Print the text. The /sep/ argument is optional, and specifies a separator string to print between ranges. Escapes such as \n are supported. |
| P/sep/ | Print the text like 'p', but prefix it with the line and column of the start and end of the range |
| c/TEXT/ | Change the text of all selections to be TEXT |
| i/TEXT/ | Insert TEXT at the beginning of each selection |
| a/TEXT/ | Append TEXT at the end of each selection |
| s/RE/REPL/ | Replace the text matching RE with the text REPL |
| = | Print the filenames and line numbers of the ranges  |
| C | Copy the text in the ranges to the clipboard. The text from the ranges are concatenated  |

For any of these commands that accept an argument (text delimited by /), you may use the escapes \n, \r, and \t to represent the newline, carriage return, and horizontal tab characters respectively.

All regular expressions in the expressions above (where "RE" occurs in the syntax tables above) use the [syntax of Go regular expressions](https://pkg.go.dev/regexp/syntax).

## Examples

For example, executing this expression will create multiple selections, one for each line that ends with an opening brace:

	!x/^.*{$/

We can add an additional 'g' expression to the end to further refine the selection to only those that also contain the word `func`. Note: addressing expressions operate on the set of current selections, so if you want to operate on the full text of the file, remove extra selections by left clicking once. The new expresssion is:

	!x/^.*{$/ g/func/

We can insert some text before those lines those lines (i.e. begin a // comment):

	!x/^.*{$/ g/func/ i/\/\//

As another example, to select from the first occurrence of `begin` in the file to the first occurrence of `end` inclusive, execute this expression:

	!/begin/,/end/

For further examples, refer to the [Tutorial](../tutorials/range-statements.md).
