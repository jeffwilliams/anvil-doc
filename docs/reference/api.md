# API Reference

Anvil provides an API that is meant to be used by programs launched from within Anvil. The API is accessed over HTTP and interacts in a REST manner. It is available to both local and remote programs; for remote programs it is tunneled through the SSH session.

## Connecting

To use the API, programs must read the ANVIL_API_PORT environment variable and open a TCP connection to the API to the local host on that port.

Once connected the program can perform HTTP requests.

## Authentication

Each request from the program must contain the HTTP header `Anvil-Sess` which must be set to the value of the environment variable ANVIL_API_SESS.

## Encoding

The contents of requests and responses may be encoded as JSON or CSV. To choose the encoding, the program should set the `Content-Type` and `Accept` headers to `application/json` or `text/csv`. Some responses from Anvil are always returned in the encoding `text/plain` regardless of the `Accept` header that the program set, such as a response containing the contents of a window body.

## Websocket Notifications

Anvil allows clients to create a websocket connection. Once created, Anvil will send notifications over the websocket. The notifications are sent using the encoding the client requested in the initial websocket GET request and their structure is the same as that returned by performing a GET on the `/notifs` URL described in the Operations section below.

## Operations

The following operations are supported by the API. In the table the number 1 is a placeholder used to represent a window id, and may be replaced with any window id value.

| Method | URL | Behaviour | Structure |
| ----- | --- |--------- | ------ |
| GET | /wins/ | List window ids and paths | array of structures with fields Id, GlobalPath, Path |
| POST | /wins/ | Create a new window and return the id | structure with field Id |
| GET | /wins/1/body | Get contents of body of window 1 | unstructured plain text |
| PUT | /wins/1/body | Set contents of body of window 1 | unstructured plain text |
| POST | /wins/1/body | Append to the contents of the body of window 1 | unstructured plain text |
| GET | /wins/1/body/info | Get info about window body (i.e. length) | structure with field Len, the number of UTF-8 characters in the window body |
| GET | /wins/1/body/cursors | Get info about cursors in the window body | array of integers. Each element represents the position of a cursor as an offset of the number of UTF-8 characters from the beginning of the file |
| PUT | /wins/1/body/cursors | Set position of cursors in the window body | array of integers. The semantics are the same as GET. |
| PUT | /wins/1/body/insert | Insert text at each cursor | unstructured plain text |
| GET | /wins/1/info | get window information, such as file paths | structure with fields Id, GlobalPath, Path |
| GET | /wins/1/selections | get window selections | array of structures with fields Start, End, Len |
| GET | /wins/1/tag | Get the tag of window 1 | unstructured plain text |
| PUT | /wins/1/tag | Set the tag of window 1 | unstructured plain text |
| GET | /jobs | List the running jobs | array of structures with the field Name |
| POST | /execute | Execute a command as if it was clicked. The command is executed as if it was run from the window with the id specified in the request, or as if it was run from the editor tag if the window id is set to -1 | a structure with the fields Winid, Cmd, Args. Args is an array of strings |
| GET | /notifs | Get any pending notifications for the current API session. The notifications are then cleared. | array of structures with fields WinId, Op, Offset, Len, Cmd. The Op field describes the type of operation: 0 is an insert to the body of window with id WinId at Offset of length Len; 1 is a delete in the body of the window with id WinId of length -Len; 2 is the execution of the command Cmd that was executed from the window with id WinId; 3 is sent when a window is Put; 4 is sent when a file is closed (all Zeroxed windows with that file in the tag have been closed with Del); and 5 is sent when a file is first opened. Op 2 is only notified for the commands registered by the program using the /cmds URL. |
| POST | /cmds | Create a new client-defined command. If it already exists, register interest in it. | an array of strings where each element is a command name that does not contain spaces. |
| GET | /ws | Upgrade connection to a websocket | (does not return) |
| GET | /info | Retrieve info about Anvil | structure with fields ConfDir, Title |

## Sample Program 

This section contains an example program which uses the Anvil API. It is a shell script which formats C code and uses the CSV encoding when communicating with Anvil through the API. 

To use it, execute it from the tag or body of a window containing C source code. If there is no selection, the entire file is formatted. If there is a selection only that section of the file is formatted. 

The program demonstrates that extending Anvil through its API can be done as simply as writing a shell script.

```
#!/usr/bin/env bash

#
# Run clang-format on selected parts of text in an Anvil window body.
#

BASE_STYLE=Mozilla

clang_parts=""

# Get the selections of the current window in CSV format and strip off the CSV header line.
selections=`curl -s -H 'Accept: text/csv' -H "Anvil-Sess: $ANVIL_API_SESS" http://localhost:$ANVIL_API_PORT/wins/$ANVIL_WIN_ID/selections | tail -n +2`
if [ "$selections" != "" ]
then
  for sel in $selections
  do
    offset=`echo $sel | cut -d, -f1,1`
    length=`echo $sel | cut -d, -f3,3`

    clang_parts="$clang_parts -offset $offset -length $length"
  done
fi

# Get contents of window, pipe it through clang-format, then put the result back into the window.

curl -s -H "Anvil-Sess: $ANVIL_API_SESS" http://localhost:$ANVIL_API_PORT/wins/$ANVIL_WIN_ID/body | \
  clang-format -style="{BasedOnStyle: $BASE_STYLE, IndentWidth: 4, ColumnLimit: 0}" $clang_parts | \
  curl -X PUT -s -H "Anvil-Sess: $ANVIL_API_SESS" --data-binary @- http://localhost:$ANVIL_API_PORT/wins/$ANVIL_WIN_ID/body



```

