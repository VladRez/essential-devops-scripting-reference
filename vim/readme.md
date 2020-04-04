# VI/VIM
VI and VIM is a command-line based text editor used in Unix environment. The VIM editor is the successor of an older editor called VI, VI's features are a subset of VIM. Any unix system is going to have VIM installed, if not then it will most likely have VI installed. 

Sometimes the systems has constraints that don't have the resources to load a UI or don't have a graphics card such as a wireless router. VIM is useful for making edits in remote environments especially when ssh-ing into it. 

## Installation
If VIM is not installed then install it with: 

```
sudo apt-get install vim vim-common
```

VIM in many ways is it's own language optimized in making edits to files efficient:

+ Shift indentation on blocks of text.
+ Syntax highlighting and markup for many programming languages.
+ Interactive interface within the shell.
+ Vim uses [ANSI escape codes][ANSI] to control a cursor and position blocks of text on the screen. 
+ All settings can be modified in `~/.vimrc` file.

## Basic Operation

Start VIM by typing `vim` in the shell.

### Modes

There are generally two modes:
+ Insert Mode - Edit document.
+ Command Mode - Navigate and perform basic edit operations on the document.
+ Visual Mode - Select and edit content

#### Basic Editing

VIM will start with command mode. 

To edit we need to be in insert mode, enter this mode by typing `i` and you will see `--INSERT--` the bottom of the screen. 

Start typing:

```sh
color="red"
echo $color
```

Hit `Esc` or type ctr-c to exit out of insert mode

### Saving Files

Since we started vim with a new file we need to save the file.

+ `:w` - To save, example `:w script.sh`
+ `:q` - to exit VIM type:
+ `:wq` - to edit the same file and quit and the same time you can combine commands.
+ `:q!` - To discard changes use
+ `:o` - To load a file that already exists, example `:o script.sh`

### Navigating files

In Command Mode, To Navigate the document:

+ `k` - Move Up
+ `j` - Move Down
+ `h` - Move Left
+ `l` - Move Right
+ `:Explore` - Open Directory listing
    + `e: path/` - Display contents of the path.
+ `f` + `search_char` - Jump from current position to `char`.
	+ `f + $` - Jump to next `$` on the line.
+ `t` + `search_char` - Jump from current position to `char`.
	+ `t + $` - Jump to next character position before `$` on the line.

Commands can be run N amount of times by typing a number before a command.

+ `gg` - Jump to beginning of document.
+ `G` - Jump to end of document
+ `^` or `0` - Home or Jump to the beginning of the line.
+ `G` - Jump to the end of the document.
+ `$` -Jump to the end of the current line.
+ `j` - Join two lines

#### Split Screen
+ `:split` - Split Screen Horizontally.
+ `:vsplit` - Split Screen Vertically.
+ `ctr-w` + arrow keys - Switch between screens.
+ `ctr-w>` - Increase window size.
+ `ctr-w` - Decrease window size.
+  [More Details][windowsplit]

### Operators

+ `dd` - Cut or delete entire line.
	+ Inserted into clipboard (paste buffer).
+ `x` - Cut ordelete character in front of the cursor.
	+ Inserted into clipboard (paste buffer).
+ `u` - Undo
+ `ctr-r` - Redo
+ `p` - Paste text from clipboard (paste buffer)

#### Deletion

All start with `d` followed by a command.
+ `dd` - Delete entire line.
+ `dG` - Delete from the current position to the end of the document.
+ `dgg` - Delete from current position to the start of the document. 
+ `dj` - Delete current line and the one line below.
+ `dk` - Delete the current line and one above.
+ `dh` - Delete character to left of cursor.
+ `dl` - Delete character to right of cursor.

### Search by Regex

+ `/search_word` - To search forward.
	+ `Enter` then `n` key will go to next match.
	+ `Enter` then `N` key will go to previous match.
+ `?search_word` - To search backwards.

#### Search and Replace 

+ `s/search_keyword/replace/` - Search and replace the first instances on the line
	+ `s/search/replace/g` - Use `g` flag to replace all instance on the line
	+ `%s/search/replace/g` - Use `%s` to search every line in the file.
+ `\(keyword\)` - Capture group.
    + `\1 \2` - Reference capture group.

#### Search and Delete
+ `dn` - Delete next result.
+ `dN` - Delete previous result.
+ `d/pattern` - Delete everything until pattern forward.
+ `d?pattern` - Delete everything until pattern backwards. 

## Visual Mode

Hit `v` enter into visual mode, `--VISUAL--` will appear at the botton of vim.

+ All commands for navigation work in command mode as well.
	+ Select line by line by pressing capital `V`to go into visual Line select mode.

+ Search and replace work the same way by pressing `:`.
+ `y` - "yank" or copy text.
+ `x` - Cut or Delete selected text.
+ `>` - Indente right.
+ `<` - Indent left.
+ `:r!` - run selected block in a terminal and paste the result in the current document.
	+ `:r! echo hi there`
+ `:norm i//` - For Each selected line insert `//` in front.
    + `norm x` - Delete first character of each line.
        `:norm xx` - Delete first two characters of each line.

[ANSI]:"https://en.wikipedia.org/wiki/ANSI_escape_code"
[windowsplit]:"https://vi.stackexchange.com/questions/514/how-do-i-change-the-current-splits-width-and-height"
