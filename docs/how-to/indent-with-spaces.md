# How to Indent with Spaces

If you wish to have Anvil always insert spaces rather than tabs, in your [`settings.toml`](../reference/config.md#settingstoml) configuration file, add the following settings:

    [general]
    exec = ["Tab '    '"]

and restart Anvil. These settings will cause the command `Tab '    '` to be run when Anvil is started, in the context of the editor tag. When Tab is run from the editor tag it sets the string that the tab key will insert for all windows, which in this example is four spaces.

If instead you want to temporarily change tab for a session, run the Tab command manually from the editor tag. If you want to change tab for a specific window, run the Tab command from the tag or body of that window. To automatically set the tab string to a different value for specific windows, use the [`ado`](../reference/useful-tools.md#ado) command.
