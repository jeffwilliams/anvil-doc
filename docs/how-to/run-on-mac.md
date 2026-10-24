# How to Run Anvil on Mac

If you download the binary version of Anvil from the [Download](../download.md) page, you need to take special steps to run the binary on your Mac. Currently the MacOS binaries are signed, but not with an official code-signing certificate. When run, you may observe dialog boxes that complain that Anvil cannot be checked for malicious software. You can prevent this by running the command `xattr -d com.apple.quarantine anvil`, where `anvil` is replaced with the full path to the Anvil binary.
