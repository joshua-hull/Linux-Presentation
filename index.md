# Clemson ACM Linux Workshop

!SLIDE
# Linux 101
### Brought to you by Clemson ACM
We're on [Steam](http://steamcommunity.com/groups/clemsonacm) & [Facebook](https://www.facebook.com/groups/283823058297107/)!
### Speakers:
Joshua Hull - Chief Presenter  
Austin Anderson - ACM President

!SLIDE left
# Coming up
1. What's up with Linux?
2. The linux file system
3. Terminal Power
4. Getting owned by Permissions
8. Working from Other Machines
6. Your free webhosting at people.cs.clemson.edu
7. Wrap-up

!SLIDE bottom-left
# What's up with Linux?
}}} images/Tux-simple.svg

!SLIDE left
# Linux: A Short History
- Created in 1991 by __Linus Torvalds__
- Written in C and Assembly
- Uses a _Unix-like_ file structure (more on that later)
- Kernel is still being maintained by Torvalds & open source contributors
- You could contribute if you wanted!

!SLIDE left
# What's a Distribution?
- A "flavor" of Linux with small differences from the others
- __All__ have many similarities
- Might differ in...
    -  _Desktop Environment_, the set of programs that handle... the desktop
        -  Examples are __Gnome__ and __KDE__
    -  _Package manager_
    -  Default _applications_
    -  Behind-the-scenes _settings_
-  Some common distributions are Ubuntu (and children Xubuntu, Kubuntu), Fedora, Debian, and Arch Linux (not for the faint of heart) -- you configure _everything_

!SLIDE left
# Big Names in *nix
* __Linus Torvalds__ - creator of Linux, _extremely passionate_.
* GNU Project - "GNU's Not Unix", connected to open source software licensing (like the GNU Public License, or GPL)
* Greg Kroah-Hartman: Linux Kernel maintainer and all around awesome dude.

!SLIDE left
# "Kernel" and Other Scary Words
- __Kernel__ is the part of Linux that interacts with your PC's hardware.
- __Shell__ refers to the program that handles your terminal environment with things like the _prompt_ and coloring.
- __Bash__ is the default shell.
- __Grub__ is a common Linux _boot manager_ that remembers how to get from turning your computer on into the OS.
- __PATH__ is an _environment variable_ that remembers where to look for executables when you type one in the terminal
- __Version control systems__ like __Git__, __SVN__, and __Mercurial__ allow you to easily implement histories of a project. Linux uses Git!
    - Web handin uses Mercurial as a backend and provides a tutorial for connecting to Handin on your machine
- __`make` and `Makefile`s__ are a _build system_ that allow you to define rules for running multiple commands at once. Very useful for compiling code.

!SLIDE left
# "Building from Source"
- When you can't get a pre-compiled executable
- Download the source code and run...
1. `./configure`
2. `make`
3. `sudo make install`
4. Didn't work? Read README

!SLIDE left
# Packaging systems
- Easy way to install many applications pre-configured for your OS
- Different distributions have their own __Package Managers__
    - All package managers need to be run using `sudo`
    - `apt-get` - used on Debian based system, including Ubuntu.
        - `apt-get update` - update metadata
        - `apt-cache search <package>` - find package
        - `apt-get install <package>` - install package
        - `apt-get dist-upgrade` - update all packages
    - `yum` - used on Red Hat based system, including Fedora
    - `pacman` - used on Arch Linux

!SLIDE bottom-left
# The Linux File System

!SLIDE left
# Basic Hierarchy
- Based on _one_ root directory, not drives like C: or D:
- Physical devices (drives, output) and important folders are _mounted_ to subdirectories of `/`
    - `/home` - where user's files normally live
    - `/dev` - device nodes. Don't mess with things here.
    - `/mnt` - where you can mount things like USB drives.
    - `/usr` - where system libraries and the like are.
    - `/bin` - stores system executables
## Some distros are a little different in how they manage these folders.

