# Installing Anvil

Anvil is built as a statically-linked binary. It's sufficient to simply copy the binaries to an appropriate place. However, for Windows an installer is provided that installs Anvil and also adds convenient shortcuts to Windows Explorer for launching it.

Anvil is built using GIO, and for some operating systems GIO has extra dependencies that must be installed. See the [GIO Install page](https://gioui.org/doc/install) for the correct dependencies for your OS.

=== "Linux"

    1. Download the archive that matches your platform from the [download](../download.md) page.
    2. Extract the archive. For example:
 
        `tar xzf anvil-v0.1-linux-amd64.tar.gz`
    3. Set the PATH environment variable to contains the directory just unpacked.
      * If you are using bash, in your .bashrc add the line:

        `export PATH=$PATH:path_to_anvil_directory`
      * (Optional) To install for all users instead, copy the binaries from the unpacked directory to `/usr/bin` 

=== "Windows - Copy Binaries"
    1. Download the archive that matches your platform from the [download](../download.md) page.
    2. Extract the archive.

=== "Windows - Installer"
    1. Download the Windows installer from the [download](../download.md) page.
    2. Run the installer and choose an install directory

