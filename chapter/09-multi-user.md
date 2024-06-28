<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="08-text-editors.md">&lt;&lt; Previous Chapter: 8 - Text editors</a>
     |
  <a href="10-additional.md">Next&nbsp;Chapter:&nbsp;10&nbsp;&#8209;&nbsp;Additional&nbsp;hints,&nbsp;tweaks&nbsp;and&nbsp;information&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 9 - Multiuser capability

<a id="multiuser-intro"></a>

## 9.1 Introduction to shared computing

By design Unix and GNU / Linux are multiuser operating systems. The multiuser capability of Linux is not a recent innovation, but rather a feature that is deeply embedded into the design of the operating system. Considering the environment in which Unix was created, this makes perfect sense. Years ago, before computers were personal, they were large, expensive, and centralized. A typical computer system consisted of a large central computer located in one building, hooked up by terminals located throughout the campus. The computer would support many users at the same time. To make this practical, a method had to be devised to protect users from each other. After all, the actions of one user could not be allowed to crash the computer, nor could one user interfere with the files belonging to another user.

> [!NOTE]
> Even the command prompt reflects the multiuser capability and remote access capability:
> ```
> username@machinename current_working_directory $
> root@machinename current_working_directory #
> ```

To uderstand the Unix security model, one needs to learn the core terminology:
1. [**Identity**](#indentity)
    - Constitutes from a **User Identity** and one or more **Group Identities**.
2. [**Ownerhip** of files and directories](#ownership)
    - Is governed by a **User Owner** and a **Group Owner**.
3. [**Permissions attributes** of files and directories](#permission-attributes).
    - Grant or refuse permissions to read, write and/or execute.
    - When a user owns a file or directory, he has control over its access.

Users can belong to a group (consisting of one or more users) who are given access to files and directories by their owners.

In addition to granting access to specific group(s), an owner may also grant some set of access rights to everybody, which in Unix terms is referred to as the world or the group of **other**s. It can be considered as a group with all the users on the system. Basically, anyone with access to the system belongs to this group.

> [!NOTE]
> Every single file and directory has the information about who owns it and who has the right to change or read it.

<a id="indentity"></a>

## 9.2 Identity (user + group)

When user accounts are created users are assigned:
1. A numerical **user id (uid)**
2. A numerical primary **group id (gid)**

> [!NOTE]
> Some distributions (such as Solus) start the numbering of regular user accounts and groups at 1000.
>
> All *user id numbers* and *group id numbers* are mapped to textual usernames and groupnames for the sake of the humans.
>
> You do not have nested groups in GNU / Linux (i.e. one group cannot be sub group of another).

> [!IMPORTANT]
> Traditionally unix-like systems assigned regular users to a common group such as "users", but modern practice is to create a unique, single-member group with the same name as the user. This makes certain types of permission assignment easier.

To find out information about your identity try:
- **` $ groups↵ `** to see what groups you belong to.
- **` $ id↵ `** to reveal the user id and group id numbers.

Like so many things in Linux, more information can be found from a couple of text files:
1. User database is stored in **` /etc/passwd `**, which defines user accounts by holding information about username, uid number, primary gid number, account name, home directory, and login shell.
2. All the groups defined in the system, and any supplementary groups the user may belong to (if any) are stored in **` /etc/group `**.
3. User passwords and password expiry information is stored in **` /etc/shadow `**.

> [!NOTE]
> The three files above are all **DSV-format** (Delimiter Separated Values) with colon **` : `** as the value separator. Data files in this style are expected to support inclusion of colons in the data fields by backslash escaping. More generally, code that reads them is expected to support record continuation by ignoring backslash-escaped newlines.

### Shadow password system [^miller-shadow]

[^miller-shadow]: [Scott Miller - The /etc/shadow file in depth, published 2016](http://mangolassi.it/topic/8057/)

Despite the name ` /etc/passwd `, passwords are stored elsewhere in ` /etc/shadow `. In the old days, decades ago, Unix systems kept user passwords stored, in plain text, in the ` /etc/passwd ` file (hence its name.) This, for very obvious reasons, was not at all good. But there was no simple solution to this as any change to an encrypted password system would break backwards compatibility with the ` /etc/passwd ` file and with any tools that depended on it (see [Chapter 10, Section: Encrypted password system](10-additional.md#edit-shadow)). The solution was to make a new file, the ` /etc/shadow ` file that would "shadow" the ` /etc/passwd ` file and provide a place for a new encrypted password along with some additional password controls. So while having a separate file is a bit bizarre today, it has an historic context that makes sense. No functionality is lost and the additional complexity is nominal. Unlike the ` /etc/passwd ` and ` /etc/group ` files, ` /etc/shadow ` is protected and normal users cannot see its contents. This provides an additional level of security for it. There is no need for users to see what ` /etc/shadow ` contains, but other files are useful to see what accounts are available, groups exists and who are members of them.

> The shadow password system was first introduced in the mid-1980s by Sun's SunOS UNIX system and by 1990 was widely copied and essentially ubiquitous in Unix systems. So the shadow concept is used in most Unix and has been in GNU / Linux since inception. BSD however uses ` /etc/master.passwd ` instead.

### Special user id: root (0)

If we examine the contents of ` /etc/passwd ` and ` /etc/group `, we notice that there is a user "uid 0", which is required by any unix system. It is the superuser account, and it as all the rights. Calling the "uid 0" account on any unix system "root" is a very strongly held convention. Though "root" is just a string, just a name, and in theory the actual username for "uid 0" can differ, the OS itself won't care, but some applications might not quite like it because they expect there to exist a privileged account named "root".

Another interesting note is that by default, modern GNU / Linux distributions do not have a root password set. Modern GNU / Linux use the [sudo program](https://www.sudo.ws/about/intro/) to allow (regular) users to run commands as root (see [Section: Sudo program](#sudo-program)). And when the sudo program asks for password authentication, every one supply their own password. After authentication, the system will invoke the requested command as root. Thus no specific root password is needed, which would have to be shared by many users; And thus pose a security risk.

### Change user-identity

The command **` $ su `** stands for Switch User.
- ` $ su margaret↵ ` = Switch user to margaret
- ` $ su edward↵ ` = Switch user to edward
- ` $ sudo su root↵ ` = Switch user to root
    - Typing root as username is optional ` $ sudo su↵ `.
    - The right to login as the root user comes from the rights granted in the ` /etc/sudoers ` file or a configuration file under ` /etc/sudoers.d/ ` directory.
    - When using ` $ sudo `, no specific root password is asked for; Instead every user use their own password.
    - Type ` # exit↵ ` to log out of root mode.

> [!WARNING]
> By running the ` $ sudo su↵ ` command once will switch the shell to continuous root access. This removes the need to type in ` $ sudo ` repeatedly before commands. This may be convenient, but may also increase the risk of causing accidental damage in certain situations.

> [!TIP]
> Sudo comes with a ticketing system, that allows a user to run privileged commands for a period of time without the need to repeatedly authenticate. When a user invokes sudo and enters their password, they are granted a ticket for 5 minutes. Each subsequent sudo command updates the ticket for another 5 minutes.

<!-- https://sysadminsage.com/linux-list-of-groups/
### Change group-identity = $ newgrp

```
$ sudo groupadd group-3↵   # Create new group
$ usermod -a -G group-1,group-2,group-3 margaret↵ # Add user to groups-1...3
$ sudo groupdel group-3↵   # Delete group-3

$ newgrp group-3↵   # Log in to group-3
$ id -gn↵           # Print current group
$ newgrp↵           # Change back to the original login group

$ groups margaret↵  # View the groups margaret is assigned to
$ id margaret↵      # View the groups margaret is assigned to
$ getent group↵     # View all groups on the system
```
-->

<a id="sudo-program"></a>

### The sudo program <!--update internal links if changed-->

**Sudo** stands for *super user do* and originates from the verb **to supervise**, i.e. to be in charge of somebody or something and make sure that everything is done correctly, safely, etc.

The regular user does not have write access to a file system other than their own home directory. Maintenance operations, such as updating programs, are performed with the root account via the command ` $ sudo ... ` or ` $ sudo su root↵ `. Such a system is good for data security, as it reduces the possibility of unitended damage and makes misuse more difficult.

In Linux, <ins>even the administrators run as a standard user normally</ins>. When activities such as installing updates or apps, or changing config files arise, the system prompts for the user's password or ask to login as another user who has administrator privileges. Once the elevated activity is completed, one reverts back to working as a standard user with restricted access rights.

> In the early 1980's the standard way of executing commands as a superuser was using the ` $ su root↵ ` command, which enables the user to switch to a superuser mode (username root). While this did the trick, it opened a lot of opportunities for human error; It was just too easy to forget you’re in root mode and end up causing inadvertent damage to the system. [^sudo-hist]
>
> Bob Coggeshall and Cliff Spencer thought of a better way working at the SUNY/Buffalo Computer Science at the time. Instead of constantly switching, why not simply create a tool that enables executing individual commands as a superuser, without changing the actual user id in the shell. The ` $ sudo ` command was born an slowly began to make its way into other research groups and was formally open sourced in 1985. Today sudo counts 9944 lines of code (up from 153 lines in the original release) and is maintained by Todd C. Miller. Over 30 years in age, it still continues to receive code contributions and regularly issues new releases. [^sudo-hist]

[^sudo-hist]: [Aleksandar Bradic - Inventing the Unix sudo command, published 2014](https://hackaday.com/2014/05/28/interview-inventing-the-unix-sudo-command/)

The **` $ sudo `** program allows an administrator to set up configuration files under ` /etc/sudoers.d/ ` to define specific commands that particular users are permitted to execute under an assumed identity and elevated privileges. Even the administrator himself must use ` $ sudo ` to run commands that require elevated privileges.

There is no specific root password to be shared between users. When sudo prompts for a password authentication, every user supply their own password. After authentication, the system will invoke the requested command as root.

This convention allows a system administrator to delegate authority without revealing their own password or a specific root account password. It is the sudo configuration files that grant certain users (or groups of users) the ability to run some commands as root (or another user). Use **` $ sudo -l↵ `** to see what privileges are granted by sudo to you specifically.

Sudo comes with a ticketing system, that allows a user to run privileged commands for a period of time without the need to repeatedly authenticate. When a user invokes sudo and enters their password, sudo caches the credentials for 5 minutes, per user, per terminal session. Each subsequent sudo command updates the ticket for another 5 minutes. This timeout is configurable at compile-time only.

Sudo may be configured to maintain a log of each command run, so that system administrators can trackback the person responsible for any undesirable changes in the system.

<a id="ownership"></a>

## 9.3 Ownership (of files and directories)

In the unix-like security model, to ensure that a file or directory can be accessed, modified or executed by the intended user(s) only, every file and directory in GNU / Linux have (and is required to have):
1. A user owner, which is a single user.
    - You cannot have 2 users owning the same file.
    - When you create a file, you become the owner of the file.
2. A group owner, which is a single group.
    - You cannot have 2 groups owning the same file.
3. In addition rights can be granted to everybody (group other).
    - Other(s) can be considered as a super group with all the users on the system. Basically, anyone with access to the system belongs to this group.

### Beware when creating files with sudo involved

When creating a file, the current identity becomes the owner of the file.
- a) It is clear that root becomes the owner of a file created under the # prompt (that is after ` $ sudo su root↵ `). (The ownership can be changed later on of course.)
- b) Creating files with sudo may have unexpected results, ending up with files owned by root or a regular user. This is of course just an oversight by the user:
    - With command ` $ sudo echo Aaa > Aaa.txt↵ ` only echo gets run under sudo (i.e. as root), but the redirection to file is run non-privileged (i.e. the user's own user-id). Thus the owner of the newly created file is the common user.
    - To end up with a root owned file, and as echo doesn't need to be run privileged, a better alternative would be ` $ echo Aaa | sudo tee Aaa.txt > /dev/null↵ `. Note how ` /dev/null ` is used here to stop duplicate output to the screen.

> [!NOTE]
> Even under root identity, the ownership of a file doesn't change to root if the file being changed already exists. The original ownership is retained.

### Change ownership (of files and directories)

The **` $ chown `** command stands for Change Ownership (of a file or directory):

` $ chown <user> <filename>↵ ` <br>= Change user-owner. Group-owner remains unchanged.

` $ chown :<group> <filename>↵ ` <br>= Change group-owner. User-owner remains unchanged.

` $ chown <user>:<group> <filename>↵ ` <br>= Change both user- and group-owners.

` $ chown <user>: <filename>↵ ` <br>= Change both user- and group-owners. Group-owner will change to the primary group of the specified user.

> [!NOTE]
> In older versions of Unix, the ` $ chown ` command only changed file ownership (not group ownership). For that purpose, a separate command, ` $ chgrp ` was used. It works much the same way as chown, except for being more limited.

<a id="permission-attributes"></a>

## 9.4 Permission attributes (of files and directories)

| SymBinOct | Permission on a FILE | Permission on a DIRECTORY |
|:--- |:--- |:--- |
| `--- 000 0` | Denied from opening the file. | Denied from listing files stored in the directory. |
| `--x 001 1` | \<unfit\> | \<unfit\> |
| `-w- 010 2` | \<unfit\> | \<unfit\> |
| `-wx 011 3` | \<unfit\> | \<unfit\> |
| `r-- 100 4` | Authorised to open the file. | Restricted authority to list only names of files stored in the directory. |
| `r-x 101 5` | Authorised to open or execute the file. | Authorised to list files stored in the directory including file properties (such as permissions, dates and file size). |
| `rw- 110 6` | Authorised to open and modify the file. **This is the base permission for files.** | \<unfit\> |
| `rwx 111 7` | Authorised to open, modify and execute the file. | Authorised to add, remove and rename files stored in the directory. **This is the base permission for directories.** |

> [!NOTE]
> The ability to delete and rename files is determined by directory attributes. Consider a scenario where you have write permission on a file, but do not have write permission on the directory where the file is stored. You will be able to modify the file contents. But you will not be able to rename, move or remove the file from the directory.

### Who can change permission attributes?

You need the read permission to read from a file, and the write permission to write to a file; But <ins>you need to own a file to modify its metadata</ins>. Only the *user owner* of the file or "uid 0" i.e. the root user can change the mode of a file.

"Group people" can not change permission attributes. However write access to the directory containing the file allows you to take the ownership of the file. Assuming that you have read permissions to the file and write permissions to the directory then you can take ownership of a file:

```
$ mv tiedosto tiedosto.tmp↵
$ cp tiedosto.tmp tiedosto↵
$ rm tiedosto.tmp↵
```

If you want security for a file, then the folder (where the file is located) must not have write permission on the owner group. Group people can't chmod, but you also need to deny the add, delete, rename folder permissions; Through which one could otherwise capture file ownership. Note that, denying write permission to a directory does not take away the permission to modify or truncate a file inside the directory, however.

The owner of a file may change the group of the file to any group of which that owner is a member. But a privileged process may change the group arbitrarily. "Uid 0" i.e. root always has full access to the system and can control the entire GNU / Linux including files, processes, applications, etc.

### How to change permission attributes

The ` $ chmod ` command stands for change mode. Use this command to make permission changes to an existing file or directory:

```
           + add
           - remove
           = set
           ↓
  $ chmod ??? <path>↵
         ↗   ↖
   u user     x execute
   g group    w write
   o other    r read (or any combination of these such as rwx)
   a all
   (or any combination of these such as ugo)
```

### Special permission attributes (setuid, setgid, sticky) [^shotts]

Though we usually see an octal permission mask expressed as a three digit number, it would be technically more correct to express it in four digits, because (in addition to read, write, and execute permission) there are three other (less used) permission settings.

#### Sticky bit [^shotts]

The **Sticky bit** (octal 1000) is a holdover from ancient Unix, where it was possible to mark an executable file as "not swappable". On files, modern unix ignores the sticky bit, but if applied to a directory, it prevents users from deleting or renaming files unless the user is either the owner of the directory, the owner of the file, or the superuser. This is often used to control access to a shared directory such as ` /var/tmp/ `.

#### Set group ID [^shotts]

On most systems, if the **Set group ID** bit (or setgid bit = octal 2000) is set on a directory:
- Newly created files in the directory will be given the group ownership of the directory rather the group ownership of the file's creator.
- Newly created subdirectories inherit the Set group ID bit of the parent directory.

This is useful in a shared directory when members of a common group need access to all the files in the directory, regardless of the file owner's primary group. Lessening the need to use ` $ chmod ` or ` $ chown ` to share new files.

#### Set user ID [^shotts]

The third less-used setting is the **Set user ID** bit (or setuid bit = octal 4000).

A **setuid program** runs not with the privileges of the user calling it, but with the privileges of the owner of the executable. This feature can be used to give restricted, program-controlled access to things like the password file that non-administrators should not be allowed to modify directly.
- The setuid bit answers the question: How can a low privilege users change their password, when it is stored in a file only accessible by the root user?
```
$ ls -la /etc/shadow↵
-rw------- 1 root root 787 13. 9. 16:05 /etc/shadow
```

- The answer is the **setuid concept** through the *Set user ID* bit. A setuid program (such as ` $ passwd `) is run with the program owner’s privilege (without a password). Just like any other program, except it has that special marking. You may search for other files with setuid permission by typing ` $ sudo find / -user root -perm -4000 -exec ls -ldb {} \;↵ `. The search results include ` $ mount ` and ` $ umount `.

Every process has two User IDs: 1) **Real User ID (RUID)** which identifies the real owner of a process. 2) **Effective User ID (EUID)** which identifies the privilege of a process. Access control is based on EUID:
- a) When a normal (non setuid) program is executed: RUID and EUID both equal to the ID of the user who runs the program.
- b) When a program is executed with the *Set user ID* bit applied to the executable: RUID still equal to the user ID of the user who runs the program. But EUID equals to the owner ID of the executable file. And if the program is owned by root the program runs with the root privilege.

<a id="single-user-mode"></a>

## 9.5 Single User Mode

Single (user) mode is a recovery or maintenance mode to gain super user root access without any credentials or password. For this you need to have physical access to the machine. To enter single user mode, temporarily append ` single ` to your boot options:

1. By default, (U)EFI installations will not show the boot menu, and boot directly into the operating system (such as Solus).
    - a) By hitting ` Space ` bar (repeatedly) during boot, the boot menu should appear. It may take a couple of goes to get the timing right.
    - b) You may wish to configure your operating system to display the boot menu by default (on every startup):

```
$ sudo clr-boot-manager set-timeout 30↵
$ sudo clr-boot-manager update↵
# These are for (U)EFI only,
# not GRUB / legacy-BIOS.
```

2. Once in the boot menu (UEFI or GRUB) highlight the desired kernel and press ` E ` key. Find a good spot to append ` single ` (such as rigth next to ` quiet `). Finally press the ` Enter ` key on UEFI or ` F10 ` on GRUB / legacy-BIOS.

> [!NOTE]
> These changes to boot parameters are not persistent. Any change to the kernel boot options made this way will only affect the current boot.

3. When you get to the shell prompt in single user mode, the hard drive is propably mounted read only. The recommended method is to run file system check to ensure nothing is corrupted. ). Then remount to enable write.

