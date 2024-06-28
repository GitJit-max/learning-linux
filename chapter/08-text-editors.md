<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="07-advanced-terminal.md">&lt;&lt; Previous Chapter: 7 - Advanced terminal usage</a>
     |
  <a href="09-multi-user.md">Next&nbsp;Chapter:&nbsp;9&nbsp;&#8209;&nbsp;Multiuser&nbsp;capability&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 8 - Text editors

A **text editor** is a simple computer program that allows users to create, change, or edit plain text files. Traditionally text editors were used for creating computer programs, web pages, etc. Today text editors are most commonly used for things like editing configuration files, simple note taking, analyzing log files, middleware for stripping formatting from copy-pasted text and making some quick find and replace operations; Not so much for programming or creating documents, as it was in the past.

Traditional [terminal-based text editors](#cli-text-editors) can be categorized in 1) [line oriented](#line-editors) and 2) [screen oriented](#screen-editors) text editors. Screen oriented editors, feature the ability to modify any visible text on the screen by moving the cursor to its location. For most purposes, line oriented editors were superseded by screen oriented editors, because line editors were relics from the days of teletypes, when terminals used to print, on paper, very slowly.

[Modern text editors](#gui-text-editors) for the desktop can be 1) very simple plain text editors offering a minimal set of features (such as ` $ gedit ` and ` $ xed `), or 2) advanced text editors offering a wide range of features and a plugin system such as [Kate](https://kate-editor.org/about-kate/).

<a id="cli-text-editors"></a>

## 8.1 CLI text editors

<a id="line-editors"></a>

### Line editors: Ed and Sed [^raymond]

> In 1969 Dennis Ritchie and Ken Thompson (original developers of the C language and the Unix operating system), while at Bell Labs, developed ed, a simplified form of qed (quick editor).

[GNU ed](https://www.gnu.org/software/ed/) is a clone of the original ` $ ed ` editor for Unix, and thus a classic example of a line-oriented text editor. It is truly Unix-minimalist way of plain-text editing. It has a simple, austere instruction based CLI, and there is no screen display. Unbelievable as it may seem to a modern reader, most of Unix's original code was written with this editor. As an **instruction based** editor, the user must specify a particular line of text, before making any changes. Let's see ` $ ed ` in action with the following listing:

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

[GNU sed](https://www.gnu.org/software/sed/) (stream editor) is also closely related to Ed. Many of the basic commands are the same, though non-interactive and designed to be invoked through command-line switches, rather than from standard input. It takes text input, performs some operation (or set of operations) on it, and outputs the modified text. ` $ sed ` is typically used for extracting part of a file using pattern matching or substituting multiple occurrences of a string within a file. [^gnu-sed]

[^gnu-sed]: [GNU - GNU sed, accessed 2024](https://www.gnu.org/software/sed/)

```
$ sed -i "$ a Aaaa\nBbbb" sample.txt

$ sed '4d' input.txt > output.txt # Delete the 4th line in a file
```

> [!NOTE]
> Back in the early years of Unix, Ed was used to create, display, modify and otherwise manipulate text files, both interactively and via shell scripts. Then Ed became primarily a program-driven editing tool for scripts; A role to which editors with more elaborate modes of interactivity were and still are unsuited. For this reason most unices, still even today, include an implementation of ` $ ed ` and ` $ sed `.

<a id="screen-editors"></a>

<a id="screen-editor-vi"></a>

### Screen editor: Vi [^raymond]

> In 1976 William Joy / Bill Joy (of e.g. Sun Microsystems), while at the University of California at Berkeley, releases the screen oriented text editor vi, together with its line oriented counterpart ex. (Vi and ex are different interfaces to the same program behind it; one screen oriented, one line oriented.)

Vi stands for Visual Interface. The original Vi editor was the first attempt to bolt a visual interface onto the command set of Ed. Like Ed, it's commands are generally single keystrokes, and it is particularly well suited to use by touch-typists. The original Vi didn't have mouse support, editing menus, macros, assignable key bindings, or any form of user customization. In line with the religion of Ed, the Vi partisans considered the lack of these features a virtue. On this view, one of vi's most important virtues is that you can start editing immediately on a new Unix system without having to carry along your customizations or worrying that the default command bindings will be dangerously different from what you're used to. One characteristic of Vi that beginners tend to find frustrating is a result of its terse single-keystroke commands.
- Vi has a moded interface (as in modes); You are either in the command mode or in the text-insertion mode. In text-insertion mode, the only commands that work are the ` Esc ` key for mode exit and the cursor-movement keys (on newer versions). In command mode, typing text will be interpreted as commands and do odd, and probably destructive, things to your content.

> [!NOTE]
> Today most unix like systems and macOS ship Vim as ` $ vi `. Vim is a greatly improved version of the old UNIX editor, with full Vi compatibility maintained. And it runs on almost all flavours of UNIX.

Over the years, Vi(m) has bulked up considerably. The modern versions add mouse support, editing menus, multiple files in separate buffers, customization with a run-control file and unlimited undo (the original Vi could only undo the last command). Vi(m) looks rather bloated and flabby. There are hundreds of commands, many of them duplicative. Most users don't know more than 5% of the command set. Over the years, Vi(m) has had progressively more and more special-purpose C code bolted onto it to perform tasks that Emacs would attack with Lisp code modules and subprocess control. The extensions are not, as in Emacs, libraries loaded as needed. Users pay the overhead for the resulting code bloat all the time. As a result, the size difference between a modern Vi(m) and a modern Emacs is not nearly as great as one might expect.

> [!NOTE]
> Press ` Esc, :qa!, Ent ` to exit Vi(m). Any other instruction to use Vi(m) is beyond the scope of this tutorial. But those interested to learn more, can start with this tutorial: [Karim Buzdar - Working With Vi Editor in Linux, published 2018](https://vitux.com/working-with-vi-editor-in-linux/).


### Screen editor: Emacs [^raymond]

> In 1976 Richard Stallman, Guy Steele, and Dave Moon, while at MIT, release EMACS.

[GNU Emacs](https://www.gnu.org/software/emacs/) stands for Editing MACroS. It was originally written in the late 1970's as a set of macros in an editor called TECO, then reimplemented several times in different ways. Objectives of the Emacs design are far more broad than most other text editors. Emacs wants to be a unified interface to all tools that operate on text. Emacs can give you capabilities resembling those of a conventional integrated development environment and beyond. You're not limited by the imagination of the IDE designer. You can tweak, customize, and add task-related intelligence using Emacs Lisp.
- Emacs is a big, feature-laden program with a great deal of customizability. Emacs has an entire programming language (Lisp) inside it that can be used to write arbitrarily powerful editor functions.
- Emacs could be considered a virtual machine or framework around a collection of small, sharp tools (the modes) that happen to be written in Lisp. But one doesn't have to learn Lisp to use Emacs.
- Unlike Vi, Emacs doesn't have interface modes; Instead, commands are normally control characters or prefixed with an ` Esc `.
- Emacs is correspondingly harder to learn than Vi. Learning how to customize Emacs is an entire art in itself.
- Now deprecated MicroEmacs and Pico were small editors that cloned the default keybindings and appearance of Emacs without emulating its extensibility. GNU Nano is an "easy-to-use" text editor originally designed as a replacement for Pico, but nowadays implements several features that Pico lacked such as undo, redo and syntax highlighting.

> [!NOTE]
> Press ` Ctrl + X, Ctrl + C ` to exit Emacs.

### Screen editor: Ne

[Ne](https://ne.di.unimi.it) stands for Nice Editor. It is a screen oriented console text editor intended to provide an alternative to Vi that will be more familiar to beginners and modern users. It has been ranked as one of the best console text editors for GNU / Linux because:
- It is portable across all POSIX-compliant operating systems such as GNU / Linux and macOS.
- It remains usable on slow remote connections.
- It can pipe a marked block of text through any command line filter.
- It supports many features common in advanced text editors such as syntax highlighting, regular expressions, autocomplete, configurable menus and configurable keybindings.
- It has support for UTF-8 encoding.

Ne uses GUI-derived keyboard shortcuts (such as ` Ctrl + Q ` to quit and ` Ctrl + O ` to open a file) instead of the multi-mode command structure of Vi and Emacs. Ne also has a menu bar that is opened by pressing ` Esc ` followed by any arrow key.

### The default text editor [^visual-vs-editor]

[^visual-vs-editor]: [Stack Exchange - VISUAL vs. EDITOR, accessed 2024](https://unix.stackexchange.com/questions/4859/visual-vs-editor-what-s-the-difference)

The default text editor is defined by environment variables ` EDITOR ` and ` VISUAL `. ` EDITOR ` used to be for instruction-based editors like ` $ ed `. When editors with graphical terminal user interface (such as ncurses) came about, the editing process changed dramatically, and thus need for another variable arose.
- On a modern GNU / Linux the terminal GUI editors and desktop GUI editors can both provide the same functionality; So you can set ` VISUAL ` to either ` $ export VISUAL="/usr/bin/ne"↵ ` or ` $ export VISUAL="/usr/bin/gedit"↵ `.
- However, ` EDITOR ` is meant for a fundamentally different workflow. Especially people who use slow serial lines to connect to embedded systems over dicey connections might still appreciate being able to have a preferred line mode editor distinct even from a visual editor like Vim, Nano or Ne.

> [!TIP]
> Pressing ` Ctrl + X, Ctrl + E ` on a half typed command on the current shell prompt, will move the unfinished command to your editor of choice, where you can finish the command before it gets executed.

<a id="gui-text-editors"></a>

## 8.2 Modern text editors

` $ gedit ` was the default text editor for the Gnome desktop environment until 2022. It has also been available for other desktop environments, but the future remains uncertain. <https://en.wikipedia.org/wiki/Gedit>

` $ gnome-text-editor ` is a simple text editor developed by Gnome Builder's creator Christian Hergert. Gnome Text Editor became the default editor for the Gnome desktop environment in 2022, but is also available for other desktop environments. <https://en.wikipedia.org/wiki/GNOME_Text_Editor>

` $ xed ` is a simple text editor developed by the Linux Mint community for the Cinnamon desktop environment. <https://en.wikipedia.org/wiki/Xed>

` $ kate ` is an advanced text editor developed by the KDE community, but is also available for other desktop environments. <https://kate-editor.org/>

<!-- # References -->

[^raymond]: [Eric Steven Raymond - The Art of Unix Programming, published 2003](https://www.arp242.net/the-art-of-unix-programming/)
