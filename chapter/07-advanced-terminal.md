<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="06-inter.md">&lt;&lt; Previous Chapter: 6 - Interoperability</a>
     |
  <a href="08-text-editors.md">Next&nbsp;Chapter:&nbsp;8&nbsp;&#8209;&nbsp;Text&nbsp;editors&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 7 - Advanced terminal usage

Some parts of shell syntax (notably its quoting and statement-syntax rules) can be very confusing. These drawbacks generally relate to compromises in the programming-language part of the shell's design made to preserve its utility as an interactive command language interpreter [^raymond] To see how difficult things can get, take a look at [Bash Pitfalls](https://mywiki.wooledge.org/BashPitfalls), a page dedicated to common mistakes made by bash users.

<a id="multi-tasking"></a>

## 7.1 Multi tasking

The terms virtual console and terminal emulator refer to a unix-type way of dividing a physical console into several virtual consoles, each of which can run its own programs. This allowed multiple programs to be run simultaneously. Multitasking was a significant advantage over, for example, MS-DOS, which was never multitasking,

Different ways to open a desktop application (such as gedit text editor) from a terminal window:

1. Detached: ` $ nohup gedit [optional-text-file] > /dev/null &↵ `
2. Background: ` $ gedit [optional-text-file] &↵ `
    - A process in the background is immune from terminal keyboard input, including any attempt to interrupt it with ` Ctrl + C `. We can return the process to the foreground by ` $ fg %1↵ `.
3. Foreground: ` $ gedit [optional-text-file]↵ `
    - We can stop the process and place it in the background by pressing ` Ctrl + Z `. We can verify that the program has stopped by: ` $ jobs↵ `. We can continue the program's execution in the foreground by: ` $ fg %1↵ `. Or we can continue the program's execution as a background subprocess by: ` $ bg %1↵ `.

> [!TIP]
> Moving a process from the foreground to the background is handy, if we launch a graphical program from the command line, but forget to place it in the background by appending the trailing ampersand `  & `.

<a id="program-hangs-up"></a>

## 7.2 When a program hangs up

Sometimes a computer will become sluggish or an application will stop responding. In this chapter, we will look at some of the tools available at the command line that let us examine what programs are doing and how to terminate misbehaving processes. [^shotts]

<a id="kill-signals"></a>

### Kill signals <!--update internal links if changed-->

There is a **` $ kill `** command, which (despite the name) doesn't necessary kill processes, but rather sends signals. Programs, in turn, listen for signals and may act upon them as they are received. The fact that a program can listen and act upon signals allows a program to do things such as save work in progress when it is sent a termination signal. Signals are one of several ways that the operating system communicates with programs.

#### If you want to terminate a process

- a) press **` Ctrl + C `** which <ins>politely asks the current process to be terminated</ins> (by sending signal **INT** (Interrupt) = **` $ kill -2 <PID>↵ `**). This signal can be intercepted by the process, so it can clean its self up before exiting (or not exit at all). Many (but not all) command-line programs can be interrupted by using this technique.
- b) type **` $ kill -3 <PID>↵ `** which <ins>politely asks the current process to be terminated</ins>. The **QUIT** signal -3 is sent to the target process and if it is still alive enough to receive signals, it will terminate.
- c) type **` $ kill -15 <PID>↵ `** which <ins>politely asks the current process to be terminated</ins>. The **TERM** (Terminate) signal -15 is sent to the target process and if it is still alive enough to receive signals, it will terminate.
- d) type **` $ kill -9 <PID>↵ `** which <ins>immediately terminates the chosen process</ins>. The **KILL** signal -9 is never actually sent to the target program like the other signals. The signal is sent to the kernel, which immediately terminates the process. When a process is terminated in this manner, it is given no opportunity to clean up after itself or save its work and thus may leave corrupted files. For this reason, this signal should be used only as a last resort when other termination signals fail, to <ins>force close</ins> an unresponsive program or window.

#### If you want to pause a process

- a) press **` Ctrl + Z `** which <ins>politely asks the current process to be suspended</ins> (by sending signal **TSTP** (Terminal Stop) = **` $ kill -20 <PID>↵ `**). This signal can be intercepted by the program and it may choose to ignore it. When you succesfully suspend a process, you can do fancy things with it such as bring it back to the foreground.
- b) type **` $ kill -19 <PID>↵ `** which <ins>immediately suspends the chosen process</ins>. The **STOP** signal -19 is never actually sent to the target program like the other signals. The signal is sent to the kernel, which immediately suspends the process. When a process is suspended in this manner, it is given no opportunity to ignore the command.

> [!TIP]
> You can see all the signals using ` $ kill -l↵ ` in terminal.

> [!NOTE]
> With ` $ kill ` we must have superuser privileges to send signals to processes that do not belong to us.

### Process ID

