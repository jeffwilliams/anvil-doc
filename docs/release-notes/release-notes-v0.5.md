# Version 0.5 Release Notes 

## Features Added

* If CTRL+left-click is performed on a column layout box, evenly-space the windows in the column.
* Add 'P' command for range statements and improve range printing. This change adds the P command in range statements which prints the line and column of the starts and ends of ranges before printing the ranges themselves. It also fixes the heuristics to tell when to print only the line and column of a match, or both the line and column of the start and end of the match.
* Interpret escapes like `\n` in the `p` command of range statements
* Set the environment variable `ANVIL_CFG_DIR` when executing OS commands
* Add the Settag command to set the current Window tag.
* Add a new configuration file setting `exec` in the table `[general]` to execute commands on startup. 
* Add keyboard shortcuts CTRL-/ and CTRL-? to perform forward and backwards search for the term under or just preceeding the cursor.
* Print a message when setting a password for SSH
* Make Alt+Up and Alt+Down make new cursors
* Implement "Block Pasting". If you copy to clipboard when there are multiple selections, Anvil remembers the selections separately. Later if you unselect the selections and create one or more cursors in the body text and paste, each of the separate selections copied to the clipboard are pasted to a corresponding cursor. If the number of cursors equals the number of selections in the initial copy, then the selections are pasted to each cursor. If there are fewer cursors than copied selections, new cursors are created directly below the last until there are an equal number of cursors as selections, and then the text is pasted at those cursors.
* Add the `ado` command to extas. `ado` allows you define rules that, when matched, execute a command in the context of that window. After started, this command listens for files to be opened in Anvil and when one is opened, checks if the filename matches the regular expression for a rule. If it matches then the command from the rule is executed. The file format is similar to the plumbing file.

### Indent Using Spaces instead of Tab

A couple of the new features can be combined to cause Anvil to always insert spaces instead of the tab character when the Tab key is pressed. To do this, in your settings.yaml configuration file, add the following settings:

    [general]
    exec = ["Tab '    '"]

and restart Anvil. These settings will cause the command `Tab '    '` to be run when Anvil is started, in the context of the editor tag. When Tab is run from the editor tag it sets the string that tab will insert for all windows.

If instead you want to temporarily change tab for a session, run the Tab command manually from the editor tag. If you want to change tab for a specific window, run the Tab command from the tag or body of that window. To automatically set the tab string to a different value for specific windows, use the `ado` command, like in the next section.

### Customizing the Window Tag Based on the Filename

A few of the new features can be combined to have Anvil change the user-customizable part of window tags when the window filename matches a pattern. To do this, follow these steps:

1. Make sure the new `ado` command is in your execution path.

2. In your `settings.yaml` configuration file, add the following settings:

        [general]
        exec = ["ado"]

3. Create a new file in the Anvil configurion directory with the name `filehooks`. Add lines similar to the following to the file:

        match \.md$		
        do Settag " Do Acq Look ◊Fuzz ◊ mdtoc"

4. Restart Anvil

The settings in `settings.yaml` will cause Anvil to start the command `ado` on startup. `ado` will load the rules from the file `filehooks` and listen for windows to be open. When one matches the regex `\.md$` (i.e. a file with the extension .md; a markdown file) it runs the `Settag` command to set the tag of the matching window to " Do Acq Look ◊Fuzz ◊ mdtoc".

## Defects Fixed

* Ensure window tags are visible when moved to new screen. If Anvil is resized and window tags would become invisible because they are positioned below the bottom of the window, instead move them up until they are visible. 
* Fix issue in Rot with syntax highlighting. This fixes an issue where syntax highlighting breaks when you Rot arguments of different highlights. E.g., a string vs number.
* Fix issue in search when search term changed while old search item highlighted. Before the fix the following behaviour is observed: have the word `foo` twice in a window and a couple other words, but not `qux`. Then search for foo a few times, and it will alternate between the two `foo`. Then search for `qux`. It is not found, but since `foo` is highlighted it alternates between the two.
* Prevent duplicate window ids on Load
* Add Tab command to set text inserted when tab hit. Run `Help Tab` for help and examples.
* Add timeout for initial SSH message exchange. Even with a TCP connection timeout, some ssh operations can hang for a very
  long time on initial connect. This can happen, for example, when attempting to connect to a host behind an SSH proxy, and the host does not exist.
* Fix undo after backspace with multiple selections/cursors. There was an issue where if you have multiple selections or cursors, then type backspace, then the last character is deleted from all selections/cursors. However if you then undo, the deleted character from only one of the multiple selections/cursors is replaced, and the next undo does one more character and so on.
* Improve autoindent when enter pressed within leading space. There was an issue with autoindent where if you position the cursor somewhere within the leading space of the line, and then hit enter, it would make a new line with all of the leading space, rather than just the prefix up to the cursor. If there was more text after the position where the cursor was then it ends up getting indented too far: by the amount of leading whitespace plus the remainder of the leading whitespace up to the start of non-whitespace text.
* Preserve running jobs in tag and history when Load performed. If you start Anvil, execute some long-running jobs, and then execute Load, then the jobs are still present in the editor tag after Load.
