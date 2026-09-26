# Range Statements

Anvil has a language that may be used to select and perform simple operations on text. The language is very similar to the expressions that can be used with the Acme Edit command, or the Sam editor's command language. The language operates on the text in the window body in which language statements are executed. If there are selections, an expression in the language operates on those selections, and if there are no selections all the text in the body is used as input. We'll refer to this language as _Range Statements_.

Syntactically, A range statement consists of a `!` character, followed by a sequence of expressions. The statement can be executed by middle-clicking as if it were a command. The expressions in the statement are executed from left to right. Each expression takes a set of ranges as input, narrows down the text in the ranges, and passes the modified ranges as input to the next expression. The first expression operates on the selections or text in the body. The statement may optionally end in a command that takes some action on the input ranges and produces no output ranges. If there is no special command, the final ranges are turned into selections in the body.

<figure markdown>
  ![Range Statements Data Flow Diagram](../../img/range-statements.svg)
  <figcaption>Figure 1: Range Statement Data Flow</figcaption>
</figure>

!!! note

    This section is going to include a lot of regular expressions. You might want to review the basics a little before proceeding, or at 
    least prepare yourself for many [leaning toothpicks](https://en.wikipedia.org/wiki/Leaning_toothpick_syndrome).

## Simple Expressions

To make this more concrete, let's work through some examples. First, download the README.md file for the Blender toolkit from [here](../../downloads/README.blender.md.txt) and open it in Anvil, or paste it into a blank window. We'll use it as some sample text for our statements. 

In the tag, type the simple statement `!7` and execute it by middle-clicking. Before middle-clicking make sure there is nothing selected in the window body. The basic expression `7` simply selects the seventh line in the file, so the line `Blender` is selected.

Now, select all the text of the first markdown section, titled `Blender`. Select from the `Blender` heading down to and including the line just above the heading for the `Project Pages` section. Now execute the `!7` statement again. Since we have selected some text, that selection is used as the first range for the statement, rather than the full file. So in this case it will select the seventh line relative to the beginning of selection, which is a blank line just under the screenshot link.

Delete the statement `!7` from the tag and instead type `!#2`. Unselect any text in the window body and execute it. This will select the second character in the file, in this case the '!' in the HTML comment at the beginning of the file.

Try the statement `!/=+/` (make sure to unselect all text first). This will search for the regular expression `=+` (a sequence of one or more equal signs) which will select the underlining under the heading that reads "Blender".

![type:video](../../img/anvil-tut-range-expressions-1.mp4)

## Compound Expressions

These simple expressions above—line numbers, rune numbers, and regular expressions—can be combined with operators to make more complex statements. Unselect all text and then type the compound statement `!2,4` into the tag and execute it. It will select all the text from the beginning of the second line to the end of the fourth line. We've combined the simple statements `2` and `4` using the `,` operator, which outputs a range from the beginning of the first operand to the end of the second.

Now instead try `!5+/--+/`. This statement is composed of the simple statements `5` and `/--+/` combined with the `+` operator. The `+` operator will select the second expression `/--+/` executed starting from the end of the first expression (line 5). When executed with nothing selected it will select the underline under the `Project Pages` section heading. Note that it didn't instead select either of the `--` sequences that are in the HTML comment at the top of the file since we forced the regex search to start after line 5.

Let's use the same statement, but change the operator to `;` instead so that it is `!5;/--+/`. The `;` operator selects from the beginning of the first operand to the end of the second. Execute it with nothing selected and it will select all the text from the beginning of line 5 to the underlining under `Project Pages`. The distinction between the operators `,` and `;` is subtle; the second operand to ',' is evaluated starting from the beginning of the input range, whereas the second operand in ';' is evaluated starting from the end of the first operand.

![type:video](../../img/anvil-tut-range-expressions-2.mp4)

## Starting with Multiple Selections

So far we've only worked with one range at a time by creating a single selection and executing one statement. But each of these expressions operates on a set of input ranges, so let's see what happens when we use multiple selections. Select each of the following lines in the readme file separately, making three separate selections:

    - [Main Website](http://www.blender.org)
    - [Reference Manual](https://docs.blender.org/manual/en/latest/index.html)
    - [User Community](https://www.blender.org/community/)

Let's select the names of the links in these selections: "Main Website", "Reference Manual", and "User Community". First, execute the range statement `!/\[.*\]/`. Here the regular expression will match the '[' character, a series of any character, then the ']' character. In each selection this will select the name portion of the links, including the square brackets. This is close, but not quite what we want.

Modify our range statement by appending another expression that will select from the second character to the last character in each range: `#2,$-#1`. The whole statement is thus `!/\[.*\]/#2,$-#1`. Clear the selections by clicking somewhere, select the three lines again, and then execute the new statement. It will select only the names of the links.

This exercise is useful for two reasons. First, we see that an expression can follow another expression, and the ranges output from the first expression are input to the next expression. More expressions can be appended to the end to build up more complex statements.  Second, it demonstrates a systematic approach of iterative refinement for building range statements: build the first expression, test it out, then add the next expression to narrow down the ranges further. Repeat this execution and addition cycle until the expression is complete.

Note that we could have run the two expressions separately and achieved the same result. That is, we could have selected the three lines, executed the statement `!/\[.*\]/` and then executed the statement `!#2,$-#1`. Since the ranges output from the first statement would create selections, and the second statement takes the current selections as input, we'd end up with the same set of link names selected.

![type:video](../../img/anvil-tut-range-expressions-3.mp4)

## Selecting Multiple Matches

So far, each the expressions we've seen simply refine the range that was input to it. That is, for each range they receive as input then produce exactly one range as output. However, to do useful work we often want to divide a range into subranges. 

This can be done with an x expression. Given a range as input, the x finds all matches of a regular expression in that range and outputs a new range for each match. The syntax of the x expression is `x/RE/`, where RE is a regular expression.

For example, let's find the link names like we did in the previous section using the x operator. Select the following lines in the README file as one entire selection instead of three separate selections:

    - [Main Website](http://www.blender.org)
    - [Reference Manual](https://docs.blender.org/manual/en/latest/index.html)
    - [User Community](https://www.blender.org/community/)

Now execute the statement `!x/\[.*\]/x/[^\[\]]*/`. The first expression `x/\[.*\]/` in this statement finds all the link names with enclosing brackets which will produce three new ranges. The second expression `x/[^\[\]]*/` operates on each of these new ranges to strip out the brackets by only accepting non-bracket characters.

The inverse to the `x` expression is the `y` expression. Whereas `x` selects all ranges that match it's regular expression, `y` selects all ranges that do _not_ match the regular expression. 

For example, if we wanted to select all text that is not an HTML comment we could use the expression `!y/<!--(.|\n)*?-->/`. The regular expression here matches the opening of the comment `<!--`, then any number of characters which may include newline non-greedily, then the closing of the comment `-->`. Execute the statement to yield the non-comment text. Try copying the comment at the top of the file and pasting it at the bottom and then execute the statement again after unselecting the text. It will select all the text except either comment.

![type:video](../../img/anvil-tut-range-expressions-4.mp4)

## Filtering Entire Ranges

The `g` expression is used to filter ranges. For each range, if the range matches the regular expression of `g` the range will be output, otherwise it will not. For example, say we want to find all the link URLs that are related to the wiki.

We can begin with the expression `!x/\[[^]]*\]\([^)]*\)/`, the regular expression portion of which will match in order: '[', a series of non-']' characters, ']', '(', a series of non-')' characters, then ')'. Execute this statement with nothing selected, and it will select the links in the document (of which there are nine). 

Now, let's extend it. Append the expression `g/wiki/` to our statement to modify the output of the `x` expression. The full statement is then `!x/\[[^]]*\]\([^)]*\)/g/wiki/`. Out of the nine ranges output by the initial expression, the `g` expression will select only those ranges that contain the string "wiki". One way to think of the combination of `x` and `g` is that the first `x` expression is defining records to process, and the following `g` expression is filtering those records based on a field inside them.

Finally, let's append `x/\([^)]*\)/#2,$-#1` to our statement, which selects the text inside the '(' and ')' brackets of the input ranges and excludes the brackets themselves. The full statement is then `!x/\[[^]]*\]\([^)]*\)/g/wiki/x/\([^)]*\)/#2,$-#1`. Unselect everything and then execute the combined statement, and we will end up with what we wanted: the URLs of the links related to the wiki.

The inverse of `g` is `v`, which selects all ranges that do _not_ match its regular expression. For example, to select the URLs of all non-wiki links we can change our `g` to a `v` in our final statement like so: `!x/\[[^]]*\]\([^)]*\)/v/wiki/x/\([^)]*\)/#2,$-#1`

!!! note

    A note on syntax: it's perfectly cromulent to add spaces between the expressions in a statement to make it a bit more 
    readable. For example, you can write the above like so: `!x/\[[^]]*\]\([^)]*\)/  v/wiki/  x/\([^)]*\)/  #2,$-#1` if desired. 
    Just remember that a single middle-click will only execute the space-separated word under the cursor, so to execute that entire 
    expression you would need to select it all and middle-click, or surround it with lozenges ('◊').

![type:video](../../img/anvil-tut-range-expressions-5.mp4)

## Commands

All the examples we've worked through so far all basically just narrow down the selections we started with in the window body, producing new selections in the window body. This is useful since we can then perform the normal operations that are available on multiple selections such as cutting, copying, or replacing. For example, if we wanted to change the bullets used for the markdown lists in the file from `-` to `*`, we could execute `!x/^- /` to select all the bullets, then type `* ` to replace all the selections at once.

However, range statements can actually change the text in the final ranges directly instead of just producing new selections. The language defines specific commands that may be performed on the current ranges. If we wanted to change the bullets as described, we could instead use the statement `!x/^- /c/* /`. The `x/^- /` expression selects the bullets, and the `c/* /` command changes the text in all selections to `* ` (the text between the slashes).

Other than the `c` command for changing text, we can instead use the `i` command to insert text before all ranges, and the `a` command to append text to all ranges. 

For example, if we wanted to make all instances of the word "Blender" bold by surrounding them with `**`, but only if that word is not part of a link, we could concatenate the statement `!x/^.*Blender.*\n/v/http/x/Blender/`, which finds all Blender occurrences not in links, with the expression `i/**/a/**/` which inserts `**` before each range, and appends `**` after each range. The complete statement in this case is `!x/^.*Blender.*\n/v/http/x/Blender/i/**/a/**/`

Finally, we can use the `p` command to print the ranges to the +Errors window. The `p` command accepts an argument in forward slashes that will be printed between each match as a delimiter. When the ranges to be printed are not complete lines, the following p operation comes in handy to print the ranges with a newline separating them:

```
    p/
    /
```
    
That is, use a literal newline as the argument to the `p` operator. 

![type:video](../../img/anvil-tut-range-expressions-6.mp4)

## Further Reading

There are more expressions and commands allowed in range statements that we haven't covered here. Check out the [range statement reference](../reference/range-statements.md) for more details.