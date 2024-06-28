<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="01-intro.md">&lt;&lt; Previous Chapter: 1 - Introduction</a>
     |
  <a href="03-basic-terminal.md">Next&nbsp;Chapter:&nbsp;3&nbsp;&#8209;&nbsp;Basic&nbsp;terminal&nbsp;usage&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 2 - Basics

GNU / Linux has been considered difficult for beginners. Learning to use GNU / Linux can seem frustrating because the system was designed from a different perspective than, say, Windows (or its predecessor, MS-DOS), and many things are handled very differently. But keep in mind that no one learns to use a computer effectively in a week or two, even with Windows. In order to use GNU / Linux effectively, it's a good idea to learn the basics of the system, as well as something about it's history. [^linufi] I strongly suggest to check out [Chapter&nbsp;1](01-intro.md), incase you skipped it.

[^linufi]: [Linux.fi ohjesivusto - Aloittelijalle, accessed 2021](https://www.linux.fi/wiki/Aloittelijalle)

<a id="disk-partitioning"></a>

## 2.1 Disk partitioning

When partitioning a storage disk for GNU / Linux, it is important to give the (U)EFI boot partition at least 500 MB of space. The 100 MB created by Windows is too small. Problems may occur when the Linux kernel is updated. Everything may seem to work, but the Linux kernel, for example, doesn't update, and you don't even get an error message about it. Otherwise, the complex disk partitioning traditionally used in GNU / Linux distributions (even single-disk configurations) is no longer necessary on today's home computers; And it has little use in home use today. If the disk system is partitioned the old style and runs out of space, then in the worst case, the machine may even crash.

> The first function created for Linux at the request of an outsider was the ability to extend main memory with swap memory, completed on Christmas Day 1991. Torvalds ’own 386 machine (which was assembled from parts, unbranded) had four megabytes of memory, but users with a smaller number (especially one German user who originally made the request) were in trouble with the lack of main memory. This feature was significant in early 1992 because it played a major role in system performance and contributed positively to the Linux kernel. In Linux, the swap space has traditionally been located on a separate hard disk partition with its own file system optimized for swap use. The speed advantage achieved in this way is now so marginal that the same can be done well by taking the space available for virtual memory from a standard disk partition. In addition, the need for swaps has decreased or even disappeared as the amount of main memory increased. At the same time, the opposite of swap is common, in which files in mass memory, which are often needed, are copied to main memory to speed up their reading.

<a id="introduction-to-the-text-interface"></a>

## 2.2 Introduction to the text interface

**Interface** is the sum of all the ways that a program communicates with human users and other programs. Much of Unix-community tradition about program interface design may seem odd and arbitrary when you encounter that tradition for the first time (or even downright regressive, in the era of graphical user interfaces). But in spite of various blemishes and irregularities, that tradition has an inner logic to it which is worth learning and understanding. It reflects heuristics accumulated over Unix's long history about ways to do effective communication both with human beings and with other programs. [^raymond]

<a id="retained-utility"></a>

### Text interface has retained its utility [^raymond]

Weak **GUI** facilities (i.e. Graphical User Interfaces) in a modern operating system are considered a problem. The Unix lesson is the opposite, that weak text-based **CLI** facilities (i.e. Command Language Interfaces) are a less obvious but equally severe deficit. If the CLI facilities of an operating system are weak or nonexistent, you'll also see the following consequences:

- Remote system administration will be sparsely supported, more difficult to use, and more network-intensive.
- Background processes (i.e. servers and daemons) will probably be difficult to program in any graceful way.
- Even simple noninteractive programs will incur the overhead of a GUI.
- Programs will not be designed to cooperate with each other in unexpected ways (see remark below), because they can't be; Outputs aren't usable as inputs.

> Unix was always agnostic about its intended audience and designers. They expect the output of every program to become the input to another, as yet unknown, program. The implementers never assumed they knew all the potential uses the system could and would be put to.

The disadvantage of the CLI style, of course, is that it almost always has high mnemonic load (low ease), and usually has low transparency. Most people (especially non-technical end users) find such interfaces relatively cryptic and difficult to learn.

Resistance to command language interface tends to decrease as users become more expert. In many problem domains, users (especially frequent users) reach a crossover point at which the concision and expressiveness of CLI becomes more valuable than avoiding its mnemonic load.

Computing novices prefer the ease of GUI desktops, but experienced users often gradually discover that typing commands to a shell tend to gain utility as problems scale up and involve more in the way of canned, procedural and repetitive actions.

- Thus, for example, a WYSIWYG desktop-publishing program is usually the easiest route to composing relatively small and unstructured documents such as business letters. But for complex book-sized documents that are assembled from sections and may require many global format changes or structural manipulation during composition, a minilanguage formatter such as LaTex or some XML-markup processor is usually a more effective choice.

The CLI style of early Unix has retained its utility long after the demise of teletypes for reasons that

- CLI interfaces are highly scriptable (they readily support the combining of programs). The **scriptability** of an interface is the ease with which it can be manipulated by other programs. Scriptable programs are readily usable as components by other programs, reducing the need for costly custom coding and making it relatively easy to automate repetitive tasks. It is a quiet but tremendous productivity booster not available in most other software environments. GUIs are simply not scriptable at all. Every interaction with them has to be human-driven. Instead of an executive who gives high-level instructions, the user is reduced to an assembly-line worker who must carry out the same task over and over.
- Usually (though not always) CLIs have an advantage in **concision** as well. Consider modifying the color table in a graphic image. If you want to change one color (say, to lighten it by an amount you will only know is right when you see it) a visual dialogue with a color-picker widget is almost mandatory. But suppose you need to replace the entire table with a set of specified RGB values, or to create and index large numbers of thumbnails. These are operations that GUIs usually lack the expressive power to specify. Even when they do, invoking a properly designed CLI or filter program will do the job far more concisely.

Even on modern systems the graphical programs are likely calling (~40 year old) simple CLI utilities in the background (to do much of the heavy lifting).

<a id="command-language-interface"></a>

### I - Command Language Interface

**Command Language Interface** is a form of interface between the operating system and the user in which the user types commands, using a special command language (see [Section: Command language](#command-language)).

> Although systems with command language interfaces are usually considered more difficult to learn and use than those with graphical interfaces, command-based systems are usually programmable; This gives them flexibility unavailable in graphics-based systems that do not have a programming interface.

<a id="command-language"></a>

### II - Command Language

**Command Language** is a language for job control in computing. It is a domain-specific and interpreted language. Common examples of a command language are *shell for unices* or *batch for DOS/Windows*. These languages can be used directly at the command line (**interactive**), but can also automate tasks (that would normally be performed manually at the command line).

> As command languages are optimized for **interactive** use: strings don't require quotation marks, most commands are executed immediately after they're entered, most things you do with it will invoke external programs rather than built-in features, and so forth.

Command languages share the domain of lightweight automation with scripting languages, though a command language usually has stronger coupling to the underlying operating system. Command languages often have a more simple grammar and syntax compared to scripting languages. Another distinction between command languages and many scripting languages is that command languages are read, parsed, and executed in order. A syntax error in the middle of a command language script won't be detected until execution reaches it. A Perl or Python script, by contrast, is parsed completely before execution begins (This is a significant difference, but it doesn't mark a sharp dividing line. If anything it makes Perl and Python more similar to compiled languages).

<a id="command-language-interpreter"></a>

### III - Command Language Interpreter [^hoffman]

[^hoffman]: [Chris Hoffman - What's the difference between Bash and other shells?](https://www.howtogeek.com/68563/htg-explains-what-are-the-differences-between-linux-shells/#:~:text=The%20most%20prominent%20progenitor%20of,worked%20at%20AT%26T's%20Bell%20Labs.)

A **shell** is first and foremost a **command language interpreter** i.e. **command processor**. A command language interpreter executes commands read from a) a command line string, b) the standard input, or c) a specified file. The shell is implementing a *command language interface*, when it communicates with the OS's kernel through user input commands. A specific shell (such as bash) always refers to the interpreter, but often also to the language that it interprets; As many shells such as bash are also an **interpreted language**.

