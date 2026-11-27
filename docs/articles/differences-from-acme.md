Periodically, the question "What are the differences between Anvil and Acme?" pops up. There are a few major differences:

1. Anvil supports syntax highlighting. This is, of course, a radical departure from Rob Pike's [preference](https://groups.google.com/g/golang-nuts/c/hJHCAaiL0so): "Syntax highlighting is juvenile. When I was a child, I was taught arithmetic using colored rods ([Cuisenaire Rods](http://en.wikipedia.org/wiki/Cuisenaire_rods)). I grew up and today I use monochromatic numerals."

2. Anvil allows remote editing over SSH. If you open a file with a name of the form `[username@]host:/path/to/file`, then Anvil will establish an SSH connection to the host (if one doesn't already exist) and allow the user to edit the file and execute commands remotely in the context of the window.

3. Anvil allows the use of multiple cursors and selections. What's interesting about this is that the text manipulation language called ["Range Statements"](../tutorials/range-statements.md) in Anvil uses the current selections in the window as input (the initial ranges on which to operate), and those statements that produce a set of ranges when executed replace the set of selections in the window. Range Statements are mostly equivalent to the Sam language in Acme, which most people refer to as Structural Regular Expressions (but of which Structural Regular Expressions are only a subset of the language). So the practice of selecting text with the mouse or the keyboard, adjusting ranges with expressions, and switching between the two is slightly more tactile than in Acme.

4. Anvil is a bit more convenient to use with the keyboard than Acme. For example, moving the cursor up and down with ++arrow-up++ and ++arrow-down++ is standard, text can be selected using ++shift++ and navigation keys, a word can be executed using ++control+t++, and a line by ++control+enter++. A number of other common keyboard shortcuts are [supported](../reference/keyboard.md).

5. Anvil has better support for files with spaces in the name.

6. Anvil has a special syntax that makes it easier to execute commands or perform searches that contain spaces. If you surround the command or search with lozenges (i.e. `◊|wc -l◊` or `◊search term◊`) then executing or searching using ++middle-button++ anywhere within the lozenges executes or searches for the entire delimited string. This is convenient for things you do often.

7. Like Acme, Anvil allows searching forwards with ++right-button++, but Anvil also supports searching backwards with ++shift+right-button++, as well as searching for a [regular expression](../tutorials/using-the-mouse.md#right-click-searching).

8. From [Wily](http://www.cs.yorku.ca/~oz/wily/), Anvil borrows the ability to press ++escape++ to highlight the recently typed text for easy execution or searching.

9. In Acme, performing a ++right-button++ Acquires a file, searches, and plumbs. However in Anvil Acquiring and plumbing is performed using ++alt+right-button++ ([explanation](why-alt-right-click.md)) and searching with a simple ++right-button++. This is to avoid having to distinguish between a search and an acquire/plumb by checking for file existence on a remote host.
