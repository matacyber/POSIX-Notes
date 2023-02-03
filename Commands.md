# COMMANDS

## Unix Commands
- `w` - Shows all users in a machine and some stats for them
- `date` - Shows the current datetime of the machine
- `cal` - Shows a calendar
- `df` - Shows the free space on the disk
- `free` - Shows how memory is being used on the system
- `pwd` - prints the current working directory
- `ls` - list the files in the current/any working directory
- `cd` - change the working directory
	- `cd -` takes you to the directory you just came from
- `mkdir` - create a directory
- `cp` - copy files or directories
- `mv` - move a file or directory
- `rm` - remove a file or directory
	- `-i` interactive flag
	- `-r` recursive flag
	- `-f` force flag
- `touch` - create a file
- `ln` - creates a symbolic link
	- `-s` creates a symbolic link
- `type` - shows the type of a file
	- `-a` shows all the locations of that NAME
- `which` - shows the location of an executable
- `help` - gets help for a shell builtin
- `man` - shows the man page for a command
- `aprops` - displays possible commands by searching man pages
- `whatis` - displays the name and a one-line description of the man page
- `sort` - displays as a sorted list
- `uniq` - accecpts a sorted list of data from either stdin or a file
- `wc` displays the number of files, words, and bytes contained in files
- `grep` finds text patterns within files
- `tail` prints the last 10 lines
- `head` prints the first 10 lines
- `tee` reads stdin and copies it to both stdout and to one or more files. This is useful for capturing a pipline's contents at an intermediate stage of processing
- `printenv` print all enviroment variables
- `groups` lists all groups the user is part of
- `nl` number the lines of a file when reading the file
- `fold` - Wrap each line to a specified length
- `cut` - Remove sections from each line of files
- `paste` - Adds text to one or more columns of a file
- `join` - Join Lines of two files on a common field
- `comm` - Compare two sorted files line by line
- `diff` - Compare files line by line
- `patch` - Applies changes to a text file
- `tr` - Translate characters from one to another
- `sed` - Stream editor for Filtering and Transforming Text
- `aspell` - An interactive spell checker

## Less Commands
- `^` - search for lines starting with the following character

## Keyboard shortcuts
- `ctrl-a` - Go to beginning of the line
- `ctrl-e` - Go to the end of the line
- `ctrl-r` - Reverse Search
- `ctrl-f` - Go forward one char
- `ctrl-b` - Go back one char
- `ctrl-k` - Kill everyting from cursor to end of line
- `ctrl-u` - Kill everyting from cursor to beginning of line
- `ctrl-y` - "Paste" from clipboard
- `ctrl-d` - Delete current current char
- `ctrl-p` - Pull last command
- `ctrl-n` - Go down the command history

- `alt-b` - Go back a word
- `alt-f` - Go forward a word
- `alt-backspace` - Delete entire word

## History Expansion
- `!!` - Last command
- `!-n` - Last n command
- `!*` - Grab all the args from the last command
- `!:p` - Print the history expansion command
- `!^` - Grab the first arg
- `!$` - Grab the last arg
- `!:n-n` - Grab a range of args
- `!(letter)` - Search for command starting with that letter
- `!?(letter)` - Serach for command with those letters

## Arthmetic Expansion
- `$((equation))` perform the equation in the expanstion

## Brace Expansion
- `{}`
- With brace expansion, you can create multiple text strings from a pattern containing braces

## Command Expansion
- `$VAR` allows for the use of enviroment variables

## VIM
- `j` - down
- `k` - up
- `h` - left
- `l` - right
- `a` - append (edit after the cursor)
- `i` - insert (edit before the cursor)
- `dw` - delete word from cursor to beginnig of the next word
- `d$` - delete everything from cursor to the end of the line
- `de` - detele from cursor to end of word
- `(#)w` - move that number of words forward
- `(#)e` - move the cursor to the end of the number of words forward
- `0` - return to the beginning of the line
- `dd` - delete line
- `(#)dd` - delete that number of lines
- `u` - undo
- `U` - undo whole
- `ctrl-r` - redo
- `dd` - cut
- `p` - paste
- `r(letter)` - replace cursor with that letter
- `ce` - change unitl the end of the word
- `cc` - ce for the whole line
- `o` - Start new line in insert below cursor
- `O` - Start new line in insert above cursor
- `e` - Jump from word to word


## POSIX Basic vs. Extendend RegEx
- BRE metacharacters `^` `$` `.` `[` `]` `*`
- ERE metacharacters
- `^$` will match empty lines
- `^` start with
- `$` end with

- regex101.com (regex tester online)

## File Text Processing
- `join` joins data from multiple files based on a shared key field
- `comm` compares to text files
- `diff` detects differences between files
- `tr` translates characters
-

## Process Subsitution
- `<(COMMAND)` run a command within another command
