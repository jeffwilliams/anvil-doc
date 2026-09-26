# Handling Interactive Commands

OS commands run within Anvil should not be interactive. They can read standard input and write to standard output, but they should not try to stop and prompt the user for values from the terminal. Sometimes this is unavoidable, however; most often with commands that require a password such as a `git pull`, or when using scp to copy a file.

However, Anvil has a companion program named `awin` that provides a rudimentary method to interact with such programs. The awin program is similar to Acme's win program. 

To use `awin`, run the interactive command line prefixed by `awin -- `. awin will create a new window in Anvil using the API. Output from the interactive program will be appended to this window. To send a line of input to the program you can either:

  * type a line of text at the very end of the window body followed by Enter
  * execute the Send command in that window to send the arguments of Send to the program.

Except for the the very end of the body which is used to send data, the rest of the body can be modified as desired like any Anvil window.

## Demo Video

This video demonstrates the use of `awin`. In the video we create a file, encrypt it with `gpg`, and then decrypt it. To encrypt the file we run the `gpg -ca` command -- which creates an ascii-armored output file -- through awin since it prompts the user for a password. We then run the `gpg -d` command through awin to decrypt the file and view its contents. 

Note that the password is displayed in cleartext; to hide the password we cut it from the body like any regular text.

![type:video](../../img/anvil-tut-awin-1.mp4)