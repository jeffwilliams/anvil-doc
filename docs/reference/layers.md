# Layers Reference

Layers are a group of columns and windows that are shown at the same time. Layers have indexes and optionally a name. Layers with higher indexes are considered to be above layers with lower indexes.

The following commands are used to modify and change between layers:

  * [Newlyr](commands.md#newlyr): Create a new layer and switch to it
  * [Dellyr](commands.md#dellyr): Delete the current layer
  * [Up](commands.md#up): Make the layer above this one active
  * [Down](commands.md#down): Make the layer below this one active
  * [Setlyr](commands.md#setlyr): Set which layer index is active
  * [Colup](commands.md#colup): Move the current column to the layer above
  * [Colup^](commands.md#colup_1): Move the current column to the layer above, and switch to that layer
  * [Coldown](commands.md#down): Move the current column to the layer below
  * [Coldown^](commands.md#down_1): Move the current column to the layer below, and switch to that layer
  * [Cols](commands.md#cols): List all the columns and layers
  * [Lyrname](commands.md#lyrname): Set the name of the layer

Additionally there is a keyboard mode for layer movement and manipulation. To enter the mode use CTRL-Y from the base mode. The mapped keys are:

  * Up: Make the layer above the current layer active
  * Down: Make the layer below the current layer active  
  * Pg Up: Move to the highest layer
  * Pg Down: Move to the lowest layer
  * N: Create a new layer and switch to it
  * D: Delete the current layer
  * Escape: exit the keyboard mode (pop the current keymap)

You can also change which layer is active using CTRL+Scrollwheel.

## Lyrname Special Behaviour in the Editor Tag

If you type the `Lyrname` command in the editor tag, Anvil will attempt to update the argument of the command when the active layer changes. There are two cases:

  1. If the Lyrname command is present in the editor tag, and it is not delimited by lozenges (◊), then when the active layer changes if the arguments to the Lyrname command matched the name of an existing layer, then the arguments are replaced with the name of the current layer. If the current layer has no name then the Lyrname command is not modified.
  
    For example, suppose you have three layers, named "base", "", and "top layer" (the second layer is unnamed). If the layer "base" is active and the editor tag contains `Lyrname base`, then if you switch to the second (unnamed) layer, the editor tag is not modified. If you then switch to the topmost layer the command is changed to `Lyrname top layer`.

  2. If the Lyrname command is delimited by lozenges (◊), then when the active layer is changed the argument to the command is replaced with the active layer name, or "" if the active layer is unnamed.

    For example, suppose you have three layers, named "base", "", and "top layer" (the second layer is unnamed). If the layer "base" is active and the editor tag contains `◊Lyrname anything◊`, then if you switch to the second (unnamed) layer, the command is changed to `◊Lyrname ◊`. If you then switch to the topmost layer the command is changed to `◊Lyrname top layer◊`
