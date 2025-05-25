<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="09-multi-user.md">&lt;&lt; Previous Chapter: 9 - Access management</a>
     |
  <a href="../README.md">Back&nbsp;to&nbsp;cover&nbsp;page&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 10 - Appendix

<a id="installing-gnu-linux"></a>

## 10.1 Installing GNU/Linux

A GNU/Linux distribution (or several of them) can be installed in place of, or alongside Microsoft Windows and Apple macOS. You can have multiple operating systems installed on one computer. This setup is often referred to as dual-booting or multi-booting. With multiple operating systems installed, you will typically see a boot menu when you start your computer. This menu allows you to choose which operating system to boot into.

Installation of a GNU/Linux typically starts with the creation of a bootable USB drive, but most distributions can be run directly from such bootable USB drives without installing (onto the computer's internal storage drive). This allows users to try out GNU/Linux and it's various distributions without making any changes to their existing system. It’s a way to experiment, recover data from a broken system, or have a portable operating system that one can use on different machines.

### Create a bootable USB drive 

Creating a bootable USB drive is not trivial, and requires installing a boot drive creation utility such as [Rufus](https://rufus.ie/en/), [Balena Etcher](https://etcher.balena.io) or [Ventoy](https://www.ventoy.net/). In addition, you must download the correct ISO file from the official website of the distribution you want to (see [Chapter 1, Section: Suggested Distributions](01-intro.md#suggested-distributions)). The ISO file must be copied to a USB drive in a way that makes it bootable, using afore mentioned software.

### Boot from a USB drive 

Booting a computer from a USB drive may not trivial, as it usually requires changing some UEFI/BIOS system settings. Some GNU/Linux distributions cannot be installed unless the Secure Boot feature is disabled. Installation continues by changing the boot order to favor USB before the computer's internal boot drive. [^koodikanava]

The UEFI/BIOS settings can usually be accessed by pressing a hardware-specific key such as Del, Esc, F2, F10, F12 during boot-up. Ease of access to system settings also depends on the existing UEFI/BIOS settings. You may have the post boot delay time set to zero, during which pressing the hardware-specific key proves impossible - In which case you will never get in. [^koodikanava]

You can try to instruct an already running computer to boot into UEFI/BIOS from: [^koodikanava]
- The Windows command line ` Win + R ` + ` cmd.exe↵ `:
    - With the command ` shutdown /r /fw↵ `
- A GNU/Linux terminal:
    - With the command ` $ sudo systemctl reboot --firmware-setup↵ `

[^koodikanava]: [Koodi Kanava, Kimmo Kujansuu - Helpolla komennolla pääset biosiin, accessed 2025](https://www.youtube.com/watch?v=YbKrDbHRsTg)

<a id="disk-partitioning"></a>

### Disk partitioning in live mode

After a successful boot with the USB drive, you should arrive to a graphical user interface of the GNU/Linux operating system referred to as a live session. Live mode session is almost like a fully functioning instance of the operating system. In live mode, you have access to most of the features and applications as if you had installed it on your internal storage drive. Follow the on-screen prompts to begin the installation process. If not prompted, installation continues by finding the installer. Most live sessions have an "Install" icon on the desktop for this. Progressing from here requires some understanding of disk partitioning.

> [!WARNING]
> When partitioning a storage disk for GNU/Linux, it is strongly encouraged to expand the (U)EFI FAT32 boot partition to at least 500 MB. The 100 MB created by Windows will most likely prove too low in the long run. Problems may occur when the Linux kernel is updated. Everything may seem to work, but the Linux kernel, doesn't update, and you might not even get an error message about it.

**EXT4** (Fourth Extended Filesystem) is a good choice and the default filesystem for most GNU/Linux distributions. More advanced users may prefer the BTRFS (B-Tree File System) for its additional features such as snapshots - However BTRFS is slower than EXT4 especially when dealing with large data writes.

**exFAT** (Extensible File Allocation Table) and **NTFS** (New Technology File System) are good file system alternatives for partitions to be shared between different operating systems such as GNU/Linux and Microsoft Windows. Of these, exFAT is the most straightforward and the best performing. NTFS is the default file system for the Windows operating system, but Windows-level NTFS performance is currently not achievable in GNU/Linux.

#### Need for swap has decreased

The complex disk partitioning traditionally used in GNU/Linux (even single-disk configurations) is no longer necessary on today's home computers; And it has little use in home use today. If the disk system is partitioned the old style and runs out of space, then in the worst case, the machine may even crash.

> The first function created for Linux at the request of an outsider was the ability to extend main memory with **swap memory**, completed on Christmas Day 1991. Torvalds ’own 386 machine (which was assembled from parts, unbranded) had four megabytes of memory, but users with a smaller number (especially one German user who originally made the request) were in trouble with the lack of main memory. This feature was significant in early 1992 because it played a major role in system performance and contributed positively to the Linux kernel.

In Linux, the swap space has traditionally been located on a separate hard disk partition with its own file system optimized for swap use. The speed advantage achieved in this way is now so marginal that the same can be done well by taking the space available for virtual memory from a standard disk partition.

In addition, the need for swaps has decreased or even disappeared as the amount of main memory increased. At the same time, the opposite of swap is common, in which files in mass memory, which are often needed, are copied to main memory to speed up their reading (see [Chapter 2, Section: RAM-disk](02-basic.md#ram-disk)).

> [!TIP]
> Partitions can be resized, moved, deleted and created with `$ gparted ` in GNU/Linux and with ` diskmgmt.exe ` in Microsoft Windows (` Win + X ` + Disk Management).

<a id="terminal-stuff"></a>

## 10.2 Additional tips with the terminal

### Suspend to RAM

` $ systemctl suspend↵ ` = Suspend to RAM. Works by cutting off power to most parts of the machine aside from the RAM, which is required to restore the machine's state. Because of the large power savings, it is advisable for laptops to automatically enter this mode when the computer is running on batteries and the lid is closed (or the user is inactive for some time).

### Boot time

There is a command to find out how long it took to boot your GNU/Linux system:
```
$ systemd-analyze↵
Startup finished in 8.299s (firmware) + 3.081s (loader) + 1.794s (kernel) + 2.202s (initrd) + 6.983s (userspace) = 22.362s 
```

> [!TIP]
> Append the ` blame ` flag for additional details.

<!--### Screen brightness

` $ sudo light -S 30.0 -s sysfs/backlight/auto↵ ` = Decreases the screen brightness. The figure is a percentage 00.0...100.0-->

### Analyze disk space usage

The following command will display how much space is being used by folders under the root ` / ` directory:

```
$ sudo du -hsx /* | sort -rh | head -n 40↵
14G    /usr
5,4G   /home
1,4G   /var
1,3G   /lib64
96M    /root
18M    /etc
11M    /run
280K   /tmp
16K    /lost+found
4,0K   /srv
4,0K   /mnt
4,0K   /media
4,0K   /boot
0      /sys
0      /sbin
0      /proc
0      /lib
0      /dev
0      /bin
```

<a id="desktop-stuff"></a>

## 10.3 Additional tips for the desktop interface

### Launching desktop applications from the commandline

Sometimes, a program will fail to start up when launched from the graphical menu. By launching it from the command line instead, we may see an error message that will reveal the problem. Also, some graphical programs have interesting and useful command line options.

Graphical dekstop environments tend to hide the file names of programs. One way to find out the file names of executables is to browse the ["Start Menu"](https://www.freedesktop.org/wiki/Specifications/menu-spec/) [shorcuts folder](05-links.md#drag-and-drop) at ` /usr/share/applications/ ` with a file manager, right click a shortcut file and choose open with text editor. Search for the line that begins with ` Exec= ` to find out the information you are looking for.

### Keyboard shortcuts

Hold ` Alt + Tab ` repeatedly = Cycle through open windows.

` Alt + F2 ` = Run a Quick Command (instead of opening a terminal). Works also as a calculator in some distributions - But not Solus.
    
#### Virtual desktops

` Ctrl + Alt + Right ` = Open the next virtual desktop.

` Ctrl + Alt + Left ` = Return to the previous virtual desktop.

#### Zoom

- In = ` Ctrl + [+] `
- Out = ` Ctrl + [-] `
- Reset = ` Ctrl + 0 `

> [!NOTE]
> The signs ` + `, ` - ` and ` 0 ` must be pressed next to the letter keys. The corresponding characters on the numeric keypad do not work with the default settings.

<a id="edit-shadow"></a>

## 10.4 Encrypted password system

Any computer system that requires password authentication must contain a database of passwords in some form. Because password databases are vulnerable to theft, storing passwords in plaintext is dangerous. Therefore most databases store only cryptographic hashes of the user's passwords.

### Hashing 

<!-- Password cryptography uses hashing to confirm data is unchanged (integrity). -->

Passwords stored in the ` /etc/shadow ` file are actually hashes. Even the authentication system can't determine what a user's password is by merely looking at the stored value. Instead authentication is determined, without ever actually decrypting the stored password on the system. [^hashing]

When a user enters a password for authentication, the system computes the hash value for the provided password, and that hash value is compared to the stored hash for that user. Authentication is successful if the two hashes match. [^hashing]

**Hashing** is a one-way process. The hashed result cannot be reversed to expose the original data. The checksum is a string of output that is a set size. Technically, this means that hashing is not encryption because encryption is intended to be reversed (decrypted). [^hashing]

The purpose of password hashing is not to protect the system from being breached, but to protect the passwords if a breach does occur. If a password database gets hacked, and the passwords are unprotected, then malicious hackers can use those passwords to compromise users' accounts on other services, as most people use the same password everywhere. [^hashing]

Cryptography has three goals: [^hashing]
1. **Authenticity** = to prove where a file originated.
2. **Integrity** = to prove that a file has not changed unexpectedly.
3. **Confidentiality** = to keep the file content from being read by unauthorized users.

In GNU/Linux, you're likely to interact with one of two hashing methods:
1. **SHA-512** (secure hash algorithm) is suitable for cryptographic purposes such as password hashing, digital signatures and TLS/SSL certificate generation.
2. **MD5** (message digest algorithm) can be used as a checksum to verify data integrity against unintentional corruption. Historically it was widely used as a cryptographic hash function, however it has been found to suffer from extensive vulnerabilities. It remains suitable for other non-cryptographic purposes. MD5 is still widely used for non-cryptographic tasks such as verifying the integrity of data files (e.g., comparing checksums for downloads), identifying duplicate files, as the hash values can quickly match identical content.
    - Non-cryptographic [XXH64](https://github.com/Cyan4973/xxHash) hash function is a modern alternative for MD5, and is designed for speed and efficiency.

[^hashing]: [Taylor Hornby - How to Hash Passwords (The Right Way), accessed 2021](https://crackstation.net/hashing-security.htm)

### Salting 

> [!IMPORTANT]
> Hackers can crack plain hashes very quickly using lookup tables and rainbow tables. Randomizing the hashing using salt is the solution to the problem. And thus hashes in typical GNU/Linux are salted. [^hashing]

Salting is an extra step during hashing that adds an additional value to the end of the password, thereby changing the hash value produced. Salting can drastically reduce the chances of an attacker cracking passwords. The premise of salting is to protect and prevent precomputed hash attacks. Even though salts are stored in a database beside the hashes, salting adds another barrier for attackers, essentially complicating the password cracking process. This is useful when users have repeated passwords across multiple applications. The time taken for an attacker to execute a successful cracking is drastically increased with salted hashes. [^hashing]

**Salting** randomizes each hash, so that when the same password is hashed twice, the hashes are not the same. We can randomize the hashes by appending or prepending a random string, called a salt, to the password before hashing. This makes the same password hash into a completely different string every time. To check if a password is correct, we need the salt, so it is usually stored in the user account database along with the hash, or as part of the hash string itself. The salt does not need to be secret. Just by randomizing the hashes, lookup tables, reverse lookup tables, and rainbow tables become ineffective. An attacker won't know in advance what the salt will be, so they can't pre-compute a lookup table or rainbow table. If each user's password is hashed with a different salt, the reverse lookup table attack won't work either. [^hashing]

- The salt should be stored in the user account table alongside the hash. [^hashing]
    - The salt does not need to be secret. [^hashing]
- The salt needs to be unique per-user per-password. Never reuse a salt. [^hashing]
    - A new random salt must be generated each time a user creates an account or changes their password. [^hashing]
    - Every time a user creates an account or changes their password, the password should be hashed using a new random salt. [^hashing]
- The salt also needs to be long, so that there are many possible salts. [^hashing]
    - As a rule of thumb, make your salt is at least as long as the hash function's output. [^hashing]
- Should the salt come before or after the password?
    - It doesn't matter, but pick one and stick with it for interoperability's sake. [^hashing]
    - Having the salt come before the password seems to be more common. [^hashing]
- If you are writing a web application, you might wonder where to hash?
    - In a Web Application, always hash on the server. [^hashing]
    - The password should be sent to the server "in the clear" and hashed there, or you can hash twice: once on the client side and then rehash the hash on the server side. [^hashing]
    - If passwords are hashed only in the user's browser with JavaScript the client-side hash logically becomes the user's password. If a bad guy somehow steals the database of hashes from this hypothetical website, they'll have immediate access to everyone's accounts without having to guess any passwords. [^hashing]
- One goal is to make the hash function slow enough to impede attacks, but still fast enough to not cause a noticeable delay for the user. Use a standard algorithm like PBKDF2 or bcrypt. These algorithms take a security factor or iteration count as an argument (this value determines how slow the hash function will be). [^hashing]
- Compares hash strings in a way that takes the same amount of time no matter how much of the strings match (to protect against a timing attack). [^hashing]

### Howto hand edit /etc/shadow

If you want to create a hash same way ` /etc/shadow ` stores it:
1. First check the first two characters of the second field for your user account in ` /etc/shadow `:
    - If the two characters are $1, your password is encrypted with MD5.
    - If the two characters are $5, your password is encrypted with SHA256.
    - If the two characters are $6, your password is encrypted with SHA512.
2. Then use commands like:

```
$ openssl passwd -6 -salt PPfs6aO9wVajlGSb↵
Password:  my_poor_password↵

$ mkpasswd --method=sha-512 --salt=PPfs6aO9wVajlGSb↵
Password:  my_poor_password↵
```

> [!NOTE]
> The ` $ mkpasswd ` utility is part of the ` whois ` package. So you will need to install that first.

> [!WARNING]
> If you modified the above examples by using redirection to give the password, then make sure you don't leave your password in plain text inside ` ~/.bash_history `