The kernel maintains information about each process to help keep things organized. Each process is assigned a **PID** number (short for Process ID). Like files, processes also have owners and user IDs.

Many distributions offer a "System Monitor" found some where in the "Start Menu" to find out the process ID numbers. This is the equivalent of Task Manager in Windows invoked by ` Ctrl + Alt + Del `.

The terminal will offer some alternatives to find the PID(s):
- ` $ pidof firefox↵ ` will list PID(s) of a specific executable
- ` $ ps↵ ` will list processes associated with the current terminal session.
- ` $ ps x↵ ` will list processes regardless of what terminal (if any) they are controlled by.
- ` $ ps aux↵ ` will show processes belonging to every user.

The fields are:
- **USER** = Owner of the process
- **TIME** = Amount of CPU time consumed by the process.
- **TTY** (Teletype) = Controlling terminal for the process. An exlamation mark ` ? ` in the TTY column indicates no controlling terminal.
- **STAT** (Process State Codes) = Current status of the process
    - ` R ` = Running or ready to run
    - ` S ` = Sleeping or waiting
    - ` T ` = Stopped

### Process priority

Linux can run a lot of processes at a time, which can slow down the speed of some high priority processes and result in poor performance. To avoid this, you can tell your machine to prioritize processes as per your requirements. This priority is called **niceness** in Linux, and it has a value between -20 to 19. The lower the Niceness index, the higher the priority. The default value of all the processes is 0.
- To start a process with a niceness value other than the default value use: ` $ nice -n <nice value> process name↵ `
- If there is some process already running on the system, then you can re-nice: ` $ renice <nice value> -p <PID>↵ `

<a id="expansions-and-quoting"></a>

## 7.3 Expansions and quoting

The bash shell can perform expansions and substitutions (as show by examples below), which leads to the need to control it with quoting.
- Double quotes ` "..." ` suppress some expansions.
- Single quotes ` '...' ` suppress all expansions.

