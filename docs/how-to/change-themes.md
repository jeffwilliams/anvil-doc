# How to Change Themes

The fonts and colors that Anvil displays can be customized by creating the configuration file `style.js` in the Anvil [configuration directory](../reference/config.md).

There are a couple of ways to customize the Anvil theme. 

  1. You can download a different theme from the [themes](../themes/index.md) page, rename it to `style.js`, copy it to the Anvil [configuration directory](../reference/config.md), and load it in Anvil by executing the command `LoadStyle`, or by restarting Anvil.

  2. You can modify the default theme by executing the [`SaveStyle`](../reference/commands.md#savestyle) command with no argument. This will create `style.js` in the configuration directory. Then you can edit that style and load it in Anvil using `LoadStyle`, or by restarting Anvil. The `style.js` file is a JSON file described in the [Configuration Reference](../reference/config.md#stylejs)

The `LoadStyle` and `SaveStyle` commands can also load and save to a different file than the one loaded in Anvil by default in case you want to experiment with different styles without overwriting the default style.


