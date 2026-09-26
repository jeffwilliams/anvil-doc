# Environment Variables Reference

When Anvil runs an OS command, it sets various environment variables for the command. These can be useful when writing scripts to integrate with Anvil. 

The following environment variables are set:

| Variable | Semantics |
| --------------- | --------- |
| ANVIL_WIN_LOCAL_PATH | The path of the file being edited in the window where the command was executed. This path does not include the hostname (if the command was being executed remotely). |
| f | The same value as ANVIL_WIN_LOCAL_PATH, but easier to type |
| ANVIL_WIN_GLOBAL_PATH | The path of the file being edited in the window where the command was executed including the hostname in the ssh format (i.e. HOST:PATH) |
| ANVIL_WIN_LOCAL_DIR | The parent directory of the file being edited in the window where the command was executed, or the file itself if it is a directory. This path does not include the hostname (if the command was being executed remotely). |
| d | The same value as ANVIL_WIN_LOCAL_DIR, but easier to type |
| ANVIL_WIN_GLOBAL_DIR | The parent directory of the file being edited in the window where the command was executed, or the file itself if it is a directory. This includes the hostname in the ssh format (i.e. HOST:PATH) |
| b | The basename of the filename in the tag of the window |
| ANVIL_WIN_ID | The internal numeric ID of the window. This may be used in the API. |
| ANVIL_DIR | The local directory in which Anvil was started |
| ANVIL_API_PORT | The TCP port number on which the Anvil REST API is running. Connections to the API should be performed to the local host; if a remote command is executed an SSH tunnel is created so that commands may connect locally. |
| ANVIL_API_SESS | Session id used to authenticate the client program against the API. |

Custom environment variables can also be passed to the executed command by adding them to the `[env]` table in the Anvil `settings.toml` configuration file. See the [Configuration Files](config.md) reference for details.
