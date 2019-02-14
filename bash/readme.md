# Bash

Bash is a Command Line Interface (CLI), a "shell" that provide interactivity between linux system and the screen. Short for Bourne Again SHell and the successor to Bourne, one of the oldest shells used on the Unix platform and is still the default shell for many Linux distributions. 


+ Linux is configured to automatically start the binary `bin/bash` when logging into the system via CLI.
    + Known as the terminal in GUI versions of the OS.
+ Executing the command `bash` in the current bash instance will start another "child" instance. 
    + `exit` will terminate the current bash instance.
        + On the main or parent instance `exit` will stop bash and close the CLI or exit the terminal in a GUI.  

## Commands
Bash commands are formed by `<command> <flag> <arguments>...`. Not every command follows a standard convention, flags and arguments can have different order, e.g. `<command> <arguments> <flag>`
+ `<command>` - name of command.
+ `<flag>` - Also known as a switch and intended to change the behavior of the command. typically written with `-` following a character.
+ `<arguments>` - Parse input to be evaluated by the command.

Commands are generally categorized as:
+ Built-in - commands already available in bash.
    + Typing `man bash` will display all internal bash commands.
+ Binary - Commands that execute a binary file located on the file system.
    + `ls` for example, executes a binary located in `/bin/ls` 
+ Shell scripts - Text file of commands that get executed all at once.

#### Running Commands
+ `command` - commands are invoked by typing their name and hitting return key
+ `` `command` `` - back-tick takes the result of a command as standard output to be used as standard input.
    + `$((command))` - works the same way.
+ ` '' ` - Single quotes mean *literally* to avoid using commands and operations with the same characters. 
    + `<xml>` will result in an error, `'<xml>'` is the literal text.
+ ` ""  ` - Double quotes will expand variables to their values
    + ` "$variable" ` will return the value of a variable
+ `;` - Run multiple commands in one line, if one command fails all subsequent commands will attempt execute anyway.
    + `command ; command ; command `
+ `&&` - Chain commands together. If one command fails all subsequent commands will not execute.
    + `command && command && command `
+ `||` - Short Circuit, `or` operator. If the first command is successful then the second will not run
    + `command1 || command2`, if command 1 succeeds without error, command 2 will not execute.
+ `history` - display history of commands executed.
    + `history > file_history.txt`
    + `history | grep echo > history.txt` - filter by `echo` command and write to file.
#### Subshell
+ `(command)` - placing parenthesis around a command invokes the command to run in a subshell
 ### Navigating file system

#### Paths
+ `.` & `..` are relative to the current directory.
    + `./file.txt` a text file in the current directory.
    + `../file.txt` a text file in the parent of the current directory.
+ `/` & `~/` are absolution paths.
+ `~` - full path to current user directory. 
+ `pwd` - Will display the path of the current directory
+ `ls` - Will list all the files and directories in the current directory
    + `ls -a` - List all, including hidden files. 
    + `ls ./` - list current directory.
    + `ls ../` - list parent directory.
    + `ls ../../` - list parent of parent directory. 
+ Hitting `tab` key while typing a file or directory will auto-complete the name.
    + Hitting `tab` once will complete a distinct name
    + Hitting `tab` twice will give a list of similarly named files and directories.
+ `echo` - will display its arguments
    + `echo file.txt` will display `file.txt`.
+ `*` - Wild cards - Bash will search for similar named files and directories as arguments to another command.
    + `ls *.txt` list all files with .txt in the name
+ `{,}` - Brace expansion enable you to generate lists to be passed as arguments.
    + `echo text{_,}` will append a `_` and `text`, displays `text_ text` or run `echo text{_,_}` to get `text_ text_`
    + `echo a{1..3}.txt` - sequencing, `a1.txt a2.txt a3.txt`.
        + `echo a{1..10..2}.txt` - sequencing with step, `a1.txt a3.txt a5.txt a7.txt a9.txt`
    + `{a, b}{c, d}{1, 2, 3}` - to generate `ac1 ac2 ac3 ad1 ad2 ad3 bc1 bc2 bc3 bd1 bd2 bd3`


#### File Permissions
Three categories of users with three types of permissions:
+ `d` - directory
+ `r` - read
+ `w` - write
+ `x` - accessible

+ `ls -l` - Displays permissions on files and directories in current directory
```sh
drwxr-xr-x 1 vrez 197609 0 Dec  5 23:42 dir/
-rw-r--r-- 1 vrez 197609 0 Dec  5 23:42 file.txt
```

