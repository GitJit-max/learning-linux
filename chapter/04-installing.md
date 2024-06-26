<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="03-basic-terminal.md">&lt;&lt; Previous Chapter: 3 - Basic terminal usage</a>
     |
  <a href="05-links.md">Next&nbsp;Chapter:&nbsp;5&nbsp;&#8209;&nbsp;Links&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 4 - Installing applications

The topic of installing software applications is best approached by examples.

<a id="package-management"></a>

## 4.1 Package management

A GNU / Linux distribution comes pre-installed with many software applications intended for the end user. Pre-installed software can be removed and additional software can be added using the distribution specific **package manager**. The package manager always has a command line interface, but usually a graphical user interface if offered aswell (often called the **Software Center**).

Package managers simplify the process of adding, removing and updating software. When installing a new application, the package manager checks what other libraries the application needs, and automates installation these necessary **dependencies**.

Traditionally one of the most significant differences with other operating systems has been related to the open source ecosystem, and the existence of the digital distribution service like package management.

Package managers like dpkg have existed as early as 1994, and was originally a shell script. But the meaning of the phrase has evolved significantly. Package management systems became almost equivalent to other digital distribution services created much later such as the Google Play Store.

Traditionally all software offered through package management has been free and open source. But some distributions include select closed source software.

> [!NOTE]
> On a "stable" system such as Linux Mint, most packages are dated; Even 2-3 years old. Thus, users are inclined to use other installation methods such as flatpak, deb-files and compiling from source.

### Updating Solus via command line

```
$ sudo eopkg up↵ # Update everything

$ sudo eopkg up --exclude thunderbird↵ # Update everything except *an annoyingly large and frequently updated package*

$ sudo eopkg upgrade thunderbird↵ # Upgrade one specific package only (such as thunderbird)

$ sudo eopkg check | grep Broken | awk '{print $4}' | xargs sudo eopkg it --reinstall↵ # Check for and fix any corrupted packages

$ sudo eopkg install vivaldi-stable↵ # Install a specific package (such as vivaldi)
```

> Solus OS is a continuation of the previous project called Evolve OS. Thus ` $ eopkg ` stands for Evolve OS Package.

### Updating Debian derivatives via command line

```
$ sudo apt update↵ # First, update the package index
$ sudo apt upgrade↵ # Install available updates

$ sudo apt-mark hold thunderbird↵ # Hold current version
$ sudo apt update↵ # Update the package index
$ sudo apt upgrade↵ # Install available updates
$ sudo apt-mark unhold thunderbird↵ # Release hold

$ sudo apt update↵ # First, update the package index
$ sudo apt install --only-upgrade thunderbird↵ # Upgrade one specific package (such as thunderbird) and only if already installed.

$ sudo apt update --fix-missing↵ # Identify and install missing packages
$ sudo apt update --fix-broken↵ # Identify and fix broken packages

$ sudo apt update↵ # First, update the package index
$ sudo apt install vivaldi-stable↵ # Install a specific package (such as vivaldi)
```

- ` $ apt `, ` $ apt-get ` and ` $ dpkg ` are all tools within the Debian Package Management System. Advanced Packaging Tool ` $ apt-get ` manages remote repositories, resolves dependencies, and uses Debian Package Manager ` $ dpkg ` to actually make the changes of installing and removing packages. ` $ dpkg ` on itself cannot retrieve or download files from remote repositories, nor can it figure out dependencies.
- ` $ apt-get ` is a full-featured interface to ` $ dpkg `, while ` $ apt ` is a slightly stripped-back but more user-friendly version of ` $ apt-get `. ` $ apt ` and ` $ apt-get ` have some common commands, such as install, update, and upgrade, but ` $ apt ` also includes additional commands like search, show, list, and edit-sources.
- The Linux Mint maintainers have developed their own version of ` $ apt `, which is a Python wrapper for ` $ apt-get `.

> [!IMPORTANT]
> There are some common commands between ` $ apt ` and ` $ apt-get `. All of these commands can be preceded by ` $ apt ` or ` $ apt-get ` and will behave the same: install, remove, purge, update, upgrade, autoremove.


### Recommended software available through package distribution

**` vivaldi `** = Chrome based web browser alternative <https://vivaldi.com/>

**` vlc `** = DVD and video playback application <https://www.videolan.org/>

**` nemo `** = File manager <https://github.com/linuxmint/nemo>

**` loupe `** = Image viewer <https://gitlab.gnome.org/GNOME/loupe>

