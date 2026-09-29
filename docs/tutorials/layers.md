# Layers

All of the visible columns and windows in Anvil are part of an entity called a _layer_. In all of the tutorials so far we've been working in a single layer. In this tutorial we'll learn how to make and delete other layers, and how to switch to them to make them the active layer.

## Create a New Layer

To create a new layer you can run the `Newlyr` command. This creates a new layer logically "above" the highest layer, and makes it the active layer. Layers have an index, but they can also optionally have a name. Follow these steps:

  1. Open Anvil
  2. In the editor tag, type the following: `◊Lyrname base◊ Newlyr`
  3. Execute the command `◊Lyrname base◊`. This will set the name of the current layer to "base".
  4. Execute the command `Newlyr`. This will create a new layer with no columns or windows.
  5. Add some columns by executing the `Newcol` command, and create a few unnamed files by executing the `New` command.
  6. In the editor tag, change the name of the layer: replace "base" with "layer 2" in the arguments to Lyrname, then execute the command
  7. You can view the list of current layers and columns using the `Cols` command. In the editor tag, type Cols and execute it to see the layers and their corresponding columns.

### Demo Video

![type:video](../../img/anvil-tut-layers-1.mp4)

## Switch Between Layers

You can switch which layer is active using the `Up` and `Down` commands. Executing `Up` sets the layer "above" the current layer (the one with the next highest index) to be active. `Down` sets the layer below the current to be active. You can use `Setlyr` to set the active layer to the index specified as its first argument. Follow these steps:

  1. In the editor tag, type `Up Down`
  2. At the end of the last section we were in the highest of our two layers. Execute `Down` to activate the first layer. 
  3. Execute Up to activate the highest layer again. 
  4. You can also switch between layers by holding the CTRL key and scrolling the mouse scrollwheel. Hold CTRL and scroll down to reach the first layer. Then hold CTRL and scroll up to reach the topmost layer
  5. Columns can be moved between layers. Switch to the bottom layer. In the column tag for the column that has the window with the current directory listing, type this text: `Colup^ Coldown^`. Click `Colup^`. This will move the column to the layer above and switch to that layer.
  6. Click `Coldown^`. That will move the column back to the lowest layer and switch to that layer. You can also use `Colup` and `Coldown` without the caret to move the column without changing which layer is active.

Note that when you switch between layers, the argument next to the `Lyrname` command in the editor tag gets replaced with the name of the active layer. This is a special behaviour to make it easier to tell what layer is active without having to run the Cols command.

### Demo Video

![type:video](../../img/anvil-tut-layers-2.mp4)

## Delete a Layer

To delete a layer you can execute the command `Dellyr`. It will delete the current layer.

## Layer Keyboard Mode

Rather than using the commands described above you can also create, delete, and move between layers using the keyboard by invoking a special mode. When you type CTRL+Y Anvil will change to layer mode (it will push a new keymap onto the keymap stack). Pressing Up will move up one layer, while Down will move down one layer. Pressing the key N will create a new layer, and D will delete the current layer. Finally, pressing Escape will exit the layer mode and switch back to the base keyboard mode (it will pop the keymap stack).

