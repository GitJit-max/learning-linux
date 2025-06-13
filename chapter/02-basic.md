<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="01-intro.md">&lt;&lt; Previous Chapter: 1 - History of Linux</a>
     |
  <a href="03-basic-terminal.md">Next&nbsp;Chapter:&nbsp;3&nbsp;&#8209;&nbsp;Commandline&nbsp;crash&nbsp;course&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 2 - Design priciples of Unix and its decendants

GNU/Linux has been considered difficult for beginners. Learning to use GNU/Linux can seem frustrating because the system was designed from a different perspective than Windows (and its predecessor MS-DOS). Many things are handled very differently. But keep in mind that no one learns to use a computer effectively in a week or two, even with Windows. In order to use GNU/Linux effectively, it's a good idea to learn the basics of the system, as well as something about it's history. [^linufi] <!-- I strongly suggest to check out [Chapter&nbsp;1](01-intro.md), incase you skipped it. -->

[^linufi]: [Linux.fi ohjesivusto - Aloittelijalle, accessed 2021](https://www.linux.fi/wiki/Aloittelijalle)

<a id="introduction-to-the-text-interface"></a>

## 2.1 Introduction to the text interface

**Interface** is the sum of all the ways that a program communicates with human users and other programs. Much of Unix-community tradition about program interface design may seem odd and arbitrary when you encounter that tradition for the first time (or even downright regressive, in the era of graphical user interfaces). But in spite of various blemishes and irregularities, that tradition has an inner logic to it which is worth learning and understanding. It reflects heuristics accumulated over Unix's long history about ways to do effective communication both with human beings and with other programs. [^raymond-dpatterns]

<a id="retained-utility"></a>

### Text interface has retained its utility

Weak GUI facilities (i.e. graphical user interfaces) in a modern operating system are considered a problem. The Unix lesson is the opposite, that weak text-based CLI facilities (i.e. command language interfaces) are a less obvious but equally severe deficit. [^raymond-istyle]

#### Consequences of weak CLI facilities

If the CLI facilities of an operating system are weak or nonexistent, you'll also see the following consequences: [^raymond-istyle]

- Remote system administration will be sparsely supported, more difficult to use, and more network-intensive.
- Background processes (i.e. servers and daemons) will probably be difficult to program in any graceful way.
- Even simple noninteractive programs will incur the overhead of a GUI.
- Programs will not be designed to cooperate with each other in unexpected ways (see remark below), because they can't be; outputs aren't usable as inputs.

> [!NOTE]
> Unix was always agnostic about its intended audience and designers. They expect the output of every program to become the input to another, as yet unknown, program. The implementers never assumed they knew all the potential uses the system could and would be put to. [^raymond-around]

#### High mnemonic load

The disadvantage of the CLI style, of course, is that it almost always has high mnemonic load (low ease), and usually has low transparency. Most people (especially non-technical end users) find such interfaces relatively cryptic and difficult to learn. [^raymond-tradeoffs]

#### Resistance tends to decrease 

Resistance to command language interface tends to decrease as users become more expert. In many problem domains, users (especially frequent users) reach a crossover point at which the concision and expressiveness of CLI becomes more valuable than avoiding its mnemonic load. [^raymond-tradeoffs]

Computing novices prefer the ease of graphical user interface, but experienced users often gradually discover that use of the command interface tends to gain utility as problems scale up and involve more in the way of canned, procedural and repetitive actions. [^raymond-tradeoffs]

> For example, software such as Microsoft Word or Libre Office Writer, where the content looks very similar to the end result when edited, is usually the easiest route to composing relatively small and unstructured documents. But for complex book-sized documents that are assembled from sections and which may require many global format changes and structural manipulation during composition, a combination of markup language (such as Markdown) or meta-language (such as XML) with a type-setting system (such as LaTex) is usually a more effective choice. [^raymond-tradeoffs]

#### Scriptability

The CLI style of early Unix has retained its utility long after the demise of teletypes for reasons that CLI interfaces are highly scriptable, they readily support the combining of programs. The **scriptability** of an interface is the ease with which it can be manipulated by other programs. Scriptable programs are readily usable as components by other programs, reducing the need for costly custom coding and making it relatively easy to automate repetitive tasks. It is a quiet but tremendous productivity booster not available in most other software environments. [^raymond-tradeoffs]

GUIs are simply not scriptable at all. Every interaction with them has to be human-driven. Instead of an executive who gives high-level instructions, the user is reduced to an assembly-line worker who must carry out the same task over and over. [^raymond-tradeoffs]

With graphical desktop interfaces, software robotics is required to achieve the equivalent of scripting such as combining program data, streamline routine processes and minimise human error. **A software robot** runs applications as a human would. Therefore, the specification of software robots is usually not called programming, but training a virtual worker.

<!-- - Usually (though not always) CLIs have an advantage in **concision** as well. Consider modifying the color table in a graphic image. If you want to change one color (say, to lighten it by an amount you will only know is right when you see it) a visual dialogue with a color-picker widget is almost mandatory. But suppose you need to replace the entire table with a set of specified RGB values, or to create and index large numbers of thumbnails. These are operations that GUIs usually lack the expressive power to specify. Even when they do, invoking a properly designed CLI or filter program will do the job far more concisely. Even on modern systems the graphical programs are likely calling (~40 year old) simple CLI utilities in the background (to do much of the heavy lifting). -->

<a id="command-language-interface"></a>

### I - Command Language Interface

**Command Language Interface** is a way of organizing the use and communication of computer programs in textual form. The same interface allows communication both with a human, and between different programs (see [Section: Command language](#command-language)).

<a id="command-language"></a>

### II - Command Language

**Command Language** refers to the grammar rules of the computer's command interface and is strongly linked to the underlying operating system. A command language has a simpler grammar than a general-purpose programming language. Another difference between a command language and a programming language is that a command language is read, structured and executed in an orderly fashion. A syntax error in the middle of a command sequence is only detected when the execution reaches it. A programming language, on the other hand, is fully parsed before execution begins. Common examples of shell languages are *GNU Bash* and *Microsoft Batch*. A shell language is optimised for interactive use on the command line, but more complex and frequently used scripts can be stored in a file (shell scripting).

<!--
**Command Language** is a language for job control in computing. It is a domain-specific and an interpreted language. Common examples of a command language are *shell for unices* or *batch for DOS/Windows*. These languages can be used directly at the command line (**interactive**), but can also automate tasks (that would normally be performed manually at the command line).

> As command languages are optimized for **interactive** use: strings don't require quotation marks, most commands are executed immediately after they're entered, most things you do with it will invoke external programs rather than built-in features, and so forth.

Command languages share the domain of lightweight automation with scripting languages, though a command language usually has stronger coupling to the underlying operating system. Command languages often have a more simple grammar and syntax compared to scripting languages. Another distinction between command languages and many scripting languages is that command languages are read, parsed, and executed in order. A syntax error in the middle of a command language script won't be detected until execution reaches it. A Perl or Python script, by contrast, is parsed completely before execution begins (This is a significant difference, but it doesn't mark a sharp dividing line. If anything it makes Perl and Python more similar to compiled languages).
-->

<a id="command-language-interpreter"></a>

### III - Command Language Interpreter 

When you launch a terminal window, or otherwise log in to the command line, the system loads a **shell** program (such as ` $ bash `), which is first and foremost a **command language interpreter** i.e. **command processor**. It executes commands that it reads from a) a command line string, b) a specified file, or c) standard input (see [Chapter 6, Section: Standard streams](06-inter.md#standard-streams)). d) The shell program is also used in the background by various software applications and system services. [^hoffman]

[^hoffman]: [Chris Hoffman - What's the difference between Bash and other shells?, published 2017](https://www.howtogeek.com/68563/htg-explains-what-are-the-differences-between-linux-shells/#:~:text=The%20most%20prominent%20progenitor%20of,worked%20at%20AT%26T's%20Bell%20Labs.)

The shell program implements the command language interface when it communicates with other parts of the system based on the commands it receives. The shell also often refers to the language it interprets. So they are also **interpreted languages**. Shell programs are also the primary interface for many people, and so many features have been accumulated over the years, that we should refer shells as **shell environments** or **command interpreter environments**. [^hoffman]

<!-- The analogy is with a nut: outside is the shell, inside is the kernel. -->

<!--
A **shell** is first and foremost a **command language interpreter** i.e. **command processor**. A command language interpreter executes commands read from a) a command line string, b) the standard input, or c) a specified file. The shell is implementing a *command language interface*, when it communicates with the OS's kernel through user input commands. A specific shell (such as bash) always refers to the interpreter, but often also to the language that it interprets; as many shells such as bash are also an **interpreted language**.

When you sign in at the command line or launch a terminal window on GNU/Linux, the system launches a shell program. The shell programs are also used in the background by various system services. GNU/Linux distributions include many functions written as shell scripts. These scripts are commands and other advanced functions that run through a shell environment.
-->

#### Alternative shells

On most Unix-like systems, the file path of the primary shell is ` /bin/sh `. The file usually turns out to be a symbolic link to a [POSIX-compatible shell](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html), most commonly Bourne Again Shell ` /usr/bin/bash `. But you can swap out the default shell for another one, if you like.

Alternate shell environments can be installed from the operating system package manager and experimented with by calling them by filename such as ` $ sh↵ `, ` $ dash↵ `, ` $ zsh↵ ` to start that environment. Finally type ` $ exit↵ ` at the shell to leave it, and return to the default shell.

<!-- An alternative shell environment can be installed using the default package manager of the operating system. And then tried by calling it with by name (such as ` $ sh↵ `, ` $ dash↵ `, ` $ zsh↵ `). The command ` $ exit↵ ` will take you back to the original shell environment. -->

> [!TIP]
> You can generally use the ` $ chsh↵ ` (change shell) command to change the default shell. The one you see when you sign in, known as your *login shell*. Try pressing ` Ctrl + C `, if you strugle to cancel and exit the default login shell change -operation.