|   | Example | Un<br>quoted | "Double"<br>quoted | 'Single'<br>quoted |
| --- | --- | --- | --- | --- |
| Simple string | text | text | text | text |
| Filepath and **tilde expansion** | ~/\*.txt | **/home/margaret/\*.txt** | ~/\*.txt | ~/\*.txt |
| **Brace expansion** | {a,b}<br>{001..003} | **a b**<br>**001 002 003** | {a,b}<br>{001..003} | {a,b}<br>{001..003} |
| **Command substitution** | $(uname ‑o)<br>\`uname ‑o\` | **GNU/Linux**<br>**GNU/Linux** | **GNU/Linux**<br>**GNU/Linux** | $(uname ‑o)<br>\`uname ‑o\` |
| **Arithmetic expansion** | $((2+2)) | **4** | **4** | $((2+2)) |
| **Parameter expansion** | $USER | **margaret** | **margaret** | $USER |

> [!TIP]
> You can use the *display text* command ` $ echo ` to learn see the world as the shell sees it.

<a id="gnu-test"></a>

## 7.5 Square brackets: [...]

There is a [special GNU test command](https://www.gnu.org/software/coreutils/manual/coreutils.html#test-invocation) to perform a variety of checks and comparisons. It has two equivalent forms: ` $ test <expression>↵ ` and ` $ [ <expression> ]↵ `. It is interesting to note that both ` $ test ` and ` $ [ ` are actually commands. There is actually an executable named ` [ ` in the ` /usr/bin/ ` directory. The expression is actually just the arguments for the ` $ [ ` command. That's why a space character is required after. Likevise the ` ] ` is simply a required final argument. Also that's why a space character is required before the ` ] ` argument.
- The commands return an exit status of 0 if the expression is true, 1 if the expression is false, or 2 if an error occurred. Nothing gets printed on the screen though. The shell provides a parameter ($?) that we can use to examine the exit status. Or one can construct some form of if-then-clause.

```
$ [ $USER == margaret ] && echo true || echo false↵
$ test $USER == margaret && echo true || echo false↵
true

$ [ $USER == edvard ] && echo true || echo false↵
$ test $USER == edvard && echo true || echo false↵
false

$ [ $USER == margaret ]↵
$ test $USER == margaret↵
$ echo $?↵
0

$ [ $USER == edvard ]↵
$ test $USER == edvard↵
$ echo $?↵
1
```

<a id="customizing-shell-prompt"></a>

## 7.6 Customizing the shell prompt

When used interactively, the shell prompts with the value of ` PS1 ` before reading a command. If at any time a newline ` \↵ ` is typed and further input is needed to complete a command then the secondary prompt ` PS2 ` is issued. It is possible to customize these default shell prompts.

Let's examine the default ` PS1 ` prompt in Solus ` $ echo $PS1↵ `:

| Code | Function |
| --- | --- |
| \\\[  \\033[**38;5;081**m  \\\] | Will change color to aqua |
| \\u | Current username |
| \\\[  \\033[**38;5;245**m  \\\] | Will change color to grey |
| @ | Simply the at sign |
| \\\[  \\033[**38;5;206**m  \\\] | Will change color to fuchsia |
| \\H | Current hostname |
| \\\[  \\033[**38;5;245**m  \\\] | Will change color to grey |
| \\w | Current working directory |
| \\\[  \\033[**38;5;081**m  \\\] | Will change color to aqua |
| $ | Simply the dollar sign |
| \\\[  **\\e[0m**  \\\] | Removes all attributes (formatting and colors). |

> [!NOTE]
> **` \[ `** = Begins a sequence of non-printing characters (like color escape sequences).
>
> **` \] `** = Ends a sequence of non-printing characters.

Lets replace the default PS1 with something different:

```
$ export PS1='[\D{%d/%m/%Y %H:%M:%S} \u@\h \W]§'↵
[16/06/2024 18:34:38 margaret@mamas-machine ~]§

$ export PS2='\[\033[38;5;081m\]> \[\e[0m\]'    # The PS2 on Solus could use some colour and a space at the end :)
```

> [!NOTE]
> Any change to PS1 or PS2 will vanish as the shell session ends. To make the change permanent, add the export command to a new line on ` ~/.bashrc ` for user specific preference, or ` /etc/profile ` for system wide preference.

### Special prompt variables [^ss64]

[^ss64]: [SS64 - How to setup prompt statement variables, accessed 2021](https://ss64.com/bash/syntax-prompt.html)

- ` \$ ` = The default bash prompt sign.
    - a) Dollar sign $ for regular access.
    - b) Hash mark # for continuous root access.
- ` \u ` = The username of the current user
- ` \H ` = The full hostname (such as deckard.SS64.com)
- ` \h ` = The hostname, up to the first dot (such as deckard)
- ` \w ` = Current directory (full path)
- ` \W ` = Current directory (without the parent directories)
- ` \l ` = The basename of the shell's terminal device name
- The time
    - ` \t ` = in 24-hour HH\:MM\:SS format
    - ` \T ` = in 12-hour HH\:MM\:SS format
    - ` \@ ` = in 12-hour AM\:PM format
- ` \n ` = Newline
- ` \r ` = Carriage return
- ` \a ` = Bell character
- ` \\ ` = Backslash
- ` \nnn ` = Character with corresponding ASCII code (nnn = octal value)
- ` \! ` = History number of this command
- ` \# ` = Command number of this command
- ` \D{...} `
    - ` %a ` = (la) = Day (abbreviated name)
    - ` %A ` = (lauantai) = Day (full name)
    - ` %b ` = (helmi) = Month (abbreviated name)
    - ` %B ` = (helmikuu) = Month (full name)
    - ` %d.%m.%Y ` = (20.02.2021) = Day, Month, Year
    - ` %H:%M:%S ` = (10\:15\:59) = Hours, Minutes, Seconds
    - E.g. ` \D{%H:%M %A %d.%m.%Y} ` = 10\:15 lauantai 20.02.2021

For more bells and whistles visit:
- <https://misc.flogisoft.com/bash/tip_colors_and_formatting>
- <https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences>

### 8-bit (256) colors [^wiki-ansi]

Most terminal emulators understand the 8-bit color palette:

![Terminal 8-bit color palette](../asset/colors.svg)

[^wiki-ansi]: [Wikipedia - ANSI escape code, accessed 2024](https://en.wikipedia.org/wiki/ANSI_escape_code)

Using these above, you can make pink text like so:

```
\033[38;5;206m     #That is, \033[38;5;<FG COLOR>m
```

And an early-morning blueish background like so:

```
\033[48;5;57m      #That is, \033[48;5;<BG COLOR>m
```

The above foreground and background be combined like so:

```
\033[38;5;206;48;5;57m  #That is, \033[38;5;<FG COLOR>;48;5;<BG COLOR>m
```

The 8-bit colours are arranged like so:
- ` 0x00-0x07 ` = Standard 8 colors.
- ` 0x08-0x0F ` = Additional 8 high intensity colors.
- ` 0xE8-0xFF ` = Grayscale from black to white in 24 steps.
- ` 0x10-0xE7 ` = Rest of the 216 colors. <!-- 6 × 6 × 6 cube = 16 + 36 × r + 6 × g + b where (0 ≤ r, g, b ≤ 5) -->

<!-- # References -->

[^raymond]: [Eric Steven Raymond - The Art of Unix Programming, published 2003](https://www.arp242.net/the-art-of-unix-programming/)

[^shotts]: [William Shotts - The Linux Command Line, updated 2019](http://linuxcommand.org/tlcl.php)