|User|Group|Other|item|
|:---|:---:|---:|---:|
|rwx|r-x|r-x|dir/|
|rw-|r--|r--|file.txt|


+ `chmod` - give/remove permissions
    + `chmod u+x` - grant user access to file/directory.
    + `chmod u-x` - remove user permissions.
    + `chmod 707` - give/remove via octal
        + Add:
            + 4 - write
            + 2 - read
            + 1 - execute
+ `groups` - to see groups 


### Working with directories and Files
+ `mv` - move or overwrite files and directories: 
    + `mv file1.txt dest_dir/` will move "cut" `file1.txt` from current directory to `dest_dir/`.
    + `mv dest_dir/file1.txt .` will move `file1.txt` from `dest_dir/` to the current directory.
    + `mv file1.txt dest_dir/file2.txt` will move and rename the file and remove the original file. 
    + `mv file1.txt file2.txt` will overwrite the existing `file2.txt` with `file1.txt` content and remove `file1.txt`.
        + `file2.txt` doesn't have to exist. 
    + `mv dir1/ dir2` will move the exiting `dir2` inside `dir1` and removes `dir1`.
        + `dir2` doesn't have to exits 
+ `mkdir` - create a new directory:
    + `mkdir dest_dir/` will create a directory named `dest_dir`.
    + `mkdir -p dir1/dir2/dir3` wil create a directory structure `dir3` in `dir2` in `dir1` in current directory. 
        + if `dir1` already exist it will create the remaining without effecting existing files.
    + `mkdir dir{1..3}` wil create directories `dir1`, `dir2`, `dir3` in the current directory. 
+ `cat` - concatenate files / display file contents:
    + `cat file1.txt` displays the file content on the screen.
    + `cat` alone will read from the standard input (Stdin) and requires `ctr + d` or `ctrl + c` to terminate. 
    + `cat` with a non-text based argument such as an image will display non-ascii characters. Run `reset` to clear the screen
    + `cat *.txt` use of a wild card `*` will concatenate the contents of all files with a `.txt` in the name.

```sh
#file1.txt
"hello"
```

```sh
#file2.txt
"world"
```
`cat file1.txt file2.txt`
```sh
>"hello"
>"world"
>
``` 
+ `cp` - Copy contents from one file to another.
    + `cp file1.txt file2.txt`
        + `cp file1.txt dest_dir/` copies to directory as `file1.txt`
        + `cp file1.txt dest_dir/file2.txt` copies to directory as `file2.txt`. 
        + `cp file1.txt file2.txt dest_dir/` copies multiple files into a directory. 
            + `/` is not required since cp will check if last argument is a directory. 
    + `cat -r src_dir/ dest_dir/` will *recursively* copy an entire directory structure to another location.
        + Destination directory will be created if it doesn't exist. 
+ `rm` - Delete files and folders. **WARNING: THERE IS NO UNDO FOR THIS COMMAND**.
    + `rm file.txt` remove single file
    + `rm dir/` or `rmdir dir/` will only work if the directory is empty.
        + `rm -r` Requires `-r` recursive flag to delete non empty directories. 
    + `rm -rf *.txt` remove all files ending with `*.txt` , `-f` flag to force deletion of protected files. 
    + `rm -rf dir/*.txt` remove all files ending with `*.txt` in a directory `./dir` 
    + `rm -r */` - remove all directories in current directory. 
    + `rm -r *` - remove all files and directories in current directories


### Working with Files
+ `wc` - display the number of lines, words and characters in a text file.
    + `hello world` in `file.txt`, `wc file.txt` returns `1  2 12 file.txt`
    + `wc` alone will wait for a response from the standard input, key strokes until `ctr-d` end of file is invoked.
        + `man wc` to see available options.
+ `head` - display the first 5 lines in the file.
    + Useful for shortening output messages.
    + `head -n2 file.txt` display 2 lines.
    + `head -c 5` display first 5 characters. 
+ `tail` - display the last 5 lines of a file.
   <!-- + `head -n10 | tail -n5 | head -n2` - `head` and `tail` can be chained. --> 
+ `fold` - shrink the column display width by x amount characters
    + `fold -w50 file.txt` - Shrink the column with by 50 characters
        + `-sw` word wrap.
+ `>` - Write to file, also known as output redirect. 
    + `some text > file.txt` writes `some text` to `file.txt`
    + `ls > file.txt` writes the contents of the current directory to a text file.
    + The output of the redirect will be in `ls -1` format since it's easier for other applications to read line by line than in column format.
