# How to Use Pageant with Anvil

When editing remotely in Anvil often you will need an SSH key to connect to the remote host you are editing files on. One way to manage the SSH keys is using an SSH agent, which asks you for the key passwords and then stores the keys in memory so other programs can retrieve them without requiring the user to enter a password again. Anvil has the ability to load keys from SSH agents.

Pageant is an SSH Agent that runs on Windows. It is part of the [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) suite of SSH tools. Having Anvil load SSH keys from PuTTY on Windows is straighforward: you need to start Pageant with an option that directs it to create a named unix-domain socket, and set an environment variable in Anvil's environment that contains the path to the Pageant unix socket. 

The steps in more detail are:

* Pick location for the unix socket. I recommend making a folder to contain it and setting the security permissions on the folder so that only your user can read and write from it, to prevent others from using the keys. For example, the path might be `C:\Private\pageant.sock`

* Set the `SSH_AUTH_SOCK` environment variable so that it is in Anvil's environment when Anvil is started. One way to do this is through the registry. Open the registry editor and under the registry entry `Computer\HKEY_CURRENT_USER\Environment` add a new `REG_EXPAND_SZ` value with the name `SSH_AUTH_SOCK` and set the value to the path of the socket; for example `C:\Private\pageant.sock`.

* Start Pageant with the option `--unix <path-to-socket>` where <path-to-socket> is the path to the socket (i.e. `--unix C:\Private\pageant.sock`). Import your SSH keys into pageant from the GUI.

* Start Anvil

Note that currently Anvil caches the keys it retrieves from pageant, so if you add a new key any running Anvil instances will not use the new key.
