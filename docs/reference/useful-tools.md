# Useful Tools

This page lists a number of tools (simple programs) that are particularly useful to run as external commands from Anvil. Some are specifically written to use the Anvil API.

## C Development

This section lists tools useful for C development.

### Format

The Format shell script uses clang-format to format a selection of C code in Anvil. It can be downloaded [here](../../downloads/Format), and is also found in the Anvil source code under tools/format.

### Rt

When run from Anvil the Rt command reads a ctags tag file, finds the function specified as an argument, and acquires it in a window.

## aad

Anvil Auto-Dump (aad) periodically runs the Anvil Dump command to create a dumpfile. It is meant to be run from within Anvil. When started it will continue running until Anvil exits or aad is killed.

By default it will Dump to a file named 'anvil-auto.dump' every 30 seconds. These values can be overridden by command line options:
	
| Option | Semantics |
| --------------- | --------- |
| -i I, --interval I | The interval in seconds between Dumps |
| -d F, --dumpfile F | The name of the dumpfile to generate |
| -v, --verbose | Print extra info |

aad can be downloaded from the [download](../download.md) page, and can be found in the Anvil source code at `tools/aad`.

## mdtoc

The mdtoc command prints a table-of-contents for a Markdown file. When run from Anvil, the mdtoc command reads the contents of the current window body and outputs each line in the body that begins with '#'. It appends the filename and line number to each line for easy access from Anvil.

## aedit

The aedit command is meant to be used as the value of the Unix EDITOR environment variable. The EDITOR variable specifies the command to run when programs need to invoke an interactive editor, such as when git starts an editor to fill in a commit message. 

If aedit is run outside of Anvil then it launches a new Anvil instance to edit the file. When Anvil is closed, aedit exits, allowing the invoking program to continue.

If aedit is executed from within Anvil, it will open a new window in Anvil for editing the file. When the window is closed using Del aedit exits.

To use aedit only when commands are run from Anvil, set the EDITOR environment variable to aedit in the [\[env\]](config.md#table-env) section in the [Anvil settings.toml configuration file](config.md#settingstoml).

## awatch

When run from Anvil, awatch waits for files in the directory in which it is run to be Put in Anvil, and then executes it's arguments as an OS command. As well, if a line beginning with "% " is entered in the window followed by a command, that command is also run. When started it opens a Window in which it displays the command's output. It is similar to the [Watch](https://pkg.go.dev/9fans.net/go/acme/Watch) command written for Acme. 

awatch is useful to automatically compile the files in the current directory as the source files are being edited. For example, if you were creating a Go project in Linux you could run `awatch go build && echo success` to start awatch and have it compile the source code files when they are modified. It would display all the compile errors, or 'success' if the compilation was successful.

## anvsshd

anvsshd is a simple SSH server for Linux which can be run and configured as a normal user. It's useful for a couple of specific use-cases:

  * If you want to access files on a remote host and do not have permissions to modify the OpenSSH configuration to allow clients to set environment variables, you can instead run anvsshd on a different port and connect to it instead. Anvil requires SSH servers to set certain environment variables if remote commands will use the API, or if you want to use environment variables to refer to the file open in the current window in Anvil.
  * If you want to use a remote host for development with Anvil, but preparing the environment for development and compiling takes significant time. This might be the case, for example, if you are doing C/C++ cross-compiling and you need to source scripts that setup the shell environment to use the right tools and settings. You can SSH to the machine, prepare the environment, then run anvsshd which will inherit the environment variables. Subsequently, commands run from Anvil through anvsshd will execute in the prepared environment.

anvssh authenticates users by public key authentication. It reads the authorized keys from the OpenSSH configuration file `~/.ssh/authorized_keys` by default, or the value of the `-z` or `--authkeys` flags if set. It requires a host key which it reads from `~/.ssh/host_key` by default, or the `-k` or `--hostkey` flag if set. 

anvssh listens on the address 0.0.0.0 TCP port 5001 by default, but this can be overridden using the `-a` or `--addr` flag.

## adiff

adiff can be used to diff the contents of the bodies two windows. Mark the two windows by typing `&&1` and `&&2` in the windows to diff, then run `adiff`. It will open a new +Diff window with the diff. You can run `adiff clr` to remove the marks.

## ado

ado allows you define rules that, when matched, execute a command in the context of that window. After started, this command listens for files to be opened in Anvil and when one is opened, checks if the filename matches the regular expression for a rule. If it matches then the command from the rule is executed.

The rules for ado are configured in the file `filehooks` in the Anvil [configuration directory](../reference/config.md). The file format is similar to the [plumbing file](../reference/plumbing.md#plumbing-file-format). Like the plumbing file, each rule is defined my a `match` and `do` line, which define the regular expression to match and the command to run respectively. However the ado configuration file supports multiple `do` lines for a single match line. 

Below is an example `filehooks` configuration file for ado:

```
# Set a custom tag for markdown files
match \.md$		
do Settag " Do Acq Look ◊Fuzz ◊ mdtoc"

# Set a custom tag for C programming language files
match witspace.*\.[ch]$
do Tab "    "
do Settag " Do Look Rg Format Fnames "
```

## asm

asm (Anvil session manager) allows you to Dump the state of running Anvil instances prior to exiting in such a way that you can restart all of your running sessions and recover the same state as before exiting. This is useful when you have long-running Anvil sessions and need to upgrade Anvil.

In each Anvil session, run the command `asm`. This will execute the Dump command to save the state to a file under the anvil configuration directory. Then exit each Anvil session. When you are ready to restore all of the sessions, execute `asm load` from the command-line.

To clear the saved Dumpfiles, use `asm clear`. To list them use `asm list`.

Run the command `asm --help` for more information.
