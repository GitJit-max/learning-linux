<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="04-installing.md">&lt;&lt; Previous Chapter: 4 - Installing applications</a>
     |
  <a href="06-inter.md">Next&nbsp;Chapter:&nbsp;6&nbsp;&#8209;&nbsp;Interoperability&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 5 - Links

In unix it is possible to have a file referenced by multiple names. The concept of links can be confusing, but it's important to be aware of links, because you might encounter them from time to time.

<a id="drag-and-drop"></a>

## 5.1 Drag and Drop

1. When you drag a URL from Firefox (the lock icon just before the URL) and drop it to ` ~/Desktop/ ` a [desktop entry file](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) is created such as ` GitHub.desktop ` with text content like:

    ```
    [Desktop Entry]
    Encoding=UTF-8
    Name=Link to GitHub
    Type=Link
    URL=https://github.com/
    Icon=text-html
    ```

- Graphical file managers (such as Nemo) might not show the file name ` GitHub.desktop `, but instead the value of the key ` Name = Link to GitHub `.

- Double-clicking the file opens that URL in a web browser. The behaviour is similar to Windows.

- Despite its name, a .desktop file does not need to be located in ` ~/Desktop/ `. Infact all the "Start Menu" items are actually .desktop files located in ` /usr/share/applications/ `.

2. Graphical file managers (such as Nemo) provide an easy and automatic method of creating another type of shortcut. Holding **` Ctrl + Shift `** while dropping a file will create a [symbolic link](#symbolic-and-hard-links), rather than copying or moving the file. In some distributions a small menu appears whenever a file is dropped, offering a choice of copying, moving or linking the file. [^shotts]

3. In addition, there are so-called [hard links](#symbolic-and-hard-links). It is important to be aware of hard links, because you might encounter them from time to time, even though modern practice prefers symbolic links. [^shotts]

<a id="symbolic-and-hard-links"></a>

## 5.2 Symbolic and hard links [^shotts]

Links (symbolic and hard) are a way to refer to a file on disk. The best understanding of this is that both the contents of the file and a reference to the contents are stored on the disk (i.e. the name of the file), and that there may be several of these references.

> [!NOTE]
> Symbolic and hard links do not work for URLs. Use [.desktop files](#drag-and-drop) for URLs.

Symbolic links were created to overcome the two disadvantages of hard links:
1. Hard links cannot span physical devices i.e. a hard link cannot reference a file outside its own file system. This means a link cannot reference a file that is not on the same disk partition as the link itself.
2. A hard link cannot reference a directory (only a file).

A **hard link** is a reference to the inode number of a file on physical storage. Hard links must be on the same physical partition as the contents of the file itself, because the inode number is unambiguous only within the file system. A file will always have at least one hardlink because the file's name is created by a hardlink. The ` $ ls ` command has a way to reveal this information when invoked with the ` -i ` option.
- When we list a directory containing a hard link we will see no special indication of the link, unless we know what we are looking for (see [Section: Identify a hard link](#identify-a-hard-link)).
- The ` $ rm ` command deletes files, including a hard link. However, data is still accessible as long as another hard link exists; Even if you delete the original file, which is a hardlink itself. To get rid of data you must remove all hard links.
- As there can be several hard links to the same file, the space occupied by the file on the disk is not released until all the hard links to it have been removed.
    - A remove command applied to a hard link also deletes the contents of the file when deleting the last hard link.
    - When one of several hard links is deleted, the link is removed but the contents of the file itself continue to exist (its space is not deallocated) until all links to the file are deleted.

A **symbolic link** can point to any file, including different file systems or a destination that doesn't even exist (this happens if the symbolic link destination is deleted).
- The delete command applied to a symbolic link deletes only the symbolic link file; Never the file to which the link refers.
- Symbolic links contain a text pointer to the target file or directory.
- A symbolic link can be relative, so that it is interpreted in relation to its parent directory.

In most file processing operations, the links are "decompressed" so that the paths through them work normally. One thing to remember about symbolic links is that most file operations are carried out on the link's target, not the link itself. For example, if we write something to the symbolic link, the referenced file is written to. However ` $ rm ` is an exception, and when we delete a symbolic link, only the link is deleted, not the target.
- If the target file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken. In many implementations, the ` $ ls ` command will display broken links in a distinguishing color, such as red, to reveal their presence.

<a id="examples-of-links"></a>

## 5.3 Link examples

### Make links

Create a hard-link: ` $ ln  /path/to/existing_file  /path/to/new_hardlink↵ `

Create or update a symbolic-link: ` $ ln -sf  /path/to/existing_file  /path/to/symlink↵ `

### Identify soft links

Soft links are "easy" to identify using the ` $ ls -li ` command. When you list the file contents of a directory, the soft links are clearly marked using an arrow ` -> ` marker, and it contains the link as well as the path to the referenced file. For example ` $ x-terminal-emulator ` is a symbolic link to a real terminal emulator such as ` $ gnome-terminal `:

```
$ which x-terminal-emulator↵
/usr/bin/x-terminal-emulator

$ ls -li /usr/bin/x-terminal-emulator↵
266302 lrwxrwxrwx 1 root root 14  9. 5. 15:48 /usr/bin/x-terminal-emulator -> gnome-terminal
```

### Identify a hard link

Hard Links are "harder" to identify unless you know what you are looking for. It can still be identified using the ` $ ls -li ` command, where the number between the permissions column and the owner name, indicates the number of hard links to the file.

```
$ ls -li /usr/bin/c++↵
309582 -rwxr-xr-x 4 root root 1076160 21. 5. 23:19 /usr/bin/c++

$ stat /usr/bin/c++↵
  File: /usr/bin/c++
  Size: 1076160   Blocks: 2104     IO Block: 4096   regular file
Device: 259,2     Inode: 309582    Links: 4
Access: (0755/-rwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2024-06-09 06:39:35.340520475 +0300
Modify: 2024-05-21 23:19:21.184657000 +0300
Change: 2024-06-02 10:26:47.650834218 +0300
Birth: 2024-06-02 10:26:47.629834110 +0300
```

### Find all hard links

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

> [!NOTE]
> The hard link count is slightly different in the case of directories, because the unix style file system does not allow hard links on directories. The "hard link count" for a directory is the count of all immediate sub-directories (level 1) plus one for the current directory (the ` ./ ` entry) and one for the parent directory (the ` ../ ` entry).

<!-- # References -->

[^shotts]: [William Shotts - The Linux Command Line, updated 2019](http://linuxcommand.org/tlcl.php)
