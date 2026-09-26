# How to Use Ripgrep Effictively from Anvil

[Ripgrep](https://github.com/BurntSushi/ripgrep) is a fast, line-oriented search tool that recursively searches the current directory for a regex pattern, similar to grep. It can be used effectively from Anvil like other command-line tools by simply executing it as an OS command. 

However, to make the output most effective for use in Anvil a few options are recommended. By default, when run from Anvil, ripgrep prints lines that contain the names of matching files, a colon, and then the matching text without a space. For example:

    file.py:def myfunc

To allow Anvil to acquire the file at the matching line number, you can instead use the options `--no-heading`, `--line-number`, and  `--replace=' $0'`:


    file.py:20: def myfunc


With this output, if you perform an Alt+Right-Click on the filename and line number, Anvil will jump to that location.

It's easiest to configure ripgrep to use these options automatically. You can do this by creating a configuration file (for example `$HOME/.ripgreprc`) with the following contents:

    # Print filename with each line
    --no-heading
    --line-number
    # For anvil: separate the match and the file:line by a space.
    --replace= $0

Then export the environment variable `RIPGREP_CONFIG_PATH` that contains the path to that configuration file from your shell rc file. 
