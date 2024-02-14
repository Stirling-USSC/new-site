---
title: Mastering the Unix Command Line
subtitle: University of Stirling Society of Computing
author: Michael Connor Buchan <mib00150@students.stir.ac.uk>
date: 2023-11-17
draft: false
outputs: [Reveal]
---

## Unix?

Unix is an operating system developed in the 1960s and 1970s at Bell Labs by Ken Thompson, Dennis Ritchie, and others.
It was designed to be portable, multi-tasking, and multi-user, making it a powerful and flexible system.

The impact that Unix has had on the computing industry simply cannot be overstated! It was the first operating system to
be written in [the C programming language][c], which was also developed at Bell Labs by Ken Thompson and Dennis
Ritchie, it was widely adopted, forked [^1], cloned, imitated [^2], and extended upon, particularly in educational institutions,
and many of its ideas have stood the test of time, and are still commonly used in software over 50 years after its
conception!

[c]: <https://en.wikipedia.org/wiki/C_(programming_language)>

[^1]: The modern BSD family, such as Free BSD, Open BSD, Net BSD, etc, stems from the original [Berkeley Software
  Distribution][bsd], which itself stems from the original Bell Labs Unix source code.

[bsd]: <https://en.wikipedia.org/wiki/Berkeley_Software_Distribution>

[^2]: [Linux][linux] is a clone of [Unix System V][sysv], ATnT's commercial offering of Unix, first released in 1983.


[sysv]: <https://en.wikipedia.org/wiki/UNIX_System_V>

--------

## Command Lines and Shells?

> A Unix shell is both a command interpreter and a programming language. As a command interpreter, the shell provides the
> user interface to the rich set of GNU utilities. The programming language features allow these utilities to be combined.
> Files containing commands can be created, and become commands themselves. These new commands have the same status as
> system commands in directories such as /bin, allowing users or groups to establish custom environments to automate their
> common tasks. 

