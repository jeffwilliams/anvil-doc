# Editing Remote Files

In all the examples we've seen so far, we have worked on local files that exist on the computer where we're running Anvil. But Anvil is capable of editing remote files on another host as well. To do so, the remote host must provide a Unix-like environment; among other things, it must allow running the Bourne shell (`sh`) and the `cat` command. 

Once authentication is set up, you can use remote files and commands in Anvil like they are local. 

## Setting up Authentication

Anvil can authenticate with the remote SSH server using either a password, a key, or using ssh-agent. 

To use password authentication, you must first specify a password to use with the remote server using the Hostpass command:

	Hostpass <password> <server>

Hostpass accepts additional optional arguments, but we'll ignore those for now.

To use SSH key authentication, you must make a file containing the SSH key in an Anvil-specific configuration directory. If the key is not password-protected, that's all that is needed. If it is password protected you must then specify the password using the Keypass command:

	Keypass <keyfile name> <password>

Finally, if you are running Linux, have ssh-agent running, and have started Anvil with the correct ssh-agent environment variable set, then Anvil will retrieve keys from ssh-agent when attempting to authenticate with the remote host.

If you use the Hostpass or Keypass commands for authentication, they must be run each time Anvil is started. The passwords are not stored by Anvil, even in a dumpfile.

The videos below demonstrate the password and key-based authentication.

### Demo Video: SSH Password Authentication

This video demonstrates setting authentication information for a remote host `andor` using a password. It goes on to list a remote directory on `andor`.

![type:video](../../img/anvil-tut-remote-editing-3.mp4)

### Demo Video: SSH Key Authentication - Passwordless Key

This video demonstrates setting authentication information for a remote host `andor` using an SSH key that is not password protected. It first shows how to locate the Anvil sshkeys configuration directory using the About command, shows the key file that has been copied there, and then lists the remote directory.

![type:video](../../img/anvil-tut-remote-editing-1.mp4)

### Demo Video: SSH Key Authentication - Passworded Key

This video demonstrates setting authentication information for a remote host `andor` using an SSH key that is password protected.This video demonstrates applying a password for an ssh key file, then listing a directory on the remote host.

![type:video](../../img/anvil-tut-remote-editing-2.mp4)


## Remote Filename Format

Once authentication is set up, you can use remote files and commands in Anvil like they are local. The only difference is that the files and directories have a slighly different format for the name: the path for the remote file or directory is prefixed with the remote host name, and possibly with a username or port if it was opened as such. The format is almost the same as the format used for SCP remote filenames.

If we have a remote file `file` on the host `host`, the formats look like:

  * `host:file` - The file `file` in the user's home directory on `host`
  * `host:/path/to/file` - An absolute path to the file on the remote host
  * `user@host:file` - The file `file` on `host`, but Anvil authenticated as the user `user`
  * `user@host:port:file` - Like the previous, but Anvil is communicating with the SSH server running on TCP port `port` rather than the default

In addition there is an advanced form where Anvil communicates to a remote server via an intermediate SSH server acting as a proxy: `host%proxy:file`. Refer to the [Remote Editing reference](../reference/remote-editing.md#remote-path-syntax) for more info on the accepted formats.

## Running Remote Commands

When you execute an OS command from the tag or body of a window which contains a remote file, that command is executed on the remote host in the directory of the window. 

Sometimes it's convenient to run a command saved in a local file on a remote host, without going through the trouble of having to first open a file on the remote host, paste the command into that window, and then execute it. Anvil provides the `On` command for this purpose. For example, the command:

	On andor:/etc ls | wc -l
	
Will execute the command `ls | wc -l` in the directory `/etc` of the host `andor`.

Additionally, sometimes you might want to execute a command locally, even though the window is remote. You can do this by prefixing the command with `+`. For example, to execute the `ls` command locally when you middle click it somewhere in a remote window's tag or body, you can use the command:

    +ls

If you want to execute the command and also use one of the `|`, `<` or `>` prefixes, put the `+` _after_ the redirect. For example:

    >+wc



![type:video](../../img/anvil-tut-remote-editing-4.mp4)

