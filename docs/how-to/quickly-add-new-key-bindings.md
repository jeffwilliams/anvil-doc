# How to Quickly Add New Key Bindings

If you want to add new key bindings to Anvil in a simple way, follow these instructions:

  1. Create or edit the file in the Anvil configuration directory named `keymaps`. You can find where you should put this file by running the About command. Look for the line that begins with "Keymaps config file", for example:
  
        Keymaps config file: /home/user/.anvil/keymaps (was loaded on startup)
  
  2. Make sure the top of the file has a line that defines the keymap, and that it will update the base (the built-in) keymap:
  
        keymap base update
  
  3. Add your new key mapping. Use the [keymaps reference](../reference/keymaps.md), in particular the [actions list](../reference/keymaps.md#actions) to help define the new binding. For example, add a line or lines similar to:
  
        # Map Ctrl+Tab to change to the layer above, and Ctrl+Shift+Tab to change to the layer below. Ctrl also stands for Command on Mac.
        map C-Tab move-to-layer-above
        map CS-Tab move-to-layer-below
  
  4. The next time Anvil is started it will apply these new bindings. You can make Anvil reload this keymap immediately using the command `Keymap load /home/user/.anvil/keymaps` (where the path is replaced with the path to your keymaps file). It's helpful to add this to the top of the file as a comment so that it is easier to reload the bindings after editing the file by just clicking that line.
  
  Here's the complete keymap file that we created in this example:
  
        # Reload this using: ◊Keymap load /home/user/.anvil/keymaps◊
        keymap base update
        # Map Ctrl+Tab to change to the layer above, and Ctrl+Shift+Tab to change to the layer below. Ctrl also stands for Command on Mac.
        map C-Tab move-to-layer-above
        map CS-Tab move-to-layer-below
  
