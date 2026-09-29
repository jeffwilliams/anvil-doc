# Keymaps Tutorial

Anvil comes with a default set of keyboard behaviours: actions that Anvil performs when a specific key or combination of keys is pressed. You can see the default set in the [Keyboard reference](../reference/keyboard.md). In Anvil the association of a set of keys being pressed to the action that Anvil takes is called a _key mapping_.

Though Anvil provides a default, the set of keymappings in Anvil is customizable. You can write your own set of mappings and either have them loaded when Anvil starts (by making a file of keymaps in the Anvil [config directory](../reference/config.md)) or by loading them using a command when Anvil is running.

Anvil's system for managing key mappings is flexible, and you might call it _stackable keymaps_. Keymaps (a set of keybindings) can be pushed onto an internal stack. When a key is pressed, if there is a binding in the top keymap of the stack, then the action for that mapping is executed. If there is no mapping, then the next lower mapping can optionally be checked, and so on. Keymaps can be pushed onto the stack and the top keymap popped from the stack at runtime, and this can be done through a key binding on the keymap itself.

In this tutorial we will explore creating a custom keymap that we use to override some of Anvil's keys. Our keymap will be used to give Anvil the ability to type [runes](https://en.wikipedia.org/wiki/Runes), and will be activated and deactivated by a keypress.

## Building a Runic Keymap

First, create a new file named `runic.keymaps`. Put the following content into the file and save it:

```
keymap base update

map C-1 push runic

keymap runic fallthrough

map A insert-text ᚨ
map B insert-text ᛒ
map C insert-text ᚲ
map D insert-text ᛞ
map K insert-text ᚲ
map E insert-text ᛖ
map F insert-text ᚠ
map G insert-text ᚷ
map H insert-text ᚺ
map I insert-text ᛁ
map J insert-text ᛃ
map L insert-text ᛚ
map M insert-text ᛗ
map N insert-text ᚾ
map O insert-text ᛟ
map P insert-text ᛈ
# Using 9 for 'ng'
map 9 insert-text ᚾ
map R insert-text ᚱ
map S insert-text ᛊ
map T insert-text ᛏ
map U insert-text ᚢ
map W insert-text ᚹ
# Using 3 for 'th'
map 3 insert-text ᚦ
map Z insert-text ᛉ
map . insert-text ᛫
map : insert-text ᛬
map , insert-text ᛭

map ⎋ pop
```

These are the instructions that we'll use to tell Anvil to define our runic keymappings. Let's go through the file line-by-line to understand what it's doing. 

The first line declares that a keymap is starting here, that it's name is `base`:

```
keymap base update
```

The `update` flag says that when Anvil loads this keymap, if there is a keymap already named `base` that this keymap will update the bindings in it. In fact, there is a keymap named `base` in Anvil; that's what the default keymap that Anvil pushes onto the stack first is called. So in this case we are directing Anvil to override some of the bindings in that keymap.

The next line defines a mapping in that keymap:

```
map C-1 push runic
```
	
Here we may the key combination `C-1` (Ctrl+1) to perform the action `push runic`. The action `push` is used to push a new keymap onto the top of the stack, and in this case we want to push one named `runic`. The next line declares that a new keymap is starting; the one we just referred to, named `runic`:

```
keymap runic fallthrough
```

In this line the `fallthrough` flag tells Anvil that if this keymap is at the top of the stack and a key combination is pressed, and there is no mapping in this keymap for the key combination, then check the keymaps lower in the stack to see if they have a mapping for this keypress. 

After this we have several mappings for single normal keys:

```
map A insert-text ᚨ
map B insert-text ᛒ
...
```

These mappings execute the action `insert-text` which inserts the text listed as its first argument at the current cursor positions. Note that the keys must be listed in upper case. In our mapping here we do a rough transliteration of the runes to their corresponding English sounds. For example, we map  ᚨ (ansuz) to the A key because it sounds much the same. Since there is no equivalent single letter for the ingwaz rune ( ᚾ) which has the sound of 'ng' in 'song', we map it to 9. Similarly for thorn ( ᚦ) which has the sound of 'th' from 'three' in English we map to 3. Punctuation which is interchangeable in runic we map to '.', ':', and ','

The last mapping in the runic keymap specifies that when the Escape key is pressed the top keymap of the stack should be popped:

```
map ⎋ pop
```

Some of the keys like Escape are named using a special Unicode character. This is how GIO, the library that Anvil uses for rendering, specifies keys. You can see the names in the reference [here](https://pkg.go.dev/gioui.org/io/key#Name). 

If this keymap is active at the top of the stack, when Escape is pressed then the top of the stack is popped, removing this keymap from the stack. So we've effectively defined a sort of keyboard mode: when we are in the "normal" mode we can press Ctrl+1 to enter the runic typing mode. We can type some text then hit escape to return to the "normal" mode.

## Loading our Runic Keymap

Now we need to make Anvil use our newly defined keymap. From Anvil, run this command:

```
Keymap show defs
```
	
This will print a list of all the keymaps that have been loaded into Anvil. Unless you've customized Anvil, you'll only see keymaps named `base`, `window` and `layer` (depending on the Anvil version). Next let's see the current keymap stack by running this command:

```
Keymap show stack
```
	
It will print the current stack of keymaps. Again for uncustomized Anvil this will show just one stack entry, listed as "Keymap 0" with the keymap being `base`. The stack is shown in the order of bottom to top; if there were another entry in the stack it would be listed as "Keymap 1" and would be the top of the stack.

To load the newly created runic keymaps run this command:

```
Keymap load runic.keymaps
```
	
This will load our keymaps. Since the file contains a keymap named `base` our mapping for `C-1` will take effect and get added to the already loaded and active keymap named `base`. The keymap named `runic` will be loaded but is not active yet since it's not been pushed to the stack. You can view the new definition of the `base` keymap by running `Keymap show defs` again, or specifically running `Keymap show def base` to show only the base keymap. You should see a mapping for `C-1` and also the same one for `K-1` for mac folks.

Now we can use it. In a new window, type Ctrl+1 to activate the keymap. Then type the letters "anfil". You should see the runic name for Anvil[^1] appear: ᚨᚾᚠᛁᛚ

Press the Escape key to pop the keymap from the stack and so revert back to normal English letters.

This concludes the tutorial, but there are many more actions that can be performed using keymaps. Check the [keymap reference](../reference/keymaps.md) for more details.

[^1]: There's no rune that represents the "v" sound so we used f instead. Anyway since we're using runes, it might be better to use the Proto-Norse name for an anvil rather than transliterate "anvil" directly. But the closest I've found to a translation of anvil was "steði", where ð is the [voiced dental fricative](https://en.wikipedia.org/wiki/Voiced_dental_fricative). But oddly there is no equivalent rune for that, only the unvoiced, being the rune thurs or what was later called thorn in old English. 
