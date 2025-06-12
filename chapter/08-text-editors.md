<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="07-advanced-terminal.md">&lt;&lt; Previous Chapter: 7 - Advanced terminal usage</a>
     |
  <a href="09-multi-user.md">Next&nbsp;Chapter:&nbsp;9&nbsp;&#8209;&nbsp;Access&nbsp;management&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 8 - Text editors

A **text editor** is a simple computer program that allows users to create, change, or edit plain text files. Traditionally text editors were used for creating computer programs, web pages, etc. Today text editors are most commonly used for things like editing configuration files, simple note taking, analyzing log files, middleware for stripping formatting from copy-pasted text and making some quick find and replace operations; not so much for programming or creating documents, as it was in the past.

Traditional [terminal-based text editors](#terminal-based-text-editors) can be categorized in [line oriented](#line-editorsss) and [screen oriented](#screen-editors) text editors. Screen oriented editors, feature the ability to modify any visible text on the screen by moving the cursor to its location. For most purposes, line oriented editors were superseded by screen oriented editors, because line editors were relics from the days of teletypes, when terminals used to print, on paper, very slowly.

[Modern text editors](#gui-text-editors) for the desktop can be very simple plain text editors offering a minimal set of features (such as ` $ gedit ` and ` $ xed `), or considerably more advanced. Advanced text editors such as [Kate](https://kate-editor.org/about-kate/) offer a wide range of features and a plugin system.

<a id="terminal-based-text-editors"></a>

## 8.1 Terminal-based text editors

Until late 1970's, terminals with a screen were a rare luxury, let alone mice or graphic display devices. Work was done on a workstation resembling a large electric typewriter (called teletypes). <!--, which printed both the commands the user typed and the computer's responses on paper.--> Editing text files on teletypes was entirely command-based. They printed everything on paper instead of displaying it on a screen. Users relied on **line editors** using commands to modify specific lines, append new text, or delete sections. Since there was no real-time display, users had to print parts of the file repeatedly to review their changes. This method was slow and required memorizing commands for precise editing. [^petteri-jarvinen]

Line editors [GNU ed](https://www.gnu.org/software/ed/manual/ed_manual.html) `$ ed` and [GNU sed](https://www.gnu.org/software/sed/) `$ sed` faithfully follow these old principles. Although their interface is a blast from past decades, they have their own merits (see [Section: Line editors: Ed and Sed](#line-editors-ed-and-sed)).

[^petteri-jarvinen]: [Petteri Järvinen - PC-käyttäjän käsikirja 1993, page 256](https://www.petterijarvinen.fi/PC-k%C3%A4ytt%C3%A4j%C3%A4n%20k%C3%A4sikirja%20DOS%206.2%20(1993).pdf)

<a id="line-editorsss"></a>

### Line editors: Ed and Sed 

> In 1969 Dennis Ritchie and Ken Thompson (original developers of the C language and the Unix operating system), while at Bell Labs, developed ed, a simplified form of qed (quick editor). [^raymond-ed]

[**GNU ed**](https://www.gnu.org/software/ed/) is a clone of the original ` $ ed ` editor for Unix, and thus a classic example of a line-oriented text editor. It is truly Unix-minimalist way of plain-text editing. It has a simple, austere instruction based CLI, and there is no screen display. Unbelievable as it may seem to a modern reader, most of Unix's original code was written with this editor. As an **instruction based** editor, the user must specify a particular line of text, before making any changes. Let's see ` $ ed ` in action with the following listing: [^raymond-ed]

```
$ ed sample.txt↵
15    # Ed informs us the file has some text in it already.
a↵    # This is the command to append text to the file.
Aaaa↵
Bbbb↵
.↵    # This is the command to terminate the append.
w↵    # This is the command to write the file to disk.
25    # Ed informs us the new file size.
1,$p↵ # This is the command to print all lines from 1 to the last.
q↵    # This is the command to end the editing session. You may also press Ctrl + D anytime to cancel and exit ed.
```

> [!NOTE]
> Press ` Ctrl + D ` to exit ed (repeatedly if necessary).

[**GNU sed**](https://www.gnu.org/software/sed/) (stream editor) is also closely related to ` $ ed `. Many of the basic commands are the same, though non-interactive and designed to be invoked through command-line switches, rather than from standard input. It takes text input, performs some operation (or set of operations) on it, and outputs the modified text. ` $ sed ` is typically used for extracting part of a file using pattern matching or substituting multiple occurrences of a string within a file. [^gnu-sed]

[^gnu-sed]: [GNU - GNU sed, accessed 2024](https://www.gnu.org/software/sed/)

```
$ sed -i "$ a Aaaa\nBbbb" sample.txt↵  # Add rows Aaaa and Bbbb
$ sed '4d' input.txt > output.txt↵     # Delete 4th line in file
```

> [!NOTE]
> Back in the early years of Unix, ed was used to create, display, modify and otherwise manipulate text files, both interactively and via shell scripts. Then ed became primarily a program-driven editing tool for scripts; a role to which editors with more elaborate modes of interactivity were and still are unsuited. For this reason most unices, still even today, include an implementation of ` $ ed ` and ` $ sed `. [^raymond-ed]

<a id="screen-editors"></a>

<a id="screen-editor-vi"></a>

### Screen editor: Vi 

> In 1976 William Joy / Bill Joy (of e.g. Sun Microsystems), while at the University of California at Berkeley, releases the screen oriented text editor ` $ vi `, together with its line oriented counterpart ` $ ex `. Vi and ex are different interfaces to the same program behind it; one screen oriented, one line oriented. [^raymond-vi]

**` $ vi `** stands for Visual Interface. The original Vi editor was the first attempt to bolt a visual interface onto the command set of Ed. Like Ed, it's commands are generally single keystrokes, and it is particularly well suited to use by touch-typists. The original Vi didn't have mouse support, editing menus, macros, assignable key bindings, or any form of user customization. In line with the religion of Ed, the Vi partisans considered the lack of these features a virtue. On this view, one of vi's most important virtues is that you can start editing immediately on a new Unix system without having to carry along your customizations or worrying that the default command bindings will be dangerously different from what you're used to. One characteristic of Vi that beginners tend to find frustrating is a result of its terse single-keystroke commands. [^raymond-vi]

One feature that frustrates new users is vi's short one-key commands. Like line editors, vi has a moded interface (as in modes). You are either in command mode or text input mode. In command mode, typing text is interpreted as commands, and does strange and probably destructive things to the content. Switching between modes is bound to be a headache for new users. In text input mode, the only commands that work are ` Esc ` for exiting key mode, and the cursor movement keys (in newer versions). It is only in later vi implementations (such as vim) that a selection mode for selecting and editing text areas has been added. [^wiki-vi-fi]

[^wiki-vi-fi]: [Wikipedia - vi, accessed 2025](https://fi.wikipedia.org/wiki/Vi)

> [!NOTE]
> Today, on most unix like systems and macOS, ` /usr/bin/vi ` is just a symlink to ` /usr/bin/vim `, a clone from Bill Joy's original vi. Vim is a much improved version of the old UNIX editor. Full vi compatibility is maintained, which explains the confusion between the terms vi and vim. And it runs on almost all flavours of UNIX. [^raymond-vi]

Over the years, vi has bulked up considerably. The modern versions add mouse support, editing menus, multiple files in separate buffers, customization with a run-control file and unlimited undo (the original vi could only undo the last command). Vi looks rather bloated and flabby. There are hundreds of commands, many of them duplicative. Most users don't know more than 5% of the command set. Over the years, Vi has had progressively more and more special-purpose C code bolted onto it to perform tasks that Emacs would attack with Lisp code modules and subprocess control. The extensions are not, as in Emacs, libraries loaded as needed. Users pay the overhead for the resulting code bloat all the time. As a result, the size difference between a modern vi and a modern Emacs is not nearly as great as one might expect. [^raymond-vi]

> [!TIP]
> To exit vi, type: ` Esc + :qa!↵ `<br>where ` q ` stand for quit, ` a ` for all, and ` ! ` for without saving.

Any other instruction to use vi(m) is beyond the scope of this book. But those interested to learn more, can start with this tutorial: [Karim Buzdar - Working With Vi Editor in Linux, published 2018](https://vitux.com/working-with-vi-editor-in-linux/).

### Screen editor: Emacs 

> In 1976 Richard Stallman, Guy Steele, and Dave Moon, while at MIT, release EMACS. [^raymond-emacs]

[**GNU Emacs**](https://www.gnu.org/software/emacs/) stands for Editing MACroS. It was originally written in the late 1970's as a set of macros in an editor called TECO, then reimplemented several times in different ways. Objectives of the Emacs design are far more broad than most other text editors. Emacs wants to be a unified interface to all tools that operate on text. Emacs can give you capabilities resembling those of a conventional integrated development environment and beyond. You're not limited by the imagination of the IDE designer. You can tweak, customize, and add task-related intelligence using Emacs Lisp. [^raymond-emacs]
- Emacs is a big, feature-laden program with a great deal of customizability. Emacs has an entire programming language (Elisp) inside it that can be used to write arbitrarily powerful editor functions. [^raymond-emacs]
- Emacs could be considered a virtual machine or framework around a collection of small, sharp tools (the modes) that happen to be written in Elisp. But one doesn't have to learn Elisp to use Emacs. [^raymond-emacs]
- Unlike Vi, Emacs doesn't have interface modes; Instead, commands are normally control characters or prefixed with an ` Esc ` i.e. ` ^[ `. [^raymond-emacs]
- Emacs is correspondingly harder to learn than vi(m). Learning how to customize Emacs is an entire art in itself. [^raymond-emacs]

> Now deprecated MicroEmacs and Pico were small editors that cloned the default keybindings and appearance of Emacs without emulating its extensibility. [^raymond-emacs]
>
> [GNU Nano](https://www.nano-editor.org/docs.php) ` $ nano ` is an "easy-to-use" text editor originally designed as a replacement for Pico, but nowadays implements several features that Pico lacked such as undo, redo and syntax highlighting. [^raymond-emacs]

> [!TIP]
> Press ` Ctrl + X, Ctrl + C ` to exit Emacs.

### Screen editor: Ne

[**Ne**](https://ne.di.unimi.it) stands for Nice Editor. It is a screen oriented console text editor intended to provide an alternative to Vi that will be more familiar to beginners and modern users. It has been ranked as one of the best console text editors for GNU/Linux because:
- It has a menu bar that is opened by pressing ` Esc ` followed by any arrow key.
- It uses keyboard shortcuts derived from modern desktop interface such as ` Ctrl + Q ` to quit and ` Ctrl + O ` to open a file.
- It has support for UTF-8 encoding.
- It supports many features common in advanced text editors such as syntax highlighting, autocomplete, configurable menus and configurable keybindings, regular expressions (see [Chapter 6, Section: GNU Grep](06-inter.md#gnu-grep)).
- It is portable across all POSIX-compliant operating systems such as GNU/Linux and macOS.
- It remains usable on slow remote connections.
- It can pipe a marked block of text through any command line filter.

> [!TIP]
> Press ` Ctrl + Q, Y ` to exit Ne.

### The default text editor 

The default text editor is defined by environment variables ` EDITOR ` and ` VISUAL `. ` EDITOR ` used to be for instruction-based editors like ` $ ed `. When editors with graphical terminal user interface (such as ncurses) came about, the editing process changed dramatically, and thus need for another variable arose. [^visual-vs-editor]

On a modern GNU/Linux the terminal GUI editors and desktop GUI editors can both provide the same functionality; So you can set ` VISUAL ` to either a terminal-based editor such as ` $ export VISUAL="/usr/bin/ne"↵ ` or a modern desktop application such as ` $ export VISUAL="/usr/bin/gedit"↵ `. [^visual-vs-editor]

However, ` EDITOR ` is meant for a fundamentally different workflow. Especially people who use slow serial lines to connect to embedded systems over dicey connections might still appreciate being able to have a preferred line mode editor distinct even from a visual editor like Vim, Nano or Ne. [^visual-vs-editor]

> [!TIP]
> Pressing ` Ctrl + X, Ctrl + E ` on a half typed command on the current shell prompt, will move the unfinished command to your editor of choice, where you can finish the command before it gets executed.

[^visual-vs-editor]: [Stack Exchange - VISUAL vs. EDITOR, accessed 2024](https://unix.stackexchange.com/questions/4859/visual-vs-editor-what-s-the-difference)

<a id="gui-text-editors"></a>

## 8.2 Modern text editors

**` $ xed `** is a simple text editor developed by the Linux Mint community for the Cinnamon desktop environment. <https://en.wikipedia.org/wiki/Xed>

**` $ gedit `** was the default text editor for the Gnome desktop environment until 2022. It has also been available for other desktop environments, but the future remains uncertain. <https://en.wikipedia.org/wiki/Gedit>

**` $ gnome-text-editor `** is a simple text editor developed by Gnome Builder's creator Christian Hergert. Gnome Text Editor became the default editor for the Gnome desktop environment in 2022, but is also available for other desktop environments. <https://en.wikipedia.org/wiki/GNOME_Text_Editor>

**` $ kate `** is an advanced text editor developed by the KDE community, but is also available for other desktop environments. <https://kate-editor.org/>
- There is is a stripped down version of Kate called **` $ kwrite `**, with not as many features. They share code, they are different options of the same program, but they present like different programs. KWrite is more of a standard plain text editor, whereas Kate can be more of an integrated development environment. 

<!-- # References -->

[^raymond-ed]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 13<!--. Complexity-->, Section: ed](http://www.catb.org/~esr/writings/taoup/html/ch13s02.html)

[^raymond-vi]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 13<!--. Complexity-->, Section: vi](http://www.catb.org/~esr/writings/taoup/html/ch13s02.html)

[^raymond-emacs]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 13<!--. Complexity-->, Section: Emacs](http://www.catb.org/~esr/writings/taoup/html/ch13s02.html)