**` gwenview `** = Image viewer and simple editing <https://apps.kde.org/gwenview/>

**` pinta `** = Simple image editor <https://www.pinta-project.com/>

**` krita `** = Professional drawing application <https://krita.org/>

**` gufw `** = Simple dekstop firewall <https://github.com/costales/gufw>

**` kate `** = Advanced text editor <https://kate-editor.org/>

**` meld `** = Comparison of text files <https://meldmerge.org/>

**` openra `** = Remake of the classic RTS game Red Alert <https://www.openra.net/>

<a id="self-contained-formats"></a>

## 4.2 Self-contained application formats

Installing software from a second distribution package or unofficial source has even been considered avoidable and dangerous. Today, however, there are some alternative installation routes that are considered reliable, such as
- **.AppImage** files are portable self-contained executables, independent of the underlying GNU / Linux distribution. Each file includes all libraries the application depends on. AppImage does not enforce externally verified digital signatures or sandboxing, but it may be done by some applications. You can find .AppImage files in the download section of a software provider’s website.
- Applications using **Flatpak** run in a sandbox and need permissions to have access to resources such as bluetooth, network and files. These permissions are configured by the maintainer, and can be added or removed by users on their system. Flatpak allows app developers to directly provide updates to users. Although <https://flathub.org/> has become the de facto standard for getting applications packaged with Flatpak, it is possible to host a Flatpak repository that is independent of Flathub.
- **Snaps** are governed by Canonical (the company behind Ubuntu Linux distribution) and locked to their store <https://snapcraft.io/>

For self-contained software delivery, it seems like Flatpak has won. You don't see large swathes of developer marketing stories coming from the AppImage or Snap camps, nor the excitement from software vendors on these formats. But you do see them from Flatpak.

> [!NOTE]
> Self-contained application formats will always use more space on the system than common native packages.

<a id="dotdeb-files"></a>

## 4.3 Dotdeb files

The .deb format and filename extension refers to **Debian software package file**. It's used to install apps on Debian and its derivatives such as Linux Mint. You can think of deb files as "setup.exe" files in Windows. These are archives containing other files such as the application executable(s), man pages and libraries. Installing the software from a deb file means unpacking and placing all components in the correct directories on your computer.

You can find deb packages in the download section of a software provider’s website. You download the file from the internet. Navigate to ` ~/Downloads/ ` directory, using a file manager (such as nemo). And finally double-click the deb file to start the installation procedure.

### Recommended software available as dotdeb

- **Shutter Encoder** (free and open-source) <br>= Video converter <https://www.shutterencoder.com/>
- **Vivaldi** (free) <br>= Chromium based web browser <https://vivaldi.com/download/>
- **Master PDF Editor** (includes paid options) <br>= Professional pdf solution <https://code-industry.net/masterpdfeditor/>
- **ONLYOFFICE Desktop Editors** (includes paid options) <br>= Microsoft Office look-alike <https://www.onlyoffice.com/>
- **Beyond Compare** (paid after trial period) <br>= Industry standard file comparison <https://www.scootersoftware.com/home>

<a id="tarball"></a>

## 4.4 Tarball

In computing, **` $ tar `** is a computer software utility for collecting many files into one archive file, often referred to as a **tarball**, for distribution or backup purposes. The name is derived from "tape archive", as it was originally developed to write data to sequential I/O devices with no file system of their own, such as devices that use magnetic tape. [^wiki-tar]

