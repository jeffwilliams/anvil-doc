# How to Set a Custom Tag for Specific File Types

It's possible to have Anvil change the user-customizable part of window tags when the window filename matches a pattern. To do this, follow these steps:

1. Make sure the new `ado` command is in your execution path.

2. In your [`settings.toml`](../reference/config.md#settingstoml) configuration file, add a setting to launch the [`ado`](../reference/useful-tools.md#ado) command on startup:

        [general]
        exec = ["ado"]

3. Create a new file in the Anvil configuration directory with the name `filehooks`. Add lines similar to the following to the file:

        match \.md$		
        do Settag " Do Acq Look ◊Fuzz ◊ mdtoc"

4. Restart Anvil

The settings in settings.yaml will cause Anvil to start the command ado on startup. ado will load the rules from the file filehooks and listen for windows to be open. When one matches the regex `\.md$` (i.e. a file with the extension .md; a markdown file) it runs the Settag command to set the tag of the matching window to " Do Acq Look ◊Fuzz ◊ mdtoc".

