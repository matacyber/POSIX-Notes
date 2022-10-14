# Part 1: Learning the Shell

## *Notes have been adapted based on Professor Martin White's CSCI 220 - Life Beyond Python Lecture Notes*

## 1: What is the Shell
- The command line as we refer to it is really a shell, command interpreter
- There are many shells `sh`,`csh`,`ksh`, and `bash`
- The shell is a program that takes keyboard commands and passes them to the operating system to carry out

### Terminal Emulators 
- When using a graphical user interface, we need another program called a terminal emulator to interact with the shell
- They all do basically the same thing: give us access to the shell

## Your First Keystrokes

- Launch the terminal emulator!

```
[me@linuxbox ~]$
```

- This is called a _shell prompt_, and it appears whenever the shell is ready to accept input
- `username` `machinename` `current working directory` `$` `#`
- If the last character is `#` rather than `$`, the terminal has _superuser_ privileges
- This means that either we are logged in as the root user or we've selected a terminal emulator that provides superuser (administrative) privileges

### Command History
- Previous commands can be recalled from the history file (.bash\_history)
- Using `ctrl-p` or `the up arrow` you can go backwards through your history file
- Using `ctrl-n` of `the down arrow` you can go forward through your history file
- This is called command history

### Cursor Movement
- You can move your cursor forward and backward using the arrow keys
- You can also use `Ctrl-b` and `Ctrl-f` to move forward and backward respectively 

## Try Some Simple Commands

- `date` displays the current time and date
- `cal` displays a calendar of the current month
- `df` displays the current amount of free space on your disk drives
- `free` displays the amount of free memory

## Ending a Terminal Session

- Close the terminal emulator or enter the `exit` command or press `Ctrl-d` (but only when the command line is empty)

- *See Command.md for more commands and keyboard shortcuts*


## 2: NAVIGATION

### Understanding the Filesystem Tree
- Unix-like operating systems organize files in what is called a _hierarchical directory structure_
- Tree-like pattern of directories, which may contain files and other directories
- _root directory_
- Unlike Windows, which has a separate filesystem tree for each storage device, Unix-like systems always have a single filesystem tree
- Storage devices are _mounted_ at various points on the tree

### The Current Working Directory
- At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the _parent directory_) and any subdirectories below us
- The directory we are in is called the _current working directory_
- `pwd` displays the current working directory
- When we first log in (or start a terminal emulator session), our current working directory is set to our _home directory_
- Each user account is given its own home directory

### Listing the Contents of a Directory
- `ls` lists the files and directories in the current working directory or any directory

### Changing the Current Working Directory
- `cd pathname/of/the/desired/working/directory` changes your working directory
- A _pathname_ is the route we take along the branches of the tree
- Pathnames can be specified in one of two ways

### Absolute Pathnames
- An _absolute pathname_ begins with the root directory

```
[me@linuxbox ~]$ cd /usr/bin
[me@linuxbox bin]$ pwd
/usr/bin
[me@linuxbox bin]$ ls
```

- Notice how the shell prompt has changed
- (Notice some of the files in `/usr/bin`...`which`...`whereis`...and notice files _not_ in `/usr/bin`)

### Relative Pathnames
- A _relative pathname_ starts from the working directory
- `.` and `..` are special symbols to represent relative positions in the filesystem tree

### Some Helpful Shortcuts
- `cd`
- `cd -`
- `cd ~username`
- IMPORTANT FACTS ABOUT FILENAMES
  - Filenames that begin with a period character are hidden
  - When your account was created, several hidden files were placed in your home directory to configure things for your account
  - Filenames and commands in Linux are case sensitive
  - Linux has no concept of a "file extension" like other operating systems. The contents and/or purpose of a file is determined by other means
  - Limit the punctuation characters in the names of files you create to period, dash, and underscore

## 3: Exploring The System

### Options and Arguments
- Commands are often followed by one or more _options_ that modify their behavior and, further, by one or more _arguments_, the items upon which the command acts
- So most commands look something like this:

```
command -options arguments
```

- Most commands use options consisting of a single character preceded by a dash
- But many commands also support _long options_, consisting of a word preceded by two dashes
- Also, many commands allow multiple short options to be strung together