-- [Bash Reference Manual, section 1.2](https://www.gnu.org/software/bash/manual/bash.html#What-is-a-shell_003f)

--------

Shells let you:

* navigate the file system
* Run programs
* Manage processes
* And much more!

It acts as an interface between the user and the kernel, the core part of the operating system.

--------

## Why not use a GUI?

These days we're used to interacting with computers in a visual fashion, using a graphical user interface with windows,
icons, menus and a pointer. This is very intuitive for new computer users, but can be efficient for many tasks.

The command line offers a much more direct way to talk to the underpinnings of your operating system. The Unix shell
relies on text-based commands. Users enter commands manually, and the system responds with text output. This approach
offers efficiency and flexibility, allowing for precise control over system functions.

Programmers and system administrators often prefer the CLI for its scripting and automation  capabilities, and resource
efficiency (text takes up much less memory than bitmap graphics to be displayed on a screen).

--------

## What We'll Cover


* What You'll Need
* The Prompt
* Basic file management commands
    * Listing Files
    * Printing the Contents of a File
    * Other File Management Commands
    * File paths
* Shell Shortcuts
    * Tab completion
    * Shell Globbing
    * Aliases and shell configuration
    * Shell keybindings
* Common command conventions
    * Arguments
    * Output
    * Command Documentation
* Text Processing
    * Searching Through Files with `grep`
    * Redirection and the standard streams
    * Pipes and filters
* Environment variables
* The search path

--------

## What You'll Need

:::::: {.columns}

::: {.column}
### Windows

* The Windows command prompt does not use the same syntax as a Unix shell, so you'll need to install one
* **Windows 10+**: Install the [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install)
* **Or**: Alternatively, install [MSys2](https://www.msys2.org/)
:::

::: {.column}
### macOS

* macOS is based on BSD, so you already have a terminal, ready to go!
* Launch the Terminal app. You'll find it in Applications -> Utilities
:::

::: {.column}
### Linux

* Linux is a clone of Unix, so you already have everything you need!
* Launch your terminal application. Commonly installed terminals include Xterm, Gnome Terminal, or Konsole
:::

::::::

--------

## The Prompt

When you launch your terminal for the first time, you'll see something like this:

```bash
mikey@mikeys-thinkpad:~$ 
```

This is the prompt, which exists to let you know that any commands you've ran have finished [^3], and the shell is ready for
you to type another command.

The parts of the prompt are:

* The name of the logged in user ("mikey" in my case)
* The hostname of the computer you're using ("mikeys-thinkpad" in my case)
* The current directory ("~" represents my home directory, or "/home/mikey")
* An end of prompt character ("$" in my case because I'm a regular user, root's prompt ends with "#")

[^3]: If a command hangs and you'd like to cancel it, press `ctrl+c`.

--------

# Basic file management commands

--------

## Listing Files

List files with the `ls` command. It accepts several optional arguments and flags, but typing `ls` on its own will give
you a simple list of the files and directories (folders) in the current directory:

```bash
mikey@mikeys-thinkpad:~$ ls
anaconda3  books  code  Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos  README.md
```

Typing `ls -l`  will show you more information about each file, including its type, permissions, owner, group, size in
bytes, and modification date (`-l` is equivalent to `--long`):

```bash
mikey@mikeys-thinkpad:~$ ls -l
total 168
drwxr-xr-x  28 mikey mikey  30 Sep 18 10:33 anaconda3
drwxr-xr-x  19 mikey mikey  29 Sep 20 23:39 books
drwxr-xr-x  34 mikey mikey  34 Nov 16 17:11 code
drwxr-xr-x   2 mikey mikey   2 Aug 29 20:14 Desktop
drwxr-xr-x   5 mikey mikey   9 Nov 17 13:59 Documents
drwxr-xr-x   9 mikey mikey  40 Nov 15 16:53 Downloads
drwxrwxrwx 110 mikey mikey 117 Nov 17 13:59 Music
drwxr-xr-x   2 mikey mikey   5 Nov  4 17:09 Pictures
drwxr-xr-x   2 mikey mikey   2 Aug 29 20:14 Public
drwxr-xr-x   2 mikey mikey   2 Aug 29 20:14 Templates
drwxr-xr-x   2 mikey mikey   2 Aug 29 20:14 Videos
-rw-r--r--   1 mikey mikey  42 Nov 17 14:14 README.md
```

We can tell from this that:

* Most of the things in my home directory are subdirectories, as they're labelled with `d` in the first column
* `README.txt` is a regular file (labelled with '-')

You can list the contents of a subdirectory by typing its name after `ls` and any options, E.G:

```sh
mikey@mikeys-thinkpad:~$ ls code
blab    cyal                    ffstream      irc-h  libraille-cpp   mudle      openroom       qt-listview-bug  skitz-c    stirling-computing-alliance  tolk
blirc   edith                   forks         lege   lower-elements  mundistry  piper-testing  rual             skitz-cpp  third-party                  uni
circed  embedded-linux-testing  haven-backup  leged  lua-reactor     old        qirc           skitz            skitz-py   tmp
```

--------

## Printing the Contents of a File

Let's see what's inside the `README.txt` file with the `cat` command:

```bash
mikey@mikeys-thinkpad:~$ cat README.md 
This is some text in the README.txt file.
```

`cat` is short for "concatenate", because you can pass multiple files in a single command, and it will print them all in
succession:

```bash
mikey@mikeys-thinkpad:~$ cp README.md new_file.txt # cp is the copy command
mikey@mikeys-thinkpad:~$ 
mikey@mikeys-thinkpad:~$ cat README.md  new_file.txt 
This is some text in the README.txt file.
This is some text in the README.txt file.
```

Make sure you only try to cat out text files. If you try catting binary files, the binary data will be written directly
to your terminal, which will likely mess it up. If you do this by mistake, type `reset` and press enter, that should fix
your terminal.

--------

## Other File Management Commands

* `cp file1 file2` copies a file from `file1` to `file2`
* `cp -r dir1 dir2` copies directory `dir1`, and all of its contents, to `dir2`
* `mv path1 path2` moves (renames) a file or directory, from `path1` to `path2`
* `mkdir dirname` makes a new directory called `dirname`
* `mkdir -p path/with/multiple/directories` makes a directory at the given path, creating the parent directories if
  they don't already exist
* `rmdir dir1` removes empty directory `dir1`. If the directory is empty, an error is returned
* `rm file` deletes the regular file `file`
* `rm -r dir` recursively deletes the directory `dir` and all of its contents. Be careful with this one!
* `stat path` lists various pieces of metadata for the file or directory at the specified path
* `du -h path` calculates the size of `path`. `-h` means to print the size in human readable format

--------

## File paths

A file's path is a string of text that specifies where that file can be found on the file system.

* Paths that start with a `/` (slash) character, such as `/bin/bash` [^4], are called *absolute* paths, and describe how to find the file from the
  root directory (I.E. the parent directory of every file and subdirectory on your system).
* Paths that start with a directory name, like `code/blirc/README.md`, are *relative* paths. They specify where to find
  a file, starting from another directory.
* The shell lets you start a path with a `~` (tilde) character, which will expand to your user's home directory
  (`/home/<username>` on Linux, `/Users/<username>` on macOS)

To resolve relative paths into absolute paths, you need to know what they're relative to. In the shell, this is usually
the current *working directory*. You can ask what that is with the pwd command:

```bash
mikey@mikeys-thinkpad:~$ pwd
/home/mikey
```

So, if I ran `cat code/blirc/README.md`, that's equivalent to if I wrote `cat /home/mikey/code/blirc/README.md` or `cat
~/code/blirc/README.md`.

You can change the current directory with the `cd` command:

```bash
mikey@mikeys-thinkpad:~$ cd code
mikey@mikeys-thinkpad:~/code$ pwd
/home/mikey/code
mikey@mikeys-thinkpad:~/code$ ls
blab    cyal                    ffstream      irc-h  libraille-cpp   mudle      openroom       qt-listview-bug  skitz-c    stirling-computing-alliance  tolk
blirc   edith                   forks         lege   lower-elements  mundistry  piper-testing  rual             skitz-cpp  third-party                  uni
circed  embedded-linux-testing  haven-backup  leged  lua-reactor     old        qirc           skitz            skitz-py   tmp
mikey@mikeys-thinkpad:~/code$ cd .. # .. = the parent directory
mikey@mikeys-thinkpad:~$ pwd
/home/mikey
mikey@mikeys-thinkpad:~$ cd Downloads/
mikey@mikeys-thinkpad:~/Downloads$ cd # Typing cd with no parameters returns you to your home directory
mikey@mikeys-thinkpad:~$ pwd
/home/mikey
```

[^4]: Incidentally this is likely to be the path to your shell, at least on Linux. macOS defaults to using [ZSH][zsh] as
  its shell.

[zsh]: <https://www.zsh.org/>

--------

# Shell Shortcuts

--------

## Tab completion

These commands and paths can get long, but fortunately, you hardly ever have to type the entire thing! Bash has
auto-completion, triggered by pressing the `tab` character.

For example, if I want to change to my `Downloads` directory, I can type:

```bash
mikey@mikeys-thinkpad:~$ cd Do
```

At this point, pressing `tab` once does nothing [^5], because their are two directories that begin with `Do`,. Pressing `tab` a
second time asks bash to give me a list of potential completions:

```bash
mikey@mikeys-thinkpad:~$ cd Do
Documents/ Downloads/ 
mikey@mikeys-thinkpad:~$ cd Do
```

I can specify which I want by typing the next letter `w`, then pressing `tab`:

```bash
mikey@mikeys-thinkpad:~$ cd Downloads/
```

Bash completes the directory name, and adds a trailing `/` character, in case I want to chain a file or subdirectory
onto the `Downloads` folder. And yes, you could auto-complete that too!

In fact, you can auto complete files, directories, command names themselves, and with common commands, even flags! Try
typing `ls --v` and pressing `tab`, see what you get! Even third-party programs can instruct bash on how to complete
their commands, check on the web to see if your favourite software can install bash completions.

[^5]: If you're using a shell that isn't bash, like [ZSH][zsh], tab completion may work slightly differently. Experiment
  by pressing `tab` at different points while typing a command to see how it works in your shell.

--------

## Shell Globbing

The shell also provides you with some nice shortcuts for passing multiple files to a command. For example, if we have a
directory containing the following:

```bash
mikey@mikeys-thinkpad:~$ cd test
mikey@mikeys-thinkpad:~/test$ ls
another-file.txt  file1.txt  file2.txt  file3.txt  file4.txt  file5.txt
```

If we want to pass all the numbered files to `cat`, in order to concatenate them, we could write:

```bash
mikey@mikeys-thinkpad:~/test$ cat file1.txt file2.txt file3.txt file4.txt file5.txt 
```

But, even with tab completion, this is tedious. Instead, we can type:

```bash
mikey@mikeys-thinkpad:~/test$ cat file*.txt
This is file 1
This is file 2
This is file 3
This is file 4
This is file 5
```

Here `*` acts like a placeholder, and the shell will expand it to represent every file WHO's name starts with `file` and
ends with `.txt`. There are a number of these so called *glob patterns*, similar to regexp:

* `*` represents 0 or more characters
* `?` represents a single character
* `[abc]` represents any of the characters `a`, `b` or `c`
* `[a-z]` represents any character in the range `a` to `z`

So, to remove every file in the current directory, run:

```bash
rm *
```

**Note:** Be careful with the above command, especially its recursive version `rm -r *`! There's no recycle bin for
deleted files in the command line, so if you run these commands in the wrong directory, you could easily delete the
wrong data, and even break your operating system!

--------

## Aliases and shell configuration

The last way we'll explore to shorten the amount of time you spend typing commands is aliases. They let you create a
shorter name for an existing command.

For example, I often type `sudo apt update && sudo apt upgrade` to update the software on my Debian Linux machine. I can
use an alias as follows to shorten that command to just `update`:

```bash
mikey@mikeys-thinkpad:~$ alias update='sudo apt update && sudo apt upgrade'
mikey@mikeys-thinkpad:~$ alias update # without a value, the alias command prints what the alias is currently set to
alias update='sudo apt update && sudo apt upgrade'
mikey@mikeys-thinkpad:~$ update
[sudo] password for mikey: 
Hit:1 http://deb.debian.org/debian bookworm InRelease
Get:2 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]                                                                                                             
Hit:3 http://repository.spotify.com stable InRelease                                                                                                                                          
Hit:4 http://ppa.launchpad.net/pipewire-debian/pipewire-upstream/ubuntu jammy InRelease                                                                                                       
# ... so on
```

--------

## Shell keybindings

Typed a command slightly wrong and wish you could edit it? Want to run a similar, but not identical command to the last
one you ran? Don't despair, just press the up arrow! You can use the `up`, `down`, `page-up` and `page-down` keys to
scroll through your command history.

Typed a command ages ago and can't remember exactly what it was? Press `ctrl+r` to start a reverse incremental search, then
start typing a part of the command. This looks like this:

```bash
(reverse-i-search)`cd .. ': cd .. # .. = the parent directory
```

Here I've searched for "cd .. " and you can see the command I typed earlier. I can press the `left` and `right` arrow
keys to edit it, or just press `return` to execute it again.

--------

# Common command conventions

--------

## Arguments

Unix commands, naturally, start with the name of the command you'd like to execute. Following this are the command's
arguments. The program itself is free to interpret these however it wishes, however their are some common conventions
followed by almost every command you'll use on a daily basis:

* You can modify the behaviour of a command with *flags*, sometimes also called *switches*.
    * There are two types:
        * Short switches like `-a`, which have a single leading `-` (dash) character
        * Long switches like `--all`, which have two leading `-` (dash) characters
    * Commonly used long switches tend to have short equivalents, E.G. the two examples above are from the `ls` command
    * Almost every command line program accepts `--help` to print information about how to use the command, and
      `--version` to print the program's version information
* The remaining arguments are usually the names of input or output files

--------

## Output

Most Unix commands that perform some action, such as deleting a file, print nothing when they succeed. This may seem
strange compared to GUIs, where there is usually some visual feedback when an action succeeds, but you'll eventually get
used to it. Commands will, of course, tell you when there's an error:

```bash
mikey@mikeys-thinkpad:~$ rm test
rm: cannot remove 'test': Is a directory
mikey@mikeys-thinkpad:~$ rm -r test
mikey@mikeys-thinkpad:~$ # No output
```

--------

## Command Documentation

Most commands provide a manual page, which describes what the program does, what its options mean, and may provide other
information such as example invocations, author / bug reporting information, and / or a list of other, related commands.
You can read the manual page for a command by typing `man command-name`. For example:

```bash
mikey@mikeys-thinkpad:~$ man bash
BASH(1)                                                                           General Commands Manual                                                                          BASH(1)

NAME
       bash - GNU Bourne-Again SHell
    
SYNOPSIS
       bash [options] [command_string | file]
    
COPYRIGHT
       Bash is Copyright (C) 1989-2022 by the Free Software Foundation, Inc.
    
DESCRIPTION
       Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file.  Bash also incorporates useful features from the Korn and
       C shells (ksh and csh).
    
       Bash is intended to be a conformant implementation of the Shell and Utilities portion of the IEEE POSIX specification (IEEE Standard 1003.1).  Bash can be configured to be  POSIX-
       conformant by default.

# ... so on
```

To search through man-pages, use the `apropos` command, or the equivalent `man -k`:

```bas
mikey@mikeys-thinkpad:~$ apropos bash
bash (1)             - GNU Bourne-Again SHell
bash-builtins (7)    - bash built-in commands, see bash(1)
bashbug (1)          - report a bug in bash
builtins (7)         - bash built-in commands, see bash(1)
dh_bash-completion (1) - install bash completions for package
hugo-completion-bash (1) - Generate the autocompletion script for bash
rbash (1)            - restricted bash, see bash(1)
```

The numbers in brackets indicate sections of the manual. Most man-pages you'll want to read will be in section 1
"General Commands Manual" or section 8 "System Managers Manual"

--------

# Text Processing

--------

## Searching Through Files with `grep`

Where the shell excels is in processing text, particularly lines of text. Let's copy a big text file to our home
directory to experiment with:

```bash
mikey@mikeys-thinkpad:~$ cp /usr/share/common-licenses/GPL-3 license.txt
```

This file comes with any Debian or Ubuntu system, and contains the text of the GNU General Public License, which is the
license most software on your computer is distributed under. It's not the longest license in the world, but it isn't
short either!

```bash
mikey@mikeys-thinkpad:~$ wc -l license.txt  # Prints the number of lines in license.txt 
674 license.txt
mikey@mikeys-thinkpad:~$ head license.txt # Prints the first 10 lines of the file
                    GNU GENERAL PUBLIC LICENSE

                       Version 3, 29 June 2007

 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>

 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.


                            Preamble
                            
  The GNU General Public License is a free, copyleft license for
```

Let's say we want to print all the lines of this file which contain a link. We can use the `grep` command to do exactly
that:

```BASH
mikey@mikeys-thinkpad:~$ grep https:// license.txt 
 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/why-not-lgpl.html>.
```

Some common grep options are:

* `-i` or `--ignore-case`: Perform a case insensitive search
* `-v` or `--invert-match`: Print all lines that do *not* match, inverting the search
* `-r` or `--recursive`: Search an entire directory of files, including files in subdirectories

--------

## Redirection and the standard streams

You may have noticed that if you type `grep` and a search term, but forget to give it a file name, it will seemingly
just hang, and never return you back to your prompt. You may also wonder how we can save the output of a command like
`grep to a file, for later viewing.

Both these mysteries can be solved by explaining input and output streams. The shell rigs up 3 streams to your command
when you run them:

* **stdin**: STDandard INput (stream 0) the default input stream
* **stdout**: STDandard OUTput (stream 1) the default output stream where data is written
* **stderr**: STDand ERRor (stream 2) the default output stream where errors are written

By default stdin comes *from* your terminal, and stdout and stderr go *to* your terminal. That's why `grep` hangs if you
give it a filename: it's waiting for you to type some input.

We can easily redirect these streams to point to files or other places. For example, to tell grep to get its input from
`license.txt`, we can write:

```bash
mikey@mikeys-thinkpad:~$ grep https:// < license.txt 
 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/why-not-lgpl.html>.
```

This isn't very useful though, because `grep` already lets us specify an input file directly. Let's instead redirect its
output to a file:

```bash
mikey@mikeys-thinkpad:~$ grep https:// license.txt  > results.txt
mikey@mikeys-thinkpad:~$ cat results.txt 
 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/why-not-lgpl.html>.
```
We can also redirect standard error using `2>`:

```bash
mikey@mikeys-thinkpad:~$ grep https:// abcde
grep: abcde: No such file or directory
mikey@mikeys-thinkpad:~$ grep https:// abcde 2> errors.txt
mikey@mikeys-thinkpad:~$ cat errors.txt 
grep: abcde: No such file or directory
```

Or even redirect both at the same time with `&>`.

You can also redirect one stream to another, by specifying an `&` (ampersand) character, followed by a stream number,
instead of a file name:

```bash
mikey@mikeys-thinkpad:~$ grep https:// license.txt abcde 2>&1 # Redirect stderr to stdout
license.txt: Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
license.txt:    along with this program.  If not, see <https://www.gnu.org/licenses/>.
license.txt:<https://www.gnu.org/licenses/>.
license.txt:<https://www.gnu.org/licenses/why-not-lgpl.html>.
grep: abcde: No such file or directory
```

This may seem useless right now, but it will soon be obvious why it's needed.

--------

## Pipes and filters

Redirecting output into files is great, but we haven't yet discussed one of the most powerful features of the Unix
shell, Unix pipelines.

What if we wanted to take the output of one program, and *pipe* it into the input of another program? This can be
achieved easily with the `|` (pipe) character. For example, if we wanted to count the number of lines containing links
in `license.txt`, we could run:

```bash
mikey@mikeys-thinkpad:~$ grep https:// license.txt
 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/>.
<https://www.gnu.org/licenses/why-not-lgpl.html>.
mikey@mikeys-thinkpad:~$ grep https:// license.txt | wc -l
4
```

1. First, grep reads the input file `license.txt`, and checks if each line contains the pattern `https://`, printing it
   if it does
2. The matched lines are printed to grep's standard output, which is also the standard input of `wc` (the word count
   program)
