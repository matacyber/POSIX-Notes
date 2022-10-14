# The Linux Command Line Tables

## Table 9-1: File Types

|Attribute | File type|
|---|----|
|`-` | A regular file.|
|d | A directory.|
|l | A symbolic link. Notice that with symbolic links, the remaining file attributes are always `rwxrwxrwx` and are dummy values. The real file attributes are those of the file the symbolic link points to.|
|c | A character special file. This file type refers to a device that handles data as a stream of bytes, such as a terminal or /dev/null.|
|b | A block special file. This file type refers to a device that handles data in blocks, such as a hard drive or DVD drive.|

## Table 9-2: Permission Attributes

|Attribute | Files | Directories| 
|---|----|----|
|r | Allows a file to be opened and read. | Allows a directory’s contents to be listed if the execute attribute is also set.|
|w | Allows a file to be written to or truncated; however, this attribute does not allow files to be renamed or deleted. The ability to delete or rename files is determined by directory attributes. | Allows files within a directory to be created, deleted, and renamed if the execute attribute is also set.|
|x | Allows a file to be treated as a program and executed. Program files written in scripting languages must also be set as readable to be executed. | Allows a directory to be entered, e.g., cd directory.|


## Table 10-1: Process States

|State | Meaning|
|---|----|
|R | Running. This means the process is running or ready to run.|
|S | Sleeping. The process is not running; rather, it is waiting for an event, such as a keystroke or network packet.|
|D | Uninterruptible sleep. The process is waiting for I/O such as a disk drive.|
|T | Stopped. The process has been instructed to stop. You’ll learn more about this later in the chapter.|
|Z | A defunct or “zombie” process. This is a child process that has terminated but has not been cleaned up by its parent.|
|< | A high-priority process. It’s possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. A process with high priority is said to be less nice because it’s taking more of the CPU’s time, which leaves less for everybody else.|
|N | A low-priority process. A process with low priority (a nice process) will get processor time only after other processes with higher priority have been serviced.|

## Table 10-4: Common Signals

|Number | Name | Meaning|
|---|---|----|
|1 | HUP | Hang up. This is a vestige of the good old days when terminals were attached to remote computers with phone lines and modems. The signal is used to indicate to programs that the controlling terminal has “hung up.” The effect of this signal can be demonstrated by closing a terminal session. The foreground program running on the terminal will be sent the signal and will terminate. This signal is also used by many daemon programs to cause a reinitialization. This means that when a daemon is sent this signal, it will restart and reread its configuration file. The Apache web server is an example of a daemon that uses the HUP signal in this way.|
|2 | INT | Interrupt. This performs the same function as CTRL-C sent from the terminal. It will usually terminate a program.|
|9 | KILL | Kill. This signal is special. Whereas programs may choose to handle signals sent to them in different ways, including ignoring them all together, the KILL signal is never actually sent to the target program. Rather, the kernel immediately terminates the process. When a process is terminated in this manner, it is given no opportunity to “clean up” after itself or save its work. For this reason, the KILL signal should be used only as a last resort when other termination signals fail.|
|15 | TERM | Terminate. This is the default signal sent by the kill command. If a program is still “alive” enough to receive signals, it will terminate.|
|18 | CONT | Continue. This will restore a process after a STOP or TSTP signal. This signal is sent by the bg and fg commands.|
|19 | STOP | Stop. This signal causes a process to pause without terminating. Like the KILL signal, it is not sent to the target process, and thus it cannot be ignored.|
|20 | TSTP | Terminal stop. This is the signal sent by the terminal when CTRL-Z is pressed. Unlike the STOP signal, the TSTP signal is received by the program, but the program may choose to ignore it.|

## Table 10-5: Other Common Signals

|Number | Name | Meaning|
|---|----|----|
|3 | QUIT | Quit.|
|11 | SEGV | Segmentation violation. This signal is sent if a program makes illegal use of memory; that is, if it tried to write somewhere it was not allowed to write.|
|28 | WINCH | Window change. This is the signal sent by the system when a window changes size. Some programs, such as top and less, will respond to this signal by redrawing themselves to fit the new window dimensions.|

## Table 11-1: Enviroment Variables

|Variable | Contents|
|---|----|
|DISPLAY | The name of your display if you are running a graphical environment. Usually this is :0, meaning the first display generated by the X server.|
|EDITOR | The name of the program to be used for text editing.|
|SHELL | The name of your shell program.|
|HOME | The pathname of your home directory.|
|LANG | Defines the character set and collation order of your language.|
|OLDPWD | The previous working directory.|
|PAGER | The name of the program to be used for paging output. This is often set to /usr/bin/less.|
|PATH | A colon-separated list of directories that are searched when you enter the name of a executable program.|
|PS1 | Stands for “prompt string 1.“ This defines the contents of the shell prompt. As we will later see, this can be extensively customized.|
|PWD | The current working directory.|
|TERM | The name of your terminal type. Unix-like systems support many terminal protocols; this variable sets the protocol to be used with your terminal emulator.|
|TZ | Specifies your time zone. Most Unix-like systems maintain the computer’s internal clock in Coordinated Universal Time (UTC) and then display the local time by applying an offset specified by this variable.|
|USER | Your username.|

## Table 11-2: Startup Files for Login Shell Sessions

|File | Contents | 
|---|-----|
|/etc/profile | A global configuration script that applies to all users.| 
|~/.bash_profile | A user’s personal startup file. It can be used to extend or override settings in the global configuration script.|
|~/.bash_login | If ~/.bash_profile is not found, bash attempts to read this script.|
|~/.profile | If neither ~/.bash_profile nor ~/.bash_login is found, bash attempts to read this file. This is the default in Debian-based distributions, such as Ubuntu.|

## Table 11-3: Startup File for Non-Login Shell Sessions

|File | Contents|
|---|----|
|/etc/bash.bashrc | A global configuration script that applies to all users.|
|~/.bashrc | A user’s personal startup file. It can be used to extend or override settings in the global configuration script.|