```
[me@linuxbox ~]$ ls -al --reverse
```

### Determining a File's Type with file
- `file` displays a brief description of the file's contents
- There are many kinds of files. One of the common ideas in Unix-like operating systems is that "everything is a file"

### Viewing File Contents with less
- `less` views text files in a scrollable format

### A Guided Tour
- The filesystem layout is specified in the [Linux Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

### Symbolic Links
- We are likely to see a directory listing with an entry like this:

```
lrwxrwxrwx 1 root root...
```

- In most Unix-like systems it is possible to have a file referenced by multiple names
- Symbolic Links are like shortcuts in Windows its a reference to another file or directory

## 4: Manipulating Files and Directories

### Wildcards
- The shell provides special characters called _wildcards_ to help rapidly specify groups of filenames
- Using wildcards (also known as _globbing_) allows you to select filenames based on patterns of characters

### mkdir&mdash;Create Directories
- `mkdir` creates directories

### cp&mdash;Copy Files and Directories
- `cp` copies files or directories

### mv&mdash;Move and Rename Files
- `mv` performs both file moving and renaming, depending on how it is used

### rm&mdash;Remove Files and Directories
- `rm` removes (deletes) files and directories
- BE CAREFUL WITH RM!
  - Unix-like operating systems do not have an undelete command
  - Be particularly careful with wildcards
  - Whenever you use wildcards with `rm`, test the wildcard first with `ls`
  - rm will delete whatever you tell it to, often without question, so be CAREFUL

> Unix was not designed to stop you from doing stupid things, because that would also stop you from doing clever things.
> -Doug Gwyn

### ln&mdash;Create links
- `ln` creates either hard or symbolic links

### Hard Links
- Hard links are the original Unix way of creating links; symbolic links are more modern
- By default, every file has a single hard link that gives the file its name
- Hard links have two important limitations...so modern practice prefers symbolic links

### Symbolic links
- They operate like a Windows shortcut
- A file pointed to by a symbolic link and the symbolic link itself are largely indistinguishable
- If you write something to the symbolic link, the referenced file is also written to
- _Broken_ links

## 5: Working With Commands

### What Exactly Are Commands
- A command can be one of four things:
  - An **executable** program like all those we saw in `/usr/bin`. Programs can be _compiled binaries_ or programs written in _scripting languages_
  - A **shell builtin** (built into the shell itself), e.g., `cd`
  - A **shell function**&mdash;a miniature shell script incorporated into the _environment_
  - An **alias**&mdash;a user-defined command, built from other commands

> If the first word of the command line does not correspond to a built-in shell command, then the shell assumes that it is the name of an executable file that it should load and run.[^1]

[^1]: Computer Systems: A Programmer's Perspective

### Identifying Commands
- `type` is a shell builtin that displays the kind of command the shell will execute, given a command name:

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type -a cd
cd is a shell builtin
cd is /usr/bin/cd
cd is /bin/cd
```

- `which` displays an executable's location
- `which` works only for executable programs

### Getting a Command's Documentation
- `help` gets help for shell builtins
- Many executables support a `--help` option that displays a description of the command's supported syntax and options
- Some programs don't support the `--help` option, but try it anyway. Often it results in an error message that will reveal the same usage information
- `man` displays a program's manual page, a formal piece of documentation intended as a reference, not a tutorial
- On most Linux systems, `man` uses `less` to display the manual page, so all of the familiar `less` commands work while displaying the page
- See Table 5-1: Man Page Organization

```
[me@linuxbox ~]$ man 5 passwd
```

- THE MOST BRUTAL MAN PAGE OF THEM ALL - _man bash_ (see p. 44)
- `apropos` displays appropriate commands  by searching the list of man pages for possible matches based on a search term
- `whatis` displays the name and a one-line description of a man page matching a specified keyword

### Creating Your Own Commands with alias
- Put more than one command on a line by separating each command with a semicolon
- `alias` creates your own command
- `unalias` removes an alias
- To see all the aliases defined in the environment, use the `alias` command without arguments
- Aliases vanish when your shell session ends

## 6: Redirection

### Standard Input, Output, and Error
- Programs send their results to a special file called _standard output_ (_stdout_) and their status messages to another file called _standard error_ (_stderr_)
- By default, both stdout and stderr are linked to the screen and not saved into a disk file
- Many programs take input from a facility called _standard input_ (_stdin_), which is, by default, attached to the keyboard
- I/O redirection allows us to change where output goes and where input comes from

### Redirecting Standard Output
- I/O redirection allows us to redefine where standard output goes
- To redirect stdout we use the `>` redirection operator followed by the name of the file
- When we redirect output with the `>` redirection operator, the destination file is always rewritten from the beginning
- Using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file
- We use the `>>` redirection operator to append redirected output to a file instead of overwriting the file
- If the file does not already exist, it is created just as though the `>` operator had been used

### Redirecting Standard Error
- Redirecting stderr lacks the ease of using a dedicated redirection operator
- To redirect stderr we must refer to its _file descriptor_
- A program can produce output on any of several numbered file streams
- The shell references stdin, stdout, and stderr as file descriptors 0, 1, and 2, respectively
- The shell provides a notation for redirecting files using the file descriptor number:

```
[me@linuxbox ~]$ ls -l /bin/usr 2> ls-error.txt
```

### Redirecting Standard Output and Standard Error to One File
- We may wish to capture all of the output of a command to a single file
- We must redirect both stdout and stderr at the same time
- Recent versions of bash provide a streamlined method for performing this combined redirection:

```
[me@linuxbox ~]$ ls -l /bin/usr &> ls-output.txt
```

### Disposing of Unwanted Output
- Sometimes we don't want output from a command
- Throw it away by redirecting output to `/dev/null`, a device file called a _bit bucket_, which accepts input and does nothing with it
- To suppress error messages from a command:

```
[me@linuxbox ~]$ ls -l /bin/usr 2> /dev/null
```

### Redirecting Standard Input
- `cat` reads one or more files and copies them to standard output
- You can use it to display files without paging

```
[me@linuxbox ~]$ cat movie.mpeg.0* > movie.mpeg
```

- Since wildcards always expand in sorted order, the arguments will be arranged in the correct order
- What happens if we enter `cat` with no arguments? `cat` copies stdin to stdout, so we see our line repeated
- We can use this to create short text files:

```
[me@linuxbox ~]$ cat > foo.txt
The quick brown fox jumped over the lazy dog.
```

- Using the `<` redirection operator, we change the source of stdin from the keyboard to the file foo.txt

### Pipelines
- The ability of commands to read data from stdin and send to stdout is used by a shell feature called _pipelines_
- Using the pipe operator `|`, stdout of one command can be _piped_ into stdin of another

```
[me@linuxbox ~]$ ls -l /usr/bin | less
```

> This is the Unix philosophy: Write programs that do one thing and do it well.
> Write programs to work together.
> Write programs to handle text streams, because that is a universal interface.
> -Doug McIlroy

### Filters
- Pipelines are often used to perform complex operations on data
- Commands used this way are referred to as _filters_
- Filters take input, change it somehow, and then output it
- `sort` displays a sorted list
- `uniq` accepts a sorted list of data from either stdin or a single filename argument and, by default, removes any duplicates from the list
- `wc` displays the number of lines, words, and bytes contained in files
- `grep` finds text patterns within files
- `head` prints the first 10 lines of a file
- `tail` prints the last 10 lines
- `tail` allows you to view files in real time. This is useful for watching the progress of log files as they are being written
- `tee` reads stdin and copies it to both stdout and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing

```
[me@linuxbox ~]$ ls /usr/bin | tee ls.txt | grep zip
```

### Redirection Takeaways
- `>` redirect stdout to a file (will overwrite the contents of the file)
- `>>` redirect stdout to a file (will append to the contents of the file)
- `<` redirect to stdin
- `2>` redirect stdout to a file
- `2> /dev/null` redirect stderr to /dev/null (throw away the output)
- `&>` redirect to stdout and stderr at the same time
- `|` pass the stdout of one command to the stdin of another command

## 7: Seeing the World as the Shell Sees It

### Expansion
- Each time you type a command line and press the Enter key, bash performs several processes upon the text before it carries out your command
- The process is called _expansion_. With expansion, you enter something, and it is expanded into something else before the shell acts upon it
- `echo` prints its text arguments on stdout

```
[me@linuxbox ~]$ echo *
```

### Pathname Expansion
- The mechanism by which wildcards work is called _pathname expansion_
- An expansion such as `echo *` does not reveal hidden files

### Tilde Expansion
```
[me@linuxbox ~]$ echo ~
[me@linuxbox ~]$ echo ~+
[me@linuxbox ~]$ echo ~-
```

### Arithmetic Expansion
- Arithmetic Expansion allows us to use the shell prompt as a calculator:

```
[me@linuxbox ~]$ echo $((2 + 2))
```

- Arithmetic expansion supports only integers

### Brace Expansion
- With _brace expansion_, you can create multiple text strings from a pattern containing braces:

```
[me@linuxbox ~]$ echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back
[me@linuxbox ~]$ echo Number_{1..5}
Number_1 Number_2 Number_3 Number_4 Number_5
[me@linuxbox ~]$ echo {Z..A}
Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
[me@linuxbox ~]$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

### Parameter Expansion

```
[me@linuxbox ~]$ echo $USER
```

### Command Substitution

- Allows us to use the output of a command as an expansion

```
[me@linuxbox ~]$ echo $(ls)
```

- There is an alternative syntax for command substitution that uses back quotes:

```
[me@linuxbox ~]$ echo `ls`
```

### Quoting
- _Word splitting_ by the shell removes extra whitespace
- By default, word splitting looks for the presence of spaces, tabs, and newlines and treats them as _delimiters_ between words
- The shell provides a mechanism called _quoting_ to selectively suppress unwanted expansions

### Double Quotes
- If you place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters
- The exceptions are dollar sign, backslash, and back tick
- This means that word splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter exapnsion, arithmetic expansion, and command substitution are still carried out

### Single Quotes
- If we need to suppress all expansions, we use _single quotes_

### Escaping Characters
- To quote only a single character, we can precede a character with a backslash, called the _escape character_
- Often this is done inside double quotes to selectively prevent an expansion

## 8: PERMISSIONS

- Unix-like operating system differ from MS-DOS systems in that they are not only _multitasking_ systems but also _multiuser_ systems
- This means that more than one person can use the computer at the same time

### Owners, Group Members, and Everybody Else
- In the Unix security model, a user may _own_ files and directories such that the user has control over its access
- Users can belong to a _group_ consisting of one or more users who are given access to files and directories by their owners
- An owner may also grant some set of access right to everybody, which in Unix terms is referred to as the _world_
- `id` displays information about your identity

### Reading, Writing, and Executing
- Access rights to files and directories are defined in terms of read access, write access, and execution access

```
[me@linuxbox ~]$ > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
```

- The first 10 characters are the _file attributes_
- The first of these characters is the _file type_
- The remaining nine characters of the file attributes, called the _file mode_, represent the read, write, and execute permissions for the file's owner, the file's group owner, and everybody else
- `chmod` changes the mode (permissions) of a file or directory
- Only the file's owner or the superuser can change the mode of a file or directory
- `chmod` supports two distinct ways of specifying mode changes: octal number representation and symbolic representation

### Changing Identities
- There are three ways to take on an alternate identity:
  - Log out and log back in as the alternate user
  - Use the `su` command
  - Use the `sudo` command
- `su` allows you to assume the identity of another user and either start a new shell session with that user's ID or issue a single command as that user
- `sudo` allows an administrator to set up a configuration file called `/etc/sudoers` and define specific commands that particular users are permitted to execute under an assumed identity
- The choice of which command to use is largely determined by which Linux distribution you use
- `chown` changes the owner and group owner of a file or directory. Superuser privileges are required to use this command

### Changing Your Password
- `passwd` sets or changes a password

### Permission Takeaways
- `-rwxrwxrwx`
- `r` = 4
- `w` = 2
- `x` = 1

- So 777 would be `rwxrwxrwx`
- 741 would be `rwxr----x`
- Add each set of in the set of 3 to get each number
- `rwx` would be 4+2+1 = 7
- `r-x` would be 4+1 = 5

## 9: PROCESSES

- Modern operating systems are usually _multitasking_, meaning that they create the illusion of doing more than one thing at once by rapidly switching from one executing program to another
- The Linux kernel manages this through the use of _processes_
- Here are some tools to examine what programs are doing and how to terminate processes

### How a Process Works
- When a system starts up, the kernel initiates a few of its own activities as processes and launches a program called init
- init runs a series of shell scripts (located in `/etc`) called _init scripts_, which start all the system services
- Many of these services are implemented as _daemon programs_, programs that just sit in the background
- Programs launching other programs is expressed in the process scheme as a _parent process_ producing a _child process_

> If the user types `date`, the shell creates a child process and runs the `date` program as the child.
> While the child process is running, the shell waits for it to terminate
> -Modern Operating Systems

- The kernel maintains information about each process
- For example, each process is assigned a _process ID_ (_PID_), assigned in ascending order, with init always getting PID 1
- Like files, processes also have owners and user IDs, effective user IDs, etc.

> Processes in UNIX have their memory divided up into three segments: the **text segment** (i.e., the program code), the **data segment** (i.e., the variables), and the **stack segment**.
> The data segment grows upward and the stack grows downward.
> Between them is a gap of unused address space.
> The stack grows into the gap automatically, as needed, but expansion of the data segment is done explicitly by using a system call, `brk`, which specifies the new address where the data segment is to end.
> The text segment is normally immutable, not changing during execution.
> The data segment starts out at a certain size and initialized with certain values, but it can change and grow as need be.
> The stack is initially empty but grows and shrinks as functions are called and returned from.
> Often the text segment is placed near the bottom of memory, the data segment just above it, with the ability to grow upward, and the stack segment at a high virtual address, with the ability to grow downward, but different systems work differently.
> -Modern Operating Systems

### Viewing Processes with ps
- `ps` is the most commonly used command to view processes
- TTY is short for _teletype_ and refers to the _controlling terminal_ for the process

```
[me@linuxbox ~]$ ps x
```

- STAT is short for _state_ and reveals the current status of the process
- See Table 10-1: Process States

### Viewing Processes Dynamically with top
- `top` displays a continuously updating (by default, every three seconds) display of the system processes listed in order of process activity
- The `top` display consists of two parts: a system summary at the top of the display, followed by a table of processes sorted by CPU activity

## Controlling Processes

### Interrupting a Process
- In a terminal, pressing CTRL-c _interrupts_ a program

### Putting a Process in the Background
- Let's say we wanted to get the shell prompt back without terminating the program
- Place the program in the _background_
- Think of the terminal as having a _foreground_ (with stuff visible on the surface, like the shell prompt) and a background (with hidden stuff below the surface)
- To launch a program so that it is immediately placed in the background, follow the command with `&`

```
[me@linuxbox ~]$ vi &
[1] 555
[me@linuxbox ~]$ ps
PID TTY   TIME      CMD
407 pts/2 00:00:00  bash
555 pts/2 00:00:00  vi
558 pts/2 00:00:00  ps
[me@linuxbox ~]$ jobs
[1]+  Stopped       vi
```

- The message `[1] 555` is part of a shell feature called _job control_
- We have started job number 1 that has PID 555
- We can see our process if we run `ps`
- `jobs` gives us a way to list the jobs that have been launched from our terminal

### Returning a Process to the Foreground
- A process in the background is immune from keyboard input, including any attempt to interrupt it with a CTRL-c
- To return a process to the foreground, use the `fg` command followed by a percent sign and the job number (called a _jobspec_)

```
[me@linuxbox ~]$ fg %1
vi
```

- If we have only one background job, the jobspec is optional

### Stopping (Pausing) a Process
- Sometimes we'll want to stop a process without terminating it
- To stop a foreground process, type CTRL-z

### Signals
- See Table 10-4: Common Signals
- Processes, like files, have owners, and you must be the owner of a process (or the superuser) to send it signals will `kill`
- A complete list of signals can be seen with `kill -l`
- `killall` sends signals to multiple processes matching a specified program or username