+ `>>` - Append to the end.
    + `other text >> file.txt` writes `some text other text`.
+ `<` - Input redirect.
    + `wc -c < file.txt` will take the contents of `file.txt` and pass it as arguments using standard in. 
+ `|` - pipe, takes the output of one command and feeds it as input to another.
    + `cat file.txt | wc` will take the contents of the `file.txt` and use it as stdin for the `wc` command.
    + `ls -1 -a | wc -l` count number files and directories there is in the current directory.
+ `xargs` - takes the result of a command and puts it in (use stdin) as arguments for another command.
    + `echo there | xargs echo hi` - results in `hi there`
+ `sed` - Insert, delete, search and/or replace,s in a file or stream of data. 
    + `sed s/hello/hi/ file.txt` - for each line replace the first instance of `hello` with `hi`
    + `/1` - first instance, `/2` second instance.
    + `/g` - global (all instances).
    + `/r` - required to escape meta characters in regex. 
<!--+ `awk` - Search and filter by data in a field.-->
+ `grep` - Filter from a list or a file.
    + `grep qu words.txt` show every line that contains `qu`.
        + Use `-i` for case insensitivity.
    + `-E` flag is required to escape meta characters in regex searches.
+ `egrep` - Filter from standard in.
    - `echo "The order number is #3424-Q9348" | egrep -o '[0-9]+\-Q[0-9]+'` - Will use regex to extract the order number from the string.


### Working with compressed files
+ `unzip` - un-zip `.zip` files.
    + `unzip data.zip`.
+ `gunzip` - read compressed data from standard input and return data to standard output.
    + `cat data.zip | gunzip > data.csv` - `cat` a compressed file to standard output, (normally displayed as non-ascii symbols), pipe `|` this data into `gunzip` and write it to a text file. 

### Working with files on network
+ `curl` takes a url and prints it to standard out.
    + `curl https://chronicdata.cdc.gov/views/g4ie-h725/rows.csv?accessType=DOWNLOAD`
    + `curl https://link > file.csv` will save the contents into a file.


## System

### Exit Codes
+ `$?` - If a command was successful an system 'exit code' will return a `0`, otherwise it will return an error code
    + `echo $?` - To display exit code after the completion of a command, code may differ depending on the system. 
    + `cannot execute binary file` error will return `126` on MINGW64.
    + `No such file or directory` error will return `127` on MINGW64.
+ `test` - test a command without invoking and error
    + `test -f file.txt` - test if file exists. 

### Jobs and Processes
+ `ctr-z` - Postpones a running application to the background.
    +  `vim file.txt` while editing a file, this application can be postponed by `ctr-z`
    + Multiple postponed applications are added to a job list.
    + `comand &` - Add a process to the background without running it.
        + `vim file.txt &` - Adds open a file with vim as job  
+ `jobs` - To see jobs that have been placed in the background.
+ `fg` - Resume the first job in the background.
    + `fg %5` - Resume the fifth job in the background.
+ `bg` - Run a process in the background. 
+ `kill` - Terminate a process.
    + `kill %%` - Terminate top most job.
    + `kill %3` - Kill job number 3.
    + `kill -9 %1` - Use the Operating System to force terminate an application.
+ `pgrep` - Search for a running process. 
+ `pkill` - Terminate specific process.
+ `pid` - Terminate process by ID. Every running process has an ID. 
+ `sleep` - pauses the system for x amount of seconds.
    + `sleep 5` - pause for 5 seconds.
<!--+ `screen` - Displays information on running terminals.
    + `screen -list` - Information on running terminals. 
    + `screen -x processname` - Information on running terminal screen.
    + `ctr-ad` - To detach from the terminal. 
    check out using screen in node.js
-->
### Working with Date and Time
+ `date` - Display detailed current date.
    + `date +'%H:%M:%S'` displays time in HH:MM:SS format
    + `date +'%M/%D/%Y'` displays date in MM/DD/YYYY format
    + `date +'%F %T'` display YYYY-MM-DD HH:MM:SS format
    + ``echo `date` '+%F %T' >> log.txt some text `` append a time stamp to the end of a file.
    +  ``echo some text > `date` '+%F'`` - create a time-stamp (or procedurally made) file name and write `some text` into it.
    + `$(($(date '+%d')+3))` - add 3 to current day. 
+ `cal` - Displays current month, this will not work in all shells.
    + `cal 2018` - Display all of 2018.