When you sign in at the command line or launch a terminal window on GNU / Linux, the system launches a shell program. The shell programs are also used in the background by various system services. GNU / Linux distributions include many functions written as shell scripts. These scripts are commands and other advanced functions that run through a shell environment.

> Most Unix-like systems contain the file ` /bin/sh ` that is either the Bourne shell, or a symbolic link, or hard link, to a compatible shell (most commonly to /bin/bash).

Most GNU / Linux distributions include the bash shell by default. But you can swap out the default shell for another one, if you like.
- The first shell environment was the **Thompson Shell**, developed at Bell Labs and released in 1971. Shell environments have been building on the concept ever since, adding a variety of new features, functionality, and speed improvements. For example, Bash offers command and file name completion, advanced scripting features, a command history, configurable colors, command aliases, and a variety of other features that weren’t available back in 1971 when the first shell was released.
- The most prominent progenitor of modern shells is the **Bourne Shell** (also known as **sh**) which was named after its creator Stephen Bourne who worked at AT&T’s Bell Labs. Released in 1979, it became the default command-interpreter in Unix because of its support for command substitution, piping, variables, condition testing, and looping, along with other features. It did not offer much customization for users, and didn’t support such modern niceties as aliases, command completion, and shell functions (though this last one was eventually added).
- The **C shell**, or **csh**, was developed in the late 1970s by Bill Joy at University of California, Berkley. It added a lot of interactive elements with which users could control their systems, like aliases (shortcuts for long commands), job management abilities, command history, and more. Over time, lots of people fixed bugs in and added features to the C shell, culminating in an improved version of csh known as **tcsh**.
- David Korn from Bell Labs worked on the **KornShell**, or **ksh**, which tried to improve the situation by being backwards-compatible with the Bourne shell’s language but adding many features from the csh shell. It was released in 1983, but under a proprietary license. It wasn’t free software until the 2000s, when it was released under various open-source licenses.
- The GNU Project developed a free software shell to be part of its free operating system and named it the **Bourne Again Shell**, or **bash**. Bash has been improved in the decades since its first release in 1989 and remaind still the default shell on most GNU+Linux distributions today. It’s also the default shell on Apple’s macOS.

While the Linux community has settled on bash in the years since, developers didn’t stop creating new shells.
- Kenneth Almquist created a Bourne Shell clone known as **Almquish Shell**, also known as **A Shell** and **ash**. It was also POSIX compatible and became the default shell in BSD, a different branch of Unix. The ash shell is more lightweight than bash, which makes it popular in embedded Linux systems.
- Debian developed a shell environment based on ash and called it **dash**. It’s designed to be POSIX-compliant and lightweight, so it’s faster than bash, but won’t have all its features. Ubuntu uses the dash shell as its default shell for non-interactive tasks, speeding up shell scripts and other tasks running in the background. Ubuntu still uses bash for interactive shells, however, so users still have the full-featured interactive environment.
- One of the most popular newer shells is **Z Shell**, or **zsh**. Created by Paul Falstad in 1990, zsh is a Bourne-style shell that contains the features you’ll find in bash, plus even more. For example, zsh has spell-checking, the ability to watch for logins/logouts, some built-in programming features like bytecode, support for scientific notation in syntax, allows for floating-point arithmetic, and more features.
- Another newer shell is the **Friendly Interactive Shell**, or **fish**, released in 2005. It has a unique command language syntax that’s designed to be a bit easier to learn, but what you learn through using fish won’t help you Bourne-derived shells.

You don’t need to choose a shell. Your operating system chooses your default shell for you. Sit down in front a GNU / Linux distribution (or a Mac) and you’ll almost always have a bash shell environment. On embedded Linux systems or BSD systems, you’ll end up with the (Bourne-based) ash shell.
- It’s easy to switch to a new shell to try it out. Just install the shell from your distribution’s package manager and type the command (such as ` $ sh↵ `, ` $ dash↵ `, ` $ zsh ↵ `) to launch the shell. Then type ` $ exit↵ ` at the shell to leave it and return to your current shell.
- You can generally use the ` $ chsh↵ ` (Change Shell) command to change the default shell you see when you sign in, known as your *login shell*. See tip below, if you strugle to cancel the default login shell change -operation.

> [!TIP]
> Stopping the current program or operation in a terminal session could be overwhelming when you are new to the terminal emulator. You may try the following keyboard shortcuts to exit some commandline situations:
>
> | Keys | Use case |
> |:--- |:--- |
> | ` Ctrl + D ` | End text input |
> | ` Ctrl + C ` | Interrupt current process |
> | ` q ` | Quit ` $ less ` and ` $ more ` |
> | ` Ctrl + X ` | Exit ` $ nano ` |
> | ` Ctrl + X, Ctrl + C ` | Exit ` $ emacs ` |
> | ` Esc, :qa!, Ent ` | Exit ` $ vi ` |
> | ` Alt + F4 ` | Close current window |

### IV - Command Prompt

