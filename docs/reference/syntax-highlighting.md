# Syntax Highlighting

Anvil supports syntax highlighting. The colors used for the different syntax elements are defined in the [style configuration file](config.md#stylejs). Synax highlighting is enabled and disabled using the [Syn command](commands.md#syn).

The current syntax highlighting implementation in Anvil is slow. For that reason, if a file being edited is more than 2 MiB syntax highlighting is disabled.