!SLIDE left
# Everything is a File
- Linux sees every object as a subclass of a file.
- Folders, links, output devices, executables are all "files"!

!SLIDE left
# Where are my .exes?
- File extensions categorize, not restrict
- A file with any name could be executed
    - `a.out`, `prog1`, `.bashrc`
- Files starting with a dot like `.bashrc` are usually _hidden_ from listings
- Running a command like `sl` is really just running an executable file within the PATH

!SLIDE bottom-left
# Terminal Power

!SLIDE left
# echo "Simple navigation commands"
- Stuck? `Ctrl+c` force quits the running program.
- `pwd` lists your current directory
- `cd directory` moves the terminal to `directory`
- `ls` lists files and folders in the current directory
    - `ls -l` gives additional file information
    - `ls -a` shows even `.hidden-files`

!SLIDE left
# echo "Simple navigation commands"
## THERE IS NO TRASHCAN. DELETION IS PERMANENT.
- `mv orig.file new.file` moves `orig.file` to `new.file`
    - Use this for moving and __renaming__!
- `cp orig.file clone.file` copies `orig.file` to `clone.file`
- `rm file` removes a file
    - `rm -r directory` deletes a directory


!SLIDE left
# --Flags?! : Command Structure
- Generally `command -one-letter-flag --longer-flag parameter [optional parameter] parameter-list...`
- Some flags need their own value arguments after them
    - `ping -c 12` OR `ping --count=12`
- Structure varies by program: try `progname --help` or `-h` for a guide simpler than `man progname`
- Many commands use `--verbose` or `-v` to print _more_ useful information. Verbosity is good!

!SLIDE left
# Terminal Symbols & Shorthand
- `.` (one dot) is the _current directory_
- `..` (two dots) is the _parent directory_
- `/` is the _root directory_
- `~` is your _user directory_
- `!!` is the _previously entered command_
    - Use `sudo !!` to run the last command under sudo

!SLIDE left
# Terminal Symbols & Shorthand
- `\` begins an escape character sequence
    - `\n` is a newline character
    - `\ ` (space) inserts a space into one argument (otherwise the argument will break)
    - `\\` actually inserts a backslash
    - `$(command)` or ``command`` inserts the output of `command` into 
    - `command&` will run `command` in the background

!SLIDE left
# Messing with Output
- Any text output you see in the terminal comes from __standard out__ (the same stream as __cout__ in C++ and __printf()__ in C)
    - `echo input` - print `input` to standard out
    - `cat input.file` - print contents of `file` to the terminal
- Many commands like `grep` and `less` read from __standard in__ (__cin__ in C++, what __scanf()__ reads from in C) if no other args are specified
    - `grep pattern input.file` prints lines from `input.file` that match/contain the search pattern (could be as simple as one word)
    - `less input.file` allows you to read up and down through a large chunk of data

!SLIDE left
# Piping and Redirection
- __Piping__ with `command-a | command-b` connects the _standard output_ of `command-a` to _standard input_ of `command-b`, for chaining commands
    - `command-a | less` pipes `command-a`'s output into less for easy reading
- __Redirection__ handles using file contents for standard in / out
- `progname > output.file` overwrites `output.file` with `progname`'s output 
    - `>>` _appends to_ `output.file` with `progname`'s output 
    - `&>` overwrites `output.file` with `progname`'s _error output_ 
    - `&>>` _appends to_ `output.file` with `progname`'s _error output_ 
- `progname < input.file` uses `input.file`'s content as input for `progname`

!SLIDE left
# Shell History
##"How did I run that again?"
- Press the up key to cycle through your previously entered commands
- `history` - print previous commands
- Try it with grep -- `history | grep ls`

!SLIDE left
# Shell configuration
- On your home machine, you could replace __bash__ with another shell like __zsh__ or __ksh__
- Editing `~/.bashrc` can customize your shell with functions, __aliases__, and __functions__.
- Aliases are simple: `alias sl=echo "Steam Locomotive"`
- There are a ton of tutorials on customizing the shell, so we'll skip it for now.

!SLIDE left
# `man` and Other Awesome Commands
- `man` - summons an _extensive_ manual page for about anything
    - `man stdio.h`, `man grep`, `man man`
- `tar` - manage tarball (.tar) and tarball + gzipped (.tgz, .tar.gz) archives
    - `tar -xzf` (e__x__tract __z__e __f__iles!!) `<archive>`
        - `tar -xf` for just `.tar`
    - `tar -czf` (__c__reate __z__e __f__iles!!) `archivename.tgz files...` to create an archive
    - [Relevant XKCD comic](http://imgs.xkcd.com/comics/tar.png)
- `sl` summons a steam locomotive!
- `touch name.file` creates an empty `name.file` if none exists
- `nano [edit.file]` opens a simple editor
- `curl -O [URL]` copies a file from the web

!SLIDE left
# Shell Scripts
- put commands into a file to run them all at once repeatidly
- add `#!/bin/bash` as the first line
- one command per line
- `chmod u+x script.sh`
- `./script.sh`

