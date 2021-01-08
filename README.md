# scr-obsidian-html
Front-end script to publish obsidian to an HTML target. Renders into flat folder structure due to obsidian-html link presumption.

# Installation
Requires the following:
* https://github.com/kmaasrud/obsidian-html
* https://github.com/dev-west/scr-obsidian-html
* GNU coreutils 8.23 `realpath`

Execute in the obsidian-html repo directory:
> sudo python3 setup.py develop

This installs additional required resources for obsidian-html and adds 'obsidian-html' to your PATH so it can be run in any folder.

# Usage
Edit the script to change the base obsidian folder, the target HTML folder, and other options.

Note--resources referenced by the `![[ ]]` syntax should be in a folder below the .md that references it. If it's not found there, the script will move then to the base folder and begin crawling folders there looking for a file of the same name. There is an option in the script for another default resource location. These resources will be all be placed into a single `Assets` folder in the destination. The `footer.html` file presumes this location, as the parser does not create a href for `![[ ]]` resources quite correctly.

# Future
I'd like that the output be rendered into the same folder structure as the source, but this will require either addressing obsidian-html's output a href links after the fact, or modifying the source py code. Will be investigated in future.

Paser issues:
* no .html extensions on output
* codeblocks do not prevent md formatting
* tags render as h1 when near top of page
* assert failure without extra space around ordered lists (maybe unordered as well)
* `![[ ]]` linked resources not linked correctly in html

Had been hoping to get through this project without PHP, but used in the template file for ease of linking the header and footer. May work on an updated parser to address these issues and practice python and/or PHP.
