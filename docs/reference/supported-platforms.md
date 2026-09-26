# Supported Platforms and Limitations

## Supported Platforms

Anvil runs on Windows, Linux, MacOS, and FreeBSD. The MacOS port is not as thoroughly tested as the others.

Anvil can edit remote files on Linux. It may be possible to edit remote files on other Unix systems but it hasn't been tested.

# Limitations

Anvil has a number of limitations:

  * Anvil only supports UTF-8 encoded text, and so by extension ASCII text.
  * Anvil only supports TTF fonts
  * Anvil expects Unix line endings: lines must end with a newline only. Text that contains carriage returns followed by newlines is stripped of carriage-returns when pasted into Anvil.
  * Editing remote files requires the remote host to be running SSH, and the following commands to be available:
    * `sh`
    * `cat`
    * An `ls` command that supports the `-A` (do not list implied . and ..) and `-p` (append '/' indicator to directories) options.
    * A `find` command that supports the `-maxdepth` option
    * `sort`
