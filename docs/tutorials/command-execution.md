# Command Execution

The previous tutorials already introduced command execution, but this section expands on that knowledge.

## Built-In Commands

Anvil has quite a few built-in commands. Some of these are shown by default in the tags of the editor, columns, and windows, such as `Newcol`, `Help`, `New`, and so on. All of the built-in commands begin with a capital letter to help avoid name collisions with OS commands, which are usually lower-case. Some of the commands have a version with a "\*" suffix, such as `Cmds` and `Cmds*`. The * version of these commands is more verbose.

To list all of the built-in commands, execute the `Help` command, which is usually present in the editor tag. Help lists all the commands, a brief synopsis, and each command has a lozenge-enclosed string that can be executed to show the detailed help. Alternately, you can consult the [command reference](../reference/commands.md)  for explanations.

In this section we'll go over a few of the commands that are either useful enough to warrant highlighting, or need extra explanation than is provided in the Anvil help. 

### Recent, Wins and Cmds

These three commands are helpful for organization when you have a lot of windows open.

The Recent command lists files that had been opened in Anvil but have since been closed. There is a maximum number of recent files that Anvil will remember.

The Wins command lists the files currently open in Anvil.

The `Cmds` command lists recently executed commands. For each command it lists the start and end time, the full command, and if the command exited unsuccessfully it lists the error code. The `Cmds*` version is like the plain version, but also lists the host and directory the command was executed on as an `On` command, which means it can be highlighted and executed to replay the command on the same host it was executed on.

#### Demo Video

In the video below we open a few files and run the Wins command to list the open files. Then we close `dir/file3.txt` and run the Recent command, showing that it was recently open. Then we close `file2.txt` and run Recent again, showing both files. Finally we run a couple OS commands (ls, cat), try to run a command that doesn't exist (unknown-command), and then run Cmds to list the recently run OS commands. Note that the exit code for unknown-command is listed, since it failed.

![type:video](../../img/anvil-tut-cmds-recent.mp4)

### Title

The `Title` command changes the name of the window as displayed in the window titlebar. All the arguments to `Title` are treated as part of the name. This can be useful to help disambiguate which project is being edited in which instance of Anvil.

![type:video](../../img/anvil-tut-cmds-title.mp4)

### Do, Acq and On

`Do` runs its arguments as a command, but in the directory of the current window. It's useful to run a command shown in one window in the directory or on the host of another window by using the [middle-left click execution](../tutorials/using-the-mouse.md#middle-click) technique.

`Acq` is like the Do command, but for opening files. Acq attempts to acquire (open or plumb) its argument as if it were being opened from the context of the current window.

`On` runs a command in a different directory or on a different host. The first argument is a path: either a local directory, or a host and directory in ssh notation. The remaining arguments are taken as the command and arguments to execute.

### Clr

`Clr` deletes the contents of the body of the window in which it is run. This is most useful for +Errors windows, where you might want to clear the results of previous executions of commands.

### Dump and Load

`Dump` and `Load` are used to save and restore the editor state respectively. `Dump` stores the state to a file in the current directory named `anvil.dump` by default, but when given an argument dumps to the named file instead. Similarly, `Load` loads from `anvil.dump` by default, or the file named by the argument when given. When Anvil is started from the command line, the -l option can be used to load a dump file.

Most of the editor state is stored, such as the title; the column, editor and window sizes and tags; the command history; and the contents of any unsaved, unnamed windows.

#### Demo Video

The video below demonstrates `Dump` and `Load`. First, we load a previously created dumpfile `anvil.dump` by executing Load with no arguments. Note that there is an unnamed, unsaved file in the bottom left that is restored from the dumpfile. The video runs the Cmds command to demonstrate that Load restores the list of commands that had been previously run in the session.

Next, we create a different dumpfile by closing a few windows then executing `Dump simple.dump`. Then we load the default dumpfile `anvil.dump` by again executing Load, and then load our new dumpfile by executing `Load simple.dump`.

![type:video](../../img/anvil-tut-cmds-dump.mp4)

### Syn

