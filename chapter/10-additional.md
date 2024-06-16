<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="09-multi-user.md">&lt;&lt; Previous Chapter: 9 - Multiuser capability</a>
     |
  <a href="../README.md">Back&nbsp;to&nbsp;cover&nbsp;page&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 10 - Additional hints, tweaks and information

<a id="terminal-stuff"></a>

## 10.1 Terminal related

` $ systemctl suspend↵ ` = Suspend to RAM. Works by cutting off power to most parts of the machine aside from the RAM, which is required to restore the machine's state. Because of the large power savings, it is advisable for laptops to automatically enter this mode when the computer is running on batteries and the lid is closed (or the user is inactive for some time).

` $ systemd-analyze↵ ` = Display the system boot up time to find out how long does it take to boot your GNU / Linux system. Append the ` blame ` flag for additional details.

` $ sudo light -S 30.0 -s sysfs/backlight/auto↵ ` = Decreases the screen brightness. The figure is a percentage 00.0...100.0

Many terminal commands will print a message only if something goes wrong. Often times as you insert a command and hit enter, the command gets executed but you do not see a result. The copy command ` $ cp `will overwrite existing files silently. The ` $ rm ` command removes files from the system without confirmation. This is because the unix shell is unobtrusive and silent by design (see [Chapter 2, Section: Design tropes of unix shell utilities](02-basic.md#design-tropes-of-unix)). By default most commands will not print confirmation messages upon success. However, many commands accept the ` -v ` parameter to change this behaviour (v is hort for verbose):

```
$ mkdir -v Aaaa
mkdir: created directory 'Aaaa'

$ rmdir -v Aaaa
rmdir: removing directory, 'Aaaa'
```

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

## 10.2 Desktop related

### Program file names

Sometimes, a program will fail to start up when launched from the graphical menu. By launching it from the command line instead, we may see an error message that will reveal the problem. Also, some graphical programs have interesting and useful command line options.

Graphical dekstop environments tend to hide the file names of programs. One way to find out the file names of executables is to browse the *"Start Menu" shorcuts folder* at ` /usr/share/applications/ ` with a file manager, right click a shortcut file and choose open with text editor. Search for the line that begins with "Exec=" to find out the information you are looking for.

### Keyboard shortcuts

- Hold ` Alt + Tab ` repeatedly = Cycle through open windows.
- ` Ctrl + Alt + Right ` = Open the next virtual desktop.
- ` Ctrl + Alt + Left ` = Return to the previous virtual desktop.
- ` Alt + F2 ` = Run a Quick Command (instead of opening a terminal).
    - Works also as a calculator in some distributions - But not Solus.
- Zoom
    - In = ` Ctrl + [+] `
    - Out = ` Ctrl + [-] `
    - Reset = ` Ctrl + 0 `

> [!NOTE]
> The signs ` + `, ` - ` and ` 0 ` must be pressed next to the letter keys. The corresponding characters on the numeric keypad do not work with the default settings.

<a id="edit-sudoers"></a>

## 10.3 Editing sudo configuration

### The sudo configuration files

To manage the *sudo's configuration file(s)* or *the sudoers file(s)* it is possible to a) edit the primary configuration file ` /etc/sudoers ` or b) make a new configuration file under the ` /etc/sudoers.d/ ` directory.

> It is recommended to put custom configuration into files in the ` /etc/sudoers.d/ ` directory, because typically ` /etc/sudoers ` is under control of the package manager, and if the package manager wants to upgrade it, one has to manually inspect any local changes and approve how they are merged into the new version. Modifications done directly in the ` /etc/sudoers ` file may even break updates. By placing local changes into a file in the ` /etc/sudoers.d/ ` directory, one garantees that upgrades can proceed automatically. And any changes made to files in ` /etc/sudoers.d ` remain in place if after system upgrade. This can prevent user lockouts when the system is upgraded. The ability to have stand alone files makes it simple for an application to enable sudo capability on installation and remove them when it is uninstalled. Automated configuration tools can also use this capability.
- Exceptions are files that end with the tilde ` ~ ` character or contain the period ` . ` character. This convention of ignored files is done for the convenience of package managers and also so that backup files from editors are ignored.
- Sudo defines that in case of multiple lines matching for a user, the last one stands. That is any files under ` /etc/sudoers.d/ ` are parsed after ` /etc/sudoers ` file. So potentially a file in ` /etc/sudoers.d/ ` could restrict permissions for someone.

> [!IMPORTANT]
> Make sure the /etc/sudoers file contains the line:
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

1. The **user specifier** accepts ` user_names `, ` %group_names ` and ` #uids `.
    - One may specify a single user or group or a list of them separated by a comma ` , `
2. ` ALL ` is a common choice for the **host list**.
3. The **command specifier** accepts a path to an executable,
    - Followed by optional allowed arguments such as
        - ` /usr/bin/some-app ` = Any arguments allowed.
        - ` /usr/bin/some-app "" ` = No arguments allowed at all.
        - ` /usr/bin/some-app some-argument ` = Only "some-argument" allowed as argument.
    - One may specify a single command or several separated by a comma ` , `

### Safety

A comment ` # This file MUST be edited with the 'visudo' command ` on the ` /etc/sudoers ` file states you should not edit sudoers directly, by opening it in a text editor, but instead edit it with ` $ visudo `, which prevents editing conflicts and checks for syntax errors before saving the modifications to disk. By default, visudo doesn't honor the ` VISUAL ` or ` EDITOR ` environment variables, used by many programs to determine the default text editor. There is a hard-coded list of one or more editors that visudo uses. The default is ` $ vi ` (hence the name visudo).

> [!TIP]
> In reality, you don't have to use the cumbersome ` $ visudo `. You can use a text editor of your choice such as ` $ gedit ` or ` $ ne `. It is possible to wall your self out of the system if the ` /etc/sudoers ` file or any file under ` /etc/sudoers.d/ ` directory is malformed. Sufficient safety can be achieved by having a second terminal instance running as root ` $ sudo su↵ `. There is no need for the sudo command once you are logged in as root as indicated by the ` # ` prompt. And any changes can be tested on another terminal instance running as an ordinary user. This way you can verify, that whatever you just did, left sudo running properly. If not, you have the root window to fix it.

<a id="edit-shadow"></a>

## 10.4 Encrypted password system

### Hashing [^hashing]

[^hashing]: [Taylor Hornby - How to Hash Passwords (The Right Way), accessed 2021](https://crackstation.net/hashing-security.htm)

Passwords stored in the ` /etc/shadow ` file are actually hashes. The purpose of password hashing is not to protect the system from being breached, but to protect the passwords if a breach does occur. If a password database gets hacked, and the passwords are unprotected, then malicious hackers can use those passwords to compromise users' accounts on other services, as most people use the same password everywhere.

Cryptography has three goals:
1. **Authenticity** = to prove where a file originated.
2. **Integrity** = to prove that a file has not changed unexpectedly.
3. **Confidentiality** = to keep the file content from being read by unauthorized users.

Password cryptography uses hashing to confirm data is unchanged (integrity). **Hashing** is a one-way process. The hashed result cannot be reversed to expose the original data. The checksum is a string of output that is a set size. Technically, this means that hashing is not encryption because encryption is intended to be reversed (decrypted). In Linux, you're likely to interact with one of two hashing methods: MD5 and SHA512.

Any computer system that requires password authentication must contain a database of passwords in some form. Because password databases are vulnerable to theft, storing passwords in plaintext is dangerous. Therefore most databases store only cryptographic hashes of the user's passwords. In such a system even the authentication system can't determine what a user's password is by merely looking at the stored value; Instead...
- When a user enters a password for authentication, the system computes the hash value for the provided password, and that hash value is compared to the stored hash for that user. Authentication is successful if the two hashes match.
- When you sign in to a GNU / Linux, the authentication process compares the stored hash value of your password against a hashed version of the password you typed in. If the two checksums are identical, then the original password and what you typed in are identical. In other words, you entered the correct password. This is determined, however, without ever actually decrypting the stored password on your system.

### Salting [^hashing]

Hackers can crack plain hashes very quickly using lookup tables and rainbow tables. Randomizing the hashing using salt is the solution to the problem. And thus hashes in typical GNU / Linux are salted.

Salting is an extra step during hashing that adds an additional value to the end of the password, thereby changing the hash value produced. Salting can drastically reduce the chances of an attacker cracking passwords. The premise of salting is to protect and prevent precomputed hash attacks. Even though salts are stored in a database beside the hashes, salting adds another barrier for attackers, essentially complicating the password cracking process. This is useful when users have repeated passwords across multiple applications. The time taken for an attacker to execute a successful cracking is drastically increased with salted hashes.

**Salting** randomizes each hash, so that when the same password is hashed twice, the hashes are not the same. We can randomize the hashes by appending or prepending a random string, called a salt, to the password before hashing. This makes the same password hash into a completely different string every time. To check if a password is correct, we need the salt, so it is usually stored in the user account database along with the hash, or as part of the hash string itself. The salt does not need to be secret. Just by randomizing the hashes, lookup tables, reverse lookup tables, and rainbow tables become ineffective. An attacker won't know in advance what the salt will be, so they can't pre-compute a lookup table or rainbow table. If each user's password is hashed with a different salt, the reverse lookup table attack won't work either.

- The salt should be stored in the user account table alongside the hash.
    - The salt does not need to be secret.
- The salt needs to be unique per-user per-password. Never reuse a salt.
    - A new random salt must be generated each time a user creates an account or changes their password.
    - Every time a user creates an account or changes their password, the password should be hashed using a new random salt.
- The salt also needs to be long, so that there are many possible salts.
    - As a rule of thumb, make your salt is at least as long as the hash function's output.
- Should the salt come before or after the password?
    - It doesn't matter, but pick one and stick with it for interoperability's sake.
    - Having the salt come before the password seems to be more common.
- If you are writing a web application, you might wonder where to hash?
    - In a Web Application, always hash on the server.
    - The password should be sent to the server "in the clear" and hashed there, or you can hash twice: once on the client side and then rehash the hash on the server side.
    - If passwords are hashed only in the user's browser with JavaScript the client-side hash logically becomes the user's password. If a bad guy somehow steals the database of hashes from this hypothetical website, they'll have immediate access to everyone's accounts without having to guess any passwords.
- One goal is to make the hash function slow enough to impede attacks, but still fast enough to not cause a noticeable delay for the user. Use a standard algorithm like PBKDF2 or bcrypt. These algorithms take a security factor or iteration count as an argument (this value determines how slow the hash function will be).
- Compares hash strings in a way that takes the same amount of time no matter how much of the strings match (to protect against a timing attack).

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
