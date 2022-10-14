# Part 2: Configuration and the Environment

## 1: THE ENVIRONMENT

- The shell maintains a body of information during our shell session called the _environment_
- While, most programs use _configuration files_ to store program settings, some programs will also look for values stored in the environment to adjust their behavior

### What Is Stored in the Environment?
- The shell stores two basic types of data in the environment, although, with bash, the types are largely indistinguishable
- They are _environment variables_ and _shell variables_
- Shell variables are bits of data placed there by bash, and environment variables are basically everything else
- In addition to variables, the shell also stores some programmatic data, namely _aliases_ and _shell functions_

### Examining the Environment
- `set` shows both the shell and environment variables as well as any defined shell functions
- `printenv` only displays environment variables
- One element of the environment that neither `set` nor `printenv` displays is aliases
- `alias` without arguments displays aliases


## How Is the Environment Established?
- When we log on to the system, the bash program starts and reads a series of configuration scripts called _startup files_, which define the default environment shared by all users
- This is followed by more startup files in our home directory that define our personal environment
- The exact sequence depends on the type of shell session being started

### Login and Non-login Shells
- There are two kinds of shell sessions: a login shell session and a non-login shell session
- A _login shell session_ is one in which we are prompted for our username and password
- A _non-login shell session_ typically occurs when we launch a terminal session in the GUI
  - Login shells read one or more startup files: `/etc/profile`, `~/.bash_profile`, `~/.bash_login`, and `~/.profile`
  - Non-login shell sessions read the startup files: `/etc/bash.bashrc` and `~/.bashrc`
  - In addition tor reading the startup files above, non-login shells inherit the environment from their parent process, usually a login shell
- The `~/.bashrc` file is probably the most important startup file from the ordinary user's point of view, since it is almost always read

## Modifying the Environment

### Which Files Should We Modify?
- To add directories to your PATH or define additional environment variables, place those changes in `.bash_profile` (or equivalent, according to your distribution&mdash;for example, Ubuntu uses `.profile`)
- For everything else, place the changes in `.bashrc`

### Activating Our Changes
- The changes we have made to our `.bashrc` will not take effect until we close our terminal session and start a new one, because the `.bashrc` file is only read at the beginning of a session
- We can force bash to reread the modified `.bashrc` file with the following command:

```
[me@linuxbox ~]$ source .bashrc
```

## 2: CUSTOMIZING THE PROMPT
- Like so many things in Linux, the shell prompt is highly configurable

### Anatomy of a Prompt
- Our default prompt looks something like this:

```
[me@linuxbox ~]$
```

- Notice that it contains our username, our hostname, and our current working directory
- The prompt is defined by an environment variable named `PS1` (short for _prompt string 1_)

### Trying Some Alternative Prompt Designs
- Let's add a bell to our prompt:

```
$ PS1="\a\$ "
```

- Now we should hear a beep each time the prompt is displayed
- This could get annoying, but it might be useful if we needed notification when an especially long-running command has been executed
- Next, let's try to make an informative prompt with some hostname and time-of-day information:

```
$ PS1="\A \h \$ "
17:33 linuxbox $
```

- Adding time-of-day to our prompt will be useful if we need to keep track of when we perform certain tasks
