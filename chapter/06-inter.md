<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="05-links.md">&lt;&lt; Previous Chapter: 5 - Links</a>
     |
  <a href="07-advanced-terminal.md">Next&nbsp;Chapter:&nbsp;7&nbsp;&#8209;&nbsp;Advanced&nbsp;terminal&nbsp;usage&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 6 - Interoperability

**Interoperability** or **interprocess communication (IPC)** is the ability of software processes to talk to each other and work together with little effort from the user. Such modularity and extensibility is one of the oldest and most persistent design tropes of unix. The power of a system comes more from the relationships among programs, than from the programs themselves.

<a id="ipc-techniques"></a>

## 6.1 Simple IPC Techniques [^raymond]

Unix has always provided several ways for processes to communicate relatively easy:

1. The simplest of all design patterns is having no input and no output; Just a **numeric exit status** (see [Section: Exit status and comparison](#exit-status-and-comparison)). Good examples for use of such mechanic are commands ` $ test `, ` $ rm ` and ` $ touch `
    - ` $ test -r <file>↵ ` = True if the file exists and is readable.
    - ` $ test -w <file>↵ ` = True if the file exists and is writable.
    - ` -u `, ` -g `, ` -k ` = True if the file exists and has the setuid, setgid or sticky bit set.

2. Simple, transparent, **textual data formats** that can be passed through pipes and sockets, that enable the combined use of commands by first executing one command and then passing the output as input to the next command. Most shell programs have two I/O data streams available to it: **Standard input** and **standard output** (see [Section: File descriptor](#file-descriptor)).

3. <ins>Handing off tasks to specialist programs.</ins> They key point is that the specialist program does not handshake with the parent while they are running. Thus this is often called **shelling out** to the called program.

4. The use of **tempfiles** as communications drops between cooperating programs is one of the oldest IPC technique there is. Despite drawbacks, tempfiles still have a niche over more elaborate methods. And sometimes, nothing else will do; The calling conventions of your child process may require that it be <ins>handed a file to operate on</ins>.

5. One way for two processes on the same machine to communicate with each other is for one to send the other a signal. **Signals** were originally designed into unix as a way for the operating system to notify programs of certain errors and critical events (see [Chapter 7, Section: Kill signals](07-advanced-terminal.md#kill-signals)). Nevertheless, signals can be useful for some IPC situations (and the POSIX-standard signal set includes two signals, SIGUSR1 and SIGUSR2, intended for this use).
    - A technique often used with signal IPC is the so-called **pidfile**. Programs that will need to be signaled will write a small file to a known location (often in /var/run or the invoking user's home directory) containing their process ID (PID). Other programs can read that file to discover that PID.

<a id="classic-shell-io"></a>

## 6.2 Classic shell IO

### CLI interface patterns [^raymond]

There can be different CLI interface design patterns for a) Novice and nontechnical end-users and b) Those which serve expert users and maximize scriptability. Unix is in many ways better adapted to the needs of power users.

Every program has initially available to it (at least) two I/O data streams called standard input and standard output.
- A **source** program requires no input, it's output is controlled only by startup conditions. A classic example would be ` $ who `, ` $ ps ` and ` $ ls `.
- A **filter** program takes data on standard input, transforms it in some fashion, and sends the result to standard output. A classic example would be ` $ grep `, which prints only those lines that match the pattern given.
- A **sink** program is a filter-like program that consumes standard input, but emits nothing to standard output. This interface pattern is unusual, and there are few examples.
- A **cantrip** program outputs only a numeric exit status. A classic example would be ` $ test `, ` $ rm ` and ` $ touch `.

All these patterns have very low interactivity. Programs don't get any more scriptable than this. In addition there are also interactive design patterns and many browser like and editor like programs, but they are not quite so scriptable (as in generating sequences of commands).

### I/O redirection

<a id="file-descriptor"></a>

#### File descriptor <!--update internal links if changed-->

Every file has an associated **file descriptor (FD)** number. When a program is executed the output is sent to file descriptor of the screen, and you see program output on your monitor. If the output is sent to file descriptor of the printer, the program output will be printed.

The shell file descriptors are:
- FD 0 = **stdin** = Standard Input
- FD 1 = **stdout** = Standard Output
- FD 2 = **stderr** = Standard Error

Programs such as ` $ ls ` actually send their results to a *special file* called **standard output** (often expressed as stdout) and their status messages to another *special file* called **standard error** (stderr). By default, both standard output and standard error are linked to the screen and not saved into a regular file.
- I/O redirection allows us to change where that output goes. To redirect standard output to a regular file instead of the screen, we use the redirection operator ` > `, followed by the target filepath.
- The target file can be ` /dev/null ` to suppress messages from the command. The ` /dev/null ` is a special system file often referred to as the bit bucket, which accepts input and does nothing with it. Sometimes we don't want output from a command, we just want to throw it away. This applies particularly to error messages and status messages.

> [!NOTE]
> Some commands such as ` $ echo ` do not read their standard input.

#### Redirection to a file

The **redirection operator ` > `** connects a command with a file. Using the **append operator ` >> `** will result in the output being appended to the file. If the file does not already exist, it is created just as though the ` > ` operator had been used.

| Operator | Redirection |
| --- | --- |
| **` 1> `** or **` > `** | Redirect stdout to file by overwriting. |
| **` 1>> `** or **` >> `** | Redirect stdout to file by appending. |
| **` 2> `** | Redirect stderr to file by overwriting. |
| **` 2>> `** | Redirect stderr to file by appending. |
| **` &> `** | Redirect both stdout and stderr to file by overwriting. |
| **` &>> `** | Redirect both stdout and stderr to file by appending. |

The numbers 1 and 2 are file descriptors (see [Section: File Descriptor](#file-descriptor))

#### Input redirection and substitution

By using the **input redirection** symbol **`  <  `**, you can take input data from a file instead of typing it:

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

Let's try piping with an example: ` $ ls -l /usr/bin | less↵ `
- Now try up and down arrow keys to scroll through the content, and ` q ` to quit.
- ` $ more ` and ` $ less ` are filters for paging text one screenful at a time. More is older and primitive. Less is the enhanced version of more. The naming is a pun: Less is more.

Let's continue with another example: ` $ ls -l /usr/bin | tee list.txt | less↵ `
- Here ` $ tee ` is used to capture the data between pipes. The tee command (from capital letter T) is named after plumbing terminology for a T-shaped pipe splitter. This splits or copies the standard input (i.e. the output of the previous command) to both 1) one or more files and 2) the standard output for use by the next command as input, allowing the data to continue down the pipeline.

#### Xargs

Some programs such as ` $ echo ` and ` $ stat ` in ` -f ` mode do not read their standard input. If you need to pipe in a command that doesn’t accept standard input you may use ` $ xargs `, which performs an interesting function; It converts standard input into an argument list for another command. In most cases there are many alternatives to achieve the same goal such as:

```
# a) Will not work as intended
$ which ls & stat -f -↵
standard input does not work in file system mode

# b) Will not work as intended
$ stat -f <(which ls)↵
  File: "/dev/fd/63"
    ID: e00000000 Namelen: 255     Type: pipefs
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 0          Free: 0          Available: 0
Inodes: Total: 0          Free: 0

# c, d, e) Will work as intended
$ which ls | xargs stat -f↵     # Equals: $ stat -f /usr/bin/ls
$ which ls | stat -f `xargs`↵   # Equals: $ stat -f /usr/bin/ls
$ which ls | stat -f $(xargs)↵  # Equals: $ stat -f /usr/bin/ls
File: "/usr/bin/ls"
    ID: 62851ebc76790d48 Namelen: 255     Type: ext2/ext3
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 24159833   Free: 18766614   Available: 17527818
Inodes: Total: 6176768    Free: 5672251
```

One can use the ` -n # ` argument to delimit standard input by space, to make the specified command execute multiple times (with any initial arguments followed by items read from standard input):

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

**Semicolon ` ; `** causes sequential execution of commands, with each one running <ins>even if the previous command failed</ins>. To demonstrate, the following command will cause an alert bell sound multiple times with a one second interval:

```
$ echo -e "\a" ; sleep 1 ; echo -e "\a" ; sleep 1 ; echo -e "\a" ; sleep 1 ; echo -e "\a"↵
```

**Double ampersand ` && `** causes sequential execution of commands, with each one running <ins>only if the previous command did not fail</ins>. This can be especially handy for when you have a couple of commands to run, but you don’t want the second to be run if the first fails.

```
$ echo Aa && echo Bb > /root/Bb.txt && echo Cc↵
Aa
bash: /root/Bb.txt: Permission denied

$ echo Aa ; echo Bb > /root/Bb.txt ; echo Cc↵
Aa
bash: /root/Bb.txt: Permission denied
Cc
```

**Double vertical bars ` || `** causes sequential execution of commands, with the last one running <ins>only if the first command failed</ins>. This type of construct is useful for handling errors in (scripts).

```
$ test -e ~/Desktop && echo "Path found" || echo "Path not found"↵
Path found

$ test -e ~/Desktip && echo "Path found" || echo "Path not found"↵
Path not found
```

> [!NOTE]
> A fail is interpreted as returning a non-zero exit status (see [Section: Exit status and comparison](#exit-status-and-comparison)).

#### Asynchronous execution

**Trailing ampersand `  & `** directs the shell to run the command(s) in the background, in a separate sub-shell, as a job, asynchronously. This way you can continue using the shell, and not have to wait for the command(s) to terminate.

For example:

```
$ sleep 4 & sleep 2 &↵
[1] 12712
[2] 12713
$           # You can continue typing here straight away
```

Usually, if you run a text editor (such as gedit) from the terminal, you will be unable to continue using the terminal, until you close the text editor. But, by appending the ampersand operator, you can make it run in the background and continue to use the shell immediately:

```
$ gedit .bashrc &↵
[1] 12872
$           # You can continue typing here straight away
```

> [!NOTE]
> After entering the command, the shell prompt returns, but some funny numbers are printed too. This message is part of the shell and kernel maintaining information about each process to help keep things organized. Each process is assigned a PID (Process Identity). Type ` $ ps↵ ` to show processes associated with the current terminal session.

### Grep

**Grep** is short for Global Regular Expression Print.

**Regular expressions** (regex or regexp) are search patterns supported in many programming languages, but also present in some software applications and commandline utilities; Especially with unix text-processing utilities. Regular expressions make it possible to concisely express complicated matching requirements. But they can be hard to read and write.

**`$ grep `** filters standard input (or text file contents) with a regular expression, which can be a simple string or a very complex pattern.
- GNU grep supports three regular expression syntaxes: Basic, Extended and Perl-compatible. To interpret the pattern as an extended regular expression, use the ` -E ` or ` -P ` option.

> [!NOTE]
> The regex syntax is beyond the scope of this tutorial. But those interested to learn more can start with the official Perl Documentation:
>
> - [Metacharacters](https://perldoc.perl.org/perlre#Metacharacters)
> - [Character Classes and other Special Escapes](https://perldoc.perl.org/perlre#Character-Classes-and-other-Special-Escapes)

The following example filters the home dir listing to files and directories starting with " D" or " P":

```
$ grep -E '( D| P)' <(ls -la ~)↵
drwxr-xr-x  3 user user   4096 14. 6. 13:25 Desktop
drwxr-xr-x  2 user user   4096 10. 6. 19:51 Documents
drwxr-xr-x  5 user user   4096 10. 6. 19:25 Downloads
drwxr-xr-x  2 user user   4096 10. 6. 17:16 Pictures
drwxr-xr-x  2 user user   4096 12.11.  2023 Public
```

<a id="exit-status-and-comparison"></a>

### Exit status and comparison [^shotts]

[^shotts]: [William Shotts - The Linux Command Line, updated 2019](http://linuxcommand.org/tlcl.php)

Commands (including the scripts and shell functions we write) issue a value to the system when they terminate, called an **exit status**. This value, which is an integer in the range of 0 to 255, indicates the success or failure of the command’s execution.
- By convention, a value of zero always indicates success and any other value indicates failure.
- Many programs simply exit with a value of 1 upon failure. But some programs (such as RAR for Linux below) use different exit status values to provide diagnostics for errors. Man pages often include a section entitled “Exit Status,” describing what codes are used.

| Code | Description |
| ---:| --- |
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
> The shell provides two extremely simple builtin commands that do nothing except terminate with either exit status 0 or 1. The **` $ true↵ `** command always executes successfully (0) and the **` $ false↵ `** command always executes unsuccessfully (1). There is also an **` $ exit #↵ `** command which accepts a single, optional argument, which becomes the script’s exit status. When no argument is passed, the exit status defaults to the exit status of the last command executed. Using ` $ exit ` command in this way allows a script to indicate failure. The exit command appearing on the last line of the script is a formality though, because when a script runs off the end (i.e. reaches end of file), it terminates with an exit status of the last command executed. Similarly, shell functions can return an exit status by including an integer argument to the **` $ return #↵ `** command.

> The unix API doesn't use exceptions. Even the C language lacks a facility for throwing named exceptions with attached data. Thus, the C functions in the unix API indicate errors by returning a distinguished value (usually −1 or a NULL character pointer) and setting a global errno variable.
> - In retrospect, this is the source of many subtle errors. Programmers in a hurry often neglect to check return values.

<a id="sockets"></a>

## 6.3 Sockets

All modern operating systems implement a version of the Berkeley socket interface that originated with a 1983 BSD Unix. It became the standard interface for applications running in the Internet. Even the Winsock implementation for Microsodt Windows, created by unaffiliated developers, closely followed the standard. [^wiki-bsd-sockets] The term socket is also used for the software endpoint of interprocess communication, which often uses the same API as a network socket. [^wiki-network-socket]

[^wiki-bsd-sockets]: [Wikipedia - Berkeley sockets, accessed 2024](https://en.wikipedia.org/wiki/Berkeley_sockets)

[^wiki-network-socket]: [Wikipedia - Network socket, accessed 2024](https://en.wikipedia.org/wiki/Network_socket)

> [!NOTE]
> The use of the term socket in software is analogous to the function of an electrical connector.

Sockets are usually the right thing to use for bidirectional IPC no matter where your cooperating processes are located. Sockets are supported in all recent unices, under Windows, and under classic macOS as well.
- Two programs communicating over a socket typically see a bidirectional byte stream (there are other socket modes and transmission methods, but they are of only minor importance). The byte stream is both 1) sequenced (that is, even single bytes will be received in the same order sent) and 2) reliable (socket users are guaranteed that the underlying network will do error detection and retry to ensure delivery). [^raymond]

<a id="d-bus"></a>

### D-Bus [^free-bus]

[^free-bus]: [Freedesktop Wiki - What is D-Bus?, accessed 2024](https://www.freedesktop.org/wiki/Software/dbus/)

**D-Bus** is a <ins>message-oriented</ins> middleware mechanism that allows communication between multiple processes running concurrently on the same machine. D-Bus is part of the freedesktop.org project and many GNU / Linux applications have the ability to communicate with each other through D-Bus.
- a) D-Bus can be a mediator for many programs. For example, information on an incoming voice-call received through Bluetooth or VoIP can be propagated and interpreted by any currently-running music player, which can react by muting the volume or by pausing playback until the call is finished.
    - Clients should instruct the bus that they are interested in receiving certain signals from a particular object, since a D-Bus bus only passes signals to those processes with a registered interest in them.
    - Browsing the existing bus names, objects, interfaces, methods and signals in a D-Bus bus using ` D-Feet ` package.
- b) Also, the message bus can be used by any two apps to communicate directly without going through the message bus daemon.
    - D-Bus makes it simple and reliable to code a "single instance" application, a program that restricts itself to running only one instance at a time. And a way for the second instance to pass any command line arguments to the original instance before exit.

<!-- # References -->

[^raymond]: [Eric Steven Raymond - The Art of Unix Programming, published 2003](https://www.arp242.net/the-art-of-unix-programming/)


