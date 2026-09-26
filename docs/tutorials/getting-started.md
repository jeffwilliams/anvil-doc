# Getting Started

This tutorial will walk you through the basic steps of installing Anvil and editing your first file. We'll use Anvil to write a simple html file.

By the end of the tutorial you will know:

* how to launch Anvil
* how to navigate between different columns and windows
* how the mouse is used in Anvil
* how to use multiple selections
* how to launch external commands

This tutorial assumes you have access to the bash shell under Linux, and the command prompt in Windows.

## Install Anvil

In this tutorial we'll install Anvil by downloading the executable. If you instead want to download the source and compile it, follow the instructions [here](dead link).

Navigate to the [Releases](dead link) page. Download the latest executable by clicking on ?. Move this executable binary to a local directory and ensure that directory is in your path:

=== "Linux"

    Assuming the anvil binary has been downloaded to `/home/$USER/Downloads` run the follow steps in bash:

    ```
    [ -f ~/bin ] || mkdir ~/bin
    cp /home/$USER/Downloads/anvil ~/bin
    chmod +x ~/bin/anvil
    export PATH=$PATH:/home/$USER/bin
    ```

    To make the change that adds Anvil to your path persistent in bash, edit your `$HOME/.bashrc` file and add the line: 
    ```
    export PATH=$PATH:/home/$USER/bin
    ```

=== "Windows"

    Assuming the anvil executable has been downloaded to `C:\Downloads` perform the following steps:

    * Using Windows Explorer, make the directory `C:\Program Files\Anvil`. 
    * Copy the Anvil executable from `C:\Downloads` to `C:\Program Files\Anvil`
    * Add the directory `C:\Program Files\Anvil` to the Windows path:
      * Launch the Control Panel.
      * Choose System→About→Advanced System Settings
      * Select ‘Environment Variables’
      * Edit the environment variable ‘Path’ and add the directory `C:\Program Files\Anvil`
    * You will need to restart any Power Shell or Command prompt instances to have the environment variable take effect

## Launch Anvil

First make a new directory where we'll be working on the shell script. This can be any path, but for the purposes of this tutorial we'll assume it's `/home/$USER/anvil-tut-script` on Linux or `C:\temp\anvil-tut-script` on Windows.

Once created, launch Anvil from that directory:

=== "Linux"

    ```
    cd /home/$USER/anvil-tut-script
    anvil
    ```

=== "Windows Command Prompt or PowerShell"

    ```
    cd C:\temp\anvil-tut-script
    anvil
    ```

=== "Windows Explorer"

    Browse to the direcory in Windows Explorer. Then in the address bar, type `anvil` and hit enter.

When Anvil first launches it will have two columns. The leftmost column will be empty, and the right column will have one window which displays the contents of the current directory. Since the directory is empty the window in the right column will be empty.

## Paste in the Initial Text


We'll be using this text from the beginning of `Queen of the Black Coast` by Robert E. Howard to create our page:

    HOOFS drummed down the street that sloped to the wharfs. The folk that yelled and scattered had only a fleeting glimpse of a mailed figure on a black stallion, a wide scarlet cloak flowing out on the wind. Far up the street came the shout and clatter of pursuit, but the horseman did not look back. He swept out onto the wharfs and jerked the plunging stallion back on its haunches at the very lip of the pier. Seamen gaped up at him, as they stood to the sweep and striped sail of a high-prowed, broadwaisted galley. The master, sturdy and black-bearded, stood in the bows, easing her away from the piles with a boat-hook. He yelled angrily as the horseman sprang from the saddle and with a long leap landed squarely on the mid-deck.
    
    "Who invited you aboard?"

    "Get under way!" roared the intruder with a fierce gesture that spattered red drops from his broadsword.

    "But we're bound for the coasts of Kush!" expostulated the master.

    "Then I'm for Kush! Push off, I tell you!" The other cast a quick glance up the street, along which a squad of horsemen were galloping; far behind them toiled a group of archers, crossbows on their shoulders.


