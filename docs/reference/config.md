# Configuration Files

Anvil loads various configuration files on startup from its configuration directory. The Anvil configuration directory is a subdirectory named `.anvil` under $HOME on Linux, or %USERPROFILE% on Windows. Running the 'About' command in Anvil shows the path to the config directory on the line beginning with 'Config directory:', and like any path can be opened in Anvil using ALT-Right Click.

If the configuration directory is not present, or a configuration file that Anvil would load is not present, then Anvil uses default values.

The list of configuration files is below. The settings.toml and style.js config files are described in the following sections, while the plumbing and sshkeys configuration have their own pages.

  * settings.toml: Miscellaneous settings for Anvil
  * style.js: Defines Anvil's style: the colors and fonts used for UI elements. 
  * [plumbing](plumbing.md): Defines the plumbing rules
  * [sshkeys/](remote-editing.md): a subdirectory containing SSH keys used for remote editing
  * keymaps: A keymaps file that Anvil loads on startup after the built-in keymaps are loaded. See the file [format section](keymaps.md#keymap-file-format) in the keymaps reference for details about the format.
  
## settings.toml

This file contains miscellaneous settings for Anvil in [TOML](https://toml.io/en/) format. Use the command `PrintCfg settings.toml` to print the contents of a sample configuration file to the +Errors window, which includes comments explaining the purpose of the settings. The contents can be saved to the file `settings.toml` in the configuration directory.

The settings are explained below:

### Table [general]

* exec: A list of commands to execute on startup. For example:

```
exec=[
  "ado", 
  "aad" 
]       
```

### Table [layout]

* editor-tag: If set, the value of this setting is used as the default editor tag.
* column-tag: If set, the value of this setting is used as the default column tag.
* window-tag: If set, the value of this setting is used as the default window tag.

### Table [typesetting]

* replace-cr-with-tofu: when set to true, Anvil shows carriage-return characters as the "tofu" character (a box). When false (the default) carriage-return characters are shown as whitespace.

### Table [ssh]

* shell: shell specifies the shell to use when commands are executed on a remote system. The default is "sh".
* close-stdin: close-stdin controls if stdin is closed for remote programs when they are executed using middle-click. Some programs require this to operate properly such as ripgrep, while others require stdin to be open even if it is not read, like man(1). The default is false.
* conn-timeout: This setting specifies the SSH connection timeout in seconds

### Table [env]

The values in this table define additional environment variables that will be set by Anvil when it executes an OS command. For example, if this section is defined as:

    [env]
    EDITOR="aedit"
    PAGER="less"

then Anvil would set the environment variable EDITOR to aedit, and PAGER to less in the environment of programs it executes.

### Table [alias]

The values in this table define command aliases. A command alias associates a name with a list of commands. When the command alias is executed in Acme, the list of commands defined for the alias are run instead. 

For example, if this section is defined as:

    [alias]
    Light="LoadStyle /path/to/style-light-bg.js"
    Lc=">wc -l"

Then if the command Light is executed in Anvil, then `LoadStyle /path/to/style-light-bg.js` is run instead. If the command `Lc` is run, then `>wc -l` is executed, and the count of lines in the current window is printed.

Aliases may accept arguments and may consist of multiple commands. In the alias value you may use the placeholders `$1`, `$2`, ..., `$9` to substitute the first through ninth arguments, respectively. Use `$*` to substitute all of the arguments separated by space. Multiple commands are separated by semicolon. For example, if this section were defined as: 

    [alias]
    Cfiles='New $1.h; New $1.c'

Then executing `Cfiles draw` would open new windows for editing `draw.h` and `draw.c`.

**Warning:** Aliases do not guarantee sequential execution of each of the commands in the definition. If you tried to define an alias to perform `echo -n 'line count:'; >wc -l` for example, the `wc` command's output could be printed before the `echo` command's output.

## style.js

This file defines Anvil's style in [JSON](https://www.json.org) format which define the colors and fonts used for UI elements. Anvil only supports TTF fonts. All color related settings must be specified as strings which are three-channel hex color codes beginning with a pound, for example: "#f0f0f0".

The settings are explained below:

  * Fonts: This array defines the list of fonts that Anvil uses. Each element in the list is an object with the fields FontName and FontSize. In an Anvil window these fonts can be cycled through by using the command Font.
    * FontName may be set to the full path to a TTF font file, the name of a font in platform specific user and system font directories, or one of the special values defaultVariableFont or defaultMonoFont. The values defaultVariableFont and defaultMonoFont refer to internal fonts built into Anvil, and are a variable-width and monospace font respectively. For paths and names, Go uses the [findfont](https://github.com/flopp/go-findfont) library to locate the fonts.

  * TagFgColor, TagBgColor: The foreground and background colors of the window, column and editor tags.
  * BodyFgColor, BodyBgColor: The foreground and background colors of window bodies.
  * LayoutBoxFgColor, LayoutBoxUnsavedBgColor, LayoutBoxBgColor: The layout box outline color, the fill color for an unsaved file, and the fill color for a saved file respectively.
  * ScrollFgColor, ScrollBgColor: The color of the "button" and background of window scrollbars
  * GutterWidth: The width of the column on the left side of a window that contains the scrollbar and layout box in pixels
  * WinBorderColor: The color of the border around a window
  * WinBorderWidth: The width in pixels of the border around a window
  * PrimarySelectionFgColor, PrimarySelectionBgColor: The foreground and background colors of the primary selection
  * SecondarySelectionFgColor, SecondarySelectionBgColor: The foreground and background colors of secondary selections
  * ErrorsTagFgColor, ErrorsTagBgColor: The foreground and background colors of the tags of +Errors windows
  * TabStopInterval: The distance between each tabstop in the window body
  * Syntax: This setting is an object with fields to colorize various syntax-highlighting elements. The supported colors are:
    * KeywordColor: Keywords
    * NameColor: Names/identifiers
    * StringColor: Strings
    * NumberColor: Numbers
    * OperatorColor: Operators
    * CommentColor: Comments
    * PreprocessorColor: Preprocessor statements (C and C++)
    * HeadingColor: Headings (for example in Markdown)
    * SubheadingColor: Subheadings
    * InsertedColor: Inserted text (for diffs)
    * DeletedColor: Deleted text (for diffs)
  * CursorProg: A program that defines how to draw the cursor. The language used is described in the section "cursor language" below.

### Cursor Language

!!! note

    This language might be changed in a way that is not backwards compatible later if it's determined not to be flexible enough. It might be made more general to allow drawing lines of a given width rather than just defining shapes.

This language specifies a series of graphical operations that describe the shape and color of a cursor. A program in this language describes one or more filled shapes that are overlayed to form the cursor. The language consists of a series of statements separated by semicolons (;). Each statement is a word followed by comma-separated arguments in parenthesis.

The shape drawing statements move a "pen" along some contour. The series of these statements form the perimiter of a shape, similar to Logo or SVG.

The following statements are allowed:

  * **color**: this sets the color to be used for shapes that follow. The arguments are the color represented as Red, Blue, Green, Alpha components in the range 0-255. For example, this is black: `color(0,0,0,255)`
  * **begin**: begin a shape
  * **move**: move the pen to the relative coordinates without drawing. The arguments are the X and Y coordinates. For example, to move left one unit: move(-1,0)
  * **line**: draw a line from the current position to the relative coordinates. To move right 3.5 units: line(3.5,0)
  * **close**: close the current shape. This is the compliment to `begin`.

The arguments to the statements are floating point numbers in units of font points. The only exception is that the constant `lh` or `-lh` may be used to represent the font's line-height or negative line-height respectively.

Shapes drawn later in the program are overlayed over those drawn earlier.