<!--
> [!TIP]
> The change-shell-command ` $ chsh↵ ` can be used to permanently change the default shell, so it will load automatically at login. The ` $ chsh ` process can be cancelled by pressing the ` Ctrl + C ` keyboard shortcut.
-->

<!--
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
-->

#### Alternative shell: Thompson Shell

**Thompson Shell ` $ sh `** was the first Unix shell. It was introduced in the first version of Unix in 1971. [^wiki-thompson-shell] It was written by Kenneth Thompson, an American computer science pioneer who worked at Bell Labs for most of his career. [^wiki-ken-thompson]

[^wiki-thompson-shell]: [Wikipedia - Thompson shell, accessed 2025](https://en.wikipedia.org/wiki/Thompson_shell)

[^wiki-ken-thompson]: [Wikipedia - Ken Thompson, accessed 2025](https://en.wikipedia.org/wiki/Ken_Thompson)

> Shell environments have been building on the concept ever since, adding a variety of new features, functionality, and speed improvements. For example, Bash offers [command and file name completion](03-basic-terminal.md#autocomplete)), advanced scripting features, a [command history](#bash-history), [configurable colors](07-advanced-terminal.md#8-bit-256-colors), [command aliases](03-basic-terminal.md#alias), and a variety of other features that were not available back in 1971 when the first shell was released. [^hoffman]

#### Alternative shell: Bourne Shell

The most prominent progenitor of modern shells is the **Bourne Shell ` $ sh `** which was named after its creator Stephen Bourne who worked at AT&T’s Bell Labs. Released in 1979, it became the default command-interpreter in Unix because of its support for features such as [command substitution](07-advanced-terminal.md#expansions-and-quoting), [piping](06-inter.md#pipelines), variables, [condition testing](07-advanced-terminal.md#square-brackets), and looping. It did not offer much customization for users, and did not support such modern niceties as aliases, command completion, and shell functions (though this last one was eventually added). [^wiki-bourne-shell]

[^wiki-bourne-shell]: [Wikipedia - Bourne shell, accessed 2025](https://en.wikipedia.org/wiki/Bourne_shell)

#### Alternative shell: C shell 

**C Shell ` $ csh `** was developed in the late 1970s by student Bill Joy at the University of California, Berkley. It added many interactive elements such as command history and aliases (i.e. shortcuts for long commands). [^wiki-c-shell]

Over time, lots of people fixed bugs and added features to the *C shell* This culminated in an improved version known as **TENEX C Shell ` $ tcsh `**. Although tcsh started as a branch of the original csh, it is now the main branch of the ongoing development of csh. [^wiki-c-shell]

[^wiki-c-shell]: [Wikipedia - C shell, accessed 2025](https://en.wikipedia.org/wiki/C_shell)

#### Alternative shell: Korn Shell

Bell Labs employee David Korn worked in the early 1980s to address the limitations of the existing Unix shell. The goal was to combine the best features of other shells into one powerful tool. The project attempted to improve the situation by being backwards compatible with the Bourne Shell language, but adding many features of csh. **Korn Shell ` $ ksh `** was released in 1983, but under a proprietary license that restricted distribution. It only became free software much later, when it was re-released under an open source license. [^wiki-korn-shell]

[^wiki-korn-shell]: [Wikipedia - Korn shell, accessed 2025](https://en.wikipedia.org/wiki/KornShell)

#### Alternative shell: Bourne Again Shell  

The GNU Project developed a shell, under its own free and open source license (see [Chapter 1, Section: GNU General Public -license](01-intro.md#gnu-gpl)), as part of its free operating system and named it **Bourne Again Shell ` $ bash `**. [^wiki-bash-shell]

Since its first release in 1989, bash has been improved for decades. And it is still the default shell environment for most GNU/Linux distributions. [^wiki-bash-shell] It was also the default shell for macOS until 2019. However, since macOS Catalina, it has been replaced by **Z Shell ` $ zsh `**. <!--, which is licensed by MIT to better fit the closed source nature of macOS.--> [^apple-zsh]

[^wiki-bash-shell]: [Wikipedia - Bash (Unix shell), accessed 2025](https://en.wikipedia.org/wiki/Bash_(Unix_shell))

[^apple-zsh]: [Tom Warren - Apple replaces bash with zsh, published 2019](https://www.theverge.com/2019/6/4/18651872/apple-macos-catalina-zsh-bash-shell-replacement-features)
    
> [!NOTE]
> While the Linux community has settled on bash in the years since, developers did not stop creating new shells.

#### Alternative shell: Almquist Shell 

<!-- TODO: Lisää vuosiluku -->

Kenneth Almquist created a Bourne Shell clone named **Almquist Shell**, and also known as **A Shell** and **` $ ash `**. It is designed to be POSIX-compatible and lightweight. It is faster than bash because it does not have all its features. It became the default shell in BSD, a different branch of the unix like operating systems. The ash shell is more lightweight than bash, which makes it popular in embedded GNU/Linux systems. [^wiki-almquist-shell]

Ash has been ported for the Debian platform, under the name **` $ dash `**. Ubuntu uses dash for non-interactive tasks due to its lightweight nature and low programming library dependencies. This speeds up background tasks, as well as its use as a scripting language. However, Ubuntu still uses bash for interactive shells, so users have the full-featured interactive environment. [^wiki-almquist-shell]

[^wiki-almquist-shell]: [Wikipedia - Almquist shell, accessed 2025](https://en.wikipedia.org/wiki/Almquist_shell)
    
#### Alternative shell: Z Shell

One of the most popular newer shells is **Z Shell ` $ zsh `**, started by Paul Falstad in 1990. The POSIX-compatible zsh is Bourne-style and incorporates the features of bash, but above all is customizable and extensible with plug-ins. It is probably the most feature-rich unix shell environment available today. The user community collects third-party plug-ins and themes for the [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh/) website. [^wiki-z-shell]

[^wiki-z-shell]: [Wikipedia - Z shell, accessed 2025](https://en.wikipedia.org/wiki/Z_shell)

#### Alternative shell: Friendly Interactive Shell

Another newer shell is the **Friendly Interactive Shell ` $ fish `**, released since 2005. It has a unique command language syntax that is designed to be a bit easier to learn. Features also include extensive in-use guidance. [^wiki-fish-shell]

But what you learn by using fish won't help you in bourne-like environments. Fish is not fully POSIX-compatible. The developers have chosen to ignore the standard where they felt it was necessary. [^fi-fish]

[^wiki-fish-shell]: [Wikipedia - Fish (Unix shell), accessed 2025](https://en.wikipedia.org/wiki/Fish_(Unix_shell))

[^fi-fish]: [Linux.fi ohjesivusto - Fish, accessed 2025](https://www.linux.fi/wiki/Fish)

<!-- TODO: Lisää nu shell -->

### IV - Shell prompt

The Unix **shell prompt** is the equivalent of the Windows **command prompt**
- **Shell** = the outer layer
- **Prompt** = to encourage somebody to speak
- **Command** = an order given

Shell command prompt is a signal for the user, and refers to the ability to receive commands from the user:

a) **Dollar sign ` $ `** indicates readiness to receive commands, and
    - Refers to working with usual low privileges.
b) **Hash mark ` # `** indicates readiness to receive commands, and
    - Refers to working with elevated root privileges.
c) **Other prompt symbols** may appear in some context:
    - Such as the greater than sign ` > ` and the percent sign ` % `.
d) The prompt symbol is not strictly required.
    - Users can modify the prompt to suit their taste and workflow. And it is possible to configure a shell to not display any prompt symbol. See [Chapter 7, Section: Modifying the default prompt](07-advanced-terminal.md#modifying-the-default-prompt).

<!--The dollar sign or hash mark known also as the number sign or pound sign, means that the shell is ready to accept commands from the terminal.
- The dollar sign (<span>$</span>) suggests that you are working as a regular user in Linux.
- While working as a super user (i.e. root user) the hash mark (#) is displayed. By contrast the traditional C shell prompt is a percent sign (<span>%</span>).-->

> What is the origin of the UNIX dollar prompt, you may wonder? We can only guess, but version 7 UNIX released in 1979 was the first to have the dollar sign. That’s the release which introduced the Bourne Shell, replacing the Thompson Shell used in previous versions of Unix. Version 6 UNIX didn't have the dollar sign. In the era of version 6 and earlier, before UNIX was sold commercially, it was distributed with complete source code. The switch to the dollar sign can be thought of as a result of the commercialisation of UNIX as in ` $hell `. <!--The author of Bourne Shell, Steve Bourne, was an employee of Bell Labs.--> [^dollar-prompt]

[^dollar-prompt]: [StackExchange - What is the origin of $ prompt?, accessed 2025](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)

### Terminal Emulator

A **terminal emulator** or terminal application is a computer program that emulates a legacy video terminal within some other display architecture. A terminal emulator inside a graphical user interface is called a terminal window. A terminal provides the user a *command language interface* through a shell (see [Section: Command Language Interpreter](#command-language-interpreter)).

> Before the Linux project expanded into a full operating system kernel, the author Linus Torvalds initially made a mere terminal emulator. That is, Linux was initially run in purely textual mode, completely without a graphical user interface.

#### Mac and Windows users have forgotten about the CLI

In Windows, the command line is no longer in regular use, and the ability to start the computer in command line mode is gone. In GNU/Linux, the command line still plays an important role, for both good and bad. Graphical management tools for GNU/Linux distributions have not replaced the use of the command line, as developers still find text mode most conveniant.

When Linux first came to be in 1991, most things were still text. True, Windows 3.0 was out, and MacOS had been with us since 1984 but graphics were memory hungry "nice to haves" and people worked predominantly in a textual user interface. If you wanted graphics, you had to have an expensive, powerful PC and most people did not think that was really worth the cost.

Over the years, people who used the desktop operating systems such as macOS and Windows have mainly forgotten about the fact that the command interface still exists. But for systems people, the people that want to do operations in bulk, or do them remotely, they still use the command interface often. In November 2006 Microsoft released a thing called Windows PowerShell for this exact reason. <!-- macOS gives us the bourne shell (the UNIX shell from BSD). And Linux gives us the Bash shell (the Bourne Again SHell, which is just an enhanced edition of the bourne shell that you find on a Mac). -->

<a id="cut-and-paste"></a>

## 2.2 Cut and paste

### Strange keyboard shortcuts

In a terminal window, the keyboard shortcuts most commonly used to copy and paste are:
- **` Ctrl + Shift + V `** for pasting text into a terminal window.
- **` Ctrl + Shift + C `** for copying text from a terminal window.

Elsewhere in a modern graphical desktop interface, you can use:
- The more familiar ` Ctrl + C ` for copy and ` Ctrl + V ` for paste.

#### The old meaning of these keyboard shortcuts

> [!WARNING] 
> You might have tried to use ` Ctrl + C ` and ` Ctrl + V ` to perform copy-paste inside a terminal window, and found out that they do not work. These control codes have different meanings to the shell and were assigned many years before the use of ` Ctrl + C ` to copy, and ` Ctrl + V ` to paste from session-wide clipboard, that was introduced for Macintosh in 1983 and Windows in 1990.

**` Ctrl + C `** was the **interrupt** key almost everywhere in Unix. And even now it can be used to <ins>cancel</ins> the current program or operation in a terminal session.

**` Ctrl + V `** often meant **verbatim insert**; That is, insert the following control character literally without performing any associated action (see [Chapter 3, Section: Control characters](03-basic-terminal.md#control-characters)).
- For example, a normal ` Esc ` switches to command mode in the terminal, but even now ` Ctrl + V, Esc ` will insert Esc control character in caret notation ` ^[ ` into the current position (see [Chapter 3, Section: Inserting a control character](03-basic-terminal.md#inserting-a-control-character)).

### IBM Common User Access -keys

Earlier Windows versions (1.x and 2.x), as well as IBM OS/2, only supported the **IBM CUA keys**: **` Ctrl + Ins `** to copy and **` Shift + Ins `** to paste. Infact these keyboard shortcuts have remained supported by all GNU/Linux and Windows versions to date. [^ibm-cua]

[^ibm-cua]: [Wikipedia - IBM Common User Access, accessed 2025](https://en.wikipedia.org/wiki/IBM_Common_User_Access)

### Middle mouse button

In GNU/Linux there is also an alternative way to paste content, the click of the middle mouse button.
- You can select text in one program and insert it using the middle mouse button, even without any explicit copy action. Give it a try if you can. Some desktop environments such as Ubuntu's Unity no longer support it though.
- Elements in a window will be able to receive input even when the parent window is not focused on the foreground. The focus follows the mouse so to speak.

<!--
- This can be a very useful feature that allows you to do things efficiently, but it can also be very annoying at times; Especially for those with a sensitive mouse.
    - You will find that everytime you scroll your mouse wheel too fast (which translate into a middle click), it will paste the previous copied content to your text editor, documents or any other input text field, without your knowledge.
    - As this is a system level feature, there are no easy ways to disable the mouse middle click to paste feature. Fortunately there are some [workarounds](https://www.maketecheasier.com/disable-middle-mouse-click-to-paste-feature-in-linux-quick-tips/) and hacks that can be used.
-->

<a id="text-selection"></a>

## 2.3 Text selection

> [!NOTE]
> One can highlight text only on modern GUI terminal emulator software and even then only with a mouse. Younger readers may not be aware that terminals used to print. On paper. Very slowly. When the constraint of the slow printing terminals of 1969 was gone, Unix evolved in a world of video display terminals; Many of which still had no arrow keys, or function keys. [^raymond-tale]

Still even today some users might encounter instances when they cannot use the mouse, to highlight text. And if you cannot highlight any text, how can you copy and paste it? Whatever situation you find yourself in when using a GNU/Linux, there will be a way to "copy and paste". You have options. Some of them are strange, but at least there are options. Any unix terminal will let you cut and paste on current command line:

| Keys | Use case |
|:--- |:--- |
| ` Ctrl + U ` | **Cut** the part of the **line before** the cursor (and add it to the clipboard buffer). |
| ` Ctrl + K ` | **Cut** the part of the **line after** the cursor (and add it to the clipboard buffer). If the cursor is at the start of the line, it will cut and copy the entire line. |
| ` Ctrl + W ` | **Cut** the **word before** the cursor (and add it to the clipboard buffer).  |
| ` Alt + D ` | **Cut** the **word after** the cursor (and add it to the clipboard buffer). |
| **` Ctrl + Y `** | **Paste** (the last text that was cut and copied). |

<a id="bash-history"></a>

### Bash history

Bash remembers the commands you type, and by default stores them in a history file ` ~/.bash_history ` which persists between sessions.

Old commands can be retrieved for reuse

a) With the arrow keys
    - ` Up arrow ` will scroll through the old commands.
    - ` Down arrow ` will return to the newer commands.
b) Through reverse-incremental-search
    - The feature is activated by pressing ` Ctrl + R `. Once you see the prompt ` (reverse-i-search)': _ ` start typing any part of a previous command, and bash will instantly show the most recent match. You should be able to cycle through alternatives by repeatedly hitting ` Ctrl + R `. Once you find the command you want, press ` Enter ` to run it again, or use ` Left arrow ` or ` Right arrow ` keys to edit it first.

> [!NOTE]
> Reverse-incremental-search is a feature borrowed from [screen editor Emacs](08-text-editors.md#screen-editor-emacs), where the same terminology is used for searching through text buffers: [^gorg-com] [^gorg-his] [^gorg-inc]
>
> **Reverse:** Because it searches backward through your command history; from the most recent command to older ones.
>
> **Incremental:** Because the search happens as you type, character by character. Each new keystroke refines the search in real time. Non-incremental search would read the entire search-string before starting to look for matching lines.
> 
> **Search:** Because you’re looking for a match in your history.

[^gorg-com]: [Gnu.org - Commands For Manipulating The History, accessed 2025](https://www.gnu.org/software/bash/manual/html_node/Commands-For-History.html)

[^gorg-his]: [Gnu.org - Searching for Commands in the History, accessed 2025](https://www.gnu.org/software/bash/manual/html_node/Searching.html)

[^gorg-inc]: [Gnu.org - Emacs Incremental Search, accessed 2025](https://www.gnu.org/software/emacs/manual/html_node/emacs/Incremental-Search.html)

<!--- To walk backwards through the commands you've used press ` Up ` arrow key multiple times
- To walk forwards through the commands you've used press ` Down ` arrow key multiple times-->

Making use of command history can be a lot more powerful than one might realize:
- [Chris Hoffman - How to use bash history, 2017](https://www.howtogeek.com/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/)
- [Dave McKay - How to use the history command, 2024](https://www.howtogeek.com/465243/how-to-use-the-history-command-on-linux/)

<a id="directory-structure"></a>

## 2.4 Directory structure

As you get acquainted with GNU/Linux, perhaps the biggest confusion, for those accustomed to Windows, is the unix-style directory structure. The directory structure of a GNU/Linux generally follows the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html). While the directory structure may not need to be touched by the base user, it should be good to know what is where.

Unix and it's derivates do not use Microsoft's way of grouping directories under drives and hard disk partitions (such as C, D, E and so on). For example, when reading (and writing to) a compact-disc, one does not refer directly to the drive but under the mount point to the directory ` /media/ `. The Unix-style directory structure was originally based on the assumption that each directory can have its own hard drive, and for a home user, this may seem absurd.

Some directories are virtual such as the ` /sys/ ` interface, that describes connections between hardware and drivers. Even the printer, mouse and keyboard are files. All this understandably adds to confusion. The fact that everything is a file, can be first understood and finally appreciated, from a programming perspective.

### Directory ≠ Folder

With release of Window 95 in 1995, Microsoft seemed to complete replace the well-established word directory with another word, folder. The convention has spread from the mid-1980s Macintosh system software, the lesson of which was sought from the pioneering work of Xerox's Palo Alto Research Center. 

Although folder and directory are essentially the same thing, they are separated by perspective.
- **Directory** is a file system object that contains files and other directories.
- **Folder** is a graphical user interface metaphor and an object-oriented counterpart to a directory. Unlike a directory, a folder can be a virtual construct that does not necessarily map directly to a specific storage location. In this sense, the new term has its legitimacy.
    - Microsoft Windows uses the concept of special folders to help present the contents of the computer to the user in a fairly consistent way that frees the user from having to deal with absolute directory paths. **Control Panel** provides access to various system features and settings. **Recycle Bin** provides an interface for managing deleted files. **This Computer** provides access to connected drives and devices.

### Special term: root

It is a little confusing that the word **root** is used for three different things:
1. The root user i.e. the system administrator.
2. The root user's home directory, found under ` /root/ `.
3. The root of the filesystem tree, marked by forward slash ` / `.

### Home directories

- Home directory for the root user is always **` /root/ `**.
- Home directories for all other users are located under **` /home/ `**.
    - When harddrives were much smaller, ` /home/ ` used to be on a different disk, and was mounted comparatively late, when the system went up.
    - In contrast ` /root/ ` was deemed essential for system maintenance purposes, and thus had to be present at any rate; Even when the *user disk* was not mounted.

> [!TIP]
> A typical non-root user's home directory would be ` /home/$USER `. The shorthand ` ~ ` or ` $HOME ` will expand to whatever the home directory is, such as ` /home/GitJit-max/ `.

>A newly created home directory is usually initialized by the Freedesktop.org [xdg-user-dirs](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/) program, so that the new user's home directory is pre-populated with basic subdirectories (such as Desktop, Documents, Downloads, Pictures) named according to the language setting.

<a id="software-applications"></a>

### Software applications

All applications are not stored at the same location, as each directory serves a unique purpose.

>  In the old days critical system binaries, or simply default minimal required binaries, would have been in ` /bin/ ` and ` /sbin/ `. Other non critical, additional binaries resided elsewhere such as under ` /usr/ `. That way ` /usr/ ` could reside on something that isn't available right at boot such as a network drive. If you wanted to do this on a modern system, it would end up being a huge hassle because modern distributions no longer properly separate ` /sbin/ ` and ` /bin/ ` from their equivalents under ` /usr/ `.

> [!NOTE] 
> Here **binary** refers to an executable; a type of binary file (i.e. file composed of something other than human-readable text) that contains machine code for the computer to execute.

#### System binaries

Traditionally, essential binaries that were available to all users (such as ` $ ls ` and ` $ find `) resided in **` /bin/ ` (binaries)**.
- These days ` /bin/ ` might just be a symlink to ` /usr/bin/ ` where such binaries have been moved.

Traditionally, essential root-only binaries (such as ` $ adduser `) resided in **` /sbin/ ` (superuser binaries)**.
- These days ` /sbin/ ` might just be a symlink to ` /usr/sbin/ ` where such binaries have been moved.

#### Shared libraries

Traditionally, essential shared library files needed (by binaries in ` /bin/ ` and ` /sbin/ `) to boot the system and run the commands in the root filesystem resided in **` /lib/ ` (libaries)**.
- These days ` /lib/ ` might just be a symlink to ` /usr/lib/ ` where such library files have been moved.

> [!NOTE] 
> Here **libraries** refer to modular development and are shared and reused by many different programs. Libraries, object files and binaries under ` /usr/lib/ ` are not intended to be executed directly by users or shell scripts. [^wiki-kirjasto]

[^wiki-kirjasto]: [Wikipedia - Kirjasto (tietotekniikka), accessed 2025](https://fi.wikipedia.org/wiki/Kirjasto_(tietotekniikka))

#### Additional software applications

Both traditionally and these days, applications installed through package management reside under **` /usr/ ` (unix shared resources)**.

Traditionally UNIX vendors (like AT&T, Sun, DEC) and third-party vendors would use  **` /opt/ `** to hold packages that you might have paid extra money for (hence the name **option packages**).
- These days ` /opt/ ` is still used by many third-party packages, such as [Master PDF Editor](https://code-industry.net/free-pdf-editor/) and [ONLYOFFICE Desktop Editors](https://www.onlyoffice.com/download-desktop.aspx?from=desktop) installed from dot-deb-packages.
- There was no ` /opt/ ` on all Unix variants such as Berkeley BSD UNIX, which used **` /usr/local/ `** for stuff that you installed yourself.

#### Directory: /usr/

The ` /usr/ ` directory contains only shareable and read-only data, no settings, no log data. Any information that is host-specific or varies with time is stored elsewhere. The most important subdirectories are:

| Dir | Use |
|:--- |:--- |
| **` /usr/sbin/ `** <br>= **` /sbin/ `** | **Most root user commands/executables** reside in ` /usr/sbin/ `. There must be no subdirectories here. [^fhs-sbin] [^fhs-usr-sbin] |
| **` /usr/bin/ `** <br>= **` /bin/ `** | **Most user commands/executables** reside in ` /usr/bin/ `, which is the primary directory of executables on the system. There must be no subdirectories here. [^fhs-bin] [^fhs-usr-bin] |
| **` /usr/lib/ `** <br>= **` /lib/ `** | There are lots of **shared libraries** available in a GNU/Linux system, capable of doing a lot of useful things. And many of those libraries can be reused by other programs. The libraries, object files and possibly even binaries under ` /usr/lib/ ` are not intended to be executed directly by users or shell scripts. Applications may use a single subdirectory. [^fhs-usr-lib] [^fhs-lib] |
| **` /usr/include/ `** | **Header files** included by mostly C programs reside here. Header files usually have a ` *.h ` extension, but you will occasionally see them with other extensions such as ` *.hpp ` or ` *.d ` or no extension at all. The topic of header files can seem daunting for those unfamiliar with C language. A header file contains function declarations, type definitions, and other global declarations that are shared across multiple source files. It allows to separate the interface (function prototypes) from the implementation (function definitions). [^fhs-usr-include] |
| **` /usr/share/ `** | The processor architecture-independent i.e. non executable, **static data files of applications** are shareable among all architecture platforms of a given OS (such as x86 32-bit, x86_64 64-bit, ARM 32-bit, ARM 64-bit, MIPS). Not to be confused being shared by different OSes or by different releases of the same OS. That is most <ins>data required by programs, that doesn't need to be modified</ins> reside here. The data stored in ` /usr/share/ ` must be purely static such as manual pages, word lists for various languages (i.e. vocabulary), XML and HTML doctype declarations, postscript printer definition files, ICC color management files. Any modifiable data is stored elsewhere. [^fhs-usr-share] |

[^fhs-sbin]: [Filesystem Hierarchy Standard: System binaries](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#sbinSystemBinaries)

[^fhs-usr-sbin]: [Filesystem Hierarchy Standard: Non-essential standard system binaries](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrsbinNonessentialStandardSystemBi)

[^fhs-bin]: [Filesystem Hierarchy Standard: Essential user command binaries)](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#binEssentialUserCommandBinaries)

[^fhs-usr-bin]: [Filesystem Hierarchy Standard: Most user commands](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrbinMostUserCommands)

[^fhs-usr-lib]: [Filesystem Hierarchy Standard: Libraries for programming and packages](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrlibLibrariesForProgrammingAndPa)

[^fhs-lib]: [Filesystem Hierarchy Standard: Essential shared libraries and kernel modules](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#libEssentialSharedLibrariesAndKern)

[^fhs-usr-include]: [Filesystem Hierarchy Standard: Header files included by C programs](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrincludeHeaderFilesIncludedByCP)

[^fhs-usr-share]: [Filesystem Hierarchy Standard: Architecture-independent data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrshareArchitectureindependentData)

> [!TIP]
> It may be useful to use library functions in your own programs. For example [VLC](https://www.videolan.org) the well known and popular media player has a versatile but less known accompanying library SDK for developers named [libvlc](https://wiki.videolan.org/LibVLC/). Libraries may be used, even if they were written in other programming languages, such as using C-language library functions from the BASIC language dialect and integrated development environment [Gambas](https://en.wikipedia.org/wiki/Gambas). [^gambas-wiki] [^gambas-extern]

[^gambas-wiki]: [Wikipedia - Gambas, accessed 2024](https://en.wikipedia.org/wiki/Gambas)

[^gambas-extern]: [Gambas Documentation - How To Interface Gambas With External Libraries, accessed 2024](https://gambaswiki.org/wiki/howto/extern)

#### Environment variable: PATH 

When the user types a CLI command, the system looks for the requested binary executable(s) in directories specified by an environment variable called PATH (see [Section: Environment variables](#environment-variables)). 

> [!IMPORTANT]
> To run a program or script located elsewhere, the location must be explicitly reported with the command. Even as little as the notation ` ./ ` to refer to the present working directory.

If you want to run an executable located outside of PATH, such as ` ~/.local/bin/somexe `, you have to include the file path in some form for this to work:

```
# a) This common mistake will not work:
margaret@laptop ~ $ cd .local/bin↵  # Switch to program directory
margaret@laptop bin $ somexe↵       # Filename is not enough
bash: somexe: command not found     # Program will not start

# b) Relative path works:
margaret@laptop bin $ ./somexe↵  # Program will start

# c) Relative path works:
margaret@laptop bin $ cd ..↵   # Switch away from program dir
margaret@laptop .local $ bin/somexe↵  # Program will start

# d) Absolute path works:
margaret@laptop .local $ ~/.local/bin/somexe↵ # Program will start
```

If the directory ` ~/.local/bin/ ` would have been included in PATH, the program could have been started by calling it by the filename only: ` $ somexe↵ ` from within any directory, including present working directory.

> [!TIP]
> Command ` $ echo $PATH↵ ` reveals all directories contained in PATH:
>
> ```
> $ echo "$PATH" | tr ':' '\n'↵
> /home/margaret/.local/bin
> /usr/sbin
> /usr/bin
> /snap/bin
> ```

### Dynamic data

Static and dynamic data are separated in different directories:
- **Dynamic data** is likely to change.
- **Static data** remain relatively unchanged.

The **` /var/ `** (variable) directory tree is used to store the application **data that is likely to change** such as kernel logs, server logs, pending emails, ongoing downloads, package management files.

Applications must generally not add directories to the top level of ` /var/ `. Instead following subdirectories, or symbolic links are used:

| Dir | Use | RAM<br>Disk |
|:--- |:--- | --- |
| **` /var/cache/ `** | Application **cache data stored to serve future requests faster**. The data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere. Cache data must remain valid between restarts. And the application must be able to recreate or restore deleted cache (unlike buffer data in ` /var/spool/ `). [^fhs-cache][^wiki-cache] |   |
| **` /var/lib/ `** | Variable **state information that programs modify while they run and must not be exposed to regular users**. An application, or a group of inter-related applications, should generally use a subdirectory for their data. There is one required subdirectory ` /var/lib/misc/ ` which is intended for state files that dont need a subdirectory. [^fhs-lib] |   |
| ` /var/lock/ ` <br>= **` /run/lock/ `** | Some programs follow a convention to create a **lock file to indicate use of a particular device or file**, so other programs can take care not to use the locked device or file simultaneously. [^fhs-lock][^tldp-var] | ✓ |
| **` /var/log/ `** | Information of many events and activities are stored in **log files**, either directly in this directory or in a suitable subdirectory. Log entries can be used to debug problems, and to monitor and understand system operation. [^fhs-log] |   |
| **` /var/opt/ `** | **Variable data of the option packages** installed in ` /opt/ `. Data is stored in a subdirectory named after the software package. [^fhs-opt] |   |
| ` /var/run/ ` <br>= **` /run/ `** | **Dynamic data relevant to running processes that is not stored on disk, but kept in volatile memory**; <!--or disk-based swap--> But takes on the appearance of a mounted file system to allow it to be more accessible and easier to manage. Run is available early in the boot process, and may be needed by certain services and processes before the full operating system is loaded. Run is cleared on system reboot. Run has no write access for unprivileged users, and write access to user-specific subdirectories are for owners only. [^fhs-run] [^sandra] | ✓ |
| **` /var/spool/ `** | Spool data is **application's buffer data which awaits further processing** such as printer queues. Often spool data is deleted after it has been processed. [^fhs-spool] |   |
| **` /var/tmp/ `** | Available for programs that need **temporary files** or directories, **which are preserved between reboots**. Files and directories in this directory must not be deleted when the system boots. [^fhs-tmp] |   |

[^wiki-cache]: [Wikipedia - Cache (computing), accessed 2025](https://en.wikipedia.org/wiki/Cache_(computing))

[^sandra]: [Sandra Henry-Stocker - Exploring /run on Linux, published 2019](https://www.networkworld.com/article/967547/exploring-run-on-linux.html)

[^fhs-spool]: [Filesystem Hierarchy Standard: Application spool data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varspoolApplicationSpoolData)

[^fhs-tmp]: [Filesystem Hierarchy Standard: Temporary files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#vartmpTemporaryFilesPreservedBetwee)

[^fhs-run]: [Filesystem Hierarchy Standard: Run-time variable data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varrunRuntimeVariableData)

[^fhs-opt]: [Filesystem Hierarchy Standard - Variable data for /opt](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varoptVariableDataForOpt)

[^fhs-lock]: [Filesystem Hierarchy Standard - Lock files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varlockLockFiles)

[^tldp-var]: [Linux System Administrators Guide - The /var filesystem, accessed 2025](https://tldp.org/LDP/sag/html/var-fs.html)

[^fhs-log]: [Filesystem Hierarchy Standard - Log files and directories](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varlogLogFilesAndDirectories)

[^fhs-cache]: [Filesystem Hierarchy Standard - Application cache data](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#varcacheApplicationCacheData)

### Removable media mount points

**Mounting** is a process by which a computer's operating system makes files and directories on a storage device available. Mounting is a prerequisite for displaying the contents of the file system. If the partition of an internal-storage-drive or optical-drive is not mounted, it will only appear as a device file under ` /dev/ `. Playing a DVD movie or writing to a blank DVD does not require mounting, but mounting is required if the contents of the disc are to be handled by the file manager. [^wiki-mount] [^fi-mount]

[^fi-mount]: [Linux.fi ohjesivusto - mount, accessed 2025](https://www.linux.fi/wiki/Mount)

[^wiki-mount]: [Wikipedia - Mount (computing), accessed 2025](https://en.wikipedia.org/wiki/Mount_%28computing%29)

| Dir | Use |
|:--- |:--- |
| **` /media/ `** or <br>**` /run/media/ `** | Mount points for physical media such as a Blu-ray disc, a USB flash drive, or additional partitions of an  internal storage drive (such as the *Windows C: drive* incase of dual booting). [^fhs-media] |
| **` /mnt/ `** | Mount points for a temporarily mounted filesystems such as a network directory or a [VMware Shared Folder](https://techdocs.broadcom.com/content/broadcom/techdocs/us/en/vmware-cis/desktop-hypervisors/workstation-pro/17-0/using-vmware-workstation-player-for-linux-17-0/setting-up-shared-folders-for-a-virtual-machine-linux/mounting-shared-folders-in-a-linux-guest-linux.html) (i.e. a directory shared between a local virtual machine and the host system) [^fhs-mnt] |

[^fhs-media]: [Filesystem Hierarchy Standard - Mount point for removable media](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#mediaMountPoint)

[^fhs-mnt]: [Filesystem Hierarchy Standard - Mount point for a temporarily mounted filesystem](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#mntMountPointForATemporarilyMount)

### Hardware connection points

| Dir | Use |
|:--- |:--- |
| **` /sys/ `**<br>(system) | A virtual directory exposing some hardware, driver and kernel features. It takes on the appearance of a mounted file system to allow it to be more accessible and easier to manage. [^fhs-sys] |
| **` /dev/ `**<br>(devices) | A virtual directory that describes hardware devices such as internal storage drives and exposes some special "devices" such as a random number generator. [^fhs-dev] See [Section: Device files](#device-files) and [Section: Special device files](#special-device-files) for more information . |

[^fhs-sys]: [Filesystem Hierarchy Standard: Kernel and system information virtual filesystem](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#sysKernelAndSystemInformation)

[^fhs-dev]: [Filesystem Hierarchy Standard: Device files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#devDeviceFiles)

<a id="device-files"></a>

### Device files

Device access in unix is very different from Windows, where the internal storage drives and optical drives are represented as drive letters such as C: D: E: G: H: In unix all device entry points reside in the ` /dev/ ` directory as "files". [^hoffman-2016]

Let's explore references to internal storage drives in the ` /dev/ ` directory:
- For example, if the first *internal SATA SSD storage drive* had three primary partitions, they would be named and numbered as ` /dev/sda1 `, ` /dev/sda2 ` and ` /dev/sda3 `.
- For example, if the first *internal SATA HDD storage drive* had three primary partitions, they would be named and numbered as ` /dev/hda1 `, ` /dev/hda2 ` and ` /dev/hda3 `.
- And if the first *internal M.2 SSD storage drive* had three primary partitions, they would be named and numbered as ` /dev/nvme0n1p1 `, ` /dev/nvme0n1p2 ` and ` /dev/nvme0n1p3 `.
- An *internal Blu-ray drive* could be named and numbered as ` /dev/scd0 `
- These are all just references to the drives and partitions. The data content is exposed elsewhere through mount points (see [Section: Removable media mount points](#removable-media-mount-points)).

> [!NOTE]
> Knowledge of this internal storage naming convention will first come in handy when installing a distribution and having to select partitions or even make changes to existing partitions using a partition editor such as [GParted](https://en.wikipedia.org/wiki/GParted).

<a id="special-device-files"></a>

### Special device files

The ` /dev/ ` directory does not just contain "files" that represent physical devices. Here are three of the most notable special "devices" it also contains:

| File | Use |
|:--- |:--- |
| **` /dev/random `** | Is a random number generator you and all the applications can tap into. Truly random numbers are challenging to generate. The ` /dev/random ` kernel feature of Linux can promise up to 256 bits of security, if you wanted a source of randomness for generating cryptographic keys. [^man-ran] |
| **` /dev/zero `** | A read from ` /dev/zero ` will return as many bytes containing the value zero as was requested. Uses include wiping storage devices to ensure that no data remains, creating large empty files such as disk images, simulating memory or storage scenarios for testing, and benchmarking storage performance. [^fhs-special] |
| **`/dev/null `** | All data written to `/dev/null ` is discarded. [^fhs-special] Think of it as a black hole. [^hoffman-2016] |

> [!TIP]
> By default terminal commands produce error messages and other output that they print to the standard output (i.e. normally the terminal). If you want to run a command and do not care about its output, you can redirect that output to ` /dev/null `, which immediately discards it. Instead of having every command implement its own *quiet mode* you can use this method with any command like this ` $ somecommand > /dev/null↵ ` [^hoffman-2016]

[^fhs-special]: [Filesystem Hierarchy Standard: Devices and special files](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#devDevicesAndSpecialFiles)

[^man-ran]: [Michael Kerrisk - Linux manual page, accessed 2024](https://www.man7.org/linux/man-pages/man7/random.7.html)

### RAM disk 

All modern GNU/Linux distributions offer some of the volatile random-access memory as a RAM disk, mounted onto **` /dev/shm/ `** (shared memory). It takes on the appearance of a mounted file system to allow it to be more accessible and easier to manage. [^ramdisk]
- It can be used just like normal disk space; creating and manipulating files and directories, but with better performance compared to being stored on hard disk.
- It is an efficient means of sharing and passing data between programs. One program will create a memory portion, which other processes can access. Hence the name shared memory.
- A sophisticated image viewer could use it for temporary storage location of files extracted from zip archives to prevent unnecessary wear of the user's internal storage drive.
- Because the data resides in RAM, it will be cleared in the event of power loss, whether intentional (computer reboot or shutdown) or accidental (power failure or system crash). [^wikiram]

[^ramdisk]: [Riccardo - RAM Disk on Linux, published 2011](https://linuxaria.com/pills/ram-disk-on-linux)

[^wikiram]: [Wikipedia - RAM drive, accessed 2024](https://en.wikipedia.org/wiki/RAM_drive)

> The virtual filesystem types udev and tmpfs, don't take up disk space or occupy more RAM than used. Size and how much is available is just upper limit as to how much RAM it may use. [^ramdisk]

### Everything is a file 

In unix "everything is a file". Directories are files. Files are files. Printer, mouse and keyboard are files. Your screen is a file. The defining feature that "everything is a file" is an oversimplification. But understanding what it means will help you understand how unix and it's derivatives work. Many things on unix appear in your file system and behave as "files", but they are not actually files. They are special "files" that represent hardware devices, system information, a random number generator and what not. Almost everything in a unix-style file-system appears and behaves as files, to make data and functionality more accessible and manageable. [^hoffman-2016]

> [!TIP]
> For example to find information about your CPU, you do not need a special command that tells you your CPU info. You can just read the contents of ` /proc/cpuinfo ` as if it were a text file. You can use standard commands to print this file’s contents to the terminal. Or you can open ` /proc/cpuinfo ` in a text editor to view its contents. [^hoffman-2016]
>
> Note that ` /proc/cpuinfo ` is not actually a text file. The os kernel and the ` /proc/ ` directory or file system are exposing this information to us as a "file". This allows us to use familiar tools to view and work with the information. The same directory also contains other similar "files" such as ` /proc/uptime ` and ` /proc/version `. [^hoffman-2016]

[^hoffman-2016]: [Chris Hoffman - What does "everything is a file" mean in Linux?, published 2016](https://www.howtogeek.com/117939/htg-explains-what-everything-is-a-file-means-on-linux/)

<a id="shell-environment"></a>

## 2.5 Shell environment

### Control information 

Traditionally programs in unix-like environments look for **control information** in five places in their startup-time environment: [^raymond-live]
1. System wide [configuration files](#configuration-files) in ` /etc/ `.
2. System-set [environment variables](#environment-variables).
3. User specific [configuration files](#configuration-files) in the user's home directory.
4. User-set [environment variables](#environment-variables).
5. Switches and arguments passed to the program on the command line that invoked it (see [Chapter 3, Section: Command line options](03-basic-terminal.md#command-line-options)).

There is a strong convention that well-behaved Unix programs that use more than one of these places should look at them in the order given, allowing later settings to override earlier ones. <!--These queries are usually done in the order listed above. That way, later (more local) settings override earlier (more global) ones. Settings found earlier can help the program compute locations for later retrievals of configuration data.--> In particular, environment settings usually override dotfile settings, but can be overridden by command-line options. Some programs have command-line options that specify where the dotfile should be looked for. <!--It is good practice to provide a command-line option (like ` -e ` of ` $ make `) that can override environment settings or declarations in run-control files. -->This way the program can be scripted with well-defined behavior regardless of the run-control files or environment variables. [^raymond-live]

Which of these places are looked at depends on how much persistent configuration state a program needs to keep around between invocations. [^raymond-live]
- Programs designed mainly to be used in a batch mode (such as generators or filters in pipelines) are usually completely configured with command-line options. Good examples of this pattern include ` $ ls `, ` $ grep ` and ` $ sort `. [^raymond-live]
- At the other extreme, large programs with complicated interactive behavior may rely entirely on run-control files and environment variables, and normal use involves few command-line options or none at all. Email clients and firewalls are a good example of this pattern. [^raymond-live]

### Configuration files

<!--A **configuration file**
- Is a local file used to control the operation of a program.
- Must be <ins>static</ins> and cannot be an executable binary.-->

**Configuration** refers to the process of adjusting software settings according to specific requirements and needs. A **configuration file** contains such settings related to the software's customizability.

> [!NOTE]
> On Unix and unix-like systems, configuration files are text files, so that they are easily readable and editable by both machine and human.

#### Run-control files

<!--
When we log on to the system, the bash program starts, and reads a series of configuration scripts called startup files, which define the default environment shared by all users. This is followed by more startup files in our home directory that define our personal environment.

A **run-control file** or **script**
- Is a file of declarations or commands associated with a program that it interprets on <ins>startup</ins>.
- RC stands for "runcom" i.e. run commands. And in fact, this is exactly what the file contains, <ins>commands that the shell should run</ins>.

The exact sequence depends on the type of shell session being started; Which There are two kinds:
1. **Login shell session** is one in which we are prompted for our username and password.
2. **Non-login shell session** typically occurs when we launch a terminal session in the graphical user interface.
-->

Some configuration files are sets of commands called shell scripts. The shell executes such sets of commands at startup, so they can also be called startup files.
- When looking at file names, you sometimes come across the file extension "rc", which stands for **run commands**. Configuration files in the form of a command set are therefore referred to as **runcom file** or **run-control file**.

Different runcom files are read or skipped depending on the type of shell session being started (see [Wikipedia - Unix shell configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files)). The shell environment is therefore different depending on:

a) Whether the shell is used in the background by various software applications or system services, without direct interaction with the user (**non-interactive shell session**).
b) Whether the main session is started without logging in (**non-login shell session**), which typically occurs when starting the main session in a desktop terminal window.
c) Whether there was a prompt for a username and password (**login shell session**), which typically occurs when switching from a graphical desktop environment to a textual TTY environment (see [Chapter 7, Section: Virtual terminals](07-advanced-terminal.md#virtual-terminals)).

#### Location of configuration files

<ins>Configuration files that affect all users</ins> are located:

1. Directly under ` /etc/ `
2. In a subdirectory under ` /etc/ ` named after the program

<ins>User-specific</ins> configuration files are located:

3. At the top level of the home directory as hidden files
4. In the home directory, in a hidden subdirectory named after the program
5. In a shared hidden directory ` ~/.config/ `

<!--
Programs can also have **run-control** or **dot-directories**.
- **` ~/.config/ `** for the <ins>user-specific settings</ins>.
- **` /etc/ `** (Etcetera) for the <ins>system-wide settings</ins> i.e. configuration shared by all users at a site.

Thus with a fictional program called ` $ seekstuff ` that has both **site-wide** and **user-specific** configuration, an experienced unix user would expect to find the former at ` /etc/seekstuff/ ` and the latter at ` ~/.seekstuff/ ` in the user's home directory.

> [!NOTE]
> User-specific configuration information is often carried in a hidden run-control file in the <ins>user's home directory</ins>. Such files are often called **dotfiles** because they exploit the unix convention that a filename beginning with a dot is normally invisible to directory-listing tools, to reduce clutter.

User-specific configuration files are located in <ins>the user's home directory</ins> a) at the top level of the directory as a hidden file, b) in a hidden directory named after the program, or c) in a shared hidden directory **` ~/.config/ `**.
-->

> [!NOTE]
> By default, hidden files are not visible in file managers to reduce visual clutter.

> [!NOTE]
> Hidden files are often called **dot-files** or **dot-directories**, because dot ` . ` at the beginning of a file name makes it hidden (see [Chapter 3, Section: Period as mark to hide files](03-basic-terminal.md#period-as-mark-to-hide-files)).

#### Location of bash control files

<!-- Many startup script -files exist (or have existed in the past) such as ` .bash_profile `, ` .bash_login `, ` .profile `. -->

In a bash session, the shear number and reading order of configuration files may seem absurd (see [Wikipedia - Unix shell configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files)). If one configuration file cannot be found, the shell will try to read another, but not necessarily all. There are also differences among GNU/Linux distributions, and not just between shell variants.

On modern GNU/Linux the two most important startup files are:
1. **The most important system-wide startup file ` /etc/profile `**: applies to all users for the original Bourne Shell (sh) or any Bourne compatible shells (such as bash, zsh, ksh and ash).
2. **The most important user-specific startup file ` ~/.bashrc `**, but for the Bourne Again Shell only (bash). Other shells use their own startup files such as ` ~/.cshrc ` and ` ~/.zshrc ` (see [table](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files)).

> [!NOTE]
> The main bash configuration file for the root user can be found in the root user's home directory: ` /root/.bashrc `.

<a id="environment-variables"></a>

### Environment variables

> [!NOTE]
> The term **variable** refers to a named data store from which data can be retrieved and into which data can be written. In the Unix environment, there is a set of settings stored in environment variables that are intended to be common to all programs.

Unix style **environment variables** are name-value pairs. Both names and values are strings by type. The naming convention for unix style environment variables favors only capital letters ` A...Z `, numbers ` 0...9 ` and underscore ` _ `. 

Environment variables are inherited. When a new program starts, it receives the environment variables of the parent. Changes to environment variables affect down stream only.

Environment variables are not application-specific. They are <ins>shared among several programs</ins>. What both user and system environment variables have in common, is that it would be annoying to have to replicate the information they contain in a large number of application run-control files. And extremely annoying to have to change that information everywhere when your preference changes.

<!--When a unix program starts up, the environment accessible to it includes <ins>a set of name to value associations</ins> (names and values are both strings) called **environment variables**.
- Some of these are set manually by the user. Others are set by the system at login time, or by your shell or terminal emulator (if you're running one).
- Environment variables are <ins>application-independent preferences that need to be shared by a large number of different programs</ins>. 
- Typically, the user sets these variables in his or her shell session startup file.-->

> [!TIP]
> All environment variables and their values can be listed by running ` $ printenv↵ `
>
> The value of a single environment variable can printed by running ` $ echo $VARIABLE_NAME↵ `
>
> Users can make permanent changes to environment variables in their shell startup file (namely ` ~/.bashrc `).

<!--
> [!CAUTION]
> There is one traditional unix design pattern that we do not recommend for new programs. Sometimes, user set environment variables are used as a lightweight substitute for expressing a program preference in a run-control file. The venerable [NetHack](https://www.nethack.org) dungeon-crawling game introduced in 1987, for example, used to read ` NETHACKOPTIONS ` environment variable for user preferences. This was an old-school technique. Modern practice would lean toward parsing them from a ` .nethack ` or ` .nethackrc ` file. -->

<a id="well-known-variables"></a>

#### Well-known environment variables

There are a number of well-known environment variables you can expect to find defined on startup of a program from the unix shell. These, and especially ` HOME `, will often need to be evaluated before you read a local dotfile.

| Name | Use |
|:--- |:--- |
| ` USER ` | Current user login name (BSD convention) <!--Login name of the account under which this session is logged in (BSD convention).--> |
| ` LOGNAME ` | Current user login name (POSIX convention) <!--Login name of the account under which this session is logged in (System V convention).--> |
| ` HOME ` | Absolute filepath to the home directory of the current user. <!--This variable is important, because m--> Many programs use it to find user specific dotfiles. |
| ` COLUMNS ` | Width of the current terminal (unit of measurement is the number of characters). <!--The number of character-cell columns on the controlling terminal or terminal-emulator window.--> |
| ` LINES ` | Height of the current terminal (unit of measurement is the number of characters). <!--The number of character-cell rows on the controlling terminal or terminal-emulator window.--> |
| ` SHELL ` | File path of the primary shell. Applications use this to launch subroutines. <!--The name of the user's command shell (often used by shellout commands).--> |
| ` PATH ` | The list of directories that the shell searches when looking for the executable that match the command (see [Section: Software applications](#software-applications)). |
| ` TERM ` | Type of current terminal session such as ` xterm ` in a graphical desktop environment, ` linux ` in a [TTY virtual terminal](07-advanced-terminal.md#virtual-terminals) or ` vt100 ` on the [1978 video terminal](https://fi.wikipedia.org/wiki/VT100). ` TERM ` is special in that programs that create remote sessions over the network (such as telnet and ssh) are expected to pass it through and set it in the remote session. |
| ` EDITOR ` | File path of the primary [line editor](08-text-editors.md#line-editors-ed-and-sed), which should be able to work without advanced terminal functionality (like old `$ ed ` or ex-mode of `$ vi `). But actually, most unix programs first check ` VISUAL `. ` EDITOR ` can be considered a relic of the days when people had different preferences for line-oriented and visual editors. Nowadays, you can leave ` EDITOR ` unset, or set it to ` VISUAL ` by running commands like ` $ export EDITOR="$VISUAL"↵ ` and ` $ export VISUAL="/usr/bin/nano"↵ `. |
| ` VISUAL ` | File path of the primary [screen editor](08-text-editors.md#screen-editors). If you invoke the default text editor from the command line with the keyboard shortcut `Ctrl + X, Ctrl + E `, bash will first try ` VISUAL `, and only then, if it fails, bash will try ` EDITOR `. |

> [!NOTE]
> When an environment variable must contain multiple fields (such as ` PATH `), a colon ` : ` is used as a field separator. This convention is also used elsewhere, especially when the fields can be interpreted as file paths. [^raymond-textual]

<!--
> Finally, note that there is a tradition (exemplified by the ` PATH ` variable) of using a <ins>colon : as a separator</ins> when an environment variable must contain multiple fields, especially when the fields can be interpreted as a search path of some sort.
> - Note that some shells (notably bash and ksh) always interpret colon-separated fields in an environment variable as filenames, which means in particular that they expand.
-->

<a id="io-after-startup"></a>

## 2.6 IO after startup

After startup, programs usually receive input or commands:

a) **In shared tempfiles**
    - As in file paths known in advance, passed to, or computed by the program.
    - See [Chapter 6, Section: Use of tempfiles](06-inter.md#use-of-tempfiles)
b) **Through a communication-bus that operate over sockets**
    - Such as [D-Bus](06-inter.md#d-bus); See [Chapter 6, Section: Sockets](06-inter.md#sockets)
c) **Through standard streams**
    - See [Chapter 6, Section: Standard streams](06-inter.md#standard-streams)
d) **Through POSIX signals**
    - See [Chapter 6, Section: POSIX-signals](06-inter.md#posix-signals)

<!--After startup, programs normally get input or commands from:
1. Data and commands presented on the program's [standard input](06-inter.md#file-descriptor).
1. Inputs passed through [inter process communication](06-inter.md#ipc-techniques) such as [D-Bus](06-inter.md#dee-bus).
1. [Files in known locations](06-inter.md#ipc-techniques) such as a data file name passed to or computed by the program.-->

**Programs can emit results in all the same ways**: to files, over a communication bus, as standard output and standard error. These several competing interface styles, are all still alive for a reason; They're optimized for different situations.

**In addition, programs, commands, scripts and shell functions all issue a value to the system when they terminate**: This value called [exit status](06-inter.md#exit-status-and-comparison) ` $? ` is an integer in the range of 0...255. <!--**In addition, when the program closes, it leaves behind an exit status ` $? `** to indicate any errors that occurred during execution. This value is an integer in the range of 0...255.--> By convention, zero indicates success, and any other value indicates failure. Some commands use different values to provide diagnostics for errors, while many commands simply exit with a value of 1 when they fail. Man-pages often describe what codes are used in the section entitled *EXIT STATUS*. However, a zero always indicates success [^shotts-exit]. See [Chapter 6, Section: Exit status and comparison](06-inter.md#exit-status-and-comparison).

[^shotts-exit]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 27, Section: Exit Status](http://linuxcommand.org/tlcl.php)

<a id="design-tropes-of-unix"></a>

## 2.7 Design tropes of unix shell utilities

The initial release of Unix (in the 1960’s) had some important design attributes that live on today: <!--With unix shell utilities the theme is, and has been, to:-->

### Modularity

**Break the system into independent components:** Small, modular utilities, that do one thing, and do them well. These programs are rock solid because they can be debugged and improved separately. Simple utilities that do one thing, can be combined in different ways to do complicated things. The unix tradition encourages building additional components, rather than complicating old programs with new features. [^raymond-composition]

**Support plugging in new pre- and post-processors without disturbing old ones:** Unix was always agnostic about its intended audience and designers. They expect the output of every program to become the input to another, as yet unknown, program. The implementers never assumed they knew all the potential uses the system could and would be put to. [^raymond-workbench]

### Plain text as universal interface

**Have all the tools communicate with each other through human readable text:** Plain text is a universal interface by itself. Data is more tractable and discoverable than program logic. If programs do not accept and emit simple text streams, they are much more difficult to debug, and it's much more difficult to hook them together (using binary input formats) [^raymond-composition]

### Terseness 

**Programs should shut up if there is nothing interesting or surprising to say:** The *singular taste of old Unix* was partly a consequence of poverty. This *silence is golden* rule evolved originally because Unix predates video displays. Younger readers may not be aware that terminals used to print. On paper. Very slowly. On the slow printing terminals of 1969, each line of unnecessary output was a serious drain on the user's time. That constraint is long gone, but **terseness** (i.e. using few words, and often not seeming polite or friendly) has remained a central feature of the style in command-line programs. So don't assume that historical origin specifies current utility. [^raymond-silence]

Many unix shell utilities will print a message only if something goes wrong. By default, most programs do not print confirmation messages upon success, nor do they show indication of progress. <!--However, many commands accept the ` -v ` parameter to change this behaviour (v is hort for verbose).--> Most unix shell utilities do not emit unrequested data at all. <!--Often times as you insert a command and hit enter, the command gets executed but you do not see a result. --> A good example of this mechanic is ` $ cp ` which overwrites and ` $ rm ` which removes existing files from the system silently without request for confirmation and without indicating that the operation was successful. [^raymond-silence]

If a program wants to support a progress indicator or produce detailed printouts (for error diagnostics, or to help the user), they should be disabled by default. The user is required to turn on such a mode himself with the command line parameter ` -v ` or ` --verbose `, in which case the additional information is provided in the standard output and/or the standard error such as: [^raymond-silence]

```
$ mkdir -v Aaaa↵
mkdir: created directory 'Aaaa'
    
$ rmdir --verbose Aaaa↵
rmdir: removing directory, 'Aaaa'
```

There are good reasons for this *rule of silence* to have long outlasted the slow teletypes, on which Unix was born: [^raymond-golden]
- The user's vertical screen space is still precious. Junk messages are a careless waste of the human user's bandwidth. They're one more source of distracting motion on a screen that may be mediating for more important foreground tasks, such as communication with other humans. [^raymond-golden]
- The Unix principle states that a program should be able to communicate not just  with human users but with other programs. Programs that babble don't tend to play well with other programs. If a CLI program emits status messages to standard output, then programs that try to interpret that output will be put to the trouble of interpreting or discarding those messages, even if nothing went wrong. [^raymond-golden]

### Fail loudly

**Unix shell utilities fail loudly and as quickly as possible:** Software should be transparent in the way that it fails (as well as in normal operation). It's best when software can cope with unexpected conditions by adapting to them. But the worst kinds of bugs are those in which the repair doesn't succeed and the problem quietly causes corruption, that doesn't show up until much later. Therefore, write your software to cope with incorrect inputs and its own execution errors as gracefully as possible. But when it cannot, make it fail in a way that makes diagnosis of the problem as easy as possible. [^raymond-repair]

### Lack of request for confirmation

Unix shell utilities are unobtrusive and silent by design. Even the potentially destructive ` $ rm ` command removes files from the system without request for confirmation, let alone without indicating that the operation was successful. 

**Programs should request confirmation only when there is good reason:** to suspect that the answer might be: No! No! No! Even then programs should support a yes-option ` -y ` to authorize potentially destructive actions. A good example of such mechanic is ` $ fsck `, the filesystem check and repair tool, that would normally require confirmation. [^raymond-cmdopt]

### Lack of cosmetic detail <!--Avoid noise-->

**Programs should avoid printing irrelevant information to standard output:** You might have wondered why there are no headers on the output of the ` $ ls -la↵ `. The answer lies yeat again on a unix tradition. The unix commandline tools typically avoid adding nonessential information (i.e. noise) and (re)formatting in ways that might make the output more difficult for downstream programs to parse. The most common offenders are considered cosmetic touches like headers, footers, blank or ruler lines, summaries and <!--conversions like adding -->aligned columns. [^raymond-filter]

<a id="textual-formats"></a>

## 2.8 Textual formats

Unix has long-standing traditions about how textual data formats ought to look. The traditional textual format is easily searched and transformed using the *traditional CLI tools* such as ` $ grep `, ` $ sed `, ` $ tr ` and ` $ cut `: [^raymond-textual]

```
$ whatis grep sed tr cut↵
grep   - print lines that match patterns
sed    - stream editor for filtering and transforming text
tr     - translate or delete characters
cut    - remove sections from each line of files
```

### One record per line

One record per line makes it easy to extract records with text-stream tools. [^raymond-textual]

### Less than 80 characters per line

Less than 80 characters per line makes the format browseable in an ordinary-sized terminal window. [^raymond-textual]

### Colon (:) as field separator 

In one-record-per-line formats, use colon ` : ` or any run of whitespace as a field separator. [^raymond-textual]
- Classic examples of the colon-convention include ` /etc/group `, ` /etc/passwd ` and ` /etc/shadow `. [^raymond-textual]
- Data files in this style are expected to support inclusion of colons (:) in the data fields by backslash escaping ` \: `. <!--More generally, code that reads delimiter separated values is expected to support record continuation by ignoring backslash-escaped newlines.--> Also if your fields must contain instances of the field separator(s), use a backslash ` \\ ` as the prefix to escape them. [^raymond-textual]
- If many records must be longer than 80 characters, consider a stanza format: Multiple lines per record, with a record separator line of ` %%\n ` or ` %\n `. The separators make useful visual boundaries for humans eyeballing the file. [^raymond-textual]

### Indifference of alternate whitespace

No distinction should be allowed between space, tab or any number of consecutive whitespace. Anything else has potential for serious headaches, because the tab settings on text editors are different. [^raymond-textual]

### Favor hex over octal

Favor the hexadecimal system (base-16) and avoid the octal system (base-8). Hex-digit pairs are easier to eyeball and map into bytes, because two characters in the base-16 hexadecimal system correspond directly to one byte i.e. eight consecutive bits of the binary system (base-2). [^raymond-textual]

### Favor ISO8601-format for date and time

Times and dates are a particular bother, because they're hard for downstream programs to parse. Any such additions should be optional and controlled by switches. If your program emits dates, it's good practice to have a switch that can force them into [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) **YYYY-MM-DD** and **hh:mm:ss** formats. Or better yet, use those by default. [^raymond-filter]

### Hash mark (#) as an introducer for comments

Use hash mark ` # ` as an introducer for comments. It is good to have a way to embed annotations and comments also in data files. [^raymond-textual]
    
### Support for special characters through backslash notation

#### Unicode or ASCII symbol

Many languages and fonts contain symbols that could not be condensed on the keyboard. But they can be inserted with the backslash notation:

| Use | To input |
|:--- |:--- |
| ` \u???? ` | a [Unicode-symbol](https://en.wikipedia.org/wiki/List_of_Unicode_characters) by its hexadecimal value (base 16)<br>such as ` $ printf "\u2665"↵ ` to produce the ` ♥ ` symbol. |
| ` \x?? ` | an [ASCII-symbol](https://www.ascii-code.com) by its hexadecimal value (base 16)<br>such as ` $ printf "\x40"↵ ` to produce the ` @ ` symbol. |
| ` \??? ` | an [ASCII-symbol](https://www.ascii-code.com) by its octal value (base 8)<br>such as ` $ printf "\100"↵ ` to produce the ` @ ` symbol. |

#### Control character

The basic character set includes **control characters**, which usually have no visible representation, but are intended to trigger some action that controls the hardware or data processing.

| Use | To |
|:--- |:--- |
| ` \n ` | **Line feed** causes the device to put the printing position on the <ins>next line</ins>. In modern systems it also moves the printing position to the start of the line (which would be the leftmost position for left-to-right scripts, such as the alphabets used for western languages, and the rightmost position for right-to-left scripts such as the hebrew and arabic alphabets). |
| ` \f ` | **Form feed** started a new sheet of paper. With the advent of computer terminals that did not physically print on paper and so offered more flexibility regarding screen placement, erasure, and so forth, printing control codes were adapted. Form feeds, for example, usually cleared the screen, there being no new paper page to move to. | 
| ` \r ` | **Carriage return** causes the device to put the caret at the edge of the paper at which writing begins (which would be the leftmost position for left-to-right scripts, such as the alphabets used for western languages, and the rightmost position for right-to-left scripts such as the hebrew and arabic alphabets). In modern systems it also moves the printing position to the next line. |
| ` \t ` | **Horizontal tab** cause the output device to move the printing position to the next tab stop in the direction of reading. Tab derives from the word tabulate, which means: to arrange data in a tabular, or table, form. When a person wanted to type a table (of numbers or text) on a typewriter, there was a lot of time-consuming and repetitive use of the space bar and backspace key. To simplify this, a horizontal bar was placed in the mechanism called the tabulator rack. Pressing the tab key would advance the carriage to the next tabulator stop. [^wiki-tab] |
| ` \b ` | **Backspace** moves the printing position one character space backwards. On printers, including hard-copy terminals, this is most often used so the printer can overprint characters to make other, not normally available, characters. On video terminals and other electronic output devices, there are often software (or hardware) configuration choices that allow a destructive backspace. |
<!--| ` \[ ` | Backslash with open square bracket ` \[ ` is used to change the properties of the printed text in the terminal such as formatting and color (see [Chapter 7, Section: Customizing the shell prompt](07-advanced-terminal.md#customizing-the-shell-prompt)). |
**Escape sequences** were used to trigger a wide variety of instructions to control the behaviour of the terminal, such as moving the cursor, formatting text, switching LED lights and clearing the screen (see [VT100 User Guide - Commands and control sequences](http://www.braun-home.net/michael/info/misc/VT100_commands.htm)).-->

[^wiki-tab]: [Wikipedia - Tab key, accessed 2025](https://en.wikipedia.org/wiki/Tab_key)

#### Newline

> [!NOTE]
> When typing on a computer, you don't usually have to pay attention to how text is divided into lines. If text does not fit on a single line, most software can automatically move the last word after a space to the next line. However, this was not obvious in the early days of word processing.

The system had to be specifically instructed to perform a line break, in the same way that a typewriter had to move the typing head to the beginning of a new line whenever a line was full. Therefore, two characters were added to the ASCII character set. One moved the cursor to the beginning of the line (**carriage return**) and the other to the next line (**line feed**). [^kirjotuskone]

Only later was it realised that two separate characters were not necessarily needed. The line break could be programmed to occur with a single character, but different systems came up with different solutions. For the line break, some systems started to use only *carriage return* (code **` CR \r \x0D `**), others only *line feed* (code **` LF \n \x0A `**). Problems arose, of course, when text files were moved from one system to another and control code practices were different. But this was at a time when there were few dreams of flexible transfer of data between different programs, machines and systems. [^kirjotuskone]

[^kirjotuskone]: [Jukka Korpela - Kirjoituskoneista tietokoneisiin, accessed 2025](https://jkorpela.fi/rv/1.1.html).

### XML 

XML (extensible markup language) can be a simplifying or a complicating choice: [^raymond-xml]
- XML is itself rather bulky. [^raymond-xml]
    - It can be difficult to see the data amidst all the markup. [^raymond-xml]
- The most serious problem with XML is that it doesn't play well with traditional unix tools. Software that wants to read an XML format needs an XML parser. This means bulky, complicated programs. [^raymond-xml]

One application area in which XML is clearly winning is in markup formats for document files. [^raymond-xml]
- Compressed XML (such as \*.docx and \*.odt) combines space economy with some of the advantages of a textual format. Notably, it avoids many problems that come with binary formats. [^raymond-xml]

<a id="binary-formats"></a>

## 2.9 Binary formats 

### Textualizers 

Whenever you face a design problem that involves editing some kind of complex binary object, the unix tradition encourages asking first off whether you can write a tool that can do a **lossless mapping to an editable textual format and back**. [^raymond-trans]

### Browser 

If the binary object is dynamically generated or very large, then it may not be practical or possible to capture all the state with a textualizer. In that case, the equivalent task is to write a **browser**. [^raymond-trans]
- The paradigm example is ` $ fsdb `, the file-system debugger supported under various unixes. There is a Linux kernel equivalent called ` $ debugfs `. [^raymond-trans]
- Another example would be ` $ psql `, which is used to browse PostgreSQL databases. [^raymond-trans]

<!--
> [!IMPORTANT]
> Don't bother compressing or binary-encoding just part of the file.
-->

<!-- # References -->

[^raymond-dpatterns]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 11<!--. Interfaces-->, Section: User-Interface Design Patterns<!-- in the Unix Environment-->](http://www.catb.org/~esr/writings/taoup/html/interfacechapter.html)

[^raymond-istyle]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 3<!--. Contrasts-->, Section: Preferred User Interface Style](http://www.catb.org/~esr/writings/taoup/html/ch03s01.html)

[^raymond-tradeoffs]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 11<!--. Interfaces-->, Section: Tradeoffs between CLI and Visual<!-- Interfaces-->](http://www.catb.org/~esr/writings/taoup/html/ch11s04.html)

[^raymond-around]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 3<!--. Contrasts-->, Section: What Goes Around, Comes Around](http://www.catb.org/~esr/writings/taoup/html/ch03s03.html)

[^raymond-tale]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 13<!--. Complexity-->, Section: A Tale of Five Editors](http://www.catb.org/~esr/writings/taoup/html/ch13s02.html)

[^raymond-live]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 10<!--. Configuration-->, Section: Where Configurations Live](http://www.catb.org/~esr/writings/taoup/html/ch10s02.html)

[^raymond-textual]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 5<!--. Textuality-->, Section: Unix Textual File Format<!-- Conventions-->](http://www.catb.org/~esr/writings/taoup/html/ch05s02.html)

[^raymond-silence]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 1<!--. Philosophy-->, Section: Rule of Silence](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)

[^raymond-composition]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 1<!--. Philosophy-->, Section: Rule of Composition](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)

[^raymond-workbench]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 8<!--. Minilanguages-->, Section: <!--Case Study: -->The Documenter's Workbench<!-- Tools-->](http://www.catb.org/~esr/writings/taoup/html/ch08s02.html)

[^raymond-golden]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 11<!--. Interfaces-->, Section: Silence Is Golden](http://www.catb.org/~esr/writings/taoup/html/ch11s09.html)

[^raymond-filter]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 11<!--. Interfaces-->, Section: The Filter Pattern](http://www.catb.org/~esr/writings/taoup/html/ch11s06.html)

[^raymond-cmdopt]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 10<!--. Configuration-->, Section: Command-Line Options](http://www.catb.org/~esr/writings/taoup/html/ch10s05.html)

[^raymond-repair]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 1<!--. Philosophy-->, Section: Rule of Repair](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)

[^raymond-xml]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 5<!--. Textuality-->, Section: XML](http://www.catb.org/~esr/writings/taoup/html/ch05s02.html)

[^raymond-trans]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 6<!--. Transparency-->, Section: Transparency<!-- and Editable Representations-->](http://www.catb.org/~esr/writings/taoup/html/ch06s02.html)

