# scr-obsidian-html
Front-end script to publish obsidian to an HTML target.

## Oboe usage
obsidian-html has been migrated to a new package by its auther for broader `.md` support and includes new features that overlaps with parts of this script. I recommend that you evaluate that author's new project instead of this script: https://github.com/kmaasrud/oboe. I've found that there is still pre- and post-processing necessary for my usage, so this project provides that functionality. kmaasrud/oboe is still under development and this project will be updated periodically to step along with that project. The differences are summarized here:
* Obsidian links `.md` files presuming a flat folder structure. oboe has an option `-d` to keep the folder structure or by default, operate only on the particular folder wherein the executable is run. When oboe operates with the `-d` option, the links in the resulting `.html` files do not include the retained folder structure, and so are broken. When oboe operates without the `-d` option, it only operates in the current folder. scr-obsidian-html enumerates all folders in the vault and executes oboe within each folder with the output set to a single folder. This allows for the flat link methodology to create working `.html` links.
* Obsidian links to embedded files without respect to the folder where those files are stored. oboe does not copy these external files to the output along with the `.html` output files.
* Block quotes have excess white space around them, which causes excessive space around the blockquote html, which requires additional space. This is trimmed in `footer.html`.
* The page title is pulled from the first `<h1>` tag in the output `.html`, as the `{TITLE}` provided by oboe is inconvenient in the header/footer template I'm using.
* The anchors used in Obsidian are of the form `link#anchor|label`, which should get transformed into `<a href="link#anchor">label</a>`, but instead appears to get transformed into `<a href="link">anchorlabel</a>`. This is fixed in `footer.html`.

# Installation
Requires the following:
* https://github.com/kmaasrud/oboe
* https://github.com/dev-west/scr-obsidian-html
* GNU coreutils 8.23 `realpath`
* python & pip

Execute in the obsidian-html repo directory:
> pip install git+https://github.com/kmaasrud/oboe

This installs an executable into `~/.local/bin`. This location is hard-coded in scr-obsidian-html. If you need to put the oboe executable somewhere else, update the 2 locations in the script (lines 115 and 121).

# Usage
Edit the script to change the base obsidian folder, the target HTML folder, and other options.

Note--resources referenced by the `![[ ]]` syntax should be in a folder below the .md that references it. If it's not found there, the script will move then to the base folder and begin crawling folders there looking for a file of the same name. There is an option in the script for another default resource location. These resources will be all be placed into a single `Assets` folder in the destination. The `footer.html` file presumes this location, as the parser does not create a href for `![[ ]]` resources quite correctly.