!SLIDE bottom-left
# Getting Owned by Permissions

!SLIDE left
# Users, Root and Groups
- _Users_ are unique accounts
- _Root_ is the __superuser__ and can do _anything_.
    - __DON'T TRY TO USE ROOT ON THE CU MACHINES__.
    - Run one command as root with `sudo <command>` and temporarily login with `sudo su`
- Users in the same _Groups_ share permissions pertaining to that group
    - E.g. users in `sudoers` can use `sudo` (the admin group might be different on other distros)
    - Users can be in multiple groups
- `man chmod` and `man chgrp` for more info on permissions and groups

!SLIDE bottom-left
# Working from other machines

!SLIDE left
# Getting to your files with SSH
- `ssh username@access.cs.clemson.edu` starts a remote connection to the Lab computer
- Pick one of the servers listed in the message and `ssh` to it
- __DON'T RUN/COMPILE ON access.cs.clemson.edu__

!SLIDE left
# Using a VM
- VirtualBox
    - Can run a Linux VM inside of Windows/Mac OS X

!SLIDE left
# Windows: Cygwin?
## __Bad Idea.__

!SLIDE left
# Your Free Clemson Web Hosting
- Run `cd /web/home/username/public_html`
    - Trust us, it's there
- Files you put there will be served on the web at `people.cs.clemson.edu/~username/`
- Change permissions so the web server can access them
    - `chmod a+r [serving files]`
    - `chmod a+g [sub-directories]`

!SLIDE bottom-left
# Wrap-up

!SLIDE left
# Final warnings
## NEVER RUN A RANDOM COMMAND FROM THE INTERNET
- __DON'T CHEAT__
    - Professors use advanced software that checks the algorithms your code uses
    - Changing variable names won't help
- Don't use `sudo` on the lab machines
    - They yell at you and phone home to the sysadmins 
- Want to install something? Email `ithelp@clmeson.edu` and put `School of Computing` in the subject line.

!SLIDE left
# The snapshot system
- Contents are in `~/.snapshot`
- Keeps hourly, nightly, and weekly backups of files in `~`
- Especially useful when you accidentally overwrite a project at 2 am
## SNAPSHOTS ARE UNIQUE TO CLEMSON. DON'T RELY ON IT!

!SLIDE left
# Further resources
- `http://www.cs.clemson.edu/help/linux-workshop/soc_linux_cheatsheet.pdf` -- the cheatsheet we're distributing
- `http://www.cs.clemson.edu/help/linux-workshop`
    - Steps to install a VM just like the lab machines
    - submit/handin information is deprecated
- Plug a long command into [ExplainShell.com](http://explainshell.com/) to see what it does
- We're on [Steam](http://steamcommunity.com/groups/clemsonacm) & [Facebook](https://www.facebook.com/groups/283823058297107/)!
- Lists system admin staff

!SLIDE bottom-left
# Questions
Send us feedback at `acm@cs.clemson.edu`!
