---
title: The Shell 
description: The Shell
class: gaia
_class:
  - lead
  - invert
style: |
    img[alt~="center"] {
      display: block;
      margin: 0 auto;
    }
    #img-right{
      float: right;
    }
    table{
      font-size: 18 px;
    }
size: 16:9
paginate: true
_paginate: false
marp: true
math: true
---

# The Shell

    Module Code: COMP1712

    Module Name: Computer Architectures and Operating Systems

    Credits: 15

    Module Leader: Seb Blair BEng(H) PGCAP MIET MIHEEM FHEA
    
---

## What is a shell?

- User interface for running commands
- Interactive language
- Scripting language

---

## Shell Initialisation

The initialisation file sets up the “work environment” and “customizes” the shell environment for the user. The main agenda of Shell initialisation files are to persist common shell configuration, such as:

- `$PATH` and other environment variables
- shell prompt
  - `jovyan@jupyter-seb-20blair:~/AOS/Bash$ `
- shell tab-completion
- aliases, functions
  - `alias glg = "git log --graph --oneline --decorate --all"`
- key bindings
  - `bindsym $mod+d exec $menu`

---

## Shell modes

The shell can be run in three possible modes:

- Interactive login 
- Interactive non-login 
- Non-interactive 

---
## Operations for Different Shell Modes

- Login to a remote system via SSH : **Login**, **Interactive**
- User successfully login into the system, using `/bin/login`, after reading credentials stored in the `/etc/passwd` file: **Login**, **Interactive**
- Execute a script remotely and request a terminal, e.g. `ssh user@host -t ‘echo $PWD’` : **Non-Login**, **Interactive**
- Start a new shell process, e.g. `bash`: **Non‑Login**, **Interactive**
- Execute a script remotely, e.g. `ssh user@host ‘echo $PWD` : **Non‑Login**, **Non‑Interactive**
- Run a script, `bash myscript.sh`: **Non‑Login**, **Non‑Interactive**
- Run an executable with `#!/usr/bin/env bash` shebang : **Non‑Login**, **Non‑Interactive**
- Open a new graphical terminal window/tab: **Non‑Login**, **Interactive**

---

## Shell Initialisation Files

1. System-wide startup files
    - whole system irrespective of a specific user
    - `/etc/profile` for system-wide environment configurations and startup programs for login setup
    - `/etc/bashrc` or `/etc/bash.bashrc` file contains system-wide functions and aliases including other configurations that apply to all system users

---

## Shell Initialisation Files

2. User-specific startup files
   -  files which contain configuration which applied to the specific user
   -  `~/.bash_profile` file – Stores user-specific environment and startup programs configurations. 
   -  `~/.bashrc` file – Stores user-specific aliases and functions.
   -  `~/.bash_login` file – Contains specific configurations that are normally only executed when you log in to the system.
   -  `~/.bash_history` file – Bash maintains a history of commands that have been entered by a user on the system.
   -  `~/.bash_logout` file – it’s not used for shell startup, but stores user specific instructions for the logout procedure. It is read and executed when a user exits from an interactive login shell.
---

## Order of Activation:
![](https://blog2opstree.files.wordpress.com/2020/02/shell-initailizationfiles-1.png?w=1024)

---

## A Sea of Shells

- There are 27+ Shells... 
- Default is usaully Bash (**B**ourne **A**gain **Sh**ell) in Unix, powershell in Windows
- Others include:
  - sh (Bourne **Sh**ell)
  - ksh (**k**orn **sh**ell)
  - tcsh (**t**enex **c** **sh**ell)
  - zsh (**Z**hong Shao **Sh**ell)
  - fish 

```sh
$ printenv SHELL
/bin/bash
```

<!--
 - The “t” in tcsh comes from the “T” in TENEX, an operating system. A C shell with programmable CLI compeletion, CLI editing.
 - ksh is based on bourne shell(main difference is more c-like-language expressions)
 - Zsh is now shipped with Kali Linux as default shell (inventor named it after his teacher.)
-  Fish is considered an exotic shell since it does not rigorously adhere to POSIX shell standards, at the discretion of the maintainers.
-->

---

## Shell Command Applications

- Getting information
- Navigating and working with files and directories. 
- Printing file and string contents​. 
- File compression and archiving​. Performing network operations.
- Monitoring performance and status of the system, its components and applications. 
- Running batch jobs, such as **E**xtract **T**ransform **L**oad (ETL) operations

---

## Basic CLI Utilities Desgin

![center](https://www.maizure.org/projects/decoded-gnu-coreutils/general_cli_utility.png)

<!--innovaction-->

---


## Getting Information

- `whoami` – which returns the user's username
- `id` – which returns the current user and group IDs, 
- `uname` – returns the operating system name, 
- `ps` – displays running processes and their IDs, 
- `top` – displays running processes and resource usage including memory, CPU, and IO, 
- `df` – shows information about mounted file systems, 
- `man` – fetches the reference manual for any shell command,
- `date` – prints today's date.

---

## Working with Files

- `cp` – copy file, 
- `mv` – change file name or path,
- `rm` – remove file, 
- `touch` – create empty file, update file timestamp, 
- `chmod` – change/modify file permissions, 
- `wc` – get count of lines, words, characters in file, 
- `grep` – return lines in file matching pattern

---

## Navigating & Working with Directories

- `ls` – lists the files and directories in the current directory,
- `find` – used to find files matching a pattern in the current directory tree, 
- `pwd` – prints the current, or ‘present working,’ directory, 
- `mkdir` – makes a new directory, 
- `cd` – changes the current directory to another directory, 
- `rmdir` – removes an entire directory

---

## Printing File and String Contents

- `cat` – which prints the entire contents of a file, 
- `more` – used to print file contents one page at a time, 
- `head` – for printing just the first ‘N’ lines of a file, 
- `tail` – for printing the last ‘N’ lines of a file, 
- `echo` command – which 'echoes' an input string by printing it. It can also ‘echo’ the value of a variable.

---

## Compression and Archiving

 - `tar` – which is used to archive a set of files, 
 - `gzip`/`zip` – which compresses a set of files,
 - `gunzip`/`unzip` – which extracts files from a compressed or zipped archive

---

## Networking

`hostname` – prints the host name, 
`ping` – sends packets to a URL and prints the response, 
`ifconfig` – displays or configures network interfaces on the system, 
`curl` – displays the contents of a file located at a URL, and the wget command can be used to download a file from a URL.

---
## Coreutils

All of these commands and more that come shipped by default come from the [`coreutils`](https://www.gnu.org/software/coreutils/manual/coreutils.html)

![bg right:50% 100%](https://www.maizure.org/projects/decoded-gnu-coreutils/GNU.png)

