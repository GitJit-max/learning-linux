<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="04-installing.md">&lt;&lt; Previous Chapter: 4 - Installing applications</a>
     |
  <a href="06-inter.md">Next&nbsp;Chapter:&nbsp;6&nbsp;&#8209;&nbsp;Interoperability&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 5 - Links in the file system

It is possible to have a file referenced by multiple names. The concept of file system links can be confusing, but it's important to be aware of them, because you might encounter them from time to time.

> [!IMPORTANT]
> Only some file systems support unix-style [symbolic and hard links](#symbolic-and-hard-links).

- Both symbolic and fixed links are supported by file systems designed for unix-like operating systems such as EXT4, BTRFS and ZFS.
- NTFS, the default file system for Windows, can handle symbolic links on GNU/Linux, but does not fully support hard links [^wiki-hard].
- Neiher symbolic nor hard links are supported by FAT32 or exFAT, the other two, common general purpose file systems created by Microsoft.

[^wiki-hard]: [Wikipedia - NTFS Hard links, accessed 2025](https://en.wikipedia.org/wiki/NTFS#Hard_links)

<a id="drag-and-drop"></a>

## 5.1 Drag and drop

### Freedesktop shortcut files

> [!TIP]
> Modern GNU/Linux desktop environments support Windows-like functionality of shortcut files (see [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry-spec/latest/)).

> The specification of desktop entry files are part of the [Freedesktop.org](https://www.freedesktop.org/wiki/Specifications/) project. The goal of Freedesktop.org is to create open standards and interoperability between different GNU/Linux-based desktop environments. Most Freedesktop.org projects are designed to be independent of any specific desktop environment, and improve their compatibility.
> 
> Freedesktop.org (formerly X Desktop Group) was founded year 2000 by Havoc Pennington, an American programmer and free software advocate. <!--Most freedesktop projects work independently of the desktop environment and improve compatibility between them.-->

1. Lets try creating a shortcut file by drag and drop. When you drag a URL (such as <https://github.com>) from Firefox and drop it to ` ~/Desktop/ ` a [desktop entry file](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) is created. Grab the lock icon preceding the URL.

2. Freedesktop shortcuts are actually text files. They can be opened and edited by any text editor. They may be identified by their file name extension ` *.desktop `. However modern file managers (such as Nemo) may not display the filename such as ` GitHub.desktop `. Instead they usually display a string from inside the file, specified by the value of the key: ` Name = Link to GitHub `.

3. The file content will be something like:

    ```
    [Desktop Entry]
    Encoding=UTF-8
    Name=Link to GitHub
    Type=Link
    URL=https://github.com/
    Icon=text-html
    ```
    
4. Despite the name ` *.desktop `, such files do not need to be located in the ` ~/Desktop/ ` directory. In fact, all items in the main [Desktop Menu](https://www.freedesktop.org/wiki/Specifications/menu-spec/) are ` *.desktop ` files and located in ` /usr/share/applications/ `.

5. Use of these desktop entry files is similar to how their equivalents are used in Windows. Double-clicking will trigger the functionality specified in the file, such as opening a URL (as created in the example above). 

### Symbolic link by drag and drop

Graphical file managers (such as Nemo) provide an easy and automatic method of creating another type of shortcut. Holding **` Ctrl + Shift `** while dropping a file will create a [symbolic link](#symbolic-and-hard-links), rather than copying or moving the file. In some distributions, a small menu appears whenever a file is dropped; offering a choice of copying, moving or linking the file. [^shotts-guilink]

> In addition, there are so-called [hard links](#symbolic-and-hard-links). It is important to be aware of hard links, because you might encounter them from time to time, even though modern practice prefers symbolic links. [^shotts-hard]

<a id="symbolic-and-hard-links"></a>

## 5.2 Symbolic and hard links 

Links (symbolic and hard) are a way to refer to a file on disk. The best understanding of this is that both the contents of the file and a reference to the contents (i.e. the name of the file) are stored on the disk. And that there may be several of these references.

Symbolic links were created to overcome the two disadvantages of hard links: [^shotts-syml]
1. A hard link cannot reference a directory (only a file). [^shotts-syml]
2. Hard links cannot <!--span physical devices i.e. a hard link cannot reference a file outside its own file system. This means a link cannot--> reference any file that is not on the same disk partition as the link itself. [^shotts-syml]

> [!NOTE]
> Symbolic and hard links do not work for URLs. Use [.desktop files](#freedesktop-shortcut-files) for URLs.

### Hard link

A **hard link** is a reference to the inode number of a file on physical storage. Hard links must be on the same physical partition as the contents of the file itself, because the inode number is unambiguous only within the file system. A file will always have at least one hardlink because the file's name is created by a hardlink. The ` $ ls ` command has a way to reveal this information when invoked with the ` -i ` option. [^shotts-hard]

The ` $ rm ` command deletes files, including a hard links. However, data is still accessible as long as another hard link exists. As there can be several hard links to the same file, the space occupied by the file on the disk is not released until all the hard links to it have been removed. When one of several hard links is deleted, only the link is removed; even if you delete the original file, which is a hardlink itself. The contents of the file itself continue to exist (its space is not deallocated) until all links to the file are deleted. To get rid of data you must remove all hard links. A remove command applied to a hard link also deletes the contents of the file when deleting the last hard link. [^shotts-hard]

When we list a directory containing a hard link we will see no special indication of the link, unless we know what we are looking for (see [Section: Identifying a hard link is difficult](#identifying-a-hard-link-is-difficult)).

### Symbolic link
    
A **symbolic link** can point to any file, including different file systems and destinations that do not exist; this happens also if the destination of a symbolic link is deleted.
- The remove command ` $ rm ` applied to a symbolic link, or ` Delete ` in a graphical file manager, only removes the symbolic link, never the target file to which the link refers.
- In most other file processing operations, the links are "decompressed" so that the paths through them work normally. <!--One thing to remember about symbolic links is that -->Most file operations are carried out on the link's target, not the link itself. For example, if we write something to the symbolic link, the referenced file is written to. [^shotts-syml]
- Symbolic links contain a text pointer to the target file or directory. However, a symlink file cannot be opened in a text editor. Opening a symlink always opens the target file. Reading the destination from a symlink file requires a special system call such as ` $ readlink <file>↵ `.
- A symbolic link can be relative, so that it is interpreted in relation to its parent directory.
- If the target file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken. In many implementations, the ` $ ls ` command will display broken links in a distinguishing color such as red, to reveal their presence. [^shotts-syml]

<a id="examples-of-links"></a>

## 5.3 Examples of links

### Lets make links

```
# Create a hard-link:
$ ln /path/to/existing_file /path/to/new_hardlink↵

# Create or update a symbolic-link:
$ ln -sf /path/to/existing_file /path/to/symlink↵
```

Graphical file managers (such as Nemo) provide an easy method for creating symbolic links: Holding **` Ctrl + Shift `** while dropping a file will create a symlink, rather than copying or moving the file. In some distributions, a small menu appears whenever a file is dropped; offering a choice of copying, moving or linking the file.

### Identifying symbolic links is easy

In the command interface, symbolic links are fairly easy to identify using the ` $ ls -li ` command. The list command reveals symlinks with an arrow ` -> `, with the link file on the left and the referenced file on the right. The arrow is also used in graphical file managers and appears as part of the file icon.

A good example of a symlink is ` $ x-terminal-emulator ` which points to an actual executable such as ` $ gnome-terminal `:

```
$ which x-terminal-emulator↵
/usr/bin/x-terminal-emulator

$ ls -li /usr/bin/x-terminal-emulator↵
266302 lrwxrwxrwx 1 root root 14  9. 5. 15:48 /usr/bin/x-terminal-emulator -> gnome-terminal
```

### Identifying a hard link is difficult

In the command interface, hard links can be identified with ` $ ls -li <file>↵ ` if you know what you are looking for. The number between the permissions column and the owner name, indicates the number of hard links to the file.

```
$ ls -li /usr/bin/c++↵  # Note number 4 before "root"
309582 -rwxr-xr-x 4 root root 1076160 21. 5. 23:19 /usr/bin/c++

$ stat /usr/bin/c++↵    # Note number 4 after "Links:"
  File: /usr/bin/c++
  Size: 1076160   Blocks: 2104     IO Block: 4096   regular file
Device: 259,2     Inode: 309582    Links: 4
Access: (0755/-rwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2024-06-09 06:39:35.340520475 +0300
Modify: 2024-05-21 23:19:21.184657000 +0300
Change: 2024-06-02 10:26:47.650834218 +0300
Birth: 2024-06-02 10:26:47.629834110 +0300
```

> [!NOTE]
> The number of hard links is shown also in conjunction with directories. This can be confusing, as the file system does not allow hardlinks to be created for directories. The hard links to a specific directory comes from its adjacent directories. The minimum is always two: One from the parent directory and one from the current directory (notation ` ./ `). And the number of hardlinks will increase by the number of all immediate subdirectories (notation ` ../ `).

<!-- > The hard link count is slightly different in the case of directories, because the unix style file system does not allow hard links on directories. The "hard link count" for a directory is the count of all immediate sub-directories (level 1) plus one for the current directory (the ` ./ ` entry) and one for the parent directory (the ` ../ ` entry). -->

### Lets find all hard links

Once you find a file with more than one hard-link, you might want to find all the links to the file:

```
$ sudo find / -inum 309582↵
./usr/bin/g++
./usr/bin/x86_64-solus-linux-c++
./usr/bin/c++
./usr/bin/x86_64-solus-linux-g++

$ sudo find / -samefile /usr/bin/c++↵
/usr/bin/g++
/usr/bin/x86_64-solus-linux-c++
/usr/bin/c++
/usr/bin/x86_64-solus-linux-g++
```

<!-- # References -->

[^shotts-guilink]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 4, Section: Creating Symlinks With The GUI](http://linuxcommand.org/tlcl.php)

[^shotts-hard]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 4, Section: Hard Links](http://linuxcommand.org/tlcl.php)

[^shotts-syml]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 4, Section: Creating Symbolic Links](http://linuxcommand.org/tlcl.php)