3. `wc` reads from standard input and, since it was given the `-l` option, counts the lines in the file
4. When `grep` finishes printing matches, it exits, which signals to `wc` that the end of its standard input has been
   reached
5. `wc` then prints the total line count, and exits itself

---

You can create long pipelines to achieve something more complex, like this example, which prints misspelled words in a
text file:

```bash
mikey@mikeys-thinkpad:~$ echo "thiis is a testt text file with sume mispelings in it" > test.txt
mikey@mikeys-thinkpad:~$ cat test.txt 
thiis is a testt text file with sume mispelings in it
mikey@mikeys-thinkpad:~$ cat test.txt | tr -s '[:space:]' '\n' | sort | uniq | aspell list
mispelings
sume
testt
thiis
```

--------

This is why `2>&1` to combine stdout and stderr is useful. If you'd like to pipe both into another command, you can do
so. For example, to run a command and send all its output into `nano`, a simple text editor:

```bash
mikey@mikeys-thinkpad:~$ ls --help 2>&1 | nano +1 -
```

* `LS`: Command to run
* `--help`: flag for `ls`
* `2>&1` pipe stderr (stream 2) into stdout (stream 1)
* `|` Pipe stdout into the stdin of the next command
* `nano`: A basic text editor
* `+1`: Tells `nano` to put the cursor on the first line, instead of the last one
* `-`: Explicitly tells `nano` to read from stdin, otherwise it would just open a blank file

