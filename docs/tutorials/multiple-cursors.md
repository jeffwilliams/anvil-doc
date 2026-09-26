# Multiple Cursors and Multiple Selections

This section explains and demonstrates how to use multiple cursors and multiple selections in Anvil. If you've worked through the previous sections you've seen this used a few times, such as for the CTRL-D shortcut. Here we give it a more thorough treatment. 

The main idea of multiple cursors or selections is simple: perform the same operation in multiple places at once. For example, if you have multiple cursors and type some text then the text is inserted at each cursor and the cursor is moved forward. Performing a paste with multiple cursors pastes the clipboard content at each cursor. 

Similarly if you create multiple selections and type some text, all of the selections are replaced with that text. If you create multiple selections and type backspace, then the last character in each selection is deleted, and afterwards typing will append to all selections. If you cut when there are multiple selections, each selection is cut. Delete will delete all the selections.

## Creating and Deleting Multiple Cursors

Multiple cursors can be created by holding the Alt key while left clicking. If you then left-click without holding alt, all cursors but the last are removed. If you are creating multiple cursors while holding Alt and accidentally add one to the wrong place, simply keep Alt pressed and left-click that cursor again and it alone will be removed so you can then add it to the right place.

## Creating and Deleting Multiple Selections

Creating multiple selections is similar. First, create a selection by dragging, clicking multiple times, or searching. Then while holding Alt, create new selections by dragging or clicking multiple times. If you add one to the wrong place, keep Alt pressed and click the one you want to remove.

Another method of creating multiple selections is searching. Each time the same search is executed a new selection is added for the next matching term. These can all then be manipulated at once. 

Finally, you can create multiple selections using the `x///` and `y///` operators in Range Statements, which we'll see in a later tutorial.

## Converting Selections to Cursors

If you have multiple selections and then press the Left key, the selections are replaced with cursors where the beginning of each selection was. The Right key creates cursors at the ends.

If you have multiple selections and then press the Escape key, a cursor is created at the beginning of each line that is contained in the selection. This is useful, for example, to comment out a block of text by inserting `//` or `#` at the start of each line. 

## Rotating selections

If there are multiple selections present, and the Rot command is executed then the selections are rotated: the contents of the first selection is placed at the location of the second, the contents of the second are moved to the next, and so on, with the contents of the last selection being placed where the first was.

This can be useful for swapping the order of function arguments.

## Try it: Multiple Cursors and Selections

1. Start Anvil

2. Create a new window with the New command and paste this text into the body:
```
usage() {
	printf("Usage: frobnicate <degree> [file...]\n");
	printf("\n");
	printf("Frobnicate performs a tangential resiliancy extrapolation");
	printf("of degree <degree> on the specified files.");
}

int main(int argc, char* argv[]) {
    if (argc < 2) {
		usage();
		return 1;	
    }
	do_something("arg1", 2);
}
```

3. Update the `usage()` function to print to standard error instead of standard out. 

    1. Double-click on the first "printf" word in the usage() function to select it. 
    2. Right click three times to create selections containing each other "printf". 
    3. Press the Left-arrow button on the keyboard to create cursors at the beginning of printf. Type "f".
    4. Select "(" in the first printf line.
    5. Right click three times to create selections containing each other opening brackets of printf. 
    6. Type "(stderr, " to add the first parameter.

4. Update the `usage()` function to be more specific about what "degree" is.

    1. Left click between the "<" and "degree" in the first printf line
    2. Hold Alt and left click between the "<" and "degree" in the last printf line in the function. Now there are two cursors.
    3. Type "base-" so that the "<degree>" argument is now "<base-degree>".
        
4. Change the order of the function arguments to `do_something()`.

    1. In the Tag type "Rot".
    2. Select all of the first argument ("arg") to do_something.
    3. Hold Alt and select the second argument (2) to do_something.
    4. Middle click Rot to swap the arguments so that it now reads `do_something(2, "arg1");`

## Demo Video

![type:video](../../img/anvil-tut-multi-cursor.mp4)

