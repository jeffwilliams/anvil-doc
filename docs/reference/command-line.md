# Command Line Arguments

Invoking Anvil from the command-line has the following syntax:

	./anvil [options] [file]

If [file] is specified then that file is opened in Anvil. The following options are supported:

  -d, --cd="": Change directory to the specified path before starting

  -l, --load="": Load state from the specified file that was created using [Dump](commands.md#dump)

  -p, --profile=false: Profile the code CPU usage. The profile file location is printed to stdout.

  -h: Print command-line help
