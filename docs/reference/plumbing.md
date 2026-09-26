# Plumbing Reference

Anvil allows you to define special actions that are taken when using ALT-Right Click on a word or selection, which override the default behaviour of trying to open that object as a file.

These actions are defined as rules in the file "plumbing" in the [Anvil configuration directory](config.md). Each rule consists of two parts: a regular expression pattern, and an action to take. When the word or selection (a text object) is clicked, Anvil considers each rule in the order they are defined in the plumbing file, and if the text object matches the pattern of a rule, then the action of that rule is performed and no more rules are considered. The action of a rule can be an OS command, or an Anvil command.

If a plumbing rule is executed from a remote window, the command in the action is run remotely.

## Plumbing File Format

Lines beginning with '#' in the plumbing file are comments and not executed.

Each rule in the plumbing file consists of a `match` line that defines the pattern, followed by a `do` line that defines the action to take:

	match <pattern>
	do <command>

The `<pattern>` is a regular expression. The `<command>` is an OS or Anvil command. In the command, $0 is substituted with the entire match text that matched `<pattern>`. Terms of the form $N (for N = 1, 2, 3, ...)  are substituted with the first, second, third, and higher groups in the regular expression. Groups in the regular expression are enclosed with '(' and ')'. $N may be written ${N}.

Here is an example of a simple plumbing file:

	match https?://[^ ]*
	do firefox --new-tab --url $0
	
	match .*\.jpg$
	do eog $0
	
	match .*\.pdf$
	do evince '$0'

	match ^.*\.dump$
	do Load ${0}

This example contains four rules:

  * the first rule matches URLs, and when matched opens that URL in Firefox
  * the second matches JPEG files and opens Eye of Gnome to view the image
  * the third matches PDF files and launches Evince to view them
  * The fourth matches an Anvil dump file, and loads it in Anvil

## Sample Plumbing Rules

### Open URL in Browser

These rules can be used to plumb a URL by opening it in a browser. Choose one for the browser you use. The browser binary must be in your path.

Firefox:

	match https?://.*
	do firefox --new-tab --url "$0"

Microsoft Edge:

	match https?://.*
	do start microsoft-edge:$0

Chrome:

	match https?://.*
	do chrome $0

### Load .dump file

This rule loads a .dump file as if you used the Load command.

	match ^.*\.dump$
	do Load ${0}

### Load Files from Python Exceptions

This plumbing rule can be used to open a file at the line number described in a python exception stacktrace.

	match File "([^"]*)", line (\d+)
	do Acq ${1}:${2}

For example, in the stacktrace below, selecting the line 'File "t.py", line 6, in &lt;module&gt;' and then performing plumbing would open the file example.py at line 6.

	Traceback (most recent call last):
	  File "example.py", line 6, in <module>
	    func1(arg)
	  File "example.py", line 20, in func1
	    print(nam)
	NameError: name 'nam' is not defined