The `Syn` command is used to control syntax highlighting. By default, Anvil applies syntax highlighting to files it loads if the file extension is supported by highlighting. The highlighting can be turned off by using `Syn off`. The `Syn list` command lists all the languages for which syntax highlighting is supported. Run `Syn <language>` to apply syntax highlighting for the mentioned language to the window body. This last form is useful, for example, in +Errors windows where a diff was just displayed.

#### Demo Video

![type:video](../../img/anvil-tut-cmds-syn.mp4)

## Executing OS commands

In the earlier tutorials we've already seen how to execute Operating System commands. The basic idea is that a shell command (or pipeline) can be executed using the middle-mouse button, and the output is written to an +Errors window unique to the directory where the command is executed.

While a command is executing, the first word of the command is shown in the left side of the editor tag. Once it completes it is removed.

This basic behaviour can be modified by prefixing the command to be executed with one of the characters `>`, `|`, or `<`.

Prefixing the command with `>` writes the selection in the current window to the standard input of the command being executed. If there is no selection, the entire contents of the body of the window is used instead. The output is written to the +Errors window. If there are multiple selections the command is run once for each selection.

The `|` prefix writes the selection or body to the standard input of the command, but replaces the selection or body with the standard output of the command. Again, if there are multiple selections each is replaced separately.

Finally, the `<` prefix replaces the selection or body with the standard output of the command.

When Anvil runs an OS command it exports some environment variables that can be used by the executed program, such as the full path and directory of the file in the window where the command was executed, and information that allows connecting to the Anvil API. These environment variables are described in the [environment variables reference](../reference/environment.md).

### Try it: OS Commands

Let's work on a grocery list.

=== "Linux"

    1. Open Anvil and in a new window paste the following:
    
            Grocery List
            --------

            Bananas
            Apples
            Carrots
            Cheese
            Bread
            Milk
            Eggs
            Brocolli
            Spinach
            Bok Choi
            Chick Peas
    
    
    2. Add a date to the list. Create a new empty line under Grocery List and type `<date`. Middle click on `<date` to replace it with the current date.
    
    3. Sort the list. In the tag type `|sort`. Select the lines containing the food (Bananas through Chick Peas) and then middle-click `|sort` to sort it alphabetically.
    
    4. Count how many things are in the list. In the tag type `>wc -l`, surround it with Lozenges, ensure the lines containing the food are selected, and then execute `>wc -l`.
    
=== "Windows"

    1. Open Anvil and in a new window paste the following:
    
            Grocery List
            --------

            Bananas
            Apples
            Carrots
            Cheese
            Bread
            Milk
            Eggs
            Brocolli
            Spinach
            Bok Choi
            Chick Peas
    
    
    2. Add a date to the list. Create a new empty line under Grocery List and type `<date`. Middle click on `<date` to replace it with the current date.
    
    3. Sort the list. In the tag type `|sort`. Select the lines containing the food (Bananas through Chick Peas) and then middle-click `|sort` to sort it alphabetically.
    
    4. Count how many things are in the list. In the tag type `>find /c /v ""`, surround it with Lozenges, ensure the lines containing the food are selected, and then execute `>find /c /v ""`.

### Demo Video

![type:video](../../img/anvil-tut-cmds-os.mp4)

### Killing Commands

Sometimes you might want to stop a long-running OS command. This can be done with the `Kill` built-in command. When `Kill` is executed with no arguments, it kills the first of the currently running OS commands. With an argument it kills the command whose first word matches the argument.

### Listing Commands

The `Cmds` command lists which commands have been recently executed, and the currently running commands

### Forcing Local Execution

When OS commands are executed in a remote window (a window with a file open from a remote SSH server) then the command is executed on the remote server. However, there are times you would like to run a command on the local machine, despite the window being remote. You can do this by prefixing the command with `+`. For example, to execute the `ls` command locally when you middle click it somewhere in a remote window's tag or body, you can use the command: 

    +ls

If you want to execute the command and also use one of the `|`, `<` or `>` prefixes, put the `+` _after_ the redirect. For example:

    >+wc