```
# fsck -fy↵       # Force a check even if journalling
                  # is enabled , and answers Yes to any
                  # requests to fix any problems found.
# mount -uw /↵
```

4. Finally you should be able to do what you need to do (such as reset a forgotten user password: ` # passwd margaret↵ `).

> [!WARNING]
> The ability to boot a computer into single user mode could be a major security risk, as it will give intruders immediate root access.

### Protecting against single user mode

Once someone has physical access to a machine, it becomes very hard to completely secure it. The easiest way to gain unauthorised access to a GNU / Linux system is to boot the machine into single user mode (see [Section: Single user mode](#single-user-mode)).
- By default, some distributions do not have a root password set. This can be checked by running the command ` $ sudo head -1 /etc/shadow↵ `. If no root password is set, then regardless of whether, the system is set to prompt for a password for single user mode or not, it will just load root access. This default behaviour can be [changed](https://askubuntu.com/questions/1011368/how-can-i-protect-against-single-user-mode).
- One does also need a [procedure](https://askubuntu.com/questions/76987/how-can-i-prevent-someone-from-resetting-my-password-with-a-live-cd/78051#78051) to protect unauthorised editing of bootloader settings; That is, pressing ` E ` whilst booting, to allow edits to the boot options. Once properly configured, when one tries to edit a boot loader entry, the system will ask for a boot loader specific username and password.
- However, if a "live cd" is used, a "recover linux feature" on the live session can be used to mount the file system and alter the bootloader settings. To protect against such a hack, one should make any removable media have a lower boot priority than the boot drive, and password protect the BIOS and boot option menu, to stop someone who hasn’t got access altering the boot order and booting into a disk to make changes to the system.

> [!IMPORTANT]
> Such security procedures should be used in conjunction with hard-disk encryption.

<a id="remote-use"></a>

## 9.6 Remote use

The term **terminal** or **console** refers to a device connected to a computer (such as a serial cable) that does not itself have the ability to run application programs, but acts as an additional combination of display and input devices (usually a monitor and keyboard) to which system notifications are primarily sent. Terminals flourished before the time of desktop computers, when mainframes were usually used precisely through terminals. Although PCs have almost completely supplanted traditional terminals, the possibility of remote use (ssh program) has been retained in unix-type operating systems.

<!--
- Thus, software running remotely is not installed on the local machine, and remote access to software installed on another workstation also supports graphical user interface programs. Yeas that is right, remote users can execute graphical applications and have the graphical output appear on a remote display. The X Window System supports this as part of its basic design.
-->

### SSH

For many years, unix-like operating systems have had the ability to be administered remotely. In the early days, before the general adoption of the internet, there were a couple of popular programs used to log in to remote hosts. These were the rlogin and telnet programs. These insecure programs used to transmit all their communications (including login names and passwords) in cleartext. This made them wholly inappropriate for use in the internet age. To address this problem, a new protocol called Secure Shell (SSH) was developed. SSH authenticates that the remote host is who it says it is (thus preventing man-in-the-middle attacks) and encrypts all of the communications. [^shotts]

<!-- # References -->

[^shotts]: [William Shotts - The Linux Command Line, updated 2019](http://linuxcommand.org/tlcl.php)