[^wiki-tar]: [Wikipedia - tar (computing), accessed 2024](https://en.wikipedia.org/wiki/Tar_(computing))

### Install exiftool

**ExifTool** (free and open-source) is a command line app for handling metadata of image files <https://www.exiftool.org/>

ExifTool does not need to be installed to run. However, installation makes it available to all users by placing exiftool files in the correct directories such as the main executable to ` /usr/bin/ `, documentation to `/usr/share/man ` and API libraries to ` /usr/lib64/ `.

1. Download and extract: <br><https://www.exiftool.org/Image-ExifTool-12.86.tar.gz>

2. Run commands:

    ```
    $ cd ~/Downloads/Image-ExifTool-12.86/↵
    $ perl Makefile.PL↵
    $ sudo make install↵
    ```

### Install RAR for Linux

**RAR for Linux** (paid after trial period) is a command line app for handling rar files <https://www.rarlab.com/>

1. Download and extract: <https://www.rarlab.com/rar/rarlinux-x64-701.tar.gz>

2. Run the following commands (as instructed in the included ` makefile ` text file):

    ```
    $ cd ~/Downloads/rar/↵
    $ sudo cp rar unrar /usr/bin↵
    $ sudo cp rarfiles.lst /etc↵
    $ cp default.sfx /usr/lib↵
    ```

3. If purchased, copy your ` rarreg.key ` license file to any of the following directories:

    ```
    ~/
    /etc
    /usr/lib
    /usr/local/lib
    /usr/local/etc
    # You may rename "rarreg.key" to ".rarreg.key" or ".rarregkey"
    ```

<a id="python-applications"></a>

## 4.5 Python applications

The nonprofit [Python Software Foundation](https://www.python.org/psf-landing/) recommends using ` $ pip ` or ` $ pip3 ` for installing *Python applications* and its dependencies. Pip connects to an online repository of public packages. **Pip** is a recursive acronym for Pip Installs Packages.

> [!IMPORTANT]
>
> Downloading and installing *Python applications* is a breeze, but requires the *Python development environment* installed first through the distribution's package management. These packages, like any other packages, can have differing names between the distributions such as ` pip ` for Solus and ` python3-pip ` for Linux Mint.
> ```
> $ sudo eopkg install pip↵ # Install Python Development Environment
>
> $ sudo apt-get update↵ # First, update the package index
> $ sudo apt install python3-pip↵ # Install Python Development Environment
> ```

### Install trash-cli

**` trash-cli `** (free and open-source) is a command line interface to the [FreeDesktop.org trash can](http://standards.freedesktop.org/trash-spec/trashspec-latest.html); The same trashcan used by Budgie, KDE, GNOME, XFCE and alike, but you can invoke it from the command line (and scripts). <https://github.com/andreafrancia/trash-cli/>

Trash-cli is great for trying out different install options:

1. Install for all users: <br>` /usr/bin/ `, ` /usr/lib/ `, ` /usr/share/man/ `

    ```
    $ sudo pip install trash-cli↵

    $ sudo pip uninstall trash-cli↵
    ```

2. Bleeding Edge (from sources) to for all users:

    ```
    $ sudo pip install git+https://github.com/andreafrancia/trash-cli↵

    $ sudo pip uninstall trash-cli↵
    ```

3. Install for current user: <br>` ~/.local/bin/ `, ` ~/.local/lib/ `, ` ~/.local/share/man/ `

    ```
    $ pip install trash-cli↵
    $ export PATH=~/.local/bin:"$PATH"↵

    $ pip uninstall trash-cli↵
    ```

4. Bleeding Edge (from sources) to current user:

    ```
    $ pip install git+https://github.com/andreafrancia/trash-cli↵
    $ export PATH=~/.local/bin:"$PATH"↵

    $ pip uninstall trash-cli↵
    ```

> [!NOTE]
> Changes to the environment variable ` PATH ` vanish as the shell session ends. To make the change permanent add the export command ` export PATH=~/.local/bin:"$PATH" ` to a new line on ` ~/.bashrc `.
>
> Making the addition on commanline can be a bit tricky. But fortunately run control files can be modified using a graphical text editor (invoked from commandline) like this ` $ gedit ~/.bashrc↵ ` or this ` $ xed ~/.bashrc↵ ` (depending on the default text editor provided by the operating system).

<a id="compiling-from-source"></a>

## 4.6 Compiling from source

**SourceForge** (<https://sourceforge.net>) built up a lot of goodwill in the past, being a centralized place for downloading open-source software and hosting software repositories. Over the years, more projects have moved to other repository-hosting services like GitHub. SourceForge's reputation was tarnished by the addition of adware and malware to free source installation packages.

**GNU Savannah** (<http://savannah.gnu.org>) serves as a collaborative software development management system for free software projects. It is a project of the Free Software Foundation. Unlike GitHub or SourceForge, Savannah's focus is for free software and has very strict hosting policies (including a ban against the use of non-free formats).

**GitHub** (<https://github.com>) serves as a leading collaborative software development management system for open source projects. On October 26, 2018, Microsoft acquired GitHub for US$7.5 billion. Early on, a lot of developers worried that Microsoft would reduce its free offerings to squeeze more money out of it. But instead, GitHub expanded its free service and has continued to embrace open source developers. [^git-2022]

[^git-2022]: [Frederic Lardinois - Microsoft says GitHub now has 90M active users, published 2022](https://techcrunch.com/2022/10/25/microsoft-says-github-now-has-a-1b-arr-90m-active-users)

### Compile Gambas in Solus

**Gambas** is an object-oriented dialect of the BASIC programming language, as well as the integrated development environment that accompanies it. Gambas is a recursive acronym for Gambas Almost Means Basic. Gambas is developed by the French programmer Benoît Minisini. <https://gambas.sourceforge.net/>

First, install files necessary to compile C code:

```
$ sudo eopkg install -c system.devel↵
```

Second, install depencies:

```
alsa-lib-devel, autoconf, automake, bzip2-devel, curl-devel, curl-gnutls, gcc, gdk-pixbuf-devel, git, glew-devel, glib2-devel, gmime-devel, gmp-devel, gsl-devel, gstreamer-1.0-devel, gstreamer-1.0-plugins-base-devel, gtkglext-devel, imlib2-devel, libcairo-devel, libffi-devel, libgnome-keyring-devel, libgnutls-devel, libgtk-2-devel, libgtk-3-devel, libgtk-4-devel, libgtkmm-2-devel, libgtkmm-3-devel, libpcre-devel, librsvg-devel, libtool-devel, libwebkit-gtk-devel, libwebkit-gtk41-devel, libwebkit-gtk5-devel, libxml2-devel, libxslt-devel, libxtst-devel, llvm-devel, mariadb-devel, ncurses-devel, openssl-11-devel, poppler-devel, poppler-devel, postgresql-devel, qt5-3d-devel, qt5-base-devel, qt5-svg-devel, qt5-webengine-devel, qt5-webkit-devel, qt5-websockets-devel, qt5-webview-devel, qt5-x11extras-devel, sane-backends-devel, sdl-ttf-devel, sdl1-devel, sdl1-image-devel, sdl1-image-devel, sdl1-mixer-devel, sdl1-sound-devel, sdl2-devel, sdl2-image-devel, sdl2-image-devel, sdl2-mixer-devel, sdl2-ttf-devel, sqlite3-devel, unixodbc-devel, v4l-utils-devel, zstd-devel
```

Third, download and extract the source code: <https://gitlab.com/gambas/gambas/-/archive/stable/gambas-stable.tar.bz2>

Finally, compile the code:

```
$ cd ~/Downloads/gambas-stable/↵
$ ./reconf-all↵
$ ./configure -C --disable-qt4↵
$ make -j $(nproc)↵
$ sudo make install↵
```

### Compile Gambas in Linux Mint

First, install files necessary to compile C code:

```
$ sudo apt-get update↵ # First, update the package index
$ sudo apt-get install -y build-essential↵
```

Second, install depencies:

```
autoconf, automake, g++, git, libalure-dev, libasound2-dev, libbz2-dev, libcairo2-dev, libcurl4-gnutls-dev, libdirectfb-dev, libdumb1-dev, libffi-dev, libgdk-pixbuf2.0-dev, libglew-dev, libglib2.0-dev, libgmime-3.0-dev, libgmp-dev, libgsl-dev, libgstreamer-plugins-base1.0-dev, libgstreamer1.0-dev, libgtk-3-dev, libgtk2.0-dev, libgtkglext1-dev, libimlib2-dev, libmysqlclient-dev, libncurses5-dev, libpcre3-dev, libpoppler-cpp-dev, libpoppler-dev, libpoppler-glib-dev, libpoppler-private-dev, libpq-dev, libqt5opengl5-dev, libqt5svg5-dev, libqt5webkit5-dev, libqt5x11extras5-dev, librsvg2-dev, libsdl-image1.2-dev, libsdl-mixer1.2-dev, libsdl-sound1.2-dev, libsdl-ttf2.0-dev, libsdl2-dev, libsdl2-image-dev, libsdl2-mixer-dev, libsdl2-ttf-dev, libsqlite0-dev, libsqlite3-dev, libssl-dev, libtool, libv4l-dev, libwebkit2gtk-4.0-dev, libxml2-dev, libxslt1-dev, libxtst-dev, libzstd-dev, linux-libc-dev, llvm, llvm-dev, qtbase5-dev, qtwebengine5-dev, sane-utils, unixodbc-dev
```

Third, download and extract the source code: <https://gitlab.com/gambas/gambas/-/archive/stable/gambas-stable.tar.bz2>

Finally, compile the code:

```
$ cd ~/Downloads/gambas-stable/↵
$ ./reconf-all↵
$ /configure -C --disable-qt4 --disable-keyring↵
$ make -j $(nproc)↵
$ sudo make install↵
```
