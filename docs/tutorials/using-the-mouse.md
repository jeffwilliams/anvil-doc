# Using the Mouse

Anvil is meant to allow efficient operation driven by the mouse. This section gives an overview of the main functions the mouse provides in window tags and bodies.

## Left Click

Left clicking (that is, pressing the left mouse button and releasing it) in a window body or tag moves the cursor to that position, like most editors. Left clicking and dragging (that is, pressing the left mouse button, moving the mouse while the button is pressed, then releasing) selects text. Again, like most editors.

### Left Click: Cutting

Left clicking and dragging, then pressing the middle button while the left button is still pressed, cuts the selected text into the clipboard. Since most middle buttons are mouse wheels now—which can be fiddly to click with a second finger—left clicking and dragging, then pressing the control key while the left button is still pressed will also cut the selected text into the clipboard.

### Left Click: Pasting

Left clicking, then pressing the right button while the left button is still pressed, pastes the text from the clipboard. Alternately, left clicking then pressing the shift key while the left button is still pressed will also paste.

### Left Clicking Multiple Times

Left-clicking multiple times in the same place iteratively selects more text under the cursor. Left-clicking twice (double-clicking) on a word selects that word; specifically, it selects the series of characters that consist of letters, numbers and underscores under the cursor. Triple-clicking selects the space-separated string under the cursor. Quad-clicking selects the entire line.

For example, if the body contained a line consisting of the text `void some_function() {`, then double-clicking somewhere in `some` would select `some_function`, triple-clicking would select `some_function()`, and quad-clicking would select `void some_function() {`. 

Quad-clicking is a lot of clicks to select a line, so as an alternative double-clicking on the first character in a line will select the entire line.

Double-clicking on a type of bracket (One of `(`, `[`, `{`, or their closing bracket) will select all the text within the bracket and its matching partner. Triple-clicking on a bracket will select the text including the brackets.

