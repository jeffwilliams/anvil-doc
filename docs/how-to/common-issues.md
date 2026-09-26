# Common Issues and How To Fix Them

## Anvil Environment Variables are Not Set for Remote Commands

Anvil exports some environment variables to the environment of the processes it executes, including those needed to connect to the API as described in the [environment reference](../reference/environment.md). For those to be exported for remote commands the SSH server may need to be configured to specifically allow them. 

If the remote system is running OpenSSH this amounts to adding the following line to the SSH configuration, which is usually found in the file `/etc/ssh/sshd_config`:

	AcceptEnv ANVIL_*

You may also want to accept the shortened variables describing the file path, and if you are using aedit the EDITOR environment variable:

	AcceptEnv ANVIL_* f b d EDITOR

## Run Anvil in VirtualBox

When Anvil is run in a Linux virtual machine hosted in VirtualBox, you may see sluggish performance. This is because Anvil uses OpenGL for rendering, and VirtualBox attempts to emulate the OpenGL hardware calls in software poorly. Mesa software rendering performs better than VirtualBox's implementation, so exporting the following variable to the environment before starting Anvil will switch to Mesa software rendering and improve the performance:

    export LIBGL_ALWAYS_SOFTWARE=1

## Troubleshoot Anvil Not Starting

If Anvil fails to start and prints an error similar to the following: 

    Received DestroyEvent due to the following error: gl: no OpenGL implementation could be loaded (tried ["libGLESv2.so.2" "libGLESv2.so.3.0"])

it likely means there are some dependencies of the GIO library that must be installed. See the [GIO Install page](https://gioui.org/doc/install) for the correct dependencies for your OS.

If Anvil fails to start on Linux and prints an error like:

    Received DestroyEvent due to the following error: wayland: wl_display_connect failed: no such file or directory

It may mean that wayland is not installed and also the DISPLAY environment variable is not set. Set DISPLAY to point to the correct X11 display to use.

## AltGr Key Does Not Insert Correct Character

On some keyboards when AltGr is used as a modifier along with other keys, Anvil may interpret the AltGr modifier as if the Ctrl and Alt keys were instead pressed along with the key. For example, AltGr + Q might be interpreted by Anvil as Ctrl+Alt+Q. 

If there is an action bound to that key  then the special character that the user intended to enter by pressing the key combination will not be inserted. For example, on some keyboards AltGr+Q is used to insert '@', but will instead cause Anvil to acquire a text object in the current window.

You can fix this using a key mapping in Anvil:

1. If one doesn't exist, create a keymaps configuration file. In the [configuration directory](../reference/config.md), create a file named `keymaps`.

2. Add the following content to the file:

    ```
    keymap base update
    map CA-Q insert-text @
    ```

3. After that change, new Anvil sessions will use that key mapping. In your current running sessions, you can execute the following command to reload the keymaps for the current editor session:

    ```
    Keymap load /home/USER/.anvil/keymaps
    ```

    Replace `/home/USER/.anvil/keymaps` with the path to your keymaps file.