## Working with Variables
A variable is a container for data, to store something and refer to it later. 

```sh
color="red"
```

+ You cannot have spaces when assigning variables.  
    + `color = "red"` will throw `command not found` error since text surrounding spaces are treated as separate commands. 

+ `$` sign is proceeded by the variable name to retrieve the value. 
    + `echo $color` returns `red`
    + `echo color` will return the variable name `color`.

+ Variables are local to the shell they're created in and are inaccessible to other instances. 
+ Local variable can be promote to a global/environment variable with the `export` command. 
    + `export color` will be available to all instances of the shell. 
    + Running `export` alone will display all environment variables.

Consider a bash `.sh` script:
```sh
color="red"
echo $color
```

There are two ways to run the script:
+ Pass the script to a bash binary `bash script.sh`. 
    + This will open a sub-shell and execute the script.
+ Self execution mechanism `./script.sh`
    + You have to promote permissions to do this with `chmod +x script.sh`

Since linux systems can have multiple shells, you can add a sha-bang `#!/bin/` (also known as the interpreter) at the beginning of the script to inform the system which binary should the script be parsed.
 
```sh
#!/bin/bash
color="red"
echo $color
``` 
+ `unset` will remove a variable's value, `unset color`.
    + Can be used to remove the value from a local variable after exporting it to a environment variable. 

Consider the script:
```sh
echo $shape
```

If from the current bash instance we set `shape=square` and run as `bash ./script.sh`, bash will return as a empty line. This is because a new shell instance is created and the value to `shape` is not available in that scope. However, using source command `. ./script.sh` or `source ./script.sh` we can expose the variable to the context of the current shell. 
<!--Notes:
Research:
+ less
    + ls -l /. | less
+ perl-->

### Reading from Standard Input
+ `read` will open standard input and wait for a user to type.

```sh
#!/bin/bash
echo -n 'Username?'
read USERNAME
echo "$USERNAME logged in at `date '+%T'`"
```

### Control Structures

#### for in loops
In-line : `for i in {10..100.10}; do echo $i; done` - print 10 to 100 by 10 steps.
Script
```sh
for x in {0..10};
        do echo $x;
done
```
#### While loops

+ `while` - while a condition is true, do an action.
    + In-line: ``while true; do echo `date`>>log.txt; sleep 5;done`` - infinite loop to write the date into a file. `ctr-c` to exit the loop
    + `ls -1 *.* | while read ROW; do wc -l "$ROW"; done` - will parse each file contents in the current directory to `read` and assign it to variable `row`, and this variable will be an argument to `wc -l` and return the number of lines of each word 

```sh
while true 
    do #something
done
```
#### Until loop

+ `until` -until something is true.

```sh
until false 
    do #something
done
```
### Conditions

+ `if` - If condition is true.
```sh
if true then
     #something
     elif false
        #else if something
     else
     #something else
fi
```

## Operations

Bash runs a group of binaries when starting up, this is listed in a `.bash_profiles` file located in the home directory `/home/<username>`.
+ This file will not be named the same in every linux distribution. 
    + It's named `.profile` in Ubuntu for example. 
+ Use `~/` to "expand" and to make the file available for editing, `vim ~/.bash_profile`
+ Use `./` launches a new shell and run the file, `./script.sh`. 
 
The contents of `.bash_profiles` or `.profile` with contain:

```sh
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
    # then execute .bashrc using the source command.
    # "." alias to "source" executes the script that all the variables and commands are available in the current shell instance.
        . "$HOME/.bashrc"
    fi
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

This script will run whenever the login shell gets invoked. The login shell is the first shell started when you login the system or switch to a different user, `sudo su` for example. Subsequent bash instances will not invoke the profile script. 

In short this script will:
1. See if the file `.bashrc` file exists.
    + Contains enviornment level variables and commands that are needed for bash to functoin correctly. 
2. If file exist, execute the file.
    + The `.` is an alias for `source` command. 
    + Any variables or commands defined within this script will get executed within the context of the current shell.
3. Check if `usr/local/bin` exists, if yes add it to PATH.
    +  Directory where user created binaries are held. 
    + `sudo cp logger /usr/local/bin/<name-of-binary>` to install user created binaries. 
4. Then add all your binaries to the default `PATH`.  



The role of the `PATH` is to give user access to their binaries from the command line. For example, using `ls` would be too much typing if `/bin/ls` had to be written everytime we want to list files. This is especially inconveniet for files with long directories.  
