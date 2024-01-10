---
title: POSIX
description: POSIX ppt
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

# POSIX

    Module Code: COMP1712

    Module Name: Computer Architectures and Operating Systems

    Credits: 15

    Module Leader: Seb Blair BEng(H) PGCAP MIET MIHEEM FHEA

---

## Portable Operating System Interface (POSIX)

- POSIX (Portable Operating System Interface) is a set of standard operating system interfaces based on the Unix operating system
- [IEEE Std 1003.1-2017](https://standards.ieee.org/ieee/1003.1/7101/x)
  - defines a standard interface and environment that can be used by an operating system (OS) to provide access to POSIX-compliant application
- The standard also defines a command interpreter (**shell**) and common **utility** programs
- IEEE Std 1003.1 
  - application programming interface in the C language
- IEEE Std 1003.2
  - standard shell and utility interface for the OS

---

## Aliases  

- The Open Group
  - The Open Group Base Specifications Issue 7, 2018 edition, 

- ISO/IEC refer to it as ISO/IEC 9945:2009. 
  - ISO/IEC adopted the standard in 2009 and added Technical Corrigendum 1 in late 2012 and Technical Corrigendum 2 in March 2017, putting it on par with IEEE Std 1003.1-2017.

---

## POSIX.1  Sections

- **Base definitions**: Provides common definitions for the specifications, including information about terms, concepts, syntax, service functions and command-line

- **System interfaces**: Provides details about interface-related terms and concepts, and defines the functional interfaces available to applications accessing POSIX-conformant systems.

- **Shell and utilities**: Describes the commands and utilities available to applications accessing POSIX-conformant systems, including the command language used in those systems.

- **Rationale**: Includes historical information about the standard's contents and why certain features were added or removed.

---

## C API

POSIX defines its standards in terms of the C language. Therefore, **programs are portable to other operating systems at the source code level**. Nonetheless, we can also implement it in any standardized language.

The POSIX C API adds more functions on top of the ANSI C Standard for a number of aspects:

- File operations
- Processes, threads, shared memory, and scheduling parameters
- Networking
- Memory management
- Regular expressions
- The complete description of the functions is defined in the POSIX headers.

---

## File Formats

POSIX defines rules for formatting strings that we use in files, standard output, standard error, and standard input. As an example, let’s consider the description for an output string:

```sh
"<format>", <arg1>, ..., <argN>
```

The format can contain regular characters, escape sequence characters, and conversion specifications. The conversion specifications indicate the output format of the provided arguments and are prefixed by a percent symbol followed by argument type.

---

## File Formats

As an example, let’s suppose we want to output a string that contains today’s date. We’ll use the printf utility because it follows the POSIX file format standard:


```sh
$ printf "Today's Date: %d %s, %d" 18 September 2021
Today's Date: 18 September, 2021
```

The format specifies three conversion specifications: `%d`, `%s`, and `%d`. The `printf` utility processes these conversion specifications and substitutes them with the arguments.

---


## Environment Variables

- An environment variable is a variable that we can define in the environment file, which the login shell processes upon successful login. 
- As a convention, the variable name should merely contain uppercase letters and an underscore. 
- The name can also include a digit, although the POSIX standard doesn’t recommend putting the digit at the start of the name.

For instance, we can define the environment variable for our base user directory in the form of:

```sh
XDG_BASE_DIRECTORY="/home/user/"
```

<!--
For each environment variable, the value should only be a string of characters as defined in the portable character set. 
-->
---

## Environment Variables

Any of your own implementation should respect the reserved environment variables:

- `COLUMN` defines the width of the terminal screen.
- `HOME` defines the pathname of the user’s home directory.
- `LOGNAME` defines the user’s login name.
- `LINES` defines the user’s preferred lines on the terminal screen.
- `PATH` defines binary colon-separated paths for executables.
- `PWD` defines the current working directory.
- `SHELL` defines the current shell in use.
- `TERM` defines the terminal type.
- [MORE HERE](https://www.linuxtopia.org/online_books/introduction_to_linux/linux_Reserved_variables.html)

<!--
We can name the environment variables however we like, although we should avoid defining our own environment variables with names that conflict with the environment variables of standard utilities
-->

---

## Locale

A locale defines the language and cultural convention that is used in the user environment.

A program implementation shall conform to the POSIX locale, which is identical to the C locale.

- `LC_TYPE` for character classification
- `LC_COLLATE` defines the order for characters
- `LC_MONETARY` for monetary formatting
- `LC_NUMERIC` for formatting numbers
- `LC_TIME` for date and time formatting
- `LC_MESSAGES` for program messages such as information messages and logs

---

## Character Set

- A character set is a collection of characters with codes and bit patterns for each character.
  - 010000001 $\equiv$  65 $\equiv$ A
- A standard character set is needed that conforms to the one defined by POSIX.
- POSIX recommends including at least one character set and a portable character set in implementations.
- The first eight entries in the character set should be control characters.
- The POSIX locale should include at least 256 characters from both portable and non-portable character sets.

<!--
Computers only understand binary, so character sets represent symbols that computers can process.

portable = 103 characters 
newline
alert
backaspace
tabe
newline
vertical tab 
form-feed
carriage-return
space

Non-portable extended control characters we find in ASCII
-->
---


## Regular Expressions

- RE, is a string of characters that defines a search pattern for finding text:
    - `awk`, `sed`, `grep` are implemented 
- [Basic (BRE)](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html#tag_09_03) and [Extened (ERE)](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html#tag_09_04)
- BRE and ERE should operate on a string of characters that ends with a NUL character.
- The literal escape sequence and newline character produce an undefined result. Therefore, our programs should treat them as ordinary characters.
- POSIX does not permit the use of an explicit NUL character in the REs or the text to be matched.
- Implementation should be able to perform a case-insensitive search by default.
- The length of our REs should not exceed 256 bytes in length.

---

## Directory Structure

- Most major Linux distributions conform to the F**ilesystem Hierarchy Standard (FHS)**. 
- FHS defines a configurable tree-like directory structure. 
  - The first directory in the hierarchy is the **root directory**, and all the other directories, files, and special files branch out from it.

```sh
$ tree / -d -L 1
/
├── bin -> usr/bin
├── boot
├── dev
├── etc
├── home
├── lib64 -> usr/lib
├── mnt
├── opt
...
└── var
```
---


## Utility Names

POSIX recommends that we implement the following argument syntax in our utility programs:

```sh
utility_name [-a][-b][-c option_argument]
    [-d|-e][-f[option_argument]][operand...] <parameter name>
```
- most utilities behave the same. 
- For instance, we know that the `-h` option prints a help text for almost every UNIX/Linux utility. 
- This consistency owes to the conventions described by POSIX. 
- POSIX defines several conventions for programmers about how we should implement our utility programs.

---

## OSs and POSIX Compliancy

- **Linux**
  - It’s certainly possible to create a Linux-based operating system that is entirely POSIX compliant. EulerOS is a good example of that. However, most modern programs, especially closed-source software, conform to the standard either partially or not at all.
  - As an example, the bash shell used to be completely POSIX compliant. The recent versions of bash, however, don’t conform to the POSIX standard by default. So, one can say that most Linux distributions are partially POSIX-compliant.
  
---

## OSs and POSIX Compliancy

- **Darwin**
  - Darwin is the core set for Apple’s operating systems, such as macOS and iOS. It is partially POSIX compliant. However, the recent releases of macOS are completely POSIX compliant.

- **Windows NT**
  - Microsoft Windows doesn’t conform to the standard at all because its whole design is completely different than UNIX-like operating systems. However, we can set up a POSIX compliant environment by using the WSL compatibility layer or Cygwin.


