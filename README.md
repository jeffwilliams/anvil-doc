# Quick Start

The HTML documentation is built using [MkDocs](https://www.mkdocs.org/getting-started/) with the [Material](https://squidfunk.github.io/mkdocs-material/) theme. The mkdocs-material theme requires python3.

First source your python virtual environment if needed:

  source python-venv/bin/activate

To preview the documentation, in the root directory run:

  mkdocs serve

To build the site for upload use 

  mkdocs build

# Installing mkdocs

Install mkdocs and the theme using:

    pip3 install mkdocs-material
    pip3 install mkdocs-video

In newer versions of Linux you will probably need to use a virtual environment for python. To set up mkdocs using a venv, instead from this docs directory do:

    python3 -m venv python-venv
    source python-venv/bin/activate
    pip3 install mkdocs-material
    pip3 install mkdocs-video

# Modifying

The videos in the tutorials were recorded using the following tools on Linux:

1. `simplescreenrecorder` was used to record .mkv files. These raw files are stored under img/
2. Video editing (trimming) was done using `shotcut`. 
3. .mkv files were converted to mp4 using ffmpeg: `ffmpeg -i input.mkv -codec copy output.mp4`
4. `screenkey` was used to show the mouse and keyboard events in certain videos.

Anvil was recorded at the resolution 1024x768 (actually 840x516) by starting it, creating a dumpfile, then editing its dumpfile. Start anvil, make it floating and load the dumpfile. Record from simplescreenrecorder by having it tiled in the same screen and clicking the Anvil window to record just that rectangle.

Screenshots of Anvil that were marked up with text were created using Inkscape and the originals are stored under the img/ directory as .svg files. Inkscape's "export bitmap" was used to create .png files.

# Writing release notes

Some useful tips:

* To link to a tutorial from the release notes, an example: [tutorial](../tutorials/column-rel-paths.md)
* To link to a heading in a reference: [Wrap](../reference/commands.md#wrap) Note that the heading is lowercase!
  * Dots in headings are elided in the anchor. style.js becomes stylejs: [style.js](../reference/config.md#stylejs)
  * Spaces are converted to hyphens: [Dbg Flame](../reference/commands.md#dbg-flame)
