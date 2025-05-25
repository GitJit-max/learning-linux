<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="02-basic.md">&lt;&lt; Previous Chapter: 2 - Design priciples of Unix and its decendants</a>
     |
  <a href="04-installing.md">Next&nbsp;Chapter:&nbsp;4&nbsp;&#8209;&nbsp;Installing&nbsp;applications&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 3 - Commandline crash course

Get up to speed quickly with this intensive overview, designed to teach you the basics of commandline usage in a short amount of time. More advanced essentials will be discussed later in [Chapter 7](07-advanced-terminal.md#chapter-7---advanced-terminal-usage).

<!--A crash course is a short, intensive learning program designed to teach the basics of a subject in a very limited amount of time. It's a rapid overview to get someone up to speed quickly.

A crash course is a quick, intensive learning session designed to teach the essentials of a subject in a short amount of time. It's often used to rapidly get someone up to speed on a topic.-->

<a id="clear-the-screen"></a>

## 3.1 Clear the screen

- With scrollback-ability = **` $ clear -x↵ `**
    - Keyboard shortcut **` Ctrl + L `** does the same thing.
- Without scrollback-ability = **` $ reset↵ `**
    - This will actually reset and reinitialize the whole terminal state.

<a id="special-character-dash"></a>

## 3.2 Special character: dash (-)

> [!NOTE]
> In typography and computing there are [different types of dash characters](https://en.wikipedia.org/wiki/Dash#Unicode_dash_characters). Here dash refers to the normal short hyphen ` - ` with ASCII code ` \x2D `, which is also the most commonly used form of hyphen in digital documents. On most keyboards, it is the only character that resembles a minus sign or a dash, so it is also used for these.

### Command-line argument

The whole command-line is considered as a space delimited list of **command-line arguments**. The first argument is the filename of the executable, but most of the arguments are additional instructions that affect the operation of the program. It would be up to the program code to decipher each token and decide what it is and how to work with it.

### Dash as an introducer for command-line options

- **Double dash ` --* `** is used to specify one single command-line option.
- **Single dash ` -? `** is used to specify <ins>one or more</ins> command-line options.

> [!NOTE]
> A file path as part of a shell command is not a command-line option, but an argument and a parameter.

### Dash as a reference to standard input

<!--Many tools accept a **bare dash ` - `**, not associated with any option letter, as a pseudo-filename directing the application to read from standard input (see [Chapter 6, Section: Standard streams](06-inter.md#standard-streams)).-->

Dash can also indicate standard streams (see [Chapter 6, Section: Standard streams](06-inter.md#standard-streams)). Many tools accept a **bare dash ` ␣-␣ `**, not associated with any option letter, as a pseudo-filename directing the application to read from standard input. And some programs, that print to a file by default, can be made to print to the standard output by specifying **bare dash ` ␣-␣ `** as the filename.

### Doubledash as end of options marker

It is conventional to recognize a **bare double dash ` ␣--␣ `**, not associated with any option word, as a signal to stop option interpretation and treat all following arguments literally.

> [!TIP]
> If for example you need to process a file whose name starts with one or more dash characters, you can put an additional double dash ` -- ` argument before the filename to signify the end of the options. Alternatively, a relative reference to current working directory `./ ` can be added in front of the filename. Such convention is respected by most shell commands:
>
> ```
> $ rm -- "--hard to remove.txt"↵  # Works
> $ rm ./"--hard to remove.txt"↵   # Works
> ```

> [!WARNING]
> Single quoting ` '...' ` or double quoting ` "..." ` is not enough:
>
> ```
> $ rm "--hard to remove.txt"↵   # Does not work
> rm: unrecognized option '--hard to remove.txt'
> Try 'rm ./'--hard to remove.txt'' to remove the file
> ```
>
> And on the other hand, quotation marks would be needed if the filename contains special characters such as spaces:
> 
> ```
> $ rm -- --hard to remove.txt↵  # Does not work
> rm: cannot remove '--hard': No such file or directory
> rm: cannot remove 'to': No such file or directory
> rm: cannot remove 'remove.txt': No such file or directory
> ```

<a id="command-line-options"></a>

## 3.3 Command-line options 

Three conventions for command-line options exist

1. **Unix style** **` -? `** [^raymond-cmopt]
    - In the original unix tradition, command-line options are single letters preceded by a single hyphen. Mode-flag options that do not take following arguments can be ganged together. Thus, if ` -a ` and ` -b ` are mode options then ` -ab ` or ` -ba ` is also correct and enables both.
    - A parameter to an option, if any, follows it, optionally separated by whitespace, such as ` -i input.odt -o output.pdf `.
    - In this style, lowercase options are preferred to uppercase. When uppercase options are used, it's good form for them to be special variants of the lowercase option.
2. **GNU style** **` --* `** [^raymond-cmopt]
    - The GNU style uses option keywords (rather than keyword letters) preceded by two hyphens. GNU options are easier to read than the alphabet soup of older styles. GNU-style options cannot be ganged together without separating whitespace.
    - A parameter to an option, if any, can be separated by either whitespace or a single equal sign ` = `.
    - Even with programs using the GNU style, it is good practice to support single-letter equivalents for at least the most common options. The GNU project recommends [conventional meanings](https://www.gnu.org/prep/standards/standards.html#Option-Table) for a few double-dash options in the GNU coding standards. It also lists [long options](https://www.gnu.org/prep/standards/standards.html#Option-Table) which, though not standardized, are used in many GNU programs.
3. **X toolkit style** **` -* `** (not recommended) [^raymond-cmopt]
    - The X toolkit style, uses a single hyphen and keyword options. The X toolkit style is not properly compatible with either the classic Unix or GNU styles, and should not be used in new programs.

### Commandline option: -h

> [!NOTE]
> The commandline option ` --help ` will display a help message and exit. It is not to be confused with ` -h `. The plain ` -h ` commandline option without an argument traditionally meant headers and not help.

Support for help-option is actually less common than one might expect offhand. For much of Unix's early history, developers tended to think of "on-line" help as memory-footprint overhead they could not afford. Instead they wrote manual pages (see [Section: Early unix documentation style](#early-unix-documentation-style)).

Commandline option for headers enable, suppress, or modify **headers** on a tabular report generated by the program (such as ` $ ps -h↵ `).

Option ` -h ` may also have other meanings such as formatting filesize to be **human readable**. The command ` $ ls -la -h↵ ` is a good example of this convention.

<a id="navigating-directories"></a>

## 3.4 Navigating directories

> [!IMPORTANT]
> Those used to Windows may be annoyed that directory paths do not work as expected on unix-like systems. Namely, **unix like systems use forward slash ` / ` to separate directories**. Whereas Windows uses backslash ` \ ` to separate directories.

<!--
> [!IMPORTANT]
> To separate directories:
>
> - Unices use the forward slash **` / `**
> - Windows uses the backward slash **` \ `**-->

### Current directory

Absolute pathname of the current working directory:
- **` $ pwd↵ `** = Print current working directory [^ieee-binpwd]
- **` $ echo $PWD↵ `** = Present working directory [^ieee-envpwd]
    - The value is is initialized by ` $ sh ` and then updated by ` $ cd `.

[^ieee-binpwd]: [IEEE 1003.1 Standard: Utilities: pwd, accessed 2025](https://pubs.opengroup.org/onlinepubs/9799919799/utilities/pwd.html)

[^ieee-envpwd]: [IEEE 1003.1 Standard: Other Environment Variables, accessed 2025](https://pubs.opengroup.org/onlinepubs/9799919799/basedefs/V1_chap08.html)

### Change directory

- **` $ cd <directory>↵ `** = Change directory
    - **` $ cd↵ `** (on its own) will take you to your home directory.
    - **` $ cd ~↵ `** will take you to your home directory.
    - **` $ cd $HOME↵ `** will also take you to your home directory.
    - **` $ cd -↵ `** will take you to the previous directory.
    - **` ~ `** tilde refers to current user's home directory.
    - **` ~matt `** is a way to refer to the home directory of another, named user.
    - **` ../../ `** two points move the index backwards (relative reference).
    - **` ./ `** point is a relative reference to current working directory.
    - **` / `** forward slash is the root directory (absolute reference)
        - This is where the directory structure begins.
    
### Make directory
    
- **` $ mkdir <directory(ies)>↵ `** = Make directory
    - Multiple directories can be created at once: ` $ mkdir dir1 dir2 dir3↵ `
    - **` -p `** = Nest subdirectories: ` $ mkdir -p create/nested/dirs↵ `

### List files

- **` $ ls <options> <directory>↵ `** = List directory contents
    - Current working directory is used if not otherwise specified.
    - **` -a `** = List also hidden files.
    - **` -R `** = List also files in subdirectories.
    - **` -l `** = Show additional information such as filesize.
    
> [!NOTE]
> There are no headers on the output of the ` $ ls -l↵ ` command because of a unix tradition. Unix-style command-line tools typically avoid adding cosmetic information and formatting that would complicate further programmatic processing of the output (see [Chapter 2, Section: Design tropes of unix shell utilities](02-basic.md#design-tropes-of-unix)).

> [!TIP]
> One can install alternative listing commands that support column headers such as ` $ exa `. The command ` $ exa -lh↵ ` will lists the entire contents of the current working directory with additional column headers.

<a id="finding-executables"></a>

## 3.5 Finding executables

The unix tooling comes with many commands for finding locations and information about files such as executables. The functionality is partly similar to the Properties window in Microsoft Windows.

1. **` $ ls -li <file>↵ `** provides additional information about the desired file.
1. **` $ stat <file or directory>↵ `** is short for status reveals and reveals all that the system understands about a file and its attributes. It is a kind of souped-up version of the ` $ ls -li <file>↵ ` command.
1. **` $ files <file or directory>↵ `** will try to determine the filetype (see [Section: File types and extensions](#file-types-and-file-name-extensions)).
1. **` $ whatis <program_name>↵ `** displays the description line from the man-page matching the specified program. Note that bash shell builtin commands don't have separate man-pages (see [Section: Shell builtin command](#shell-builtin-commands)).
1. **` $ whereis <program_name>↵ `** locates file paths to binary, data and man directories of the program, searching for many different possibly useful files related to the program.
1. **` $ which <program_name>↵ `** locates the entire file path of a program, by searching through the directories specified by the environment variable ` PATH `. ` $ which ` only works for executable programs, not builtins nor aliases (that are substitutes for actual executable programs).
1. Package managers are able to list a lot of information about software installed through them, such as ` $ eopkg info -F firefox↵ `.

```
$ whatis whatis whereis which↵
whatis - Display one-line manual page descriptions
whereis - Locate the binary, source, and manual page files of commands
which - Show the full path of shell commands

$ whereis firefox↵
/usr/bin/firefox
/usr/lib64/firefox
/usr/share/man/man1/firefox.1

$ which firefox↵
/usr/bin/firefox

$ file HelloWorld.gambas↵
HelloWorld.gambas: a gbr3 script executable (binary data)
```

<a id="special-character-period"></a>

## 3.6 Special character: period (.)

### Period as mark to hide files

> [!IMPORTANT]
> The unix way of implementing hidden files is likely to confuse those accustomed to Windows.

Filenames that begin with a period **` . `** are hidden. This means that a file manager (such as ` $ nemo `) or the ` $ ls ` command will not list them unless you say so.

When your account was created, several hidden files were placed in your home directory to configure things. The purpose of having these as hidden files is to reduce visible clutter on the filesystem by removing system and configuration files from view when they are not necessary.

- To list hidden files and directories on command-line type ` $ ls -la↵ `

- To temporarily reveal or conceal hidden files and directories in a graphical file manager
    a) Toggle ` Ctrl + H ` on your keyboard or
    b) Toggle ` Menu bar ` > ` View ` > ` Show hidden files `

To permanently reveal or conceal a file or a directory, simply rename it.
- To permanently hide a file such as ` sometext.txt `<br>rename it to ` .sometext.txt `.
- To permanently unhide a file such as ` .sometext.txt `<br>rename it to ` sometext.txt `.

### Period as mark for current working directory

> [!IMPORTANT]
> Period ` . ` also refers to the current working directory (see [Section: Navigating directories](#navigating-directories)).

You may have tried running a script or some other executable in the current working directory ` $ myscript.sh↵ ` only to end up with a *command not found* error. This happens because, by default the shell searches for an executable that matches with the given command only in the directories specified by the environment variable ` PATH `(see [Chapter 2, Section: Well-known environment variables](02-basic.md#well-known-variables)).

The location of an estranged executable must be specified explicitly in connection with the executable. To run a script in the current working directory one must type something like **` $ ./myscript.sh↵ `**. Where the single period ` . ` refers to the active directory. The notation is not as confusing if the executable is called from another directory such as ` $ myscripts/myscript.sh↵ `

<a id="special-character-backslash"></a>

## 3.7 Special character: backslash (\\)

> [!IMPORTANT]
> The backslash ` \ ` is an **escape character**, and changes the meaning of the symbol that follows it.

**Backslash ` \ `** escaping is used to:

a) Eliminate the special function of a character that follows it such as:
    - ` \$ ` = dollar sign ` $ `
    - ` \" ` = double quotes ` " `
    - ` \* ` = asterisk ` * `
    - ` \\ ` = back slash ` \ `
    - ` \  ` = space `   `
    - Such as cd into ` Directory with space characters `
        - ` $ cd Directory\ with\ space\ characters/↵ `
b) Insert symbols that could not be condensed on the keyboard, such as:
    - ` \u???? ` = a [Unicode-symbol](https://en.wikipedia.org/wiki/List_of_Unicode_characters) by its hexadecimal value (base 16).
    - ` \x?? ` = an [ASCII-symbol](https://www.ascii-code.com) by its hexadecimal value (base 16).
    - ` \??? ` = an [ASCII-symbol](https://www.ascii-code.com) by its octal value (base 8).

c) Insert characters that do not have a special symbol when printed, such as    :    
    - ` \t ` = horizontal tab
    - ` \v ` = vertical tab
    - ` \n ` = newline<!--, for example ` $ echo -e "Aaa\nBbb\nCcc"↵ `-->

d) Insert control codes which do not appear even indirectly, such as:
    - ` \a ` = bell or a beep (see note below)

> [!NOTE]
> The **bell code** or **bell character** is a device-control code, originally sent to ring a small electro-mechanical bell. Later on, speakers and buzzers vere equipped to perform the same function.
>
> Modern terminal emulators often integrate the warnings to the desktop environment and migth offer a **silent visual bell feature** that flashes the terminal window briefly.
>
> In ASCII and Unicode the character with the value 7 is BEL. It can be referred to by Keyboard shortcut ` Ctrl + V, Ctrl + G `, which is ^G in caret notation. Some keyboards even had the G-key located with a bell label. [^unibel]

[^unibel]: [Unipedia Wiki - Bell, accessed 2021](https://unipedia.fandom.com/wiki/Bell)

<a id="control-characters"></a>

## 3.8 Control characters 

### Relic from history

> [!IMPORTANT]
> The basic ASCII character set (American Standard Code for Information Interchange) includes **control characters**, which usually have no visible representation. Control characters are used to cause effects, other than the insertion of a symbol into text. The purpose is to initiate some action that controls the hardware or data processing. [^wiki-control]

[^wiki-control]: [Wikipedia - Control character, accessed 2024](https://en.wikipedia.org/wiki/Control_character)

Control characters are a relic from history when computers were primitive. The ASCII character set is more than a list of symbols. It was developed in the 1960s as a notation and control coding for paperless typewriters and computer terminals. The ASCII control character set is a way of communicating between a terminal and a computer. [^wiki-ascii-fi] The ASCII standard has 33 control characters that can be described as doing something when the user enters them, such as 
- Interrupting an ongoing process with the end-of-text character (ETX, ^C, ` Ctrl + C `).
- Indicating conclusion of text input, or exiting a shell by the end-of-transmission character (EOT, ^D, ` Ctrl + D `).

[^wiki-ascii-fi]: [Wikipedia - ASCII, accessed 2025](https://fi.wikipedia.org/wiki/ASCII)

### Caret notation

**Caret notation** is a printable form for control characters specifically in [ASCII](https://en.wikipedia.org/wiki/ASCII), where the character (^) known as the circumflex, appears as an independent character, without any letter below it.
- The notation assigns ^A to control-code 1, sequentially through the alphabet to ^Z assigned to control-code 26. The keys that produce control-codes outside of the range 1...26 vary between systems. Keyboards also typically have a few single keys which produce control character codes (such as ` Del `, ` Backspace `, ` Tab `, ` Enter `). [^wiki-caret]
- Control characters generated using letter keys are displayed with the upper-case form of the letter. When the Ctrl-key is held down, letter keys produce the same control characters regardless of the state of the Shift- or Caps-keys. It does not matter, whether the key would have produced an upper-case or a lower-case letter.
- There are also other ways to display these non-printing "characters" such as decimal code point, hexadecimal code point, or a two or three letter abbreviation in capital letters.

### Traditional ASCII control characters

[^wiki-caret]: [Wikipedia - Caret notation, accessed 2024](https://en.wikipedia.org/wiki/Caret_notation)

| Dec | Hex | Abr | CN | Keyboard shortcut + Use |
|:---:|:---:|:---:|:---:|:--- |
| 0 | 00 | NUL |  | **Null** was typically used to reserve space, either for correcting errors or for inserting information that would be available at a later time or in another place. It adapted to mark end of string. |
| 1 | 01 | SOH | `^A` | **Start of heading** was to mark a non-data section of a data stream. |
| 2 | 02 | STX | `^B` | **Start of text** marked the end of the header, and the start of the textual part of a stream. |
| 3 | 03 | ETX | `^C` | ` Ctrl + C ` **End of text** marked the end of the data of a message. |
| 4 | 04 | EOT | `^D` | ` Ctrl + D ` **End of transmission** was used to indicate that a slave station has completed its transmission, i.e. the end of an entire transmission or communication session to signal that no more data will follow. |
| 5 | 05 | ENQ | `^E` | When a transmission medium could transmit in only one direction at a time, **Enquire** was used by a master station to ask a slave station to send its next message. |
| 6 | 06 | ACK | `^F` | **Acknowledgment** was normally used as a flag to indicate no problem detected with current element. |
| 7 | 07 | BEL | `^G` | ` Ctrl + G ` **Bell** is intended to cause an audible signal in the receiving terminal. |
| 8 | 08 | BS | `^H` | ` Ctrl + H ` or ** Backspace ** moves the printing position one character space backwards. On printers, including hard-copy terminals, this is most often used so the printer can overprint characters to make other, not normally available, characters. On video terminals and other electronic output devices, there are often software (or hardware) configuration choices that allow a destructive backspace. |
| 9 | 09 | HT | `^I` | ` Ctrl + V, Ctrl + I ` **Horizontal tab** cause the output device to move the printing position to the next tab stop in the direction of reading. Tab derives from the word tabulate, which means: to arrange data in a tabular, or table, form. When a person wanted to type a table (of numbers or text) on a typewriter, there was a lot of time-consuming and repetitive use of the space bar and backspace key. To simplify this, a horizontal bar was placed in the mechanism called the tabulator rack. Pressing the tab key would advance the carriage to the next tabulator stop. [^wiki-tab] |
| 10 | 0A | LF | `^J` | ` Ctrl + J ` **Line feed** causes the device to put the printing position on the <ins>next line</ins>. In modern systems it also moves the printing position to the start of the line (which would be the leftmost position for left-to-right scripts, such as the alphabets used for western languages, and the rightmost position for right-to-left scripts such as the hebrew and arabic alphabets). |
| 11 | 0B | VT | `^K` | **Vertical tab** was used to speed up printer vertical movement. Some printers used special tab belts with various tab spots. |
| 12 | 0C | FF | `^L` | ` Ctrl + L ` **Form feed** started a new sheet of paper. With the advent of computer terminals that did not physically print on paper and so offered more flexibility regarding screen placement, erasure, and so forth, printing control codes were adapted. Form feeds, for example, usually cleared the screen, there being no new paper page to move to. |
| 13 | 0D | CR | `^M` | ` Ctrl + M ` or ` ↵ ` **Carriage return** causes the device to put the caret at the edge of the paper at which writing begins (which would be the leftmost position for left-to-right scripts, such as the alphabets used for western languages, and the rightmost position for right-to-left scripts such as the hebrew and arabic alphabets). In modern systems it also moves the printing position to the next line. <!--**Carriage Return** returns the carriage return to the extreme left. In modern terminals, the carriage return usually moves to the next line at the same time.--> |
| 14<br>15 | 0E<br>0F | SO<br>SI | `^N`<br>`^O` | The original purpose of ` Ctrl + N ` **Shift out** and ` Ctrl + O ` **shift in** control codes was to provide a way to shift the red and black ribbon, i.e. split on an electromechanical typewriter or teleprinter, in or out, to another colour. As the technology developed, the function adapted to switching to a different font or character set. |
| 16 | 10 | DLE | `^P` | **Data link escape** was intended to be a signal to the other end of a data link that the following character is a control character such as STX or ETX. |
| 17<br>18<br>19<br>20 | 11<br>12<br>13<br>14 | DC1<br>DC2<br>DC3<br>DC4 | `^Q`<br>`^R`<br>`^S`<br>`^T` | **Device control** codes, DC1 to DC4, were originally generic, to be implemented as necessary by each device. |
| 21 | 15 | NAK | `^U` | **Negative acknowledge** is a definite flag for, usually, noting that reception was a problem, and, often, that the current element should be sent again. |
| 22 | 16 | SYN | `^V` | **Synchronous idle** was originally sent by synchronous modems (which have to send data constantly) when there was no actual data to send. |
| 23 | 17 | ETB | `^W`| **End of transmission block** used to signify the end of a block of data during transmission. It was employed in protocols where data was sent in blocks. |
| 24 | 18 | CAN | `^X` | **Cancel** signals that the previous element should be discarded. |
| 25 | 19 | EM | `^Y` | **End of medium** signal warned that a recording medium such as tape had run out. |
| 26 | 1A | SUB | `^Z` | **Substitute** was used to padding, so that data could be sent in fixed size blocks or in place of a character that could not be represented on another device. <!--**Substitute was** intended to request a translation of the next character from a printable character to another value, usually by setting bit 5 to zero. This was handy because some media (such as sheets of paper produced by typewriters) could transmit only printable characters.--> |
| 27 | 1B | ESC | `^[` | **Escape sequences** were used to trigger a wide variety of instructions to control the behaviour of the terminal, such as moving the cursor, formatting text, switching LED lights and clearing the screen (see [VT100 User Guide - Commands and control sequences](http://www.braun-home.net/michael/info/misc/VT100_commands.htm)). |

[^wiki-tab]: [Wikipedia - Tab key, accessed 2025](https://en.wikipedia.org/wiki/Tab_key)

### Inserting a control character

> [!TIP]
> Special characters can be inserted through **verbatim insert**. <!-- The concept of verbatim insert in unix refers to a functionality where you can insert control characters directly into the terminal. -->

The bell control character **` BEL \a \x07 `** is suitable for illustrating *verbatim insert* functionality. Pressing the shortcut keys corresponding to the bell symbol ` Ctrl + G `, in a terminal window, generates the bell sound. Alternatively ` $ echo ` can be used to generate the sound of the bell character:
1. Type the initial part of the command **` $ echo␣  `**; That is "echo " with a trailing space.
2. press the keyboard shortcut keys **` Ctrl + V, Ctrl + G `** and the character ^G appears on the line. If you delete the character with the ` Backspace ` key, you will see that it is really a single character and not ^ and G in a row.
3. Finally, press enter ` ↵ ` and you should hear a beep (also a blank line will be printed). If you don't hear a beep and the text ^G is printed, something went wrong. Functionality is not correct if you type the command manually ` $ echo ^G↵ `. The bell character should be inserted by pressing ` Ctrl + V, Ctrl + G `.

> [!NOTE]
> Of course, there are alternative ways to achieve the same functionality, such as ` $ echo -e "\x07"↵ ` (see [Section: Special character: backslash (\\)](#special-character-backslash)).

<a id="special-character-space"></a>

## 3.9 Special character: space ( )

> [!WARNING]
> Files systems that are popular in GNU/Linux such as EXT4 and BTRFS have far fewer restrictions on special characters than the Windows NTFS and exFAT file systems. Every character except forward slash ` / ` and NUL ` \0 `, are allowed in filenames. However if you make any use of the shell, you will realize that there are many characters that will create a hassle; Most significantly space ` `, dash ` - `, asterisk ` * `, dollar sign ` $ `, exlamation mark ` ! `, ampersand ` & `, forwardslash ` / `, backslash ` \ `, curly brackets ` {...} `, tilde ` ~ `, at sign ` @ `, backquotes `` `...` ``.

### Recommendation to not use space in filenames

In the command interface, **the whole command-line is considered a space-separated list of command-line arguments** (see [Section: Special character: dash (-)](#special-character-dash--)).
- This is why a whitespace in the filename creates the need to use either:
    a) Double quote supression ` "..." `
    b) Single quote supression ` '...' `
    c) Backslash escaping ` \? `

```
$ rm "A Dragged Link from Firefox.desktop"↵

$ rm 'A Dragged Link from Firefox.desktop'↵

$ rm A\ Dragged\ Link\ from\ Firefox.desktop↵
```

> [!NOTE]
> The recommendation to not use spaces in filenames comes from the danger that **they might be misinterpreted by software that poorly supports them**. Arguably, such software is buggy. But also arguably, programming languages and shell scripting make it all too easy to write software that breaks when presented with filenames with spaces in them.

### Types of documentation

#### Early unix documentation style 

The early Unix documentation style and tools have several technical and cultural traits that distinguish it from the way documentation is done elsewhere. In the early history of Unix, developers produced manual pages containing essential practical information. These were stored in the ` /usr/share/man/ ` directory and were accessible by the ` $man ` command, an interface to the system reference manuals. [^raymond-docstyle]
- The classic manual pages that came with Unix have traditionally been written by programmers for their peers. The style does not hold you by the hand, but it usually points in the right direction. The style assumes an active and experienced reader. This is because Unix and its decendants are in many ways better adapted to the needs of power users. [^raymond-docstyle]
- Many times the manual page of a unix program even has a section called BUGS. In other cultures, technical writers try to make the product look good by omitting and skating over known bugs. In the unix culture, peers describe the known shortcomings of their software to each other in unsparing detail, and users consider a short but informative BUGS section to be an encouraging sign of quality work. Commercial Unix distributions euphemize it to a softer tag like LIMITATIONS or ISSUES or APPLICATION USAGE. [^raymond-docstyle]

#### Modern documentation style 

The best practices for writing documentation on modern unix program of any significant size suggest shipping three different kinds of documentation: [^raymond-bestdoc]
- **Man-pages** should be command references for the traditional unix audience, in the traditional unix style, giving details of how the program is invoked, a **quick summary** and pointers to the long-form manual incase the user needs to learn more about a specific feature or function. Huge man pages are viewed with some disfavor, and navigation within them can be difficult. All man pages follow a [common layout](https://en.wikipedia.org/wiki/Man_page) that is optimized for presentation on a simple ASCII text display, possibly without any form of highlighting or font control. [^raymond-bestdoc]
- The **long-form manual** should be a comprehensive documentation for nontechnical users. And often includes troubleshooting tips. It should be possible to use the long-form manual as a reference guide when the user encounters difficulties or needs to learn more about a specific feature or function. [^raymond-bestdoc]
- List of **frequently asked questions** (FAQ) should be an evolving resource that grows as the software support group learns what the frequent questions are and how to answer them. [^raymond-bestdoc]

#### In addition 

- A project should have a **website** to serve as a central point of distribution. [^raymond-bestdoc]

- Extra **tutorials** can take many forms such as written articles, videos, or interactive software. A tutorial is intended to teach users how to perform a specific task or achieve a particular goal. A tutorial may include quizzes or other types of assessments to help the user gauge their understanding of the material. [^raymond-bestdoc]

- With the source code, you can also expect to find a **README file**, which usually contains, installation instructions, configuration instructions, reference to user manuals, copyright and licence information, and contact details of the distributor or author. <!-- The file's name is generally written in uppercase. On Unix-like systems in particular, this causes it to stand out; Both because lowercase filenames are more common, and because the ` $ ls ` command commonly sorts and displays files in ASCII-code order, in which uppercase filenames will appear first.  --> [^wiki-readme]

[^wiki-readme]: [Wikipedia - README, accessed 2024](https://en.wikipedia.org/wiki/README)

<a id="file-types-and-file-name-extensions"></a>

## 3.10 File types and file name extensions

**Extensions** are file name suffixes that start with a period. Usually, they are two, three or four letters long. Extensions are used to distinguish between different types of files. For example, ` *.txt ` refers to a text file and ` *.jpg ` refers to an image file. [^wiki-tiedostopääte]

[^wiki-tiedostopääte]: [Wikipedia - Tiedostopääte, accessed 2025](https://fi.wikipedia.org/wiki/Tiedostop%C3%A4%C3%A4te)

### Unix tradition has no concept of file name extension 

Windows relies heavily on file name extensions to decide what to do with a file if it is double-clicked. In the unix tradition, on the other hand, there is no concept of a file name extension. Although file extensions may be used in modern GNU/Linux distributions, most utilities and applications still ignore the file extension. Instead, various heuristics are used to determine the file type. [^raymond-bag]

Even the early Apple Macintosh computers did not use file name extensions. Instead the operating system stored information about the program that created the file in the file, in order to be able to launch the file later with the same program. In the unix tradition, files did not contain such metadata either. [^raymond-bag]

Unix partisans preferred approaches that made file data self-describing, so that no metadata was needed to store within the file. Traditionally also the directory, where a file was placed, has been a good indication of the file type (see [Chapter 2, Section: Directory structure](02-basic.md#directory-structure)). [^raymond-bag]

### Even today filename name extensions are not required 

The visual metaphor at the heart of modern GUIs, files represented by icons, and opened by clicking which invokes some designated handler program, typically able to create and edit these files, has proven both successful and long-lived. [^raymond-weak]
- Unix long supported this metaphor only poorly and grudgingly. [^raymond-weak]

Even today, the filename name extensions are not required in the GNU/Linux desktop environment to determine the contents and purpose of files. For example, pdf- and odt-files get the right icon, and open in the right program, without a file name extension. [^raymond-weak]
- However, many applications can use a file name extension, and a file named with the wrong extension will no longer open correctly when clicked with the mouse. [^raymond-weak]

<!-- While extensions are also used under modern unices in several cases, most utilities and applications do not care, and use different heuristics to figure out a file type. A Unix file is just a big bag of bytes, with no other attributes / metadata. In particular, there is no capability to store information about the file type or a pointer to an associated application program outside the file's actual data. -->

<!-- Because file extensions are not required on the unix file system, you may name files any way you like. One may also use the common file extensions if they like. Anyhow, the contents and/or purpose of a file is still today determined mostly by other means such as **` $ file <file or dir>↵ `** -->

### Command to find out the file type

In the command line interface, the contents and/or purpose of a file is, still today, determined mostly by other means such as **` $ file <file or dir>↵ `**:

```
$ file SomePlainText↵
SomePlainText: Unicode text, UTF-8 text

$ file SomeTextDocument↵
SomeTextDocument: OpenDocument Text

$ file the_beginners_handbook↵
the_beginners_handbook: PDF document, version 1.5 (zip deflate encoded)

$ file ~/Desktop/↵
/home/user/Desktop/: directory

$ file /sbin↵
/sbin: symbolic link to usr/sbin

$ file /dev/null↵
/dev/null: character special (1/3)

$ file HelloWorld.gambas↵
HelloWorld.gambas: a gbr3 script executable (binary data)

$ file /usr/bin/file↵
/usr/bin/file: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /usr/lib64/ld-linux-x86-64.so.2, BuildID[sha1]=96eacae9627debefb5fa23ed58cf1ad83251f85c, for GNU/Linux 3.2.0, stripped
```

<!-- Be sure to revisit [Section: Finding executables](#finding-executables) for information on similar commands such as ` $ stat `, ` $ whatis ` and ` $ whereis `. -->

> [!NOTE]
> The file type **character special file** is an entity that handles data as a stream of bytes, such as ` /dev/null `.
>
> The file type **block special file** is an entity that handles data in blocks, such as an optical drive.

### Command types

A command can be one of four different things:

a) A reference to an [executable program](#executable), i.e. a binary file containing machine code for execution by the computer, such as ` $ ls ` and ` $ rm `.
b) A reference to [an internal command found in the shell](#shell-builtin-commands) such as ` $ cd ` and ` $ echo `.
c) A reference to a [script file](https://www.gnu.org/software/bash/manual/html_node/Shell-Scripts.html) written in the scripting language of the shell.
d) [Alias](#alias), which creates an alternative name for another command.

The shell builtin command **` $ type <command>↵ `** will show you how a specific command will be interpreted if used on the command line.

```
$ type type↵
type is a shell builtin

$ type ls↵
ls is aliased to `ls --color=auto'

$ type file↵
file is /usr/bin/file

$ type file↵
file is hashed (/usr/bin/file)
```

> [!NOTE]
> After finding the location of a command the first time, its location is remembered (i.e. hashed). The shell builtin ` $ hash ` is invoked and responsible of remembering and displaying program locations.

### Executable

An executable program can be:

a) An **executable binary file** written in a translatable programming language (such as C or C++), and compiled into machine code. Hence the name of the ` /usr/bin/ ` directory (binaries).
b) An **executable text file** written in a scripting language (such as Shell, Python or Ruby). Scripts do not need to be compiled in order to be executed. They are interpreted line by line at runtime. Despite the name, not all executable programs in the directory ` /usr/bin/ ` are binary files. The directory also contains programs written in scripting languages, as proved by running the command:

```
$ file /usr/bin/* | cut -c 1-110 | awk '{print $0}' | sort -k2↵
```

#### User-guides for program-files

> [!TIP]
> Many programs can print out a short instruction, when invoked with the command line option requesting for help ` $ <executable> --help↵ ` such as:
>
> ```
> $ firefox --help↵
> Usage: /usr/lib64/firefox/firefox [ options ... ] [URL]
>        where options include:
> 
> X11 options
>   --display=DISPLAY  X display to use
>   --sync             Make X calls synchronous
>   --g-fatal-warnings Make all warnings fatal
> 
> Firefox options
>   -h or --help       Print this message.
>   -v or --version    Print Firefox version.
> ...
> ```

> [!TIP]
> Many programs come with man-pages, a type of documentation stored in the ` /usr/share/man/ ` directory. The ` $man <binary>↵ ` program is an interface to these manuals, such as
> 
> ```
> $ man firefox↵
> FIREFOX(1)         Linux User's Manual        FIREFOX(1)
> 
> NAME
>        firefox  - a Web browser for X11 derived from the
>        Mozilla browser
> 
> SYNOPSIS
>        firefox [OPTIONS ...] [URL]
> 
>        firefox-bin [OPTIONS] [URL]
> 
> DESCRIPTION
>        Mozilla Firefox is an  open-source  web  browser,
>        designed  for  standards  compliance, performance
>        and portability.
> ...
> ```

<a id="shell-builtin-command"></a>

### Shell builtin commands <!--update internal links if changed-->

Some commands are built into the shell. These **shell builtins** are run directly in the shell, and not as external programs. They are built-in because they are such an essential part of the shell's operation, such as ` $ alias `, ` $ unalias `, ` $ echo `, ` $ printf `, ` $ logout `, ` $ cd `, ` $ pwd ` and ` $ kill `. Use ` $ compgen -b↵ ` to get a list of the all the shell builtin commands. <!-- or visit [GNU Bash Features - Shell Builtin Commands](https://www.gnu.org/software/bash/manual/html_node/Shell-Builtin-Commands.html). -->

#### User-guides for shell-builtin-commands

> [!TIP]
> Instructions for shell-builtin-commands are printed by running ` $ help <builtin_command>↵ `. Help itself is a shell builtin command, and these instructions are built into the shell itself, because they are such an integral part of the shell:
> 
> ``` 
> $ bind --help↵
> bind: usage: bind [-lpsvPSVX] [-m keymap] [-f filename] [-q name] [-u name] [-r keyseq] [-x keyseq:shell-command] [keyseq:readline-function or readline-> command]
>
> $ help bind↵
> bind: bind [-lpsvPSVX] [-m keymap] [-f filename] [-q ...
>     Set Readline key bindings and variables.
> 
>     Bind a key sequence to a Readline function or a macro,
>     or set a Readline variable.  The non-option argument
>     syntax is equivalent to that found in ~/.inputrc, but
>     must be passed as a single argument.
> 
>     Options:
>       -m  keymap         Use KEYMAP as the keymap for...
>       -l                 List names of functions.
>       -P                 List function names and bind...
>       -p                 List functions and bindings ...
>       -S                 List key sequences that invo...
>       -s                 List key sequences that invo...
>       -V                 List variable names and valu...
>       -v                 List variable names and valu...
> ```

> [!NOTE]
> There are no man-pages for the shell builtin commands:
> 
> ```
> $ type bind↵
> bind is a shell builtin
> 
> $ whatis bind↵
> bind: nothing appropriate.
> 
> $ man bind↵
> No manual entry for bind
> ```

### Shell scripting

The command-line is already versatile on its own, but more complex processes are easier to implement using scripts. In particular, it is worth saving frequently used command-sequences in a file. **Shell scripting** enables the use of algorithms and structures specific to programming languages (such as variables, conditional statements, loops and functions). Infact writing scripts for the shell to execute, can be referred to as **shell programming**.
- Scripts do not need to be compiled in order to be executed. They are interpreted.
- A script file is executed by calling it by the filename such as ` $ ./script.sh↵ `
- A shell script file starts with the string ` #!/bin/bash `.
- Scripts do not have to be saved to a file. They can also be written directly to the command line. In this case, a semicolon ` ; ` is placed between the commands.
- In the Bash shell, variable names are preceded by the dollar sign ` $ `.
- Commenting is important in any program. In shell programming, a comment is added as ` # comment `. Shell does not read lines that begin with a hash mark ` # `. Similarly, a hash mark at the beginning of a word will start a comment and cause the entire rest of the line to be ignored.

> [!TIP]
> Comments are used to enhance readability.
>
> You will also see lines in [configuration files](02-basic.md#configuration-files) that are commented out to prevent them from being used by the affected program. This is done to give the reader suggestions for possible configuration choices or examples of correct configuration syntax.

<!-- **Shell functions** are miniature shell scripts incorporated into the environment. -->


### Alias

1. **Alias** is a shell builtin command that creates an alternative name for another command. For example ` $ alias up="sudo eopkg up"↵ ` creates an alias named up (as in update).

2. The use of aliases makes working on the command-line easier and faster. For example, when invoking our newly created alias ` $ up↵ `, the shell executes the command specified for the alias, such as ` $ sudo eopkg up↵ `.

3. Calling ` $ alias↵ ` on its own will print a list of all available aliases, such as

    ```
    $ alias↵
    alias ls='ls –color=auto'
    alias up='sudo eopkg up'
    ```

4. Use unalias to remove a specific alias such as ` $ unalias up↵ `

> [!TIP]
> From time to time, you may need to use the original version of a command with the same name instead of a particular alias, by starting the command with a backward slash ` \ `. For example, the original monochrome version of ` $ \ls↵ ` is used instead of the alias ` $ ls -color=auto↵ `.

> [!NOTE]
> Aliases vanish as the shell session ends. To make an alias permanent add the alias creation command (such as ` alias up="sudo eopkg up" `) to a new line on ` ~/.bashrc `.
>
> Making the addition on commandline can be a bit tricky. But fortunately run control files can be modified using a graphical text editor. Invoke from commandline like this ` $ gedit ~/.bashrc↵ ` or this ` $ xed ~/.bashrc↵ ` depending on the default text editor provided by the operating system.

### Alternative for aliases

> [!TIP]
> The optional ` $ xdotool ` package (if available to your system) can be used to create an elegant alternative for traditional aliases. Where the command specified by the alias gets typed on the shell prompt instead of being silently executed:
> ```
> $ alias up='stty -echo ; xdotool type "sudo eopkg up" ; stty echo'↵
> $ up↵
> $ sudo eopkg up # This line was automatically generated!
> ```

- Using ` $ xdotool ` can be great if you need to fine tune the aliased command before it is executed or want a visual reminder of what is about to be executed. For new users this can prevent frustration of having to use the commandline and yeat build recollection for commands; As they are repeatedly shown to the user despite having to make the effort of typing them in and possibly making mistakes.
    - The list for xdotool key codes can be found [here](https://gitlab.com/nokun/gestures/-/wikis/xdotool-list-of-key-codes).

<a id="autocomplete"></a>

## 3.11 Autocomplete

In a bash shell prompt, as you are typing a command, filename, directory or even command options, pressing the ` Tab ` key will either automatically complete what you were typing or show all the possible results for you. You may want to add to this behaviour, so it cycles through every possible suggestion with each repeated press on ` Tab `:

1. Run command ` $ gedit /etc/inputrc↵ ` or ` $ xed /etc/inputrc↵ ` depending on the default text editor provided by the operating system.
3. Add lines: [^stack-cycle]

    ```
    # Tweak auto completion
    set show-all-if-ambiguous on
    set show-all-if-unmodified on
    set menu-complete-display-prefix on
    "\t": menu-complete             # Tab
    "\e[Z": menu-complete-backward  # Shift + Tab
    ```

3. Save as ` ~/.inputrc `, a different location to what was opened.
4. Run command ` $ bind -f ~/.inputrc↵ ` [^stack-inputrc]

> [!NOTE]
> The configuration files ` /etc/inputrc ` and ` ~/.inputrc ` are part of the GNU Readline &#8209;library, which allows users to customize how keyboard input is interpreted and processed in the Bash command-line interface and in applications that use Readline. [^softpano-inputrc]

[^stack-cycle]: [Stackexchange.com - Terminal autocomplete: cycle through suggestions, accessed 2025](https://unix.stackexchange.com/questions/24419/terminal-autocomplete-cycle-through-suggestions)

[^stack-inputrc]: [Stackoverflow.com - Inputrc file cannot be loaded, accessed 2025](https://stackoverflow.com/questions/15027186/inputrc-file-cannot-be-loaded)

[^softpano-inputrc]: [Softpanorama.org - Readline and inputrc, updated 2019](http://www.softpanorama.org/Scripting/Shellorama/Bash_as_command_interpreter/inputrc.shtml)

<a id="some-keyboard-shortcuts"></a>

## 3.12 Some useful shortcuts

New users easily encounter situations, in the command interface, from which there seems to be no way out. You may try the following to exit some commandline situations:

| Keys | Use case |
|:--- |:--- |
| ` Ctrl + D ` | End text input |
| ` Ctrl + C ` | Interrupt current process |
| ` q ` | Quit ` $ less ` and ` $ more ` |
| ` Ctrl + X ` | Exit ` $ nano ` |
| ` Ctrl + X, Ctrl + C ` | Exit ` $ emacs ` |
| ` Esc, :qa!↵ ` | Exit ` $ vi ` |
| ` Alt + F4 ` | Close current window |

The current command line can be cleared by other means than just pressing the ` Backspace `:

| Keys | Use case |
|:--- |:--- |
| ` Ctrl + C ` | Cancel |
| ` Ctrl + W ` | Delete just a word. |
| ` Ctrl + U ` | Clear up to the beginning. |
| ` Ctrl + L ` | Clear the terminal screen (with scrollback-ability). <br>Typing ` $ clear -x↵ ` does the same thing. |
| ` Alt + Shift + 3 ` | Turning current line to a comment ` # ` is especially useful if you want to keep and comment on bash history (see [Chapter 2, Section: Bash history](02-basic.md#bash-history)). |

Shorcuts specific to GUI terminal window:

| Keys | Use case |
|:--- |:--- |
| ` F11 ` | Toggle fullscreen |
| ` Control + Shift + F ` | Search or find for text displayed on current terminal window. |

<!-- # References -->

[^raymond-cmopt]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 10<!--. Configuration-->, Section: Command-Line Options](http://www.catb.org/~esr/writings/taoup/html/ch10s05.html)

[^raymond-docstyle]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 18<!--. Documentation-->, Section: The Unix Style Documentation](http://www.catb.org/~esr/writings/taoup/html/ch18s02.html)

[^raymond-bestdoc]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 18<!--. Documentation-->, Section: Best Practices for<!-- Writing Unix--> Documentation](http://www.catb.org/~esr/writings/taoup/html/ch18s06.html)

[^raymond-bag]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 20<!--. Futures-->, Section: <!--A Unix File Is -->Just a Big Bag of Bytes](http://www.catb.org/~esr/writings/taoup/html/ch20s03.html)

[^raymond-weak]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 20<!--. Futures-->, Section: Unix Support for GUIs<!-- Is Weak-->](http://www.catb.org/~esr/writings/taoup/html/ch20s03.html)


