# Command Line Arguments

Invoking Anvil from the command-line has the following syntax:

```
./anvil [options] [file]
```

If `file` is specified then that file is opened in Anvil. The following options are supported:

```
  -d, --cd="": Change directory to the specified path before starting
  -c, --debug-catg="": One or more comma-separated categories to print when -b or -g are used. The supported categories are:
  Application
  UI
  Editable
  Syntax
  API
  Filesystem
  Completion
  Plumbing
  Window
  Commands
  Column
  Config
  Editor
  Packing
  SSH
  Expressions
  FuzzySearch
  -b, --debug-stdout=false: Print debug logs to stdout
  -g, --debug-window=false: Print debug logs to +Errors window
  -f, --fonts-in-pixels=false: Consider font sizes in pixels instead of device independent units
  -l, --load="": Load state from the specified file that was created using Dump
  -p, --profile=false: Profile the code CPU usage. The profile file location is printed to stdout.
      --version=false: Print version
```