The dollar sign (<span>$</span>) or hash mark (#) known also as the number sign or pound sign, means that the shell is ready to accept commands from the terminal. The dollar sign suggests that you are working as a regular user in Linux. While working as a super user (i.e. root user) the hash mark is displayed. By contrast the traditional C shell prompt is a percent sign (<span>%</span>).

What is the origin of the UNIX dollar prompt?
- Version 7 UNIX released in 1979 was the first to have the dollar sign. That’s the release which introduced the Bourne Shell, replacing the Thompson Shell used in previous versions of Unix.Version 6 UNIX didn't have the dollar sign. (The author of Bourne Shell, Steve Bourne was an employee at Bell Labs.)
- Back in 6th edition days and before, UNIX was distributed with full source code included; Before UNIX was sold commercially. So the switch to a dollar sign could be related to commercialisation of UNIX and it's <span>$</span>hell.

> The Unix **Shell Prompt** is the equivalent of the Windows **Command Prompt**
>
> - **Shell** = the outer layer
> - **Prompt** = to encourage somebody to speak
> - **Command** = an order given

### Terminal Emulator

A **terminal emulator** or *terminal application* is a computer program that emulates a legacy video terminal within some other display architecture. A terminal emulator inside a graphical user interface is called a *terminal window*. A terminal provides the user a *command language interface* through a shell.

Before the Linux project expanded into a full operating system kernel, the author Linus Torvalds initially made a mere terminal emulator. That is, Linux was initially run in purely textual mode, completely without a graphical user interface. In Windows, the command line is no longer in basic use, and the ability to start the computer in command line mode is gone. In linux distributions, the command line is still in the highlighted part, for both good and bad. Graphical management tools for linux distributions have not replaced the use of the command line, as developers of distributions still find things to be handled most conveniently in text mode.

When Linux first came to be in 1991, most things were still text. True, Windows 3.0 was out, and MacOS had been with us since 1984 but graphics were memory hungry "nice to haves" and people worked predominantly in a text user interface. If you wanted graphics, you had to have an expensive, powerful PC and most people didn’t think that was really worth the cost. Over the years, the people who used the Desktop operating systems such as Mac and Windows have mainly forgotten about the fact that the command prompt still exists. But for systems people, the people that want to do operations in bulk, or do them remotely, they still use the command prompt often. In November 2006 Microsoft released a thing called Windows PowerShell for this exact reason. macOS gives us the bourne shell (the UNIX shell from BSD). And Linux gives us the Bash shell (the Bourne Again SHell, which is just an enhanced edition of the bourne shell that you find on a Mac).

<a id="cut-and-paste"></a>

## 2.3 Cut and paste

> [!WARNING] 
> You might have tried to use ` Ctrl + C ` and ` Ctrl + V ` to perform copy-paste inside a terminal window, and found out that they do not work. These control codes have different meanings to the shell and were assigned many years before the use of ` Ctrl + C ` to copy, and ` Ctrl + V ` to paste from session-wide clipboard, that was introduced by *Mac OS* in 1983 and *Microsoft Windows 3.x* in 1990.
- **` Ctrl + C `** was the **interrupt** key almost everywhere in Unix. And even now it can be used to <ins>cancel</ins> the current program or operation in a terminal session.
-  ` Ctrl + V ` often meant **verbatim insert**; That is, insert the following control character literally without performing any associated action (see [Chapter 3, Section: Control characters](03-basic-terminal.md#control-characters)). For example, a normal ` Esc ` switches to command mode in the terminal, but even now ` Ctrl + V, Esc ` will insert Esc control character into the current position.

Earlier Windows versions (1.x and 2.x), as well as IBM OS/2, only supported the **IBM CUA keys** **` Ctrl + Ins `** to copy and **` Shift + Ins `** to paste. Infact these shortcuts have remained supported by all GNU / Linux and Windows versions todate.

The keyboard shortcuts most commonly used to copy/paste are:
- For pasting text into a terminal window use **` Ctrl + Shift + V `**
- For copying text from a terminal window use **` Ctrl + Shift + C `**
- Elsewhere you can use the more familiar ` Ctrl + C ` for copy and ` Ctrl + V ` for paste.

In GNU / Linux there is also an alternative way to paste content, the click of the **middle mouse button**.
- You can select text in one program and insert it using the middle mouse button, even without any explicit copy action. Give it a try if you can (some desktop environments such as Ubuntu's Unity no longer support it though).
- Elements in a window will be able to receive input even when the parent window is not focused on the foreground. The focus follows the mouse so to speak.
- This can be a very useful feature that allows you to do things efficiently, but it can also be very annoying at times; Especially for those with a sensitive mouse.
    - You will find that everytime you scroll your mouse wheel too fast (which translate into a middle click), it will paste the previous copied content to your text editor, documents or any other input text field, without your knowledge.
    - As this is a system level feature, there are no easy ways to disable the mouse middle click to paste feature. Fortunately there are some [workarounds](https://www.maketecheasier.com/disable-middle-mouse-click-to-paste-feature-in-linux-quick-tips/) and hacks that can be used.

<a id="text-selection"></a>

## 2.4 Text selection

Younger readers may not be aware that terminals used to print. On paper. Very slowly. When the constraint of the slow printing terminals of 1969 was gone, Unix evolved in a world of video display terminals; Many of which still had no arrow keys, or function keys. One can highlight text only on modern GUI terminal emulator software and even then only with a mouse. Still even today some users might encounter instances when they can’t use the mouse (to highlight text). And if you can’t highlight any text, how can you copy and paste it? Whatever situation you find yourself in when using a linux computer, there will be a way to "copy and paste". You have options. Some of them are strange, but at least there are options.

Any unix terminal will let you cut and paste on current command line:
- a) **Cut** the part of the **line before** the cursor (and add it to the clipboard buffer) = ` Ctrl + U `
    - If the cursor is at the end of the line, it will cut and copy the entire line.
- b) **Cut** the part of the **line after** the cursor (and add it to the clipboard buffer) = ` Ctrl + K `
    - If the cursor is at the start of the line, it will cut and copy the entire line.
- c) **Cut** the **word before** the cursor (and add it to the clipboard buffer) = ` Ctrl + W `
- d) **Cut** the **word after** the cursor (and add it to the clipboard buffer) = ` Alt + D `
- **Paste** (the last text that was cut and copied) = ` Ctrl + Y `

<a id="bash-history"></a>

### Bash history <!--update internal links if changed-->

Bash remembers the commands you type, and by default stores them in a history file ` ~/.bash_history ` which persists between sessions.
- To walk backwards through the commands you've used press ` Up ` arrow key multiple times
- To walk forwards through the commands you've used press ` Down ` arrow key multiple times

Making use of this history can be a lot more powerful than one might realize:
- [Chris Hoffman - How to use bash history, 2017](https://www.howtogeek.com/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/)
- [Dave McKay - How to use the history command, 2024](https://www.howtogeek.com/465243/how-to-use-the-history-command-on-linux/)

<a id="directory-structure"></a>

## 2.5 Directory structure

As you get acquainted with the GNU / Linux world, perhaps the biggest confusion, for those accustomed to Windows, is the unix-style directory structure. Unix and it's derivates do not use Microsoft way of grouping directories under drives and hard disk partitions (such as C, D, E and so on). For example, when reading (and writing to) a compact-disc, one does not refer directly to the drive but under the mount point to the directory ` /media/ `. The Unix-style directory structure was originally based on the assumption that each directory can have its own hard drive, and for a home user, this may seem absurd. Some directories are virtual such as the ` /sys/ ` interface, that describes connections between hardware and drivers. Even the printer, mouse and keyboard are files. All his understandably adds to confusion. The fact that everything is a file, can be first understood and finally appropriated, from a programming perspective.

The directory structure of GNU / Linux generally follows the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html). While the directory structure may not need to be touched by the base user, it should be good to know what is where.

### Special term: root

It is a little confusing that the word **root** is used for three different things:
1. The root user, the system administrator user.
2. The root user home directory, found under ` /root/ `.
3. The root of the filesystem tree, marked by forward slash ` / `.

### Home directories

Home directory for the root user is always **` /root/ `**. Home directories for all other users are located under **` /home/ `**. A typical non-root user's home directory would be ` /home/$USER `. The shorthand ` ~/ ` will expand to whatever the home directory is, such as ` /home/GitJit-max/ `.

>A newly created home directory is pre populated with well known directories (such as Desktop, Documents, Downloads and Pictures) by the [xdg-user-dirs package](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/).

> When harddrives were much smaller, ` /home/ ` used to be on a different disk, and was mounted comparatively late, when the system went up. In contrast ` /root/ ` was deemed essential for system maintenance purposes, and thus had to be present at any rate; Even when the *user disk* wasn't mounted.

<a id="software-applications"></a>

### Software applications <!--update internal links if changed-->

> [!NOTE] 
> Here **binary** refers to an executable; A type of binary file (i.e. file composed of something other than human-readable text) that contains machine code for the computer to execute.

All applications are not stored at the same location, as each directory serves a unique purpose.

Traditionally essential CLI only (Command Line Interface) binaries that were available to all users (such as ` $ ls ` and ` $ find `) resided in **` /bin/ `** (Binaries). These days ` /bin/ ` might just be a symlink to ` /usr/bin/ ` where such binaries have been moved.

Traditionally essential root-only binaries such as ` $ adduser ` resided in **` /sbin/ `** (Superuser Binaries). These days ` /sbin/ ` might just be a symlink to ` /usr/sbin/ ` where such binaries have been moved.

Traditionally essential shared library files needed (by binaries in ` /bin/ ` and ` /sbin/ `) to boot the system and run the commands in the root filesystem resided in **` /lib/ `** (Libaries). These days ` /lib/ ` might just be a symlink to ` /usr/lib/ ` where such library files have been moved.

In the old days critical system binaries, or simply default minimal required binaries, would have been in ` /bin/ ` and ` /sbin/ `. That way, you could put ` /usr/ ` on a network drive or something that isn't available right at boot. If you wanted to do this on a modern system, it would end up being a huge hassle because modern distributions no longer properly separate ` /sbin/ ` and ` /bin/ ` from the ` /usr/ ` equivalents.

Applications installed through package management reside under **` /usr/ `** (Unix Shared Resources). The ` /usr/ ` directory contains only shareable and read-only data, no settings, no log data. Any information that is host-specific or varies with time is stored elsewhere. The most important subdirectories are:

| Dir | Use |
|:--- |:--- |
| **` /usr/sbin/ `** <br>= **` /sbin/ `** | <ins>Most root user commands/executables</ins> reside in ` /usr/sbin/ `. There must be no subdirectories here. [^fhs-sbin] [^fhs-usr-sbin] |
| **` /usr/bin/ `** <br>= **` /bin/ `** | <ins>Most user commands/executables</ins> reside in ` /usr/bin/ `, which is the primary directory of executable commands on the system. There must be no subdirectories here. [^fhs-bin] [^fhs-usr-bin] |
| **` /usr/lib/ `** <br>= **` /lib/ `** | There are lots of shared **libraries** available in a GNU / Linux system, capable of doing a lot of useful things. And many of those libraries can be reused by other programs. The libraries, object files and possibly even binaries under ` /usr/lib/ ` are not intended to be executed directly by users or shell scripts. Applications may use a single subdirectory. [^fhs-usr-lib] [^fhs-lib] |
| **` /usr/include/ `** | **Header files** included by mostly C programs reside here. Header files usually have a *.h* extension, but you will occasionally see them with other extensions such as *.hpp* or *.d* or no extension at all. The topic of header files can seem daunting for those unfamiliar with C language. A header file contains function declarations, type definitions, and other global declarations that are shared across multiple source files. It allows to separate the interface (function prototypes) from the implementation (function definitions). [^fhs-usr-include] |
| **` /usr/share/ `** | The processor architecture-independent i.e. non executable, static data files of applications are **shareable** among all architecture platforms of a given OS. Not to be confused being shared by different OSes or by different releases of the same OS. That is most <ins>data required by programs, that doesn't need to be modified</ins> reside here. The data stored in ` /usr/share/ ` must be purely static such as manual pages, word lists for various languages (i.e. vocabulary), XML and HTML doctype declarations, postScript printer definition files, ICC color management files. Any modifiable data is stored elsewhere. [^fhs-usr-share] |

[^fhs-sbin]: [Filesystem Hierarchy Standard: System binaries](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#sbinSystemBinaries)

[^fhs-usr-sbin]: [Filesystem Hierarchy Standard: Non-essential standard system binaries](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrsbinNonessentialStandardSystemBi)

[^fhs-bin]: [Filesystem Hierarchy Standard: Essential user command binaries)](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#binEssentialUserCommandBinaries)

[^fhs-usr-bin]: [Filesystem Hierarchy Standard: Most user commands](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrbinMostUserCommands)

[^fhs-usr-lib]: [Filesystem Hierarchy Standard: Libraries for programming and packages](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrlibLibrariesForProgrammingAndPa)

[^fhs-lib]: [Filesystem Hierarchy Standard: Essential shared libraries and kernel modules](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#libEssentialSharedLibrariesAndKern)

[^fhs-usr-include]: [Filesystem Hierarchy Standard: Header files included by C programs](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrincludeHeaderFilesIncludedByCP)

[^fhs-usr-share]: [Filesystem Hierarchy Standard: Architecture-independent data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrshareArchitectureindependentData)

> [!TIP]
> It may be useful sometimes to use library functions in your own programs; Even if written in other programming languages such as using C-language library functions from the BASIC language dialect and integrated development environment [Gambas](https://en.wikipedia.org/wiki/Gambas). [^gambas-wiki] [^gambas-extern]
> For example [VLC](https://www.videolan.org) the well known and popular media player has a versatile but less known accompanying library SDK for developers, [libvlc](https://wiki.videolan.org/LibVLC/).

[^gambas-wiki]: [Wikipedia - Gambas, accessed 2024](https://en.wikipedia.org/wiki/Gambas)

[^gambas-extern]: [Gambas Documentation - How To Interface Gambas With External Libraries, accessed 2024](https://gambaswiki.org/wiki/howto/extern)

These days some 3rd-party packages (such as [Master PDF Editor](https://code-industry.net/free-pdf-editor/) and [ONLYOFFICE Desktop Editors](https://www.onlyoffice.com/download-desktop.aspx?from=desktop) installed from dot-deb-packages) reside under **` /opt/ `** (Option packages). In the old days ` /opt/ ` was used by UNIX vendors (like AT&T, Sun, DEC) and 3rd-party vendors to hold packages that you might have paid extra money for (hence the name option packages).
- There was no ` /opt/ ` on all Unix variants such as Berkeley BSD UNIX, which used ` /usr/local/ ` for stuff that you installed yourself.

When the user types a CLI command, the system looks for the requested binary executables in directories specified by the an environment variable called PATH. Run this command ` $ echo $PATH↵ ` or this command ` $ echo "$PATH" | tr ':' '\n'↵ ` in a terminal, to reveal this list of directories. You should see something like:

```
/home/user/.local/bin
/usr/sbin
/usr/bin
/snap/bin
```

> [!IMPORTANT]
> To run a program or script located elsewhere, the location must be explicitly reported with the command. For example, when running a script in the current working directory, one should type something like ` $ ./myscript.sh↵ ` in the terminal. Single period ` . ` refers to the active directory and should not be added to environment variable ` PATH ` (see [Section: Well-known environment variables](#well-known-variables)).

### Dynamic data

> Many directories remain relatively static. Their contents don't change.

The **` /var/ `** (Variable) directory tree is used to store the application *data that is likely to change* such as log files, various databases and user mail. Applications must generally not add directories to the top level of ` /var/ `. Instead following subdirectories, or symbolic links are used:

| Dir | Use | RAM<br>Disk |
|:--- |:--- | --- |
| **` /var/cache/ `** | Application **cache** means <ins>data stored to serve future requests faster</ins>. The data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere. [^fhs-cache][^wiki-cache] |   |
| **` /var/lib/ `** | **Variable state information** is data that programs modify while they run, <ins>that must not be exposed to regular users</ins>. An application (or a group of inter-related applications) should generally use a subdirectory for its data. There is one required subdirectory ` /var/lib/misc/ ` which is intended for state files that don't need a subdirectory. [^fhs-lib] |   |
| ` /var/lock/ ` <br>= **` /run/lock/ `** | Some programs follow a convention to create a **lock file** for example (but not limited to) to <ins>indicate use of a particular device or file</ins>, so other programs can take care not to use the locked device or file simultaneously. [^fhs-lock][^tldp-var] | ✓ |
| **` /var/log/ `** | Most logs are stored to this directory or an appropriate subdirectory. **Log messages** <ins>can be used to debug problems, monitor and understand the operation</ins> of the system. [^fhs-log] |   |
| **` /var/opt/ `** | <ins>Variable data of the *option packages*</ins> installed in ` /opt/ ` are stored in a subdirectory named after the add-on software package. [^fhs-opt] |   |
| ` /var/run/ ` <br>= **` /run/ `** | <ins>Data relevant to running processes</ins> in ` /run/ ` is not stored on disk, but <ins>kept in memory (or disk-based swap)</ins>, that takes on the appearance of a mounted file system to allow it to be more accessible and easier to manage. [^fhs-run] [^sandra] | ✓ |
| **` /var/spool/ `** | **Spool** data <ins>is application data which awaits further processing</ins> such as printer queues. Often spool data is deleted after it has been processed. [^fhs-spool] |   |
| **` /var/tmp/ `** | **Temporary** application <ins>data preserved between system reboot</ins>s. [^fhs-tmp] |   |

[^wiki-cache]: [Wikipedia - Cache (computing)](https://en.wikipedia.org/wiki/Cache_(computing))

[^sandra]: [Sandra Henry-Stocker - Exploring /run on Linux, published 2019](https://www.networkworld.com/article/967547/exploring-run-on-linux.html)

[^fhs-spool]: [Filesystem Hierarchy Standard: Application spool data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varspoolApplicationSpoolData)

[^fhs-tmp]: [Filesystem Hierarchy Standard: Temporary files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#vartmpTemporaryFilesPreservedBetwee)

[^fhs-run]: [Filesystem Hierarchy Standard: Run-time variable data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varrunRuntimeVariableData)

[^fhs-opt]: [Filesystem Hierarchy Standard - Variable data for /opt](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varoptVariableDataForOpt)

[^fhs-lock]: [Filesystem Hierarchy Standard - Lock files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varlockLockFiles)

[^tldp-var]: [Linux System Administrators Guide - The /var filesystem](https://tldp.org/LDP/sag/html/var-fs.html)

[^fhs-log]: [Filesystem Hierarchy Standard - Log files and directories](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varlogLogFilesAndDirectories)

[^fhs-cache]: [Filesystem Hierarchy Standard - Application cache data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varcacheApplicationCacheData)

### RAM disk [^ramdisk]

[^ramdisk]: [Riccardo - RAM Disk on Linux, 2011](https://linuxaria.com/pills/ram-disk-on-linux)

All modern GNU / Linux distributions also offer some of the volatile random-access memory as a RAM disk. It is mounted onto **` /dev/shm/ `** (Shared Memory).
- It is an efficient means of sharing and passing data between programs. One program will create a memory portion, which other processes can access. Hence the name shared memory.
- It can be used just like normal disk space; Creating and manipulating files and directories, but with better performance compared to being stored on hard disk.
- A sophisticated image viewer could use it for temporary storage location of files extracted from zip archives to prevent unnecessary wear of the user's HDD or SSD.
- Because the data resides in RAM, it will be cleared in the event of power loss, whether intentional (computer reboot or shutdown) or accidental (power failure or system crash). [^wikiram]

[^wikiram]: [Wikipedia - RAM drive, accessed 2024](https://en.wikipedia.org/wiki/RAM_drive)

> The virtual filesystem types udev and tmpfs, don't take
up disk space or occupy more RAM than used. Size and how much
is available is just upper limit as to how much RAM it may use.

### Removable media mount points <!--update internal links if changed-->

**Mounting** is a process by which a computer's operating system makes files and directories on a storage device available. [^wiki-mount]

[^wiki-mount]: [Wikipedia - Mount (computing)](https://en.wikipedia.org/wiki/Mount_%28computing%29)

| Dir | Use |
|:--- |:--- |
| **` /media/ `** or <br>` /run/media/ ` | Mount points for physical media such as a Blu-ray disc or a USB flash drive. [^fhs-media] |
| **` /mnt/ `** | Mount points for a temporarily mounted filesystems such as a network directory or a [VMware Shared Folder](https://docs.vmware.com/en/VMware-Workstation-Pro/17/com.vmware.ws.using.doc/GUID-D6D9A5FD-7F5F-4C95-AFAB-EDE9335F5562.html) (i.e. a directory shared between a local virtual machine and the host system) [^fhs-mnt] |

[^fhs-media]: [Filesystem Hierarchy Standard - Mount point for removable media](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#mediaMountPoint)

[^fhs-mnt]: [Filesystem Hierarchy Standard - Mount point for a temporarily mounted filesystem](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#mntMountPointForATemporarilyMount)

### Hardware connection points

| Dir | Use |
|:--- |:--- |
| **` /sys/ `** (System) | A virtual directory exposing some hardware, driver and kernel features. [^fhs-sys] |
| **` /dev/ `** (Devices) | A virtual directory that describes hardware devices such as internal storage drives and exposes some special "devices". [^fhs-dev] See [Section: Device files](#device-files) and [Section: Special device files](#special-device-files) for more information . |

[^fhs-sys]: [Filesystem Hierarchy Standard: Kernel and system information virtual filesystem](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#sysKernelAndSystemInformation)

[^fhs-dev]: [Filesystem Hierarchy Standard: Device files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#devDeviceFiles)

### Directory ≠ Folder

With release of Window 95 in 1995, Mirosoft seemed to complete replace the well-established word directory with another word, folder. Although folder and directory are essentially the same thing, they are separated by perspective. A folder is an object-oriented counterpart to a directory. The convention has spread from the mid-1980s Macintosh operating system (the lesson of which was sought from the pioneering work of Xerox's Palo Alto Research Center) to Microsoft Windows, IBM's OS / 2, and other modern operating systems. The folder and its images belong to the graphical environment. One would think that when we drag a file to a folder with the mouse, we drag it to some actually existing objectified object and not just play a complex logical game with conventional file and directory names. In this sense, the new term has its legitimacy.

**Directory** is a file system object that contains files and other directories.

**Folder** is a graphical user interface metaphor used to represent a directory. Unlike a directory, a folder can be a virtual construct that doesn’t necessarily map directly to a specific storage location. Microsoft Windows uses the concept of special folders to help present the contents of the computer to the user in a fairly consistent way that frees the user from having to deal with absolute directory paths.

### Everything is a file [^hoffman-2016]

[^hoffman-2016]: [Chris Hoffman - What does "everything is a file" mean in linux?, published 2016](https://www.howtogeek.com/117939/htg-explains-what-everything-is-a-file-means-on-linux/)

In unix "everything is a file". Directories are files. Files are files. Printer, mouse and keyboard are files. Your screen is a file. The defining feature that "everything is a file" is an oversimplification. But understanding what it means will help you understand how unix and it's derivatives work. Many things on unix appear in your file system and behave as "files", but they aren’t actually files. They’re special "files" that represent hardware devices, system information, a random number generator and what not.

For example to find information about your CPU, you don’t need a special command that tells you your CPU info. You can just read the contents of ` /proc/cpuinfo ` "file". You can use standard commands to print this file’s contents to the terminal. Or you can open ` /proc/cpuinfo ` in a text editor to view its contents.

> [!NOTE]
> Note that ` /proc/cpuinfo ` isn’t actually a text file. The os kernel and the ` /proc/ ` directory or file system are exposing this information to us as a "file". This allows us to use familiar tools to view and work with the information. The /proc directory also contains other similar "files" such as ` /proc/uptime ` and ` /proc/version `.

<a id="device-files"></a>

### Device files <!--update internal links if changed-->

Device access in unix is very different from Windows, where the internal storage drives and optical drives are represented as drive letters like C: D: E: G: H: In unix all device entry points reside in the ` /dev/ ` directory as "files". [^hoffman-2016] Let's explore references to internal storage drives in the ` /dev/ ` directory:
- For example, if the first *internal SATA SSD storage drive* had three primary partitions, they would be named and numbered as ` /dev/sda1 `, ` /dev/sda2 ` and ` /dev/sda3 `.
- For example, if the first *internal SATA HDD storage drive* had three primary partitions, they would be named and numbered as ` /dev/hda1 `, ` /dev/hda2 ` and ` /dev/hda3 `.
- And if the first *internal M.2 SSD storage drive* had three primary partitions, they would be named and numbered as ` /dev/nvme0n1p1 `, ` /dev/nvme0n1p2 ` and ` /dev/nvme0n1p3 `.
- An internal Blu-ray drive could be named and numbered as ` /dev/scd0 `
- These are all just references to the drives and partitions. The data content is exposed elsewhere through mount points (see [Section: Removable media mount points])(#removable-media-mount-points).

> [!NOTE]
> Knowledge of this internal storage naming convention will first come in handy when installing a distribution and having to select partitions or even make changes to existing partitions using a partition editor such as [GParted](https://en.wikipedia.org/wiki/GParted).

<a id="special-device-files"></a>

### Special device files <!--update internal links if changed-->

The ` /dev/ ` directory doesn’t just contain "files" that represent physical devices. Here are three of the most notable special "devices" it also contains:

| File | Use |
|:--- |:--- |
| **` /dev/random `** | Is a random number generator you and all the applications can tap into. Truly random numbers are challenging to generate. The ` /dev/random ` on linux can promise up to 256 bits of security, if you wanted a source of randomness for generating cryptographic keys. [^man7-random] |
| **` /dev/zero `** | A read from "device" ` /dev/zero ` will return as many bytes containing the value zero as was requested. [^fhs-special] |
| **`/dev/null `** | All data written to "device" `/dev/null ` is discarded. Think of it as a black hole. [^fhs-special] [^hoffman-2016] |

[^man7-random]: [Michael Kerrisk - Linux manual page, accessed 2024](https://www.man7.org/linux/man-pages/man7/random.7.html)

> [!TIP]
> By default terminal commands produce error messages and other output that they print to the standard output (i.e. normally the terminal). If you want to run a command and don’t care about its output, you can redirect that output to ` /dev/null `. Redirecting a command’s output to /dev/null immediately discards it. Instead of having every command implement its own *quiet mode* you can use this method with any command like this ` $ somecommand > /dev/null↵ ` [^hoffman-2016]

[^fhs-special]: [Filesystem Hierarchy Standard: Devices and special files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#devDevicesAndSpecialFiles)

<a id="shell-environment"></a>

## 2.6 Shell environment [^raymond]

### Configuration files

When we log on to the system, the bash program starts, and reads a series of configuration scripts called startup files, which define the default environment shared by all users. This is followed by more startup files in our home directory that define our personal environment.

> The exact sequence depends on the type of shell session being started; Which There are two kinds: 1) **Login shell session** is one in which we are prompted for our username and password. 2) **Non-login shell session** typically occurs when we launch a terminal session in the graphical user interface.

#### What

A **run-control file** or **script**
- Is a file of declarations or commands associated with a program that it interprets on <ins>startup</ins>.
- RC stands for "runcom" i.e. run commands. And in fact, this is exactly what the file contains, <ins>commands that the shell should run</ins>.

A **configuration file**
- Is a local file used to control the operation of a program.
- Must be <ins>static</ins> and cannot be an executable binary.

#### Where

User-specific configuration information is often carried in a hidden run-control file in the <ins>user's home directory</ins>. Such files are often called **dotfiles** because they exploit the unix convention that a filename beginning with a dot is normally invisible to directory-listing tools, to reduce clutter.

Programs can also have **run-control** or **dot-directories**.
- **` ~/.config/ `** for the <ins>user-specific settings</ins>.
- **` /etc/ `** (Etcetera) for the <ins>system-wide settings</ins> i.e. configuration shared by all users at a site.

Thus with a fictional program called ` $ seekstuff ` that has both **site-wide** and **user-specific** configuration, an experienced unix user would expect to find the former at ` /etc/seekstuff/ ` and the latter at ` ~/.seekstuff/ ` in the user's home directory.

Many startup script -files exist (or have existed in the past) such as ` .bash_profile `, ` .bash_login `, ` .profile `. If one script isn't found then a shell tries to read another. There are also differences among distributions and not just shell variants. On modern GNU/Linuces the two most important startup files are:
1. The most important <ins>system-wide</ins> startup file **` /etc/profile `** applies to all users for the original Bourne Shell (sh) or any Bourne compatible shells (such as bash, ksh and ash).
2. The most important <ins>user-specific</ins> startup file is **` ~/.bashrc `** for the Bourne Again Shell (bash).

> [!NOTE]
> Root's ` .bashrc ` is found under ` /root/ ` directory as it is root's home directory.

#### How

Classically a unix program looks for **control information** in five places in it's startup-time environment:
1. Run-control files under ` /etc/ ` directory.
2. System-set environment variables (see [Section: Environment variables](#environment-variables)).
3. Run-control files in the user's home directory also called as dotfiles.
4. User-set environment variables (see [Section: Environment variables](#environment-variables)).
5. Switches and arguments passed to the program on the command line that invoked it.

These queries are usually done in the order listed above. That way, later (more local) settings override earlier (more global) ones. Settings found earlier can help the program compute locations for later retrievals of configuration data.

There is a strong convention that well-behaved Unix programs that use more than one of these places should look at them in the order given, allowing later settings to override earlier ones (there are specific exceptions, such as command-line options that specify where a dotfile should be found).

> [!NOTE]
> In particular, environment settings usually override dotfile settings, but can be overridden by command-line options. It is good practice to provide a command-line option (like "-e" of ` $ make `) that can override environment settings or declarations in run-control files. This way the program can be scripted with well-defined behavior regardless of the way the run-control files look or environment variables are set.

Which of these places are looked at depends on how much persistent configuration state a program needs to keep around between invocations.
- Programs designed mainly to be used in a batch mode (such as generators or filters in pipelines) are usually completely configured with command-line options. Good examples of this pattern include ` $ ls `, ` $ grep ` and ` $ sort `.
- At the other extreme, large programs with complicated interactive behavior may rely entirely on run-control files and environment variables, and normal use involves few command-line options or none at all. Most X window managers are a good example of this pattern.

<a id="environment-variables"></a>

### Environment Variables <!--update internal links if changed-->

When a unix program starts up, the environment accessible to it includes <ins>a set of name to value associations</ins> (names and values are both strings) called **environment variables**.
- Some of these are set manually by the user. Others are set by the system at login time, or by your shell or terminal emulator (if you're running one).
- Environment variables are <ins>application-independent preferences that need to be shared by a large number of different programs</ins>. What both user and system environment variables have in common is that it would be annoying to have to replicate the information they contain in a large number of application run-control files. And extremely annoying to have to change that information everywhere when your preference changes. Typically, the user sets these variables in his or her shell session startup file.

> [!CAUTION]
> There is one traditional unix design pattern that we do not recommend for new programs. Sometimes, user set environment variables are used as a lightweight substitute for expressing a program preference in a run-control file. The venerable [NetHack](https://www.nethack.org) dungeon-crawling game introduced in 1987, for example, used to read ` NETHACKOPTIONS ` environment variable for user preferences. This was an old-school technique. Modern practice would lean toward parsing them from a ` .nethack ` or ` .nethackrc ` file.

<a id="well-known-variables"></a>

#### Well-known environment variables

There are a number of well-known environment variables you can expect to find defined on startup of a program from the unix shell. These (especially ` HOME `) will often need to be evaluated before you read a local dotfile.

| Name | Use |
|:--- |:--- |
| ` USER ` | Login name of the account under which this session is logged in (BSD convention). |
| ` LOGNAME ` | Login name of the account under which this session is logged in (System V convention). |
| ` HOME ` | Home directory of the user running this session. The ` HOME ` variable is especially important, because many programs use it to find the calling user's dotfiles. |
| ` COLUMNS ` | The number of character-cell columns on the controlling terminal or terminal-emulator window. |
| ` LINES ` | The number of character-cell rows on the controlling terminal or terminal-emulator window. |
| ` SHELL ` | The name of the user's command shell (often used by shellout commands). |
| ` PATH ` | The list of directories that the shell searches when looking for executable commands to match a name (see [Section: Software applications](#software-applications)). |
| ` TERM ` | Name of the terminal type of the session console or terminal emulator window. ` TERM ` is special in that programs to create remote sessions over the network (such as telnet and ssh) are expected to pass it through and set it in the remote session.
| ` EDITOR ` | The name of the user's preferred line oriented text editor (often used by shellout commands). The ` EDITOR ` editor should be able to work without use of "advanced" terminal functionality (like old ` $ ed `, or the ex mode of ` $ vi `). But actually, most unix programs first check ` VISUAL `, and only if that's not set will they consult ` EDITOR `, which could be considered a relic from the days when people had different preferences for line-oriented editors and visual editors.
| ` VISUAL ` | A visual editor could be a full screen editor as such as ` $ nano `. If you invoke an editor through bash (using ` Ctrl + X, Ctrl + E `), bash will try first ` VISUAL ` editor and then ` EDITOR `, if the former fails. Nowadays, you can leave ` EDITOR ` unset, or set it to ` VISUAL ` by running commands like ` $ export EDITOR="$VISUAL"↵ ` and ` $ export VISUAL="/usr/bin/nano"↵ `.

> [!TIP]
>  To list all currently defined shell variables run ` $ printev↵ ` for a short listing, or ` $ set↵ ` for a long listing.

> [!NOTE]
> Finally, note that there is a tradition (exemplified by the ` PATH ` variable) of using a <ins>colon : as a separator</ins> when an environment variable must contain multiple fields, especially when the fields can be interpreted as a search path of some sort. Note that some shells (notably bash and ksh) always interpret colon-separated fields in an environment variable as filenames, which means in particular that they expand.

<a id="io-after-startup"></a>

## 2.7 IO after startup [^raymond]

After startup, programs normally get input or commands from
1. Data and commands presented on the program's [standard input](06-inter.md#file-descriptor).
1. Inputs passed through [inter process communication](06-inter.md#ipc-techniques) such as [D-Bus](06-inter.md#d-bus).
1. [Files in known locations](06-inter.md#ipc-techniques) such as a data file name passed to or computed by the program.

Programs can emit results in all the same ways (with output going to standard output). These several competing interface styles, are all still alive for a reason; They're optimized for different situations.

Commands (including the scripts and shell functions we write) issue a value to the system when they terminate, called an **exit status**. This value, which is an integer in the range of 0...255, indicates the success or failure of the command’s execution. By convention, a value of <ins>zero indicates success</ins>) and <ins>any other value indicates failure</ins>. Some commands use different exit status values to provide diagnostics for errors, while many commands simply exit with a value of 1 when they fail. Man pages often include a section entitled *Exit Status*, describing what codes are used. However, a zero always indicates success. [^shotts]

[^shotts]: [William Shotts - The Linux Command Line, updated 2019](http://linuxcommand.org/tlcl.php)

<a id="design-tropes-of-unix"></a>

## 2.8 Design tropes of unix shell utilities [^raymond]

The initial release of Unix (in the 1960’s) had some important design attributes that live on today. With unix shell utilities the theme is, and has been, to:
1. <ins>Break the system into independent components.</ins> Small, modular utilities, that do one thing, and do them well. These programs are rock solid because they can be debugged and improved separately. Simple utilities (that do one thing) can be combined (in different ways) to do complicated things. To do a new job, build an additional component, rather than complicate old programs with new features.
1. <ins>Support plugging in new pre- and post-processors without disturbing old ones.</ins> Unix was always agnostic about its intended audience and designers. They expect the output of every program to become the input to another, as yet unknown, program. The implementers never assumed they knew all the potential uses the system could and would be put to.
1. <ins>Have all the tools communicate with each other through human readable text.</ins> Plain text is a universal interface by itself. Data is more tractable and discoverable than program logic. If programs do not accept and emit simple text streams: a) it's much more difficult to hook them together (using binary input formats) and b) they are much more difficult to debug.
4. <ins>Programs should shut up if there is nothing interesting or surprising to say.</ins> The *singular taste of old Unix* was partly a consequence of poverty. This *silence is golden* rule evolved originally because Unix predates video displays. Younger readers may not be aware that terminals used to print. On paper. Very slowly. On the slow printing terminals of 1969, each line of unnecessary output was a serious drain on the user's time. That constraint is long gone, but **terseness** (i.e. using few words, and often not seeming polite or friendly) has remained a central feature of the style in unix programs. So don't assume that historical origin specifies current utility. There are good reasons for this "rule of silence" to have long outlasted the slow teletypes, on which Unix was born.
    - a) The user's vertical screen space is still precious. Junk messages are a careless waste of the human user's bandwidth. They're one more source of distracting motion on a screen display that may be mediating for more important foreground tasks, such as communication with other humans.
    - b) The Unix principle states that a program should be able to communicate (not just  with human users but) with other programs. Programs that babble don't tend to play well with other programs. If a CLI program emits status messages to standard output, then programs that try to interpret that output will be put to the trouble of interpreting or discarding those messages (even if nothing went wrong). It is considered better to send only real errors to standard error, and not to emit unrequested data at all.
5. <ins>Programs should request confirmation only when there is good reason</ins> to suspect that the answer might be: No! No! No!
    - Even then programs should support a "Yes" option (` -y ` without argument) to authorize potentially destructive actions for which the program (such as ` $ fsck ` the filesystem check and repair tool) would normally require confirmation.
    - If there are chatty progress messages (for debugging purposes) they are to be disabled by default and being displayed only when a so called **verbosity switch** (` -v `) is on.
6. <ins>Avoid noise.</ins> You might have wondered why there are no headers on the output of the ` $ ls -la ` command for example. The answer lies yeat again on a unix tradition. The unix commandline tools 1) typically avoid adding nonessential information (i.e. noise) and 2) typically avoid (re)formatting in ways that might make the output more difficult for downstream programs to parse. The most common offenders are considered cosmetic touches like headers, footers, blank or ruler lines, summaries and conversions like adding aligned columns.
7. <ins>Fail noisily.</ins> When you must fail, fail noisily and as soon as possible. Software should be transparent in the way that it fails (as well as in normal operation). It's best when software can cope with unexpected conditions by adapting to them. But the worst kinds of bugs are those in which the repair doesn't succeed and the problem quietly causes corruption, that doesn't show up until much later. Therefore, write your software to cope with incorrect inputs and its own execution errors as gracefully as possible. But when it cannot, make it fail in a way that makes diagnosis of the problem as easy as possible.

<a id="textual-formats"></a>

## 2.9 Textual formats [^raymond]

There are long-standing Unix traditions about how textual data formats ought to look.
1. <ins>One record per line</ins> makes it easy to extract records with text-stream tools.
1. <ins>Less than 80 characters per line</ins> makes the format browseable in an ordinary-sized terminal window.
1. In one-record-per-line formats, use <ins>colon : or any run of whitespace as a field separator</ins>.
    - Data files in this style are expected to support inclusion of colons (:) in the data fields by <ins>backslash (\) escaping</ins>. More generally, code that reads delimiter separated values is expected to support record continuation by ignoring backslash-escaped newlines. So if your fields must contain instances of the field separator(s), use a backslash (\) as the prefix to escape them. Classic examples of the colon-convention include ` /etc/group `, ` /etc/passwd ` and ` /etc/shadow `.
    - If many records must be longer than 80 characters, consider a stanza format: Multiple lines per record, with a record separator line of ` %%\n ` or ` %\n `. The separators make useful visual boundaries for human beings eyeballing the file.
1. <ins>Do not allow the distinction between tab and whitespace to be significant.</ins> This is a recipe for serious headaches when the tab settings on your users' editors are different. More generally, it's confusing to the eye.
1. <ins>Favor hex over octal.</ins> Hex-digit pairs and quads are easier to eyeball-map into bytes.
1. <ins>Times and dates are a particular bother</ins> because they're hard for downstream programs to parse. Any such additions should be optional and controlled by switches. If your program emits dates, it's good practice to have a switch that can force them into [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) **YYYY-MM-DD** and **hh:mm:ss** formats – Or, better yet, use those by default.
1. <ins>Support the backslash convention.</ins> The least surprising way to support embedding nonprintable control characters is by parsing C-like backslash escapes: ` \n ` for a newline, ` \r ` for a carriage return, ` \t ` for a tab, ` \b ` for backspace, ` \f ` for formfeed, ` \e ` for ASCII escape, ` \nnn ` or ` \onnn ` or ` \0nnn ` for the character with octal value nnn, ` \xnn ` for the character with hexadecimal value nn, ` \dnnn ` for the character with decimal value nnn, ` \\ ` for a literal backslash. A newer convention, but one worth following, is the use of ` \unnnn ` for a hexadecimal Unicode literal.
1. <ins>Use hash mark # as an introducer for comments.</ins> It is good to have a way to embed annotations and comments also in data files.

The traditional textual format is easily searched and transformed using the *traditional unix tools* such as ` $ grep `, ` $ sed `, ` $ tr ` and ` $ cut `.

```
$ whatis grep sed tr cut↵
grep	- print lines that match patterns
sed	- stream editor for filtering and transforming text
tr	- translate or delete characters
cut	- remove sections from each line of files
```
### XML

XML can be a simplifying choice or a complicating one:
- XML is itself rather bulky. It can be difficult to see the data amidst all the markup.
- The most serious problem with XML is that it doesn't play well with traditional unix tools. Software that wants to read an XML format needs an XML parser. This means bulky, complicated programs.
- One application area in which XML is clearly winning is in markup formats for document files.
- Compressed XML combines space economy with some of the advantages of a textual format. Notably, it avoids many problems that come with binary formats.

<a id="binary-formats"></a>

## 2.10 Binary formats [^raymond]

a) Whenever you face a design problem that involves editing some kind of complex binary object, the unix tradition encourages asking first off whether you can write a tool analogous to ` $ sng ` or the ` $ tic ` / ` $ infocmp ` pair, that can do a <ins>lossless mapping to an editable textual format and back</ins>. There is no established term for programs of this kind, but we'll call them **textualizers**.

b) If the binary object is dynamically generated or very large, then it may not be practical or possible to capture all the state with a textualizer. In that case, the equivalent task is to write a **browser**. The paradigm example is ` $ fsdb `, the file-system debugger supported under various Unixes. There is a linux equivalent called ` $ debugfs `. Another exmaple would be ` $ psql `, which is used to browse PostgreSQL databases.

> [!IMPORTANT]
> Don't bother compressing or binary-encoding just part of the file.

<!-- # References -->

[^raymond]: [Eric Steven Raymond - The Art of Unix Programming, published 2003](https://www.arp242.net/the-art-of-unix-programming/)
