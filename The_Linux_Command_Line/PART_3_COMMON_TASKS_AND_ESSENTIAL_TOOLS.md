# Part 3: Command Tasks and Essential Tools

## 1: Package Management
- The most important determinant of distribution quality is the _packaging system_ and the vitality of the distribution's support community
- _Package management_ is a method of installing and maintaining software on the system
- Today, most people can satisfy all of their software needs by installing _packages_ from their Linux distributor

### Packaging Systems

- Most distributions fall into one of two camps of packaging technologies: the Debian _.deb_ camp and the Red Hat _.rpm_ camp
- There are some important exceptions, such as Gentoo, Slackware, and Foresight



### Final Note
- In the chapters that follow, we will explore many programs covering a wide range of application areas
- While most of these programs are commonly installed by default, sometimes we may need to install additional packages

### Package Management Must Knows 
- `apt install {package-name}` to install a package
- `apt-cache search {package-name}` to search for a package
- `apt remove {package-name}` to delete a package
- `apt --purge remove {package-name}` to remove package and config files
- `apt update` updates the system
- `apt upgrade` upgrades the system

- `dpkg -l` to list all installed packages
- Good cheatsheet (https://www.cyberciti.biz/tips/linux-debian-package-management-cheat-sheet.html)

## 2: Storage Media

### Mounting and Unmounting Storage Devices
- The first step in managing a storage device is attaching the device to the filesystem tree
- This process, called _mounting_, allows the device to participate with the operating system

### Viewing a List of Mounted Filesystems
- `mount` mounts filesystems. Entering the command without arguments will display a list of the filesystems currently mounted

```
[me@linuxbox ~]$ mount
```

- The format of the listing is _device_ on _mount_point_ type _filesystem_type (options)_
- Note that audio CDs do not contain filesystems and thus cannot be mounted in the usual sense
- A _mount point_ is simply a directory somewhere on the filesystem tree. Nothing special about it. It doesn't even have to be an empty directory
- Unmounting a device entails writing all the remaining data to the device so that it can be safely removed

## 3: Networking

### Examining and Monitoring a Network
- The most basic network command is `ping` which sends a special network packet called an IMCP ECHO_REQUEST to a specified host
- `traceroute` displays a listing of all the "hops" network traffic takes to get from the local system to a specified host
- `netstat` is used to examine various network settings and statistics

### Transporting Files over a Network
- Most, if not all, web browsers support the _File Transfer Protocol_, and you often see URIs starting with the protocol _ftp://_
- `ftp` is used to communicate with _FTP servers_, machines that contain files that can be uploaded and downloaded over a network
- FTP (in its original form) is not secure, because it sends account names and passwords in _cleartext_
- Because of this, almost all FTP done over the Internet is done by _anonymous FTP servers_
- `wget` is useful for downloading content from both web and FTP sites

### Secure Communication with Remote Hosts
- SSH (Secure Shell) solves the two basic problems of secure communication with a remote host
  - It authenticates that the remote host is who it says it is
  - It encrypts all of the communications between the local and remote hosts
- SSH consists of two parts. An SSH server runs on the remote host, listening for incoming connections on port 22, while an SSH client is used on the local system to communicate with the remote system
- If the remote host does not successfully authenticate and after determining that the message is due to a benign cause, it is safe to correct the problem on the client side
- Use `vi` to remove the obsolete key from the `~/.ssh/known_hosts` file
- Besides opening a shell session on a remote system, `ssh` also allows us to execute a single command on a remote system:

```
[me@linuxbox ~]$ ssh remote-sys free
...
[me@linuxbox ~]$ ssh remote-sys 'ls *' > dirlist.txt
...
```

- TUNNELING WITH SSH - _encrypted tunnel_ (see p. 185)
- `scp` securely transfers files:

```
[me@linuxbox ~]$ scp remote-sys:document.txt .
```

- `sftp` is a secure replacement for `ftp`
- `sftp` does not require an FTP server to be running on the remote host. It requires only the SSH server
- This means that any remote machine that can connect with the SSH client can also be used as a FTP-like server

## 4: SEARCHING FOR FILES

### locate&mdash;Find Files the Easy Way

- `locate` performs a rapid database search of pathnames and then outputs every name that matches a given substring

### find&mdash;Find Files the Hard Way

- While `locate` can find a file based solely on its name, `find` searches a given directory (and its subdirectories) for files based on a variety of attributes:

```
[me@linuxbox ~]$ find ~
```

- The beauty of `find` is that it can be used to identify files that meet specific criteria
- It does this through the (slightly strange) application of _tests_, _actions_, and _options_

### Tests
```
[me@linuxbox ~]$ find ~ -type d | wc -l
```
- Adding the test `-type d` limited the search to directories
- See Table 17-1: find File Types
- See Table 17-2: find Size Units
- See Table 17-3: find Tests
- `find` provides a way to combine tests using _logical operators_
- See Table 17-4: find Logical Operators

### Actions
- Having a list of results is useful, but we want to act on the items on the list
- See Table 17-6: Predefined find Actions
- We can also invoke arbitrary commands with the `-exec` action
- When the `-exec` action is used, it launches a new instance of the specified command each time a matching file is found
- We might prefer to combine all search results and launch a single instance of the command:
  - By changing the trailing semicolon to a plus sign, we activate the ability of `find` to combine search results into an argument list for a single execution
  - We can also use `xargs` to get the same result:

```
[me@linuxbox ~]$ find ~ -type f -name 'foo*' -print | xargs ls -l
```

- DEALING WITH FUNNY FILENAMES
- `touch` is usually used to set or update the modification times of files, or create empty files
- Note that unlike `ls`, `find` does not produce results in sorted order. Its order is determined by the layout of the storage device
- `stat` is a kind of suped-up version of `ls` and reveals all the system understands about a file and its attributes

### Options
- Options are used to control the scope of a `find` search

## 5: ARCHIVING AND BACKUP

### Compressing Files
- `gzip` compresses one or more files
- `bzip2` is similar to `gzip` but uses a different compression algorithm, which achieves higher levels of compression at the cost of compression speed

### Archiving Files
- _Archiving_ is the process of gathering up many files and bundling them into a single large file
- `tar` is the classic tool for archiving files
- See Table 18-2: tar Modes

```
[me@linuxbox ~]$ ssh remote-sys 'tar cf - Documents' | tar xf -
```

- `zip` is both a compression tool and an archiver
- In Linux, `gzip` is the predominant compression program with `bzip2` being a close second
- Linux users mainly use `zip` for exchanging files with Windows systems

### Synchronizing Files and Directories
- `rsync` can synchronize both local and remote directories by using the _rsync remote-update protocol_, which allows `rsync` to quickly detect the differences between two directories and perform the minimum amount of copying required to bring them into sync


## 6: Regular Expressions

> I define UNIX as _30 definitions of regular expressions living under one roof_.
> -Donald Knuth

### What Are Regular Expressions?

- _Regular expressions_ are symbolic notations used to identify patterns in text
- [regex101: build, test, and debug regex](https://regex101.com/)

### grep&mdash;Search Through Text
- `grep` (_global regular expression print_) is the main program we will use to work with regular expressions
- `grep` searches text files for the occurrence of a specified regular expression and outputs any line containing a match to stdout

### Metacharacters and Literals
- Regular expression metacharacters consist of the following: `^` `$` `.` `[` `]` `-` `?` `*` `+` `(` `)` `|` `\`

### The Any Character
- `.`

### Anchors
- `^` and `$` cause the match to occur only if the regex is found at the beginning of the line or at the end of the line
- Note that `^$` will match blank lines

### Bracket Expressions and Character Classes
- There are two cases in which metacharacters are used within bracket expressions and have different meanings: `^` and `-`
  - `^` loses its special meaning and becomes an ordinary character in the set
  - How do we actually include a dash character in a bracket expression? By making it the first character in the expression

### POSIX Basic vs. Extended Regular Expressions

- POSIX splits regular expression implementations into two kinds: _basic regular expressions (BRE)_ and _extended regular expressions (ERE)_
  - With BRE, the following metacharacters are recognized: `^` `$` `.` `[` `]` `*`
  - With ERE, the following metacharacters (and their associated functions) are added: `(` `)` `{` `}` `?` `+` `|`
- However, the characters `(` `)` `{` `}` are treated as metacharacters in BRE _if_ they are escaped with a backslash
- With ERE, preceding any metacharacter with a backslash causes it to be treated as a literal
- Both `egrep` and `grep -E` support ERE
- POSIX - _the Balkanization_ (see p. 225)

### Alternation
- _Alternation_ is an ERE feature that allows a match to occur from among a set of expressions

```
[me@linuxbox]$ echo "DDD" | grep -E 'AAA|BBB|CCC'
```

- To combine alternation with other regular-expression elements, we can use () to separate the alternation:

```
[me@linuxbox]$ grep -Eh '^(bz|gz|zip)' dirlist*.txt
```

### Quantifiers
- EREs support several ways to specify the number of times an element is matched

### ?&mdash;Match an Element Zero Times or One Time
- This quantifier means, in effect, "Make the preceding element optional"

### \*&mdash;Match an Element Zero or More Times
- Like the `?` metacharacter, the `*` is used to denote an optional item; however, unlike the `?`, the item may occur any number of times, not just once

### +&mdash;Match an Element One or More Times
- The `+` metacharacter works much like the `*`, except it requires at least one instance of the preceding element to cause a match

### {}&mdash;Match an Element a Specific Number of Times
- The `{` and `}` metacharacters are used to express minimum and maximum numbers of required matches

### Final Note
- We can search the compressed Section 1 man page files:

```
[me@linuxbox]$ cd /usr/share/man/man1
[me@linuxbox man1]$ zgrep -El 'regex|regular expression' *.gz
```

- `zgrep` provides a frontend for `grep`, allowing it to read compressed files

## 7: Text Processing

## Slicing and Dicing

### cut&mdash;Remove Sections from Each Line of Files
- `cut` is used to extract a section of text from a line and output the extracted section to stdout
- The way `cut` extracts text is rather inflexible
- `cut` is best used to extract text from files that are produced by other programs

### paste&mdash;Merge Lines of Files
- `paste` does the opposite of `cut`. Rather than extracting a column of text from a file, it adds one or more columns of text to a file

### join&mdash;Join Lines of Two Files on a Common Field
- `join` joins data from multiple files based on a shared key field

## Comparing Text

### comm&mdash;Compare Two Sorted Files Line by Line
- `comm` compares two text files, displaying the lines that are unique to each one and the lines they have in common

### diff&mdash;Compare Files Line by Line
- `diff` detects the differences between files

### patch&mdash;Apply a diff to an Original
- `patch` applies changes to text files
- It accepts output from `diff` and is generally used to convert older version of files into newer versions

## Editing on the Fly

### tr&mdash;Transliterate or Delete Characters
- `tr` _transliterates_ characters. Transliteration is the process of changing characters from one alphabet to another

### sed&mdash;Stream Editor for Filtering and Transforming Text
- `sed` (_stream editor_) performs text editing on a stream of text, either a set of files or stdin
- Most commands in `sed` may be preceded by an _address_, which specifies which line(s) of the input stream will be edited
- If the address is omitted, then the editing command is carried out on every line in the input stream

### aspell&mdash;Interactive Spell Checker
- `aspell` is an interactive spellchecker

## 8: FORMATTING OUTPUT

## Simple Formatting Tools

### nl&mdash;Number Lines
- `nl` is a rather arcane tool that numbers lines. In its simplest use, it resembles `cat -n`
- `nl` supports a concept called _logical pages_ when numbering. This allows `nl` to reset (start over) the numerical sequence when numbering

### fold&mdash;Wrap Each Line to a Specified Length
- _Folding_ is the process of breaking lines of text at a specified width

### fmt&mdash;A Simple Text Formatter
- `fmt` also folds text, plus a lot more

### pr&mdash;Format Text for Printing
- `pr` is used to paginate text
