<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="08-text-editors.md">&lt;&lt; Previous Chapter: 8 - Text editors</a>
     |
  <a href="10-additional.md">Next&nbsp;Chapter:&nbsp;10&nbsp;&#8209;&nbsp;Appendix&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 9 - Access management

<a id="multiuser-intro"></a>

## 9.1 Introduction to shared computing

<!-- By design Unix and GNU/Linux are multiuser operating systems. The multiuser capability of Linux is not a recent innovation, but rather a feature that is deeply embedded into the design of the operating system. Considering the environment in which Unix was created, this makes perfect sense. -->

Years ago, before computers were personal, they were large, expensive, and centralized. One single computer would support many users at the same time. A typical computer system consisted of a large central computer located in one building, hooked up by terminals located throughout the campus. 
- Even on a home PC the command prompt reflects the unix nature of multiuser capability and remote access capability:

    ```
    user@host working_directory $ _                               
    ```

To make shared use practical, a method had to be devised to protect users from each other. After all, the actions of one user could not be allowed to crash the computer, nor could one user interfere with the files belonging to another user.

To uderstand the Unix security model, one needs to learn the core terminology:
1. An **identity** consists of a **user identity** and one or more **group identities**. Users may belong to a group, and a group consists of one or more users. See [Section: identity](#indentity).
2. The **ownership** of files and directories is determined by the **user-owner** and the **group-owner**. When a user owns a file or directory, he or she controls access to it. The owner can give others access to the files and directories they own. See [Section: Ownerhip of files and directories](#ownership).
3. File and directory **permissions attributes** grant or deny the right to read, write and execute. See [Section: Permissions attributes of files and directories](#permission-attributes). 

<!--1. [**Identity**](#indentity)
    - Constitutes from a **User Identity** and one or more **Group Identities**.
2. [**Ownerhip** of files and directories](#ownership)
    - Is governed by a **User Owner** and a **Group Owner**.
3. [**Permissions attributes** of files and directories](#permission-attributes).
    - Grant or refuse permissions to read, write and/or execute.
    - When a user owns a file or directory, he has control over its access.-->

<!--Users can belong to a group (consisting of one or more users) who are given access to files and directories by their owners.

In addition to granting access to specific group(s), an owner may also grant some set of access rights to everybody, which in Unix terms is referred to as the world or the group of **other**s. It can be considered as a group with all the users on the system. Basically, anyone with access to the system belongs to this group.

> [!NOTE]
> Every single file and directory has the information about who owns it and who has the right to change or read it.-->

<a id="indentity"></a>

## 9.2 Identity (user + group)

- When user accounts are created users are assigned:
    - A numerical **user id (uid)**
    - A numerical primary **group id (gid)**
- All user-id-numbers and group-id-numbers are mapped to textual usernames and groupnames for the sake of the humans.
- Traditionally unix-like systems assigned regular users to a common group such as "users", but modern practice is to create a unique, single-member group with the same name as the user. This makes certain types of permission assignment easier.
- Many GNU/Linux distributions start the numbering of regular user accounts and groups at 1000, and the numbers 000...999 are reserved for system services.
- You do not have nested groups in GNU/Linux (i.e. one group cannot be sub group of another).

> [!TIP]
> To find out information about your identity try:
> ```
> $ groups↵  # to see what groups you belong to.
> $ id↵      # to reveal the user-id and group-id-numbers.
> ```

### More information can be found from text files

Like so many things in GNU/Linux, more information can be found from a couple of text files:
- User database is stored in **` /etc/passwd `**, which defines user accounts by holding information about username, uid number, primary gid number, account name, home directory, and login shell.
- All the groups defined in the system, and any supplementary groups the user may belong to (if any) are stored in **` /etc/group `**.
- User passwords and password expiry information is stored in **` /etc/shadow `**.

> [!NOTE]
> The three files above are all **DSV-format** (Delimiter Separated Values) with colon **` : `** as the value separator. Data files in this style are expected to support inclusion of colons in the data fields by backslash escaping. More generally, code that reads them is expected to support record continuation by ignoring backslash-escaped newlines.

### Shadow password system 

Despite the name ` /etc/passwd `, passwords are stored elsewhere in ` /etc/shadow `. In the old days, decades ago, Unix systems kept user passwords stored, in plain text, in the ` /etc/passwd ` file (hence its name.) This, for very obvious reasons, was not at all good. But there was no simple solution to this as any change to an encrypted password system would break backwards compatibility with the ` /etc/passwd ` file and with any tools that depended on it. [^miller-shadow]


> [!IMPORTANT]
> The solution was to make a new file, the ` /etc/shadow ` file that would "shadow" the ` /etc/passwd ` file and provide a place for a new encrypted password along with some additional password controls (see [Chapter 10, Section: Encrypted password system](10-additional.md#edit-shadow)). [^miller-shadow]

So while having a separate file is a bit bizarre today, it has an historic context that makes sense. No functionality is lost and the additional complexity is nominal. Unlike the ` /etc/passwd ` and ` /etc/group ` files, ` /etc/shadow ` is protected and normal users cannot see its contents. This provides an additional level of security for it. There is no need for users to see what ` /etc/shadow ` contains, but other files are useful to see what accounts are available, groups exists and who are members of them. [^miller-shadow]

> The shadow password system was first introduced in the mid-1980s by Sun's SunOS UNIX system and by 1990 was widely copied and essentially ubiquitous in Unix systems. So the shadow concept is used in most Unix and has been in GNU/Linux since inception. BSD however uses ` /etc/master.passwd ` instead. [^miller-shadow]

[^miller-shadow]: [Scott Miller - The /etc/shadow file in depth, published 2016](http://mangolassi.it/topic/8057/)

### Special user id: root (0)

If we examine the contents of ` /etc/passwd ` and ` /etc/group `, we notice that there is a user **uid 0**, which is required by any unix system. It is the superuser account, and it has all the rights.

Calling the uid 0 account on any unix system root is a very strongly held convention. Though root is just a string, just a name, and in theory the actual username for uid 0 can differ, the OS itself won't care, but some applications might not quite like it because they expect there to exist a privileged account named root.

#### Modern systems have no root password 

Modern GNU/Linux distributions do not have a root password set (by default). Modern systems use the [sudo program](https://www.sudo.ws/about/intro/) to allow (regular) users to run commands as root (see [Section: Sudo program](#sudo-program)). And when the sudo program asks for password authentication, every one supply their own password. After authentication, the system will invoke the requested command as root. Thus no specific root password is needed, which would have to be shared by many users; and thus pose a security risk.

### Change user-identity

The command **` $ su `** stands for Switch User.
- ` $ su margaret↵ ` = Switch user to margaret. Margaret's password is required.
- ` $ su edward↵ ` = Switch user to edward. Edward's password is required.
- ` $ sudo su edward↵ ` = Switch user to edward. Edward's password is not required.
- ` $ sudo su root↵ ` = Switch user to root. Typing root as username is optional, since ` $ sudo su↵ ` does the same thing.
- ` $ exit↵ ` = Log out of another user's account.

> [!IMPORTANT]
> The right to login as another or the root user comes from the rights granted in the ` /etc/sudoers ` file or a configuration file under ` /etc/sudoers.d/ ` directory (see [Section: Editing sudo configuration](#editing-sudo-configuration)). When using ` $ sudo `, no specific root password is asked for; instead every user use their own password.

> [!NOTE]
> By running the ` $ sudo su↵ ` command once will switch the shell to continuous root access. This removes the need to type in ` $ sudo ` repeatedly before commands. Only the ` # exit↵ ` command logs you out of root mode. This may be convenient, but may also increase the risk of causing accidental damage in certain situations.

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

### The sudo program

The regular user does not have write access to a file system other than their own home directory. Maintenance operations, such as updating programs, are performed with the root account via the command ` $ sudo ... ` or ` $ sudo su root↵ `. Such a system is good for data security, as it reduces the possibility of unitended damage and makes misuse more difficult.

> [!NOTE]
> Name of the program: **sudo** stands for *super user do* and originates from the verb *to supervise*, i.e. to be in charge of somebody or something and make sure that everything is done correctly, safely, etc.

#### A better way to grant elevated rights 

In the early 1980's the standard way of executing commands as a superuser was using the ` $ su root↵ ` command, which enables the user to switch to a superuser mode (username root). While this did the trick, it opened a lot of opportunities for human error; it was just too easy to forget you’re in root mode and end up causing inadvertent damage to the system. [^sudo-hist]

Bob Coggeshall and Cliff Spencer thought of a better way working at the SUNY/Buffalo Computer Science at the time. Instead of constantly switching, why not simply create a tool that enables executing individual commands as a superuser, without changing the actual user id in the shell. The ` $ sudo ` command was born an slowly began to make its way into other research groups and was formally open sourced in 1985. Today sudo counts 9944 lines of code (up from 153 lines in the original release) and is maintained by Todd C. Miller. Over 30 years in age, it still continues to receive code contributions and regularly issues new releases. [^sudo-hist]

[^sudo-hist]: [Aleksandar Bradic - Inventing the Unix sudo command, published 2014](https://hackaday.com/2014/05/28/interview-inventing-the-unix-sudo-command/)

#### Normally, even administrators have restricted access

All users, even the administrator who has been given all possible permissions in the configuration file, will normally act as a normal user with limited permissions. When activities such as installing updates or apps, or changing config files arise, the system prompts for the user's password or ask to login as another user who has administrator privileges. Once the elevated activity is completed, one reverts back to working as a standard user with restricted access rights.

There is no specific root password to be shared between users. When sudo prompts for a password authentication, every user supply their own password. After authentication, the system will invoke the requested command as root.

> [!NOTE]
> Even the administrator himself must use ` $ sudo ` to run commands that require elevated privileges.

#### Sudoing rights are configured

The **` $ sudo `** program allows an administrator to set up configuration files under ` /etc/sudoers.d/ ` to define specific commands that particular users are permitted to execute under an assumed identity and elevated privileges. It is the sudo configuration files that grant certain users (or groups of users) the ability to run some commands as root (or another user). This convention allows a system administrator to delegate authority without revealing their own password or a specific root account password. See [Section: Editing sudo configuration](#editing-sudo-configuration).

> [!TIP]
> Use **` $ sudo -l↵ `** to see what privileges are granted by sudo to you specifically.

#### Sudo ticketing system

Sudo comes with a ticketing system, that allows a user to run privileged commands for a period of time without the need to repeatedly authenticate. When a user invokes sudo and enters their password, sudo caches the credentials for 5 minutes, per user, per terminal session. Each subsequent sudo command updates the ticket for another 5 minutes. <!--This timeout is configurable at compile-time only.-->

#### Sudo command history

Sudo may be configured to maintain a log of each command run, so that system administrators can trackback the person responsible for any undesirable changes in the system.

<a id="ownership"></a>

## 9.3 Ownership (of files and directories)

In the unix-like security model, to ensure that a file or directory can be accessed, modified or executed by the intended user(s) only, every file and directory in GNU/Linux have (and is required to have):
1. A user owner, which is a single user.
    - You cannot have 2 users owning the same file.
    - When you create a file, you become the owner of the file.
2. A group owner, which is a single group.
    - You cannot have 2 groups owning the same file.
3. In addition rights can be granted to everybody (group other).
    - Other(s) can be considered as a super group with all the users on the system. Basically, anyone with access to the system belongs to this group.

### Beware when creating files with sudo involved

When creating a file, the current identity becomes the owner of the file.

a) It is clear that root becomes the owner of a file created under the ` # ` prompt, that is after ` $ sudo su root↵ `. The ownership can be changed later on of course.

b) Creating files with sudo may have unexpected results, ending up with files owned by root or a regular user. This is of course just an oversight by the user:
    - With command ` $ sudo echo Aaa > Aaa.txt↵ ` only echo gets run under sudo (i.e. as root), but the redirection to file is run non-privileged (i.e. the user's own user-id). Thus the owner of the newly created file is the common user.
    - To end up with a root owned file, and as echo doesn't need to be run privileged, a better alternative would be ` $ echo Aaa | sudo tee Aaa.txt > /dev/null↵ `. Note how ` /dev/null ` is used here to stop duplicate output to the screen.

> [!NOTE]
> Even under root identity, the ownership of a file doesn't change to root if the file being changed already exists. The original ownership is retained.

### Change ownership (of files and directories)

The **` $ chown `** command stands for Change Ownership (of a file or directory):

` $ chown <user> <filename>↵ `
- Change user-owner.
- Group-owner remains unchanged.

` $ chown :<group> <filename>↵ `
- Change group-owner.
- User-owner remains unchanged.

` $ chown <user>:<group> <filename>↵ `
- Change both user- and group-owners.

` $ chown <user>: <filename>↵ `
- Change both user- and group-owners.
- Group-owner will change to the primary group of the specified user.

> [!NOTE]
> In older versions of Unix, the ` $ chown ` command only changed file ownership (not group ownership). For that purpose, a separate command, ` $ chgrp ` was used. It works much the same way as chown, except for being more limited.

<a id="permission-attributes"></a>

## 9.4 Permission attributes (of files and directories)

The user needs
- Read permission to read from the file.
- Read and write permissions to write to the file. 

The right to delete and rename files is
- Determined by the permissions attributes of the directory.

> [!NOTE]
> Consider a scenario where you have write permission on a file, but do not have write permission on the directory where the file is stored. You will be able to modify the file contents. But you will not be able to rename, move or remove the file from the directory.

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

### Who can change permission attributes?

Only the *user owner* of the file or the root user can change the mode of a file.

1. You must own a file to change its permission attributes i.e. change the mode of a file; mere read and write access to a file is not enough to modify its metadata. The owner of a file may change the group of the file to any group of which that owner is a member. But a privileged process may change the group arbitrarily.

2. Uid 0 i.e. root always has full access to the system and can control the entire system such as files, processes and applications.

3. Group people can not change permission attributes. However write access to the directory containing the file allows you to take the ownership of the file. Assuming that you have read permissions to the file and write permissions to the directory then you can take ownership of a file:

```
$ mv somefile somefile.tmp↵
$ cp somefile.tmp somefile↵
$ rm somefile.tmp↵
```

> [!NOTE]
> If you want security for a file, then the folder (where the file is located) must not have write permission on the owner group. Group people can't chmod, but you also need to deny the add, delete, rename folder permissions; Through which one could otherwise capture file ownership. Note that, denying write permission to a directory does not take away the permission to modify or truncate a file inside the directory, however.

### How to change permission attributes

The **` $ chmod `** command stands for change mode. Use this command to make permission changes to an existing file or directory:

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

### Special permission attributes (setuid, setgid, sticky) 

Though we usually see an octal permission mask expressed as a three digit number, it would be technically more correct to express it in four digits, because (in addition to read, write, and execute permission) there are three other (less used) permission settings. [^shotts-sperm]

#### Special flag: Sticky

The **sticky bit** (octal 1000) is a holdover from ancient Unix, where it was possible to mark an executable file as *not swappable*. On files, modern unix ignores the sticky bit, but if applied to a directory, it prevents users from deleting or renaming files unless the user is either the owner of the directory, the owner of the file, or the superuser. [^shotts-sperm]

> In the original Unix systems, the sticky bit had a different purpose compared to its modern usage. It was introduced in the Fifth Edition of Unix (1974) and was primarily used for executable files. When the sticky bit was set on an executable, it instructed the operating system to keep the program's text segment (code) in swap space after the program finished running. This allowed the program to load faster the next time it was executed, as it avoided reloading the code from slower storage. This feature was particularly useful in systems with limited memory and frequent use of certain programs, like text editors. However, as operating systems evolved and memory management improved, this functionality became obsolete. [^wiki-sticky]

> [!NOTE]
> Today, the sticky bit is used for directories in Unix-like systems, ensuring that only the file owner, directory owner, or root can delete or rename files within a directory. This is often used to control access to a shared directory such as ` /tmp/ ` and ` /var/tmp/ `. 

[^wiki-sticky]: [Wikipedia - Sticky bit, accessed 2025](https://en.wikipedia.org/wiki/Sticky_bit)

#### Special flag: Set group ID 

The **setgid bit** (octal 2000) i.e. *Set Group ID* bit has its origins in early Unix systems and serves different purposes depending on whether it's applied to files or directories. [^shotts-sperm]

> The setgid bit was introduced to allow executables to run with the permissions of the group that owns the file, rather than the group of the user executing it. [^shotts-sperm]

On most systems, when applied to a directory, setgid bit ensures that any files or subdirectories created within inherit the parent directory's group ownership, rather than the creator's default group. Newly created subdirectories also inherit the Set group ID bit of the parent directory. This is useful in a shared directory when members of a common group need access to all the files in the directory, regardless of the file owner's primary group. Lessening the need to use ` $ chmod ` or ` $ chown ` to share new files. [^shotts-sperm]

#### Special flag: Set user ID 

Today, the **setuid bit** (octal 4000) i.e. *Set user ID* bit remains a critical feature in Unix-like systems, but its use is carefully controlled to minimize security risks. Its primary purpose was (and still is) to allow users to execute programs with the privileges of the owner of the executable, rather than the privileges of the user calling it. This was a groundbreaking feature for enabling secure access to system resources. This feature can be used to give restricted, program-controlled access to things like the password file that non-administrators should not be allowed to modify directly. [^shotts-sperm]

> [!NOTE]
> The setuid bit answers the question: How can a low privilege users change their password, when it is stored in a file only accessible by the root user?
>
> ```
> $ ls -la /etc/shadow↵
> -rw------- 1 root root 787 13. 9. 16:05 /etc/shadow
> ```

- The answer is the **setuid concept** through the *Set user ID* bit. A setuid program (such as ` $ passwd `) is run with the program owner’s privilege (without a password). Passwd is just like any other program, except it has that special marking.

> [!TIP]
> You may search for other files with setuid permission by typing ` $ sudo find / -user root -perm -4000 -exec ls -ldb {} \;↵ `. The search results include setuid programs such as ` $ mount ` and ` $ umount `.

Every process has two User IDs: 1) **Real User ID (RUID)** which identifies the real owner of a process. 2) **Effective User ID (EUID)** which identifies the privilege of a process. Access control is based on EUID: [^ieee-euid]

a) When a normal (non setuid) program is executed: RUID and EUID both equal to the ID of the user who runs the program. [^ieee-euid]

b) When a program is executed with the *Set user ID* bit applied to the executable: RUID still equal to the user ID of the user who runs the program. But EUID equals to the owner ID of the executable file. And if the program is owned by root the program runs with the root privilege. [^ieee-euid]

[^ieee-euid]: [IEEE 1003.1 Standard: set user ID, accessed 2025](https://pubs.opengroup.org/onlinepubs/9799919799/functions/setuid.html)

<a id="single-user-mode"></a>

## 9.5 Single User Mode

**Single (user) mode** is a recovery or maintenance mode to gain super user root access without any credentials or password. For this you need to have physical access to the machine. To enter single user mode, temporarily append ` single ` to your boot options:

1. By default, (U)EFI installations will not show the boot menu, and boot directly into the operating system (such as Solus).

    a) By hitting ` Space ` bar (repeatedly) during boot, the boot menu should appear. It may take a couple of goes to get the timing right.
    b) You may wish to configure your operating system to display the boot menu by default (on every startup):

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
                      # is enabled, and answers Yes to any
                      # requests to fix any problems found.
    # mount -uw /↵
    ```

4. Finally you should be able to do what you need to do (such as reset a forgotten user password: ` # passwd margaret↵ `).

> [!WARNING]
> The ability to boot a computer into single user mode could be a major security risk, as it will give intruders immediate root access.

### Protecting against single user mode

Once someone has physical access to a machine, it becomes very hard to completely secure it. The easiest way to gain unauthorised access to a GNU/Linux system is to boot the machine into single user mode (see [Section: Single user mode](#single-user-mode)).
- By default, some distributions do not have a root password set. This can be checked by running the command ` $ sudo head -1 /etc/shadow↵ `. If no root password is set, then regardless of whether, the system is set to prompt for a password for single user mode or not, it will just load root access. This default behaviour can be [changed](https://askubuntu.com/questions/1011368/how-can-i-protect-against-single-user-mode).
- One does also need a [procedure](https://askubuntu.com/questions/76987/how-can-i-prevent-someone-from-resetting-my-password-with-a-live-cd/78051#78051) to protect unauthorised editing of bootloader settings; That is, pressing ` E ` whilst booting, to allow edits to the boot options. Once properly configured, when one tries to edit a boot loader entry, the system will ask for a boot loader specific username and password.
- However, if a "live cd" is used, a "recover linux feature" on the live session can be used to mount the file system and alter the bootloader settings. To protect against such a hack, one should make any removable media have a lower boot priority than the boot drive, and password protect the BIOS and boot option menu, to stop someone who has not got access altering the boot order and booting into a disk to make changes to the system.

> [!IMPORTANT]
> Such security procedures should be used in conjunction with hard-disk encryption.

<a id="remote-use"></a>

## 9.6 Remote use

The term **console** or **terminal** refers to a device connected to a computer (such as a serial cable) that does not itself have the ability to run application programs, but acts as an additional combination of display and input devices (usually a monitor and keyboard) to which system notifications are primarily sent. Terminals flourished before the time of desktop computers, when mainframes were usually used precisely through terminals. Although PCs have almost completely supplanted traditional terminals, the possibility of remote use (ssh program) has been retained in unix-type operating systems.

<!--
- Thus, software running remotely is not installed on the local machine, and remote access to software installed on another workstation also supports graphical user interface programs. Yeas that is right, remote users can execute graphical applications and have the graphical output appear on a remote display. The X Window System supports this as part of its basic design.
-->

### Remote access protocol: SSH

Up until the 1990s, before the general adoption of the internet, there were two popular programs used to log in to remote hosts: telnet in the 1970s and rlogin in the 1980s. These insecure programs used to transmit all their communications (including login names and passwords) in cleartext. This made them wholly inappropriate for use in the internet age. [^shotts-ssh]

<!-- To address this problem, a new protocol called Secure Shell (SSH) was developed. SSH authenticates that the remote host is who it says it is (thus preventing man-in-the-middle attacks) and encrypts all of the communications. [^shotts-ssh] -->

In 1995, Finnish-born Tatu Ylönen developed a new encrypted communication protocol, SSH (Secure Shell), to solve the problem by verifying that the remote host is who it says it is, preventing attacks from intermediaries and encrypting all communications. SSH works on the **TOFU** principle (trust on first use), where the server certificate is accepted the first time and the user is warned if it changes. SSH uses keys, so the user does not necessarily have to enter any passwords at all. SSH client software is now part of the default installation of most Unix like operating systems, and is usually accessible from the command line with ` $ ssh `. [^wiki-fi-ssh]

[^wiki-fi-ssh]: [Wikipedia - SSH, accessed 2025](https://fi.wikipedia.org/wiki/SSH)

<a id="editing-sudo-configuration"></a>

## 9.7 Editing sudo configuration

### The sudo configuration files

To manage sudo's configuration it is possible to 1) edit the primary configuration file ` /etc/sudoers ` or 2) make a new configuration files under the ` /etc/sudoers.d/ ` directory.

The ability to have stand alone files makes it simple for an application to enable sudo capability on installation and remove them when it is uninstalled. Automated configuration tools can also use this capability.

Sudo defines that in case of multiple lines matching for a user, the last one stands. That is any files under ` /etc/sudoers.d/ ` are parsed after ` /etc/sudoers ` file. So potentially a file in ` /etc/sudoers.d/ ` could restrict permissions for someone.

It is recommended to put custom configuration into files in the ` /etc/sudoers.d/ ` directory, because typically ` /etc/sudoers ` is under control of the package manager, and if the package manager wants to upgrade it, one has to manually inspect any local changes and approve how they are merged into the new version. Modifications done directly in the ` /etc/sudoers ` file may even break updates. By placing local changes into a file in the ` /etc/sudoers.d/ ` directory, one garantees that upgrades can proceed automatically. And any changes made to files in ` /etc/sudoers.d ` remain in place if after system upgrade. This can prevent user lockouts when the system is upgraded.

> [!NOTE]
> The following convention for ignoring files applies in ` /etc/sudoers.d/ `: Files ending in a tilde ` ~ ` or containing a dot ` . ` are ignored. This convention allows, for example, backup files to be ignored.

<!-- - Exceptions are files that end with the tilde ` ~ ` character or contain the period ` . ` character. This convention of ignored files is done for the convenience of package managers and also so that backup files from editors are ignored. -->

> [!IMPORTANT]
> Make sure the ` /etc/sudoers ` file contains the line:
>
> ```
> #includedir /etc/sudoers.d
> ```
> Most likely the default ` /etc/sudoers ` file created on installation (of the operating system) includes this directive. However, if not then you must add it yourself. Only then will the sudo program read configuration files from the ` /etc/sudoers.d/ ` directory.

### Format for user privilege specification

```
margaret ALL = (root) NOPASSWD: /usr/bin/eopkg up
   |      |      |      |                |
 Who?   Where?   | Without need to   This command
   |      |      | type a password?
User(s) Host(s)  |
                 |
    Under an assumed identity of (user root)
```

1. The user specifier accepts ` user_names `, ` %group_names ` and ` #uids `.
    - One may specify a single user or group or a list of them separated by ` , `
2. ` ALL ` is a common choice for the host list.
3. The command specifier accepts a path to an executable,
    - Followed by optional allowed arguments such as
        - ` /usr/bin/some-app ` = Any arguments allowed.
        - ` /usr/bin/some-app "" ` = No arguments allowed at all.
        - ` /usr/bin/some-app some-argument ` = Only specific argument allowed.
    - One may specify a single command or several separated by a comma ` , `

### Visudo

A comment ` # This file MUST be edited with the 'visudo' command ` on the ` /etc/sudoers ` file states you should not edit sudoers directly, by opening it in a text editor, but instead edit it with ` $ visudo `, which prevents editing conflicts and checks for syntax errors before saving the modifications to disk. By default, visudo doesn't honor the ` VISUAL ` or ` EDITOR ` environment variables, used by many programs to determine the default text editor. There is a hard-coded list of one or more editors that visudo uses. The default is ` $ vi ` (hence the name visudo).

> [!TIP]
> In reality, you don't have to use the cumbersome ` $ visudo `. You can use a text editor of your choice such as ` $ gedit ` or ` $ ne `. It is possible to wall your self out of the system if the ` /etc/sudoers ` file or any file under ` /etc/sudoers.d/ ` directory is malformed.
>
> Sufficient safety can be achieved by having a second terminal instance running as root ` $ sudo su root↵ `. There is no need for the sudo command once you are logged in as root as indicated by the ` # ` prompt. And any changes can be tested on another terminal instance running as an ordinary user. This way you can verify, that whatever you just did, left sudo running properly. If not, you have the root window to fix it.

<!-- # References -->

[^shotts-sperm]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 9, Section: Some Special Permissions](http://linuxcommand.org/tlcl.php)

[^shotts-ssh]: [<!--William Shotts - -->The Linux Command Line 2024, Chapter: 16, Section: Secure Communication<!-- with Remote Hosts-->](http://linuxcommand.org/tlcl.php)


