# Remote Editing

Anvil is able to edit remote files and run commands on remote hosts. The same operations that apply to local files, such as opening, reloading, saving, or executing commands in the directory of a window operate much the same way with remote files. The differences are:

  1. Before being able to open remote files or execute commands remotely, SSH authentication must be configured
  2. Remote paths must be prefixed with information describing which host contains the file, and optionally how to authenticate to the host
  3. Executing an OS command in the tag or body of a window always executes that command on the remote host, not the local host

The first time a remote file is opened or a remote command is run for a specific user on a host at a certain TCP port, Anvil opens an SSH session and authenticates. Afterwards the SSH session is kept open and authentication is not required again, unless the connection is broken. This means there will be a slight delay the first time a command or file is opened on a user, host, port combination, but later operations on the same tuple will be quicker.

## Configuring Authentication

Anvil can authenticate with the remote SSH server using either a password, a key, or using ssh-agent. Authentication must be configured before remote files may be opened. Connections to remote servers are not initiated at the time of configuration, but instead when the first file is opened on a host.

### Password Authentication

To use password authentication, you must first specify a password to use with each remote server using the Hostpass command. The Hostpass command has the following syntax:

	Hostpass <password> <server> [username] [port]
	
Where arguments enclosed in <> are mandatory, and those enclosed in [] are optional. If username is not specified, then the current username (as read from the USER environment variable in Unix, or USERNAME in Windows) is used. If port is not specified, 22 is used.

Authentication information is not saved to disk by Anvil, so the Hostpass command must be run each time Anvil is started.

### Key Authentication

To use SSH key authentication, you must add the SSH key to use to an Anvil-specific [configuration directory](config.md). If the key is not password-protected, no further action is needed. 

If the key is password protected you must then specify the password using the Keypass command:

	Keypass <keyfile name> <password>

Authentication information is not saved to disk by Anvil, so the Keypass command must be run each time Anvil is started.

When authentication is attempted with a host, each keyfile is tried until one matches or all fail.

### Authentication using ssh-agent

If Anvil is running on Linux it will attempt to authenticate using the SSH keys provided by ssh-agent. For this to work, ssh-agent must be running and the environment variable SSH_AUTH_SOCK must be set in Anvil's environment to the location of the unix-domain socket for communication with ssh-agent. Put another way, SSH_AUTH_SOCK must be set in the environment before starting Anvil.

## Remote Path Syntax

All paths in Anvil have the following form:

	[user@][host:[port:]][[user@]%proxy_host:[port:]]<path>
	
Where terms enclosed in [] are optional, and terms enclosed in <> are mandatory. Note that for a local path, this collapses to simply <path>. A remote path must always have the host: portion.

The terms are defined as:

  * 'user@': The username used to authenticate with a host or proxy host, followed by the '@' character
  * 'host:': The hostname or IP address where the path resides, followed by a ':' character
  * 'port:': The TCP port of the SSH server to connect to
  * '%proxy_host:': proxy_host is the hostname or IP address of an intermediate SSH server through which the connection to 'host' is proxied, preceeded by a '%' character to disambiguate, and followed by a ':' character. This is achieved using SSH tunneling, so this must be allowed in the proxy server's SSH daemon configuration.

With a remote path, if <path> is a relative path (it does not begin with a /) then it is relative to the user's home directory.

## Remote Path Examples

Following are some examples of legal remote paths:

| Path | Semantics |
| --------------- | --------- |
| host1:/tmp | The directory /tmp on host1 |
| host1:file1 | The file file1 in the home directory of the current user on host1 |
| username@host1:/tmp | The directory /tmp on host1. The SSH session is established as user 'username'. |
| host1:5001:/tmp | The directory /tmp on host1. The SSH session is established to TCP port 5001.  |
| username@host1:5001:/tmp | The directory /tmp on host1. The SSH session is established as user 'username' to TCP port 5001.  |
| host1%host2:/tmp | The directory /tmp on host1, but the connection to host1 is proxied through the SSH server on host2 |

## Environment Variable Support

Anvil exports some environment variables to the environment of the processes it executes, including those needed to connect to the API as described in the [environment reference](environment.md). For those to be exported for remote commands the SSH server may need to be configured to specifically allow them. For the OpenSSH server this amounts to adding the following line to the SSH configuration:

	AcceptEnv ANVIL_*
 
  
	