--------

# Environment variables and the search path

--------

## Shell Variables

While the shell is very conducive to being used interactively, it is, at heart, still a fully [Turing complete][tc]
programming language and, as you might expect as a result, it has variables.

[tc]: <https://en.wikipedia.org/wiki/Turing_completeness>

```bash
mikey@mikeys-thinkpad:~$ x=1
mikey@mikeys-thinkpad:~$ y=hello
mikey@mikeys-thinkpad:~$ z="string with spaces"
mikey@mikeys-thinkpad:~$ echo "x = $x, y = $y, z = $z"
x = 1, y = hello, z = string with spaces
```

All variables in the shell store text [^6], after all text is the basic unit of data that the shell processes.

[^6]: Actually, bash includes methods for working with [numbers][bash-arithmetic] and [arrays][bash-arrays], but
  they're not standard in every shell.

[bash-arithmetic]: <https://www.gnu.org/software/bash/manual/html_node/Shell-Arithmetic.html>
[bash-arrays]: <https://www.gnu.org/software/bash/manual/html_node/Arrays.html>

--------

This can be useful if, for example, you'd like to save a long path as a variable, then pass it to multiple commands:

```bash
mikey@mikeys-thinkpad:~$ ldir=/usr/share/common-licenses/
mikey@mikeys-thinkpad:~$ ls $ldir
Apache-2.0  Artistic  BSD  CC0-1.0  GFDL  GFDL-1.2  GFDL-1.3  GPL  GPL-1  GPL-2  GPL-3  LGPL  LGPL-2  LGPL-2.1  LGPL-3  MPL-1.1  MPL-2.0
mikey@mikeys-thinkpad:~$ head $ldir/Apache-2.0
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/
                        
   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
mikey@mikeys-thinkpad:~$ cp $ldir/Apache-2.0 apache-2-license.txt
```

--------

## Turning Shell Variables into Environment Variables

You can also *export* variables. If you do this, programs you run from the shell will be able to read and use their
values (E.G. to control what log messages are printed, whether error messages are printed in colour, etc.

```bash
mikey@mikeys-thinkpad:~$ python -c 'import os; print(os.getenv("MY_VAR"))' # MY_VAR is not set
None
mikey@mikeys-thinkpad:~$ MY_VAR=test python -c 'import os; print(os.getenv("MY_VAR"))' # MY_VAR is set for this command
test
mikey@mikeys-thinkpad:~$ export MY_VAR=test # MY_VAR will be set for every command started from this shell
mikey@mikeys-thinkpad:~$ python -c 'import os; print(os.getenv("MY_VAR"))' # So it will be set here
test
```

Here we've used Python to print the value of the environment variable `MY_VAR` from within the Python subprocess.