Finally, double-clicking on a type of quote (One of `"`, `'`, or '◊`) will select all the text within the quotes, while triple-clicking will select the text and quotes. If there are multiple possible matching quotes in the same line then Anvil won't select anything. For example, in the line:

	"Wage was in her early, with two joeboys," Ratz said, shoving a draft across the bar with his good hand. "Maybe some business with you, Case?"
	
if you were to double-click on the second `"` there are two possible matches for the closing quote (the first and third) so Anvil won't select anything.

### Try it: Left Click

Let's practice left clicks by doing some cutting and pasting. 

1. Start anvil. In the left column create a new empty window by middle-clicking on the `New` command in the column tag. Paste the following text into the window body, taken from _The Story of Mel, A Real Programmer_ by Ed Nather:
```
Ed Nather (utastro!nather)
A recent article devoted to the *macho* side of programming
made the bald and unvarnished statement:

Real Programmers write in FORTRAN.

Maybe they do now,
in this decadent era of
Lite beer, hand calculators, and "user-friendly" software
but back in the Good Old Days,
when the term "software" sounded funny
and Real Computers were made out of drums and vacuum tubes,
Real Programmers wrote in machine code.
Not FORTRAN.  Not RATFOR.  Not, even, assembly language.
Machine Code.
Raw, unadorned, inscrutable hexadecimal numbers.
Directly.
```

2. Left click and drag to select the word `FORTRAN.` in the third line.

3. Cut it. While still holding the left mouse button, click the middle mouse button to cut the text. 
Alternately, while still holding the left mouse button press and release the control key.

4. Select and cut the line `Machine Code.` by left-clicking the first character in the line, releasing the mouse button, left-clicking again and while holding the button, press and release the middle button. Alternately press and release the control key instead of the middle button.

5. Paste it. In the third line where we cut the text `FORTRAN`, paste the text `Machine Code.` by pressing the left-mouse button, and while holding it press and release the right mouse button. Alternately use the shift key rather than the right mouse button. The line should now read `Real Programmers write in Machine Code.`

6. Triple-click the space-separated word `*macho*` to select it, and then type 'isoteric' to replace it.

7. Double-click on the left parenthesis of `(utastro!nather)` to select the text inside. While still holding the left-mouse button after the second click, press and release middle-mouse (or control) and then press and release right-mouse (or shift) to copy the text. 

8. Paste it somewhere.

### Demo Video

![type:video](../../img/anvil-tut-using-the-mouse-1-left-click.mp4)

## Middle Click

Middle clicking is used to execute text. Middle clicking on a string of non-space characters executes that string. The string may be a built-in Anvil command (such as New) or an operating system shell command. Middle clicking a selection executes the selected text, which lets you execute commands with arguments; for example executing `New file.txt` to create a new window to edit `file.txt`, or `ls -la` to verbosely list the contents of the current directory.

!!! note

    If you're using MacOS and you only have a two-button mouse, don't worry. You can simulate a middle click by pressing the Left mouse button and while it's pressed hitting the Command key.

If you will execute a command with arguments often, you can surround it with lozenge characters (◊) so that you don't have to select it everytime you want to execute it. Middle-clicking text surrounded by lozenges executes the text, which may include spaces. Since it's hard to type lozenges, you can use the built-in ◊ command or type CTRL-L to insert a lozenge. If there are selections, executing ◊ or CTRL-L will insert a lozenge at the beginning and end of each selection.

Commands are executed in the directory of the file being edited in the window, or in the current directory when executed from the editor or column tags.

Finally, pressing and holding the middle mouse button on a command, then clicking the left mouse button will execute the command with the last selected text as an argument. The text can be selected in any window, and doesn't need to be cut or copied. If holding the middle button then pressing the left is too fiddly, you can alternately do this by pressing and holding the middle mouse button on a command, then pressing the CTRL key.

The output from commands is written to the 'Errors' window: a window with the same name as the window from which it was executed, but with "+Errors" appended to the filename. 

### Try it: Middle Click

We'll be executing some OS commands in this section, which vary depending on which OS you're running.

=== "Linux"

    1. Start Anvil. 
    2. In the left column tag, type `New unix.txt`, select it, and middle click it. This will create a new window editing `unix.txt`.
    3. In the column tag, type `ls -C`, then surround it with lozenges using the lozenge command. Click a few times inside the lozenges to list files verbosely in the current directory. 
    4. In the tag of the `unix.txt` window type `echo Hello, ` and surround it with lozenges. In the body type these words: 

            Dennis
            Ken
            Rob

    5. Execute `echo Dennis` using a dynamic argument. Select Dennis by double-clicking it. Then press the middle button on the word "echo" in the tag, and press and release the left mouse button. You should see a new Errors window created showing the text "Hello, Dennis"; the output from the command we just executed.

    6. Execute `echo Ken` in the same manner as step 5. The Errors window will show the text "Hello, Ken" below "Hello, Dennis".
    
    7. Execute `echo Rob` in the same manner as step 5. 

=== "Windows"

    1. Start Anvil. 
    2. In the left column tag, type `New unix.txt`, select it, and middle click it. This will create a new window editing `unix.txt`.
    3. In the column tag, type `dir /d`, then surround it with lozenges using the lozenge command. Click a few times inside the lozenges to list files verbosely in the current directory.
    4. In the tag of the `unix.txt` window type `echo Hello, ` and surround it with lozenges. In the body type these words: 

            Dennis
            Ken
            Rob

    5. Execute `echo Dennis` using a dynamic argument. Select Dennis by double-clicking it. Then press the middle button on the word "echo" in the tag, and press and release the left mouse button. You should see a new Errors window created showing the text "Hello, Dennis"; the output from the command we just executed.

    6. Execute `echo Ken` in the same manner as step 5. The Errors window will show the text "Hello, Ken" below "Hello, Dennis".

    7. Execute `echo Rob` in the same manner as step 5. 

### Demo Video

![type:video](../../img/anvil-tut-using-the-mouse-2-middle-click.mp4)

## Right Click

Right clicking is used to search, open files, and execute plumbing rules. Right-clicking with no modifier key performs searching, while right-clicking while holding Alt opens files or executes plumbing rules.

## Right Click: Searching

Right clicking a word in the tag or body of a window will search for that word in the body. The search starts at the cursor position, or the last term found by the previous search. Similarly, right-clicking a selection, or within a lozenge-delimited string will search for that selection literally. Below we call the text searched for the 'search term'. Holding shift when right clicking searches backwards.

As a special case, if the search term is surrounded by slashes it is treated as a regular expression rather than a literal string. For example, selecting the text `/a.*c/` and right-clicking it will search for the regular expression `a.*c`.

After a search is executed, clicking a second time on the same term will continue the search from the position of the last match, creating another selection for the next match.

There is a way to search and select all instances of a term which we'll learn about later.

### Try it: Searching

1. Start anvil. In the left column create a new empty window by middle-clicking on the `New` command in the column tag. Paste the following text into the window body, an excerpt from a classic answer posted to stack-overflow:

        You can't parse HTML with regex. Because HTML can't be parsed by regex. 
        Regex is not a tool that can be used to correctly parse HTML. As I have 
        answered in HTML-and-regex questions here so many times before, the use 
        of regex will not allow you to consume HTML. Regular expressions are a tool 
        that is insufficiently sophisticated to understand the constructs employed by 
        HTML. HTML is not a regular language and hence cannot be parsed by regular 
        expressions. Regex queries are not equipped to break down HTML into its 
        meaningful parts. so many times but it is not getting to me. Even enhanced 
        irregular regular expressions as used by Perl are not up to the task of parsing 
        HTML. You will never make me crack. HTML is a language of sufficient complexity 
        that it cannot be parsed by regular expressions. Even Jon Skeet cannot parse 
        HTML using regular expressions. Every time you attempt to parse HTML with 
        regular expressions, the unholy child weeps the blood of virgins, and Russian 
        hackers pwn your webapp. Parsing HTML with regex summons tainted souls into 
        the realm of the living. 
        
2. Search for HTML. In the body of the new window, right click on HTML to highlight the next instance of HTML. Right click it again to find and highlight the next instance of HTML in the body. Right click it to highlight the second instance. Continue right clicking until the search wraps.

3. Search for occurrences of regex and html, ignoring case. In the tag type /(?i)regex|html/. Right click it to find the first instance of regex. Click a few more times.

4. Clear the search by left clicking in the body somewhere. Then hold shift and right-click in /(?i)regex|html/ to search for the previous occurrence before the cursor.

![type:video](../../img/anvil-tut-using-the-mouse-3-right-click.mp4)

## Right Click: Opening Files

Setting aside plumbing rules—which we’ll get to in the next section—right clicking on a word or selection while holding Alt opens that file in a new window. If there is already a window for that file, it focuses that window instead. If it is a directory, then the window will display the files in the directory. 

What's more, if the word or selection is followed by a line number, or a line number and a column number, that line and column is selected. If it's followed by an exclamation mark and a regular expression, that expression is searched for in the window.

To open files or directories that contain a space in the name, you need to select the entire name before right-clicking.

## Try it: Opening Files with Right Click

We're going to practice browsing through some source code files. 

=== "Linux"

    1. Download the source code for typoh—a simple program to replace escape sequences in text and html files with unicode characters—from [here](../../downloads/typoh.tar.gz).
    
    2. Untar it 
    
    3. Start Anvil in the untarred directory. In the right pane you'll see the path `.` (the current directory) open, listing the source code files for typoh.
    
    4. Open `replacer.go`. Hold the Alt key and right click on `replacer.go` in the window for `.`. This will open it in new window.
    
    5. Find the Replace function. In the window tag type 'Replace(', highlight it, and right click it to find the Replace function.
    
    6. Search for the definition of the Typographer type. In the tag type `grep -rn 'type Typographer'`. Select it and middle-click to execute it. Anvil will open a new `./+Errors` window that will display the output of the grep command. 
    
    7. Open the definition of the Typographer type. The grep output will show a line consisting of colon-separated fields. The fields are the filename, the line number, and the matching line. Click just after the line number and type a space. Then Hold the Alt key and right click on the filename in the grep output. This will highlight the first line of the definition of Typographer type in the window for the file `main.go`.
    
=== "Windows"

    1. Download the source code for typoh—a simple program to replace escape sequences in text and html files with unicode characters—from [here](../../downloads/typoh.tar.gz).
    
    2. Untar it 
    
    3. Start Anvil in the untarred directory. In the right pane you'll see the path `.` (the current directory) open, listing the source code files for typoh.
    
    4. Open `replacer.go`. Hold the Alt key and right click on `replacer.go` in the window for `.`. This will open it in new window.
    
    5. Find the Replace function. In the window tag type 'Replace(', highlight it, and right click it to find the Replace function.
    
    6. Search for the definition of the Typographer type. In the tag type `powershell Select-String -Path \"*.go\" -Pattern \"type Typographer\"`. Select it and middle-click to execute it. Anvil will open a new `./+Errors` window that will display the output of the Select-String command. 
    
    7. Open the definition of the Typographer type. The Select-String output will show a line consisting of colon-separated fields. The fields are the filename, the line number, and the matching line. Click just after the line number and type a space. Then Hold the Alt key and right click on the filename in the grep output. This will highlight the first line of the definition of Typographer type in the window for the file `main.go`.

### Demo Video

![type:video](../../img/anvil-tut-using-the-mouse-3-right-click-part2.mp4)
    
## Right Click: Plumbing

The other thing that right clicking with Alt does is execute plumbing rules. Plumbing rules compare the word or selection just clicked against a list of patterns and actions. If one of the patterns matches, the action is executed. If none of the patterns match, then Anvil assumes the word or selection is a file and tries to open the file as described above.

Plumbing rules are defined in a configuration file loaded by Anvil on startup. More information about defining plumbing rules can be found in the [Plumbing Reference](../reference/plumbing.md).

### Demo Video

![type:video](../../img/anvil-tut-using-the-mouse-3-right-click-part3.mp4)

