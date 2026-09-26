If you've used Acme before and trying out Anvil, you may wonder why the ALT key is used to modify right clicks. In Acme, clicking the right mouse button acquires the text directly: if the text matches a plumbing rule that rule is executed; if it is a file, it is opened; otherwise a search for that text is performed. To distinguish between the last two, Acme must check the filesystem to see if the text represents a file. If it does then it can be opened as a file, and if it doesn't then that text is searched instead.

In Anvil, though, the files being opened might be on the local computer or a remote one, and to Anvil “remote” means “accessible over SSH”. If we were to distinguish between a file and a search the same way as Acme, that would require checking for the file over the network which can have significant latency. It would mean each search the user executed would have an observable delay at best, or a significant pause at worst. The experience would be frustrating.

Granted, we could guarantee that the right-clicked text does _not_ represent a remote file by checking if the file path in the tag being edited in the current window contains a colon, but if it _is_ a remote file we still can't tell if our text item is a search term or a different remote file to be opened. 




