<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="05-links.md">&lt;&lt; Previous Chapter: 5 - Links in the file system</a>
     |
  <a href="07-advanced-terminal.md">Next&nbsp;Chapter:&nbsp;7&nbsp;&#8209;&nbsp;Advanced&nbsp;terminal&nbsp;usage&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 6 - Interoperability

**Interoperability** or **interprocess communication (IPC)** is the ability of software processes to talk to each other and work together with little effort from the user. Such modularity and extensibility is one of the oldest and most persistent design tropes of unix and its decendants.

> [!IMPORTANT]
> The power of a system comes more from the relationships among programs, than from the programs themselves.

<a id="ipc-techniques"></a>

## 6.1 Simple IPC Techniques

Unix has always provided several ways for processes to communicate relatively easy:

### Numeric exit status

The simplest of all design patterns is having no input and no output; Just a **numeric exit status** (see [Section: Exit status and comparison](#exit-status-and-comparison)). Good examples for use of such mechanic are commands ` $ test `, ` $ rm ` and ` $ touch `
- ` $ test -r <file>↵ ` = Does the file exist and is it readable?
- ` $ test -w <file>↵ ` = Does the file exist and is it writable?
- ` $ test -u <file>↵ ` = Does the file exist and is the setuid bit set?
- ` $ test -g <file>↵ ` = Does the file exist and the setgid bit is set?
- ` $ test -k <file>↵ ` = Does the file exist and the sticky bit is set?

<!--    - ` $ test -r <file>↵ ` = True if the file exists and is readable.
    - ` $ test -w <file>↵ ` = True if the file exists and is writable.
    - ` -u `, ` -g `, ` -k ` = True if the file exists and has the setuid, setgid or sticky bit set.-->

> [!NOTE]
> The test command returns an exit status of 0 if the expression is true, 1 if the expression is false, or 2 if an error occurred.
> 
> Nothing gets printed on the screen though. The shell provides a parameter ` $? ` that we can use to examine the exit status. Or one can construct some form of if-then-clause. See [Chapter 7, Section: Square brackets](07-advanced-terminal.md#square-brackets). 

### Text through standard streams

Simple **textual information** can be passed through **standard streams**. Most shell programs have two I/O data streams available to it: standard input and standard output (see [Section: File descriptor](#file-descriptor)). They allow the combined use of commands. One command is executed first, and its output is passed to the next command as input. There is also a separate channel for errors: the standard error.

### Handing off tasks to specialist programs 

Handing over a task to another program, such as a decision to leave out a text editor component in an email client program, and replace the functionality of writing a message by launching a separate general-purpose text editor for this task. The key point is that the specialist program does not handshake with the parent while they are running. The higher-level process temporarily relinquishes control to the subprocess to perform the operation, and only returns to resume execution when the subprogram closes. Calling an external program from inside a script, program or another shell in this manner is often called **shelling out** to the called program. [^raymond-shellout]

<!--Handing off tasks to specialist programs.

**Shelling out** refers to invoking an external program or command from within a script, program, or another shell. Essentially, it's when a process temporarily hands over control to the operating system shell to execute a command and then returns to continue its execution after the command has completed.-->

### Use of tempfiles

The use of **tempfiles** as communications drops between cooperating programs is one of the oldest IPC technique there is. Despite drawbacks, tempfiles still have a niche over more elaborate methods. And sometimes, nothing else will do; The calling conventions of your child process may require that it be handed a file to operate on. [^raymond-tempfiles]

### POSIX-signals

One way for two processes on the same machine to communicate with each other is for one to send the other a signal. Signals were originally designed into unix as a way for the operating system to notify programs of certain errors and critical events (see [Chapter 7, Section: Kill signals](07-advanced-terminal.md#kill-signals)). Nevertheless, signals can be useful for some IPC situations, and the POSIX-standard signal set includes two signals intended for this use: SIGUSR1 and SIGUSR2. [^raymond-signl]

A technique often used with signal IPC is the so-called pidfile. Programs that will need to be signaled will write a small file to a known location (often in ` /var/run/ ` or the invoking user's home directory) containing their process ID (PID). Other programs can read that file to discover that PID. [^raymond-signl]

<a id="classic-shell-io"></a>

## 6.2 Classic shell IO

### Standard streams

Traditional ability of unix programs to communicate and exchange information relies on passing through simple textual information via **standard streams**. Every program has initially available to it (at least) two I/O data streams called standard **input** and standard **output**. They allow the combined use of commands by first executing one command and then passing the output to the next command as input. There is also a separate channel for errors: the standard **error**. <!--Most shell programs have two I/O data streams available to it: standard input and standard output. -->

### Interface patterns based on standard streams 

- **Source:** [^raymond-intpatterns]
    - Requires no input. It's output is controlled only by startup conditions.
    - A classic example would be ` $ who `, ` $ ps ` and ` $ ls `.
- **Filter:** [^raymond-intpatterns]
    - Takes data on standard input, transforms it in some fashion, and sends the result to standard output.
    - A classic example would be ` $ grep `, which prints only those lines that match the pattern given.
- **Sink:** [^raymond-intpatterns]
    - Is a filter-like program that consumes standard input, but emits nothing to standard output. <!--This interface pattern is unusual, and there are few examples.-->
- **Cantrip:** [^raymond-intpatterns]
    - Outputs only a numeric exit status (see [Section: Exit status and comparison](#exit-status-and-comparison)).
    - A classic example would be ` $ test `, ` $ rm ` and ` $ touch `.

> [!IMPORTANT]
> All these patterns have very low interactivity. Programs don't get any more scriptable than this. In addition there are also interactive design patterns and many browser like and editor like programs, but they are not quite so scriptable (as in generating sequences of commands). [^raymond-intpatterns]

> [!NOTE]
> Some commands such as ` $ echo ` do not read their standard input.

### Redirection of standard streams

Programs such as ` $ ls ` actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another special file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a regular file. I/O redirection allows us to change where that output goes.

<a id="file-descriptor"></a>

#### File descriptor <!--update internal links if changed-->

Standard streams are associated with an a **file descriptor** (FD). It is an identifier used by a processes to refer to an I/O resource such as a terminal window, pipe, or text file.
- If the program output is sent to the printer's file descriptor, it is printed on paper (such as ` > /dev/usb/lp0 `).
- If the program output is sent to a file descriptor of a terminal window, the program output is displayed on the terminal window (such as ` > /dev/pts/1 `).
- You could also redirect output from one terminal window to another such as ` > /dev/pts/2 `.

The shell file descriptors are:
- **FD 0** = ` /dev/stdin ` = Standard Input
- **FD 1** = ` /dev/stdout ` = Standard Output
- **FD 2** = ` /dev/stderr ` = Standard Error

> [!TIP]
> You can verify file descriptors with the following command:
>
> ```
> $ ls -l /proc/self/fd↵
> total 0
> lrwx------ 1 margaret 64 10. 5. 10:51 0 -> /dev/pts/1
> lrwx------ 1 margaret 64 10. 5. 10:51 1 -> /dev/pts/1
> lrwx------ 1 margaret 64 10. 5. 10:51 2 -> /dev/pts/1
> lr-x------ 1 margaret 64 10. 5. 10:51 3 -> /proc/8468/fd
> # /dev/pts stands for pseudo terminal slave
> ```

<!-- Every file has an associated **file descriptor (FD)** number. When a program is executed the output is sent to file descriptor of the screen, and you see program output on your monitor. If the output is sent to file descriptor of the printer, the program output will be printed. -->

#### Redirection to a file

To redirect standard output to a regular file instead of the screen, we use the redirection operator ` > ` or ` >> `, followed by the target filepath.
- The redirection operator **` > `** connects the command output with a text file, **overwriting** any existing content. If the file does not exist, it will be created.
- The redirection operator **` >> `** connects the command output with a text file, **appending** and thus preserving any existing file content. If the file does not exist, it will be created.

Sometimes we don't want output from a command, we just want to throw it away. This applies particularly to error messages and status messages. Redirection to target file ` > /dev/null ` will suppress and discard all output messages. This special system file is often referred to as the bit bucket. It accepts input, and does nothing with it.

| Operator | Redirection |
|:--- |:--- |
| **` 1> `** or **` > `** | Redirect stdout to file by overwriting. |
| **` 1>> `** or **` >> `** | Redirect stdout to file by appending. |
| **` 2> `** | Redirect stderr to file by overwriting. |
| **` 2>> `** | Redirect stderr to file by appending. |
| **` &> `** | Redirect both stdout and stderr to file by overwriting. |
| **` &>> `** | Redirect both stdout and stderr to file by appending. |

#### Input redirection and substitution

By using the **input redirection** symbol **`  <  `**, you can feed input data from a file, instead of typing it:

```
$ echo ~/Documents/ > store-argument.txt↵
$ ls -la < store-argument.txt↵ # Equals: ls -la ~/Documents/
```

By using the **process substitution** operator **` <(commands) `**, you can have one or more commands inplace of typed in arguments or references to text files:

```
$ diff -y <(ls -la ~/MyProject/) <(ls -la ~/MyBackup/)↵
```

#### Pipelines

The the vertical bar **pipe operator** **`  |  `** redirects the standard output of one command into the standard input of another. Piping is analogous to water pipes.

Let's approach the topic with an example: ` $ ls -l /usr/bin | less↵ `, where the output of the list command ` $ ls ` is passed to a browser called ` $ less `. Now try up and down arrow keys to scroll through the content. Finally press press ` q ` to quit ` $ less `.

> [!NOTE]
> Programs ` $ more ` and ` $ less ` are filters for paging text one screenful at a time. More is older and primitive. Less is the enhanced version of more. The naming is a pun: *less is more*.

This second example ` $ ls -l /usr/bin | tee list.txt | less↵ ` uses ` $ tee ` to capture the data between pipes. The tee command (from capital letter T) is named after plumbing terminology for a T-shaped pipe splitter. This splits or copies the standard input, i.e. the output of the previous command, to both 1) one or more files and 2) the standard output for use by the next command as input, allowing the data to continue down the pipeline.

#### Xargs can replace standard input

<!-- Some programs such as ` $ echo ` and ` $ stat ` in ` --file-system ` mode do not read their standard input. 

In most cases there are many alternatives to achieve the same goal such as: -->

Some programs such as ` $ echo ` and ` $ stat ` in ` --file-system ` mode do not read their standard input. Many programs accept the bare hyphen **` - `** as a pseudo-filename that directs to read the standard output. But not ` $ stat ` in ` --file-system ` mode. [^ieee-echo]

[^ieee-echo]: [IEEE 1003.1 Standard: Utilities: echo, accessed 2025](https://pubs.opengroup.org/onlinepubs/9799919799/utilities/echo.html#tag_20_37_06)

```
# This attempt will not work as intended:
$ which ls & stat --file-system -↵
standard input does not work in file system mode

# This attempt will not work as intended:
$ stat --file-system <(which ls)↵
  File: "/dev/fd/63"
    ID: e00000000 Namelen: 255     Type: pipefs
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 0          Free: 0          Available: 0
Inodes: Total: 0          Free: 0
```

If you need to pipe in a command that does not accept standard input you may use ` $ xargs `. <!--It performs an interesting function; --> It converts standard input into an argument list for another command.

```
# These alternatives achieve the same goal:
$ which ls | xargs stat -f↵     # Equals: $ stat -f /usr/bin/ls
$ which ls | stat -f `xargs`↵   # Equals: $ stat -f /usr/bin/ls
$ which ls | stat -f $(xargs)↵  # Equals: $ stat -f /usr/bin/ls
File: "/usr/bin/ls"
    ID: 62851ebc76790d48 Namelen: 255     Type: ext2/ext3
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 24159833   Free: 18766614   Available: 17527818
Inodes: Total: 6176768    Free: 5672251
```

#### Xargs can divide series

One can use the ` -n # ` argument to delimit standard input by space, to make the specified command execute multiple times with any initial arguments followed by items read from standard input:

```
$ echo {2007..2009}-{01..12}↵
2007-01 2007-02 2007-03 2007-04 2007-05 2007-06 2007-07 2007-08 2007-09 2007-10 2007-11 2007-12 2008-01 2008-02 2008-03 2008-04 2008-05 2008-06 2008-07 2008-08 2008-09 2008-10 2008-11 2008-12 2009-01 2009-02 2009-03 2009-04 2009-05 2009-06 2009-07 2009-08 2009-09 2009-10 2009-11 2009-12

$ echo {2007..2009}-{01..12} | xargs -n 12 echo "Row:"↵
Row: 2007-01 2007-02 2007-03 2007-04 2007-05 2007-06 2007-07 2007-08 2007-09 2007-10 2007-11 2007-12
Row: 2008-01 2008-02 2008-03 2008-04 2008-05 2008-06 2008-07 2008-08 2008-09 2008-10 2008-11 2008-12
Row: 2009-01 2009-02 2009-03 2009-04 2009-05 2009-06 2009-07 2009-08 2009-09 2009-10 2009-11 2009-12

$ echo {2007..2009}-{01..12} | xargs -n 1 echo "Row:"↵
Row: 2007-01
Row: 2007-02
Row: 2007-03
Row: 2007-04
Row: 2007-05
Row: 2007-06
Row: 2007-07
...
```

#### Xargs is able to ask for confirmation

The ` -p ` option comes in handy for learning as it prompts before execution:

```
$ ls | xargs -p -n 1 stat -f↵
stat -f Desktop?...no↵
stat -f dfgdf?...no↵
stat -f Documents?...yes↵
  File: "Documents"
    ID: 62851ebc76790d48 Namelen: 255     Type: ext2/ext3
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 24159833   Free: 18765868   Available: 17527072
Inodes: Total: 6176768    Free: 5672206
...
```

### Control operators

#### Sequential execution

**Semicolon ` ; `** causes sequential execution of commands, with each one running <ins>even if the previous command failed</ins>.

```
# To demonstrate, the following command will cause an alert bell sound multiple times with a one second interval:
$ echo -e "\a" ; sleep 1 ; echo -e "\a" ; sleep 1 ; echo -e "\a" ; sleep 1 ; echo -e "\a"↵
```

**Double ampersand ` && `** causes sequential execution of commands, with each one running <ins>only if the previous command did not fail</ins>. This can be especially handy for when you have a couple of commands to run, but you do not want the second to be run if the first fails.

```
$ echo Aa && echo Bb > /root/Bb.txt && echo Cc↵
Aa
bash: /root/Bb.txt: Permission denied

$ echo Aa ; echo Bb > /root/Bb.txt ; echo Cc↵
Aa
bash: /root/Bb.txt: Permission denied
Cc
```

**Double vertical bars ` || `** causes sequential execution of commands, with the last one running <ins>only if the first command failed</ins>. This type of construct is useful for handling errors in scripts.

```
$ test -e ~/Desktop && echo "Path found" || echo "Path not found"↵
Path found

$ test -e ~/Desktip && echo "Path found" || echo "Path not found"↵
Path not found
```

> [!NOTE]
> A fail is interpreted as returning a non-zero exit status (see [Section: Exit status and comparison](#exit-status-and-comparison)).

#### Asynchronous execution

**Trailing ampersand `  & `** directs the shell to run the command(s) in the background, in a separate sub-shell, as a job, asynchronously. This way you can continue using the shell, and not have to wait for the command(s) to terminate such as:

```
$ sleep 4 & sleep 2 &↵
[1] 12712
[2] 12713
$ _         # You can continue typing here straight away
```

Usually, if you run a text editor (such as gedit) from the terminal, you will be unable to continue using the terminal, until you close the text editor. But, by appending the ampersand operator, you can make it run in the background and continue to use the shell immediately:

```
$ gedit .bashrc &↵
[1] 12872
$ _         # You can continue typing here straight away
```

> [!NOTE]
> After entering the command, the shell prompt returns, but some funny numbers are printed too. This message is part of the shell and kernel maintaining information about each process to help keep things organized. Each process is assigned a process identity (PID). Type ` $ ps↵ ` to show processes associated with the current terminal session.

### GNU Grep


[GNU Grep](https://www.gnu.org/software/grep/) is a command-line tool `$ grep ` that filters standard input (or text file contents) with a regular expression. The expression can be a simple string or a very complex pattern.


> [!NOTE]
> GREP stands for global regular expression print. **Regular expression** (also referred to as regex or regexp) is a notation for creating search, extraction, match and substitution patterns for text. Regex functionality is supported in many programming languages, but also present in some software applications and commandline utilities; Especially with unix text-processing utilities.

GNU Grep supports three regular expression syntaxes: basic, extended and Perl-compatible. Especially when writing multi-system expressions, care must be taken as to which constructs are newer extensions. To interpret an expression as an extended regular expression, use the ` -E ` or ` -P ` command-line options. When writing expressions, care must also be taken as to whether the line break is treated as a regular character, only whether the input is treated line by line like GNU Grep.

The following example filters the home directory listing to files and directories starting with **` ␣D `** or **` ␣P `**:

```
$ grep -E '( D| P)' <(ls -la ~)↵
drwxr-xr-x  3 user user   4096 14. 6. 13:25 Desktop
drwxr-xr-x  2 user user   4096 10. 6. 19:51 Documents
drwxr-xr-x  5 user user   4096 10. 6. 19:25 Downloads
drwxr-xr-x  2 user user   4096 10. 6. 17:16 Pictures
drwxr-xr-x  2 user user   4096 12.11.  2023 Public
```

The regex syntax is beyond the scope of this tutorial. But those interested to learn more can start with the official perl documentation:
- [Metacharacters](https://perldoc.perl.org/perlre#Metacharacters)
- [Character classes and other special escapes](https://perldoc.perl.org/perlre#Character-Classes-and-other-Special-Escapes)

> [!TIP]
> Regular expressions make it possible to concisely express complicated matching requirements. But they can be hard to read and write. Web browser based regex-tools (such as <https://regex101.com> and <https://regexr.com>) are useful for a wide range of users, from beginners to advanced. They simplify the creation, testing and debugging of regex patterns.

<a id="exit-status-and-comparison"></a>

### Exit status and comparison 

Commands (including the scripts and shell functions we write) issue a value to the system when they terminate, called an **exit status**. This value, which is an integer in the range of 0 to 255, indicates the success or failure of the command’s execution. [^shotts-ext]
- By convention, a value of zero always indicates success and any other value indicates failure.
- Many programs simply exit with a value of 1 upon failure. But some programs (such as RAR for Linux below) use different exit status values to provide diagnostics for errors. Man-pages often include a section entitled *EXIT STATUS* describing what codes are used[^shotts-ext].

| Code | Description |
| ---:|:--- |
| 0 | Successful operation. |
| 1 | Warning. Non fatal error(s) occurred. |
| 2 | A fatal error occurred. |
| 3 | Invalid checksum. Data is damaged. |
| 4 | Attempt to modify an archive locked by 'k' command. |
| 5 | Write error. |
| 6 | File open error. |
| 7 | Wrong command line option. |
| 8 | Not enough memory. |
| 9 | File create error. |
| 10 | No files matching the specified mask and options were found. |
| 11 | Wrong password. |
| 12 | Read error. |
| 255 | User stopped the process. |

> [!NOTE]
> Exit status is not printed to standard output and thus nothing gets printed on the screen. The shell provides a parameter ` $? ` that we can use to examine the exit status. Or one can construct some form of if-then-clause. See [Chapter 7, Section: Square brackets](07-advanced-terminal.md#square-brackets). 

#### Commands: true, false, exit, return

The shell provides two extremely simple builtin commands that do nothing except terminate with either exit status 0 or 1:
1. The **` $ true↵ `** command always executes successfully: ` $? ` = 0.
2. The **` $ false↵ `** command always executes unsuccessfully: ` $? ` = 1

There is also an **` $ exit #↵ `** command which accepts a single, optional argument, which becomes the script’s exit status. When no argument is passed, the exit status defaults to the exit status of the last command executed. Using ` $ exit ` command in this way allows a script to indicate failure. The exit command appearing on the last line of the script is a formality though, because when a script runs off the end (i.e. reaches end of file), it terminates with an exit status of the last command executed.

Similarly internal functions in shell scripts can return an exit value by including an integer as a parameter to the command **` $ return #↵ `**, which points to the return value of the variable ` $? ` and terminates the function (see [Linuxize.com - Bash Functions: Return Values](https://linuxize.com/post/bash-functions/#return-values)). [^bash-manual-funk]

[^bash-manual-funk]: [GNU Bash Manual - Shell Functions, accessed 2025](https://www.gnu.org/software/bash/manual/html_node/Shell-Functions.html)

> The unix API doesn't use exceptions. Even the C language lacks a facility for throwing named exceptions with attached data. Thus, the C functions in the unix API indicate errors by returning a distinguished value (usually −1 or a NULL character pointer) and setting a global errno variable. In retrospect, this is the source of many subtle errors. Programmers in a hurry often neglect to check return values.

<a id="sockets"></a>

## 6.3 Sockets

All modern operating systems implement a POSIX or IEEE 1003.1 compliant version of the Berkeley socket interface for sending and receiving data between endpoints. The standard originated with BSD Unix in 1983. It became the standard interface for applications running on the Internet. Even the Winsock implementation for Microsoft Windows, created by unaffiliated developers, closely follows this standard (see [IEEE 1003.1 Standard: Sockets](https://pubs.opengroup.org/onlinepubs/9799919799/functions/V2_chap02.html#tag_16_10)). [^wiki-bsd-sockets] 
The term socket is also used for the software endpoint of interprocess communication, which often uses the same API as a network socket. [^wiki-network-socket]

[^wiki-bsd-sockets]: [Wikipedia - Berkeley sockets, accessed 2024](https://en.wikipedia.org/wiki/Berkeley_sockets)

[^wiki-network-socket]: [Wikipedia - Network socket, accessed 2024](https://en.wikipedia.org/wiki/Network_socket)

POSIX sockets are usually the right thing to use for bidirectional IPC no matter where your cooperating processes are located. Sockets are supported on all modern operating systems such as GNU/Linux, Windows, and macOS. [^raymond-psock]

> Two programs communicating over a socket typically see a bidirectional byte stream. There are other socket modes and transmission methods, but they are of only minor importance. [^raymond-psock]
>
> The byte stream is sequenced and reliable. That is, even individual bytes are received in transmission order and socket users are guaranteed that the underlying network will perform error detection and retry if necessary to ensure delivery. [^raymond-psock]

<a id="dee-bus"></a>

### D-Bus 

Many GNU/Linux applications can communicate with each other via D-Bus. **D-Bus** is a message-oriented middleware mechanism that allows communication between multiple processes running concurrently on the same machine.  [^free-bus]

[^free-bus]: [Freedesktop Wiki - What is D-Bus?, accessed 2024](https://www.freedesktop.org/wiki/Software/dbus/)

> D-Bus is part of the [Freedesktop.org](https://www.freedesktop.org/wiki/Specifications/) project. The goal of Freedesktop.org is to create open standards and interoperability between different GNU/Linux-based desktop environments. Most Freedesktop.org projects are designed to be independent of any specific desktop environment, and improve their compatibility.

a) D-Bus can be a mediator for many programs. For example, information on an incoming voice-call received through Bluetooth or VoIP can be propagated and interpreted by any currently-running music player, which can react by muting the volume or by pausing playback until the call is finished. [^free-bus]
    - Clients should instruct the bus that they are interested in receiving certain signals from a particular object, since a D-Bus bus only passes signals to those processes with a registered interest in them. [^free-bus]
b) In addition, any two applications can use the communication bus to communicate with each other. <!--, directly without communication via the dbus [daemon](https://dbus.freedesktop.org/doc/dbus-daemon.1.html) message bus.-->
    - The D-Bus bus makes it simple and reliable to code a *single instance* application. That is, a program that limits itself to executing only one instance at a time. In this case, the D-Bus message is a means of passing to the first instance the command line arguments received by the second instance at startup (before it closes).

> [!TIP]
> Desktop application [GNOME D-Spy](https://gitlab.gnome.org/GNOME/d-spy) is a simple GUI for browsing existing bus names, objects, interfaces, methods and signals in a D-Bus.

<!-- # References -->

[^shotts-ext]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 27, Section: Exit Status](http://linuxcommand.org/tlcl.php)

[^raymond-shellout]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 7<!--. Multiprogramming-->, Section: Handing off Tasks<!-- to Specialist Programs-->](http://www.catb.org/~esr/writings/taoup/html/ch07s02.html)

[^raymond-tempfiles]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 7<!--. Multiprogramming-->, Section: Tempfiles](http://www.catb.org/~esr/writings/taoup/html/ch07s02.html)

[^raymond-signl]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 7<!--. Multiprogramming-->, Section: Signals](http://www.catb.org/~esr/writings/taoup/html/ch07s02.html)

[^raymond-intpatterns]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 11<!--. Interfaces-->, Section: Unix Interface Design Patterns](http://www.catb.org/~esr/writings/taoup/html/ch11s06.html)

[^raymond-psock]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 7<!--. Multiprogramming-->, Section: Sockets](http://www.catb.org/~esr/writings/taoup/html/ch07s02.html)

