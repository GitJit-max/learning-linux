<!-- Start of auto generated content -->

> [!TIP]
> The table of contents can be accessed by pressing the unordered list icon ![octicon](../asset/octicon-list-unordered.svg) on top the right corner.

<p align="center">
  <a href="../README.md">&lt;&lt; Back to cover page</a>
     |
  <a href="02-basic.md">Next&nbsp;Chapter:&nbsp;2&nbsp;&#8209;&nbsp;Design&nbsp;priciples&nbsp;of&nbsp;Unix&nbsp;and&nbsp;its&nbsp;decendants&nbsp;&gt;&gt;</a>
</p>

<!-- End of auto generated content -->

# Chapter 1 - History of Linux

Knowing about the past helps understand how things are today. So let's start by looking at the history of Linux and the views and opinions of a few selected individuals.

<a id="branching"></a>

## 1.1 Branching

In 1983 an American programmer and human rights activist Richard Stallman launched the [Free Software movement](https://www.fsf.org), with a plan to develop a complete free operating system named GNU. It was not designed from scratch. It was a free clone of an existing but proprietary operating system called Unix. GNU has the same commands and system calls as a Unix, and all parts of GNU were made compatible with the original Unix variants. People who used an original Unix could switch over with ease.

> The name **GNU** came from a tradition of the time. If there was an existing program, and you wrote something similar to it, inspired by it, you could give credit by giving your program a name saying it is not the other one (i.e. a recursive acronym). So Stallman gave credit to Unix for the technical ideas with the name GNU, a recursive acronym for *GNU is Not Unix*.

> [!NOTE]
> The term **clone** is often used in a negative sense. A clone can be seen as a copy of an idea, but on the other hand it can also be a tribute to an imitated original work. Sometimes clones give rise to a new genre and the imitated work becomes the parent work of the genre.

### Three main branches

Unix has evolved to a whole family of operating systems called unices. Like any history going back over 60 years, the history of Unix and its descendants is messy. To simplify things, we can roughly divide unices into three groups or main branches:

1. **The proprietary commercial Unix operating systems** came first. These are not quite as common today, but some of them are still out there (such as Solaris, HP-UX and AIX).
2. **The BSD (Berkeley Software Distribution)** group of unix descendants was developed in academia. BSD lives on today through FreeBSD, NetBSD, and OpenBSD.
3. **GNU/Linux**, the last and most known group of unix descendants has it's roots in the [Free Software Movement](https://www.fsf.org) and respect for users freedom (see [Section: Digital technology against freedom](#digital-technology-against-freedom)).

### Licensing is a significant difference

Both GNU/Linux and the BSDs are free and open-source. They have more things in common than they do different, so one might wonder why they both exist? Mainly because of the philosophical differences about the way one should build an operating system and license it. And licensing is a significant difference:
- **GNU/Linux use the [GNU General Public License](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html):** If you modify the Linux kernel and distribute it, you have to release the source code for your modifications.
- **The BSDs use the [BSD license](https://en.wikipedia.org/wiki/BSD_licenses):** If you modify BSD and distribute it, you do not have to release the source code at all. You are free to do whatever you like with the BSD code. You are not obligated to release the source code, although you can do so if you whish. Manufacturers creating devices may choose BSD for the operating system, instead of GNU/Linux, so they will not have to release the code.

<a id="quality-of-free-and-open-source"></a>

## 1.2 Quality of free and open-source

> GNU/Linux distributions are developed and maintained by companies as well as individuals, hobbyists, volunteers, and community users. Large, successful companies ship their distributions to the commercial market along with expensive support contracts. Sometimes distributions are a product of individuals and relatively small groups of people. Typically, most open-source contributors to any given project are volunteer programmers contributing in order to be rewarded by the reputation incentives and increased usefulness of the software to themselves. A central individual or core group steers the project. Other contributors may drop in and drop out sporadically. [^raymond-open]

People <!--from outside the GNU/Linux world (especially non-technical people)--> are prone to think software that is free and open-source is <!--necessarily--> inferior to the commercial kind, shoddily made, unreliable and will cause more headaches than it saves. [^raymond-best]

It is true that open source can not promise better quality, higher reliability, more flexibility. Free software is not always as convenient, as its proprietary competitors. Free software is sometimes low quality, unreliable, inflexible. Developers of proprietary software are not incompetent. Sometimes they produce a program that is powerful and reliable, even though it does not respect the users' freedom. For free software advocates, glitches and missing features are never a source of shame. Any piece of free software that respects users' freedom has a strong inherent advantage over a proprietary competitor that does not. Even if it has other issues, free software always has freedom. [^notsuper]

However in general, open-source software is written by people who care about it, need it, use it themselves, and are putting their individual reputations among their peers on the line by publishing it. They also tend to have less of their time consumed by meetings, retroactive design changes, and bureaucratic overhead. They can therefore be both more motivated and well positioned to do excellent work; sometimes even more so than wage slaves toiling Dilbert-like to meet impossible deadlines in the cubicles of proprietary software houses. Open-source packages may lack polish and have documentation that assumes much, but the vital parts will usually work quite well. Many mature open-source packages are of high quality, and even functionally superior to proprietary equivalent. In the open-source world developers are never forced (by a deadline) to close their eyes, hold their noses, and ship. [^raymond-best] 

[^notsuper]: [Benjamin Mako Hill - Free Software Isn't Practically Superior, updated 2011](https://www.gnu.org/philosophy/when-free-software-isnt-practically-superior.html)

<a id="culture-of-open-source-works"></a>

## 1.3 Culture of open-source works

The technique of open-source development evolved as an unconscious folk practice in the Unix community for more than a quarter century, many years before it was analyzed and labeled in the late 1990s. The early Unix community was a paradigmatic example of open source in action before the AT&T divestiture in 1983 (see remark below). While the pre-divestiture Unix code was technically and legally proprietary, it was treated as a commons within its user and developer community. Volunteer efforts were self-directed by the people most strongly motivated to solve problems. The Berkeley campus of the University of California emerged early as the single most important academic hot-spot in Unix development. Unix research had begun there in 1974, and was given a substantial impetus when Ken Thompson (the designer of the original Unix operating system at Bell Labs) taught at the University during a 1975-76 sabbatical. The first BSD release had been in 1977 from a lab run by a then-unknown grad student named Bill Joy. By 1980 Berkeley was the hub of a sub-network of universities actively contributing to their variant of Unix. Ideas and code from Berkeley Unix were feeding back from Berkeley to Bell Labs. [^raymond-origins]

> This divestiture was initiated by the filing in 1974 by the United States Department of Justice of an antitrust lawsuit against AT&T. AT&T was, at the time, the sole provider of telephone service throughout most of the United States. Furthermore, most telephonic equipment in the United States was produced by its subsidiary, Western Electric. This vertical integration led AT&T to have almost total control over communication technology in the country, which led to the antitrust case, United States versus AT&T. The plaintiff in the court complaint asked the court to order AT&T to divest ownership of Western Electric. [^breakup]

[^breakup]: [Wikipedia - Breakup of the Bell System, accessed 2021](https://en.wikipedia.org/wiki/Breakup_of_the_Bell_System)

After the breakup of Bell System mandated by the United States Department of Justice in 1982, AT&T promptly rushed to commercialize Unix System V; a move that nearly killed Unix. Most Unix boosters thought that the divestiture (taking money away from where you have invested it) was great news. What none realized at the time was that the productization of Unix would destroy the free exchanges of source code that had nurtured so much of the system's early vitality. Knowing no other model than secrecy for collecting profits from software and no other model than centralized control for developing a commercial product, AT&T clamped down hard on source-code distribution. Bootleg Unix tapes became far less interesting in the knowledge that the threat of lawsuit might come with them. Contributions from universities began to dry up. No individual could afford Unix, not with the \$40,000 price-tag on a source-code license. To make matters worse, the big new players in the Unix market promptly committed major strategic blunders. One was to seek advantage by product differentiation; A tactic which resulted in the interfaces of different Unixes diverging. This threw away cross-platform compatibility and fragmented the Unix market. AT&T, fixated on minicomputers and mainframes, tried several different strategies to become a major player in computers, and badly botched all of them. A dozen small companies formed to support Unix on PCs. All were underfunded, focused on selling to developers and engineers, and never aimed at the business and home market that Microsoft was targeting. [^raymond-wars]

> [!IMPORTANT]
> To sum up: Unix flourished when its practices most closely approximated open source, and stagnated when they did not. Fortunately the old-time unix culture has largely reinvented itself in the open-source movement. [^raymond-new]

<a id="economic-sustainability"></a>

## 1.4 Economic sustainability

To make open-source development economically sustainable, the choices come down [^raymond-problems]
1. **To singing for your supper:** Getting paid through tips and donations.
2. **Running a corner shop:** A small, low-overhead service business.
3. **Finding a wealthy patron:** Some large firm that needs to use and modify open-source software for its business purposes.

> [!IMPORTANT]
> One important subproblem related to the increasing difficulty of sustaining really large software businesses is how to organize end-user testing. Real end-user testing demands facilities, specialists, and a level of monitoring that are difficult for the distributed volunteer groups characteristic of open-source development to arrange. [^raymond-problems]

<a id="time-sharing"></a>

## 1.5 Time-sharing

Unices emerge from a 1960's to 1970's model of computing called **time-sharing**. That is allowing multiple users to interact concurrently with a single computer by sharing of a computing resource among multiple users at the same time. Time-sharing was born out of the realization that any single user would make inefficient use of a computer. Typically an individual enters bursts of information followed by long pauses. But a large group of users working at the same time would mean that the pauses of one user would be filled by the activity of others. With the rise of microcomputing in the early 1980s, time-sharing became less significant. Individual microprocessors were sufficiently inexpensive that a single person could have all the CPU time dedicated solely to their needs, even when idle. [^wikitime]

[^wikitime]: [Wikipedia - Time-sharing, accessed 2021](https://en.wikipedia.org/wiki/Time-sharing)

Internet brought the general concept of time-sharing back into popularity. Expensive corporate server farms costing millions can host thousands of customers all sharing the same common resources. As with the early serial terminals, web sites operate primarily in bursts of activity followed by periods of idle time. This bursting nature permits the service to be used by many customers at once, usually with no perceptible communication delays. [^wikitime] For public Internet servers the GNU/Linux family is generally counted as dominant (with 65 % market share), powering well over twice the number of hosts as Windows Server (with 25 % market share). [^server-marketshare] The supercomputer field is completely dominated by GNU/Linux. All 500 of the fastest supercomputers in the world run GNU/Linux. [^top500]

[^server-marketshare]: [Fortune Business Insights - Server Operating System Market Volume, accessed 2025](https://www.fortunebusinessinsights.com/server-operating-system-market-106601)

[^top500]: [Top500.org - List Statistics by Operating system Family, accessed 2025](https://www.top500.org/statistics/list/)

<a id="philosophy-of-the-gnu-project"></a>

## 1.6 Philosophy of the GNU project

Nowadays there are millions using the GNU operating system, but most of them don't know they are using GNU. People call the system Linux. This is a widespread practice which is not nice. Since the Free Software movement wrote the biggest parts of the code, one should give them atleast equal mention, and call the system *GNU+Linux* or *GNU/Linux*. But there is another reason to do this. The reason for developing GNU was unique. GNU is the only operating system developed for the purpose of freedom. Not for technical motivations. Not for commercial motivations. GNU was written for your freedom. A finnish programmer Linus Torvalds, the person who wrote the kernel component for the GNU project (called Linux) doesn't agree with the Free Software movement. He does not state that people deserve freedom. He says he likes convenient, reliable, powerful software and tells people that those are the important values. [^philo]

[^philo]: [Philosophy of the GNU Project, updated 2022](https://www.gnu.org/philosophy/)

### Digital technology against freedom

Without a free operating system, it's impossible to have freedom (see [Section: Digital society](#digital-society)). And by free software, the Free Software movement, means software that respects users' freedom. Ultimately there are just two possibilities with software: 1) either the users control the program or 2) someone else controls the program (and through it has power over the users). A nonfree program is an instrument of unjust power that nobody should ever have. [^philo]

The developer who has control of the program often feels tempted to introduce malicious features to further exploit or abuse the users. There are many ways in which our freedom is being attacked by digital technology. [^philo]

#### Addictive by design

Functionalities added for the sole purpose of luring users into frequent and intensive use of the program, with the goal of causing [addiction](https://www.gnu.org/proprietary/proprietary-addictions.html) and spending more and more money.

#### Deliberate incompatibility

[Deliberate incompatibility](https://www.gnu.org/proprietary/proprietary-incompatibility.html) comes in many forms such as forcing users to buy a new version of the program after a Windows major version upgrade, or blocking users from switching to any other program by use of secret formats and protocols.

#### Crippled by design

[Proprietary jail](https://www.gnu.org/proprietary/proprietary-jails.html) is an operating system designed to impose censorship of which applications the user can install.

DRM means functionalities designed intentionally to [restrict](https://www.gnu.org/proprietary/proprietary-drm.html) what users can do such as playing a bluray disc.

[Tyrant](https://www.gnu.org/proprietary/proprietary-tyrants.html) is a malicious device that prevents users from installing a different or modified operating system. These devices have measures to block execution of anything other than the approved system.

#### Designed to force approval

[Harassing](https://www.gnu.org/proprietary/proprietary-interference.html) comes in many forms such as annoying the users to switch their web browser.

#### Designed to listen for remote commands

[Back doors](https://www.gnu.org/proprietary/proprietary-back-doors.html) listen for remote commands to mistreat the user.

#### Designed to be server dependent

[Tethering](https://www.gnu.org/proprietary/proprietary-tethers.html) a product or program means designing it to work only by communicating with a specific server. In some cases, tethering is used to do specific nasty things to the users. Tethers also contain a time bomb, since it means you can't use the program when the server get shutdown eventually.

#### Designed to monitor the user

[Surveillance](https://www.gnu.org/philosophy/free-digital-society.en.html#surveillance) means snooping and tracking users. Computers are ideal for any tyrant who wants to crush opposition. They are ideal for surveillance. Anything we do with computers, the computers can record. They can record the information in a perfectly indexed searchable form in a central database. Computerized surveillance makes it possible to centralize and index all this information so that an unjust regime can find it all, and find out all about everyone. If a dictator takes power, which could happen anywhere, people realize this and they recognize that they should not communicate with other dissidents in a way that the state could find out about. But if the dictator has several years of stored records of who talks with whom, it's too late to take any precautions. He already has everything he needs to realize: *OK, this guy is a dissident, and he spoke with him. Maybe he is a dissident too. Maybe we should grab him and torture him.* [^philo]

### Digital society

It is not true to assume that participating in a digital society is good. Being in a digital society can be good or bad, depending on whether that digital society is just or unjust. [^philo]

People should campaign to put an end to digital surveillance. One can't wait until there is a dictator and it would really matter. And besides, it doesn't take an outright dictatorship to start attacking human rights. Today we see censorship imposed in countries that are not normally thought of as dictatorships, such as UK, France, Spain, Italy, Denmark. Censorship is not new, it existed long before computers. But 20 years ago, we thought that the Internet would protect us from censorship, that it would defeat censorship. Then the opposite happened. Goverments have went to great lengths to impose censorship on the Internet. We must recognize that a country that imposes censorship on the Internet is not a free country. And is not a legitimate government either. [^philo]

> [!IMPORTANT]
> If we have an unjust digital society, we should cancel these projects for digital inclusion and launch projects for digital extraction. [^philo]

The most important point about free software is that schools should teach exclusively free software. There should be nothing proprietary in the education. Proprietary developers offer gratis copies to schools, because they want schools to make children dependent. The idea is to direct students down the path of permanent dependence. To teach people the use of proprietary software, is to teach **dependence** (i.e. the state of needing the help and support of somebody or something in order to survive or be successful). Schools should never do that because it's the opposite of their mission. Some people say: *Let's have the school teach both proprietary software and free software, so the students become familiar with both.* But that's like saying the schools are supposed to teach both good habits and bad ones. [^philo]

<a id="the-birth"></a>

## 1.7 The birth of GNU & Linux

Back in the 1980s, computers were hugely expensive (worth millions of dollars in todays money) and were only used in large companies and universities. The only "real" operating system was Unix. In addition, computer manufacturers began shutting down and patenting the source code of their software to prevent it from being used on competitors’ computers. Today, in 2020, we can see that the restrictions of equipment manufacturers have gone even further (see [Section: Digital technology against freedom](#digital-technology-against-freedom) for examples).

In January 1984, Richard Stallman, a U.S. programmer, founder of the Free Software Foundation, and later advocate of free software, began the development of a free operating system like Unix. This project, called GNU, brought together existing free software *such as window system X* as well as taking action on what was not yet *such as operating system kernel Hurd, text editor Emacs, GNU Compiler Collection GCC, GNU C-library (glibc), GNU-binary utils (binutils), command language interpreter bash, coreutils-package, image processing program GIMP, and desktop environment GNOME.* 

The development of the system's kernel, Hurd, proved more difficult than expected. But because GNU was designed to be compatible with existing Unix variants, individual GNU components could be used before the entire GNU operating system was completed. The dream of a completely free operating system came true when Finnish programmer Linus Torvalds released a Linux kernel under the GPL license in 1992, which could be combined with programs compiled by the GNU project. Since then, free software has received a lot of publicity and the supply has increased tremendously. As a name, Linux became the forefront of free operating systems even though it was just a kernel. This led to confusion over the names of the distributions: GNU or Linux?

The development of Linux began in part with Torvalds' dissatisfaction with the MS-DOS operating system from Microsoft. Torvalds was interested in Unix, which was considered by computer enthusiasts to be the only street-credible operating system. Unix was popular but too expensive for home use. The Unix machines at the time <!--were worth millions of euros and--> were only used in large companies and universities. Linux does not contain the original (copyrighted) Unix source code. Torvalds had found materials that contained system calls from the Sun OS version of Unix, which was often used on machines of the Finnish military, and created code to perform similar tasks for his own project. <!--The other parts of the GNU/Linux operating system are based on the GNU project (launched in 1984 before Linux). Hurd's development of the GNU kernel proved to be more difficult than expected, and the dream of a completely free operating system only came true when Linus Torvalds released a Linux kernel under the GPL in 1992, which could be combined with programs compiled by the GNU project.--> Torvalds first published his Linux project in 1991 on the newsgroup *comp.os.minix*.

Early versions of Linux had been released under a license written by Torvalds himself, which did not allow the kernel to be distributed for money. Thanks to open source, people around the world were able to take part on the development of Linux. The current license is GPL2 and Torvalds has said he opposes the transition to version 3 (due to the usage restrictions it added). Torvalds continues to lead Linux programming and has described his decision to release the Linux kernel under the GPL license as the best thing he has ever done.

<a id="eight-pieces"></a>

## 1.8 Linux distros aren’t just the kernel

The general populace has gravitated to the name Linux and this name has largely stuck. However Linux distributions are not just the Linux kernel. They all contain other critical software such as a bootloader (systemd-boot or grub), a shell (such as bash), shell utilities (such as ls, mkdir, echo), daemons (i.e. background processes), a graphical server (such as x.org, mutter, kwin), a desktop environment (such as budgie, gnome, kde, unity) and more. [^8pieces]

[^8pieces]: [Chris Hoffman - 8 Pieces That Make Up Linux Systems, published 2013](https://www.howtogeek.com/177213/linux-isnt-just-linux-8-pieces-of-software-that-make-up-linux-systems/)

All these different programs are developed by different, independent development groups (many of which by the GNU project). All these are combined by distributions, where they build on top of each other to make a complete operating system. This is unlike Windows, which is developed entirely by Microsoft. [^8pieces]

### Boot loader

<!--1. When you turn on your computer, your computer’s BIOS or UEFI firmware loads a boot loader (the first program to load with any operating system). A boot loader might boot your GNU/Linux system almost instantly if you only have a single operating system installed, but it’s still there.-->

The first program to open with any operating system is the *UEFI/BIOS first stage boot loader* on the motherboard. The **second stage boot loaders** are NTLDR for the Windows operating system and GRUB or systemd-boot for the GNU/Linux operating system. The first and second stage boot loaders may work very quickly, but they still exist.

### Kernel

The second stage boot loader starts the kernel of the operating system. This is the part of the system that’s actually called Linux. The **kernel** is the core of the system that speaks directly to the hardware. It manages your CPU, memory, and input/output devices such as keyboard, mouse, and display. All other software runs above the kernel. The kernel is the lowest-level piece of software, which interfaces with the hardware. It provides a layer of abstraction above the hardware, dealing with all the different hardware quirks so the rest of the system can care about them as little as possible. [^8pieces]

> [!NOTE]
> The Linux kernel is the operating system’s core, developed by the Finnish programmer Linus Torvalds (**kernel** = the inner part of a nut or seed or the central, most important part of an idea or a subject). <!--In everyday language, Linux has become the name for an operating system family built around the Linux kernel. Officially, we are talking about unix-like GNU/Linux desktop distributions, which form a complete operating system with desktop environments and application libraries, and not just the operating system kernel.-->

### Background processes

**Background processes** are the next pieces of software loaded after the kernel. This happens before you see the graphical login screen. Windows refers to such processes as services, while unix-like systems refer to them as daemons. Daemons are system-level processes you generally do not notice. For example ` $ crond ` manages scheduled tasks and ` $ syslogd ` manages system log. The letter d at the end stands for daemon. [^8pieces]

### Shell

Another important part of a GNU/Linux operating system is a **shell** (such as bash), which provides a command processor interface. When you open a terminal window, you see a shell prompt, but even if you’re just using a graphical desktop, shells are running and being used in the background.

### Vital shell utilities

The shell provides some basic [built-in commands](03-basic-terminal.md#shell-builtin-commands), but most of the shell commands in use are not built into the shell. Many **vital shell utilities** such as copy ` $ cp `, remove ` $ rm ` and list ` $ ls ` come as part of the [GNU Core Utilities package](https://en.wikipedia.org/wiki/List_of_GNU_Core_Utilities_commands). A GNU/Linux system would not function without these critical utilities.

### Graphical server

The graphical system is run by a **graphical server** (typically X.Org, Mutter, KWin), which interfaces with your video card, monitor, mouse, and other devices. The graphical server does not provide the full desktop environment, just a graphical system that desktop environments and toolkits can build on top of.

> **Wayland** and **X11** are display server protocol standards.
>
> **X.Org** is the most widely used server compositor that implements X11. Over time there have been other implementations such as TinyX for embedded systems.
>
> **Weston** is an reference server compositor that implements Wayland. However various desktop environments have their own Wayland-based compositors instead of using Weston, such as GNOME has **Mutter**, and KDE Plasma has **KWin**.

### Widget toolkit

A **widget toolkit** (such as GTK and Qt) provides elements such as buttons and drop-down menus for creating graphical user interfaces. The choice of toolkit is usually a decision for the software developer, but in some cases you will see support for several alternative toolkits built into a software application.

### Desktop environment

A **desktop environment** (such as Budgie, GNOME, KDE Plasma, Xfce) provides the computer user with a graphical user interface with a desktop at the bottom and various documents on top, as the metaphor suggests. The aim is to provide an instinctive way of using the computer as if it were a physical desktop.

In some cases, the desktop environment can be switched each time the user logs on to the system. This is because the **login menu** is also a sub-program (such as ` $ slick-greeter ` or ` $ lightdm-gtk-greeter `).

Desktop environments typically include their own set of **utility programs**, which are built to fit the desktop environment as a whole. For example, GNOME includes the ` $ nautilus ` file manager developed as part of GNOME, KDE Plasma includes the ` $ dolphin ` file manager developed as part of the KDE project, and Linux Mint Cinnamon includes the ` $ nemo ` file manager developed as part of Linux Mint. Many of these applications have a good reputation and can be used in other desktop environments.

### Additional applications

Not all desktop applications are part of a desktop environment. For example, Firefox and Libreoffice are just **software applications** that can be used on top of any desktop environment.

GNU/Linux distributions take all this software, combine it to work well together, and add their own necessary utilities such as **system installers** so you can actually install the operating system, as well as **package managers** for installing additional software and keeping your installed software updated (see [Chapter 4, Section: Package management](04-installing.md#package-management)). [^8pieces]

<a id="gnu-gpl"></a>

## 1.9 GNU General Public -license

Free software and open source software are not the same thing and are not mutually exclusive. Free software uses its own licenses. The Free Software Foundation encourages you to use the established and good [GNU General Public License](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html), instead of creating your own license. And it has become one of the most popular free software distribution licenses.

Richard Stallman, the founder of the Free Software Movement:
1. Invented the concept of copyleft: Change and redistribute but don't strip off this freedom.
2. And wrote (with lawyers) the GNU GPL, which implements copyleft.

**Copyleft** says that anyone who redistributes the software, with or without changes, must pass along the freedom to further copy and change it. Copyleft guarantees that every user has freedom. To copyleft a program, one first state that it is copyrighted. Then one adds distribution terms, which are a legal instrument that gives everyone the rights to use, modify, and redistribute the program's code, or any program derived from it, but only if the distribution terms are unchanged. Thus, the code and the freedoms become legally inseparable.

Proprietary software developers use copyright to take away the users' freedom. The Free Software movement use copyright to guarantee freedom. That's why they reversed the name, changing copy*right* into copy*left*. The *left* in copyleft is not a reference to the verb leave; only to the direction which is the mirror image of right.

> [!NOTE]
> Once software is licensed under the GNU GPL, a commercial operator cannot, for example, buy it to stop the development, to exclude a competitor.

<a id="unix-or-unix-like"></a>

## 1.10 UNIX or Unix-like

It is conceivable that Unix is a plural word, referring to its numerous implementations. Unix is a set of operating systems of the same type (but not exactly the same). The family of unices (the multitasking, multiuser computer operating systems) derive from the original AT&T Unix development starting in the United States of America, in the 1970's at Bell Labs research center. It was initially intended for use inside the Bell System. AT&T licensed Unix to outside parties in the late 1970's, leading to a variety of both academic and commercial Unix variants from vendors including University of California, Berkeley (BSD), Microsoft (Xenix), IBM (AIX), and Sun Microsystems (Solaris). [^wiki-uni]

[^wiki-uni]: [Wikipedia - Unix, accessed 2021](https://en.wikipedia.org/wiki/Unix)

GNU/Linux system developers generally aim for compliance with [POSIX / IEEE 10003 standards](https://pubs.opengroup.org/onlinepubs/9799919799/), which form the core of the commercial [Single UNIX specification](https://unix.org/online.html). For all intents and purposes, a typical modern GNU/Linux distribution (such as Ubuntu) is a Unix, but strictly speaking no system can claim to be Unix without being certified. Very few Linux based operating systems are submitted for compliance with the *Single UNIX Specification*. So instead people say GNU/Linux distributions are unix-like, even though they are nearly fully compliant with the *Single UNIX Specification*.

### Linux

**Linux®** is a registered trademark of Linus Torvalds.

While the software used in a GNU/Linux distribution may be run on genuine certified Unix, the GNU/Linux distributions are said to be "only" like Unix. Certification from the trademark owner would cost money, and would be contrary to the nature of free software.

### Android

**Android®** is a trademark of Google LLC.

Google's Android operating system is based on the Linux kernel, for smartphones and tablets, but it is not Unix-like. Linux makes up the core part of Android, but Google has not added all the typical software and libraries (see [Section: Linux distros aren’t just the kernel](#eight-pieces)) you’d find on a Linux distribution like Ubuntu. <!--Android does not include an X server (like Xorg), so--> You cannot run standard graphical GNU/Linux applications on Android.

### UNIX

**UNIX®** (in capital letters) is a registered trademark of The Open Group. The right to use the trademark in question requires that 1) The system meets the *Single UNIX Specification* requirements of *The Open Group* and 2) The certification fee and annual trademark royalties are paid to *The Open Group*.

The following operating systems are UNIX® certified: macOS (BSD), AIX (System V), Solaris (System V), HP-UX (System V), EulerOS (GNU/Linux), Inspur K-UX (GNU/Linux); Although some have expired and not renewed their license.

### macOS

**macOS®** is a registered trademark of Apple Inc.

MacOS is a UNIX 03 registered product and conforms to the Single UNIX 03 specification (full compliance). However macOS (previously known as OS X) is actually based on open-source projects and a descendant of the BSD family. It’s a bit different from other BSDs. While the low-level kernel and other software is open-source BSD code, most of the rest of the operating system is closed-source macOS code. Apple built macOS (and iOS) on top of BSD so they would not have to write the low-level operating system themselves (just as Google built Android on top of the Linux-kernel).

<!-- MacOS has a very strong unifying idea that is very different from Unix's: *The Mac Interface Guidelines*. These specify in great detail what an application should look like and how it should behave. -->

MacOS has a very strict set of interface rules, very different from Unix's. Apple's interface guidelines have of course evolved over the years, from the 1992 booklet [Macintosh Human Interface Guidelines](http://interface.free.fr/Archives/Apple_HIGuidelines.pdf) to the up-to-date online [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines). However, a very strong unifying idea is that developers can only create applications that are aligned with Apple's design philosophy. And an app that deviates from them is effectively not allowed to be sold on Apple's app stores [^ei-saa-kauppaan]. The guidelines define in great detail what an app should look like and how it should behave. The guidelines cover such things as layout, typography, colour scheme, navigation and user interaction.

[^ei-saa-kauppaan]: [Juha Metsäkallas - Otsikoimaton artikkeli, published 2019](https://finnababilejo.fi/artikolo/juha_metsakallas/2019/12/ja-muut-nappylat/)

The Macintosh's unifying idea is so strong that all programs have a graphical user interface. Most software applications have no command language interface at all (see [Chapter 2, Section: Command Language Interface](02-basic.md#command-language-interface)). Scripting facilities are present but most Mac programmers never learn them (see [Chapter 2, Section: Text interface has retained its utility](02-basic.md#retained-utility)). The consistency of the guidelines influenced the culture of Mac users in significant ways. Ports of programs that did not follow the guidelines have been summarily rejected by the Mac user base and failed in the marketplace.

<a id="distro-family"></a>

## 1.11 The GNU/Linux family

The Unix-like operating systems, running a Linux kernel, form a plethora of distributions. There are roughly 300 to 700 different GNU/Linux distributions (depending on the calculation method).

Many distributions are derivations of an existing distribution. This is mainly because the major effort in creating a distribution is designing and creating a package management system, the default way for users to install and uninstall software from a software repository. This is no small undertaking. Even putting the software engineering aside, hosting a software repository takes time, effort, and expense. This leads to families or genealogies of distributions. [^apt-or-get] ![Linux Distributions Timeline](https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg)

[^apt-or-get]: [Dave McKay - Should you use apt or apt-get?, published 2023](https://www.howtogeek.com/791055/apt-vs-apt-get-whats-the-difference-on-linux/)

The major branches of popular established GNU/Linux families are:
1. Debian 1993
    - Knoppix 2000
    - Ubuntu 2004
2. Slackware 1993
    - SUSE 1994
3. Red Hat 1994
    - Mandrake 1998
    - CentOS 2003
    - Fedora 2003
4. Gentoo 1999 (formerly Enoch)
5. Arch 2002

> [!NOTE]
> It doesn't make things any easier for newcomers when there is so much choice. But newcomers can concentrate on a handful of disributions (see [Section: Suggested distributions](#suggested-distributions)).

<a id="the-cost-of-gnu-linux"></a>

## 1.12 The cost of GNU/Linux

Whether you pay nothing, a little, or a lot for a distribution depends on what you need from it and the business model the distributor works to. For example, Red Hat Enterprise Linux (RHEL) and SUSE are both commercial GNU/Linux distributions which have business level support contracts. Red Hat offers a 10-year lifecycle, divided into full support and maintenance support phases, followed by an extended lifecycle phase at an additional cost. SUSE products are supported for up to thirteen years. Both offer round-the-clock service level support for businesses that rely on their Linux systems to meet their critical needs. Subscribers also pay for other related services such as licensing, documentation, paid staff, end-user feature enhancements and telephone hotline support. Note however, that just because you have paid for the software, does not necessarily mean that it’s better. [^ross]

[^ross]: [Alistair Ross - The Ultimate Linux Newbie Guide, accessed 2021](https://linuxnewbieguide.org/overview-of-chapters/chapter-3-choosing-a-linux-distribution/)

Even free distributions can incur costs. In the workplace, GNU/Linux almost always increases training costs.

<a id="popularity-of-gnu-linux-desktop"></a>

## 1.13 Popularity of GNU/Linux desktop 

Unix has it's architectural strengths of a server operating system (see [Section: Time-sharing](#time-sharing)), but has proved capable of reinventing itself as a desktop client; one could argue that perhaps even more so than any of its client-operating-system competitors (such as Windows) have been of reinventing themselves as servers. [^mckay]

[^mckay]: [Dave McKay - Why Desktop Linux Still Matters, published 2020](https://www.howtogeek.com/676963/why-desktop-linux-still-matters/)

But even though GNU/Linux is great for personal computers, this does not show in user numbers. GNU/Linux accounts only for a tiny percentage of the overall desktop market share. <!--Dirk Hohndel (who was then the chief Linux and open-source technologist at Intel) predicted that in 1999, GNU/Linux would penetrate the PC desktop market and displace Windows. This never happened and it likely never will. The perennial 2 % has been around roughly since 2005 compared to ~ 88 % for Windows and ~ 9 % for macOS (which is a certified Unix by the way). Does that mean Linux on a desktop PC is irrelevant? Not at all!--> It seems the majority of people <!--(even those at a tech talk)--> want to be able to run either the same software as their friends or what they use at work. They either buy a computer or laptop and get Windows by default. Or they buy a Mac because they were told it was simpler to use. Or they got an Apple computer because they like their iPhone. People buy computers like they buy microwaves. They do not care what makes them go, they just want to reheat food. [^mckay]

Hardware that ships with GNU/Linux preinstalled doesn't really make new converts for the OS. Dell and HP have offered hardware options pre-installed with GNU/Linux (since 2007 and 2004, respectively). And there’s a new wave of both budget-friendly and high-end laptops and computers designed for GNU/Linux. These devices are selling to the established GNU/Linux user base. [^mckay]

### Most people do not want a GNU/Linux

When asked from people who understand a bit more about operating systems, the reasons they give for not running GNU/Linux are variations on a set of the following themes:
- Gaming on Linux has improved over recent years, but Windows is still the only platform for serious gaming.
- Linux will not run a certain software such as Photoshop, AutoCAD or Microsoft Office. This is a deal-breaker for many people. Most people are not interested in alternatives.
- Reluctance to tinker. They just want to get on with their work.
- Reluctance to learn something "new" such as the the command line.
- They do not want to be different. They want to use the same things their friends and family use.
- They do not have an opinion on personal freedoms (see [Section: Philosophy of the GNU project](#philosophy-of-the-gnu-project).

### GNU/Linux desktop is used by

- Universities, businesses, charities, councils, administrations.
- People who used a Unix or GNU/Linux at college or professionally.
- People interested in free and open-source software.
- People interested in privacy.
- Longtime devotees and hobbyists.
- People who want to extend the life of hardware that is too old to use the latest Windows (with an alternative up-to-date operating system).
- Computer science majors and developers, lots of developers.
    - If the world runs on GNU/Linux (see [Section: Time-sharing](#time-sharing)), the world needs GNU/Linux developers.
    - The Windows Subsystem for Linux (WSL) was Microsoft’s way of luring them back.
<!-- - People who came to Linux for any reason and found themselves at home. -->

<!-- The city of Munich famously switched from Windows to Linux in 2004 and, equally famously, swapped back 10 years later. They’re now in the process of reverting to Linux. Barcelona’s transition from Windows to Linux is currently underway. They’re replacing all desktop applications with open-source alternatives. They’ll swap over to Linux when the only proprietary software in use is the operating system. The idea is the staff will already be familiar with the applications, so the hop to Linux will not be much of a culture shock. Using Linux at work might change what people feel comfortable running when they get home. --> <!-- Possibly partially outdated -->

<!-- In China, we might soon see a large spike in the number of people using Linux desktops as a result of the U.S. trade embargo with Huawei. Beijing has ordered every one of its government and public institutions to replace all computer equipment and software sourced from outside China, including Windows. They’ve also created their own Deepin-based Linux distribution to help them achieve this, called the Unity Operating System (UOS). --> <!-- Possibly partially outdated -->

<a id="whats-wrong-with-gnu-linux"></a>

## 1.14 What's wrong with GNU/Linux

If you can have your full productivity without any problems using GNU/Linux, then by all means, switching to GNU/Linux is a good, smart choice. Alas, for many people, this is science fiction. And stating *just use Linux* for every one is a wishful dream. Many can't cope with the switch. Hardware question is a gamble and at the end of the day, there are applications that you don't get. [^dedo-2019] However compromising for ideology could be worth it (see [Section: Philosophy of the GNU project](#philosophy-of-the-gnu-project)).

[^dedo-2019]: [Igor Ljubuncic - Windows 7 End of Support: What Next?, published 2019](https://www.dedoimedo.com/computers/windows-7-end-of-support-guide.html)

### Toolchains over products 

Unix people are all about infrastructure. They are plumbers and stonemasons. They design from the inside out, building mighty engines to solve abstractly defined problems like *How do we get reliable packet-stream delivery over unreliable hardware and links?* Unix people then wrap thin and often profoundly ugly interfaces around the engines. [^raymond-culture]

By contrast, macOS programmers are all about the user experience. They're architects and decorators. They design from the outside in, asking first *What kind of interaction do we want to support?* And then building the application logic behind it to meet the demands of the user-interface design. This leads to programs that are very pretty, but the infrastructure might be weak and rickety. [^raymond-culture]

In many ways this kind of parochialism (i.e. only being interested in small issues that happen in your local area, and not being interested in more "important" things) has served the unix people well. They are the keepers of the Internet. Their software and their traditions dominate serious computing (the applications where 24/7 reliability and minimal downtime is a must). There is no other software technical culture that comes anywhere close to the unix track record. And it is one to be proud of. [^raymond-culture]

The GNU/Linux developers are extremely good at building solid infrastructure, but the problem is that most of the computers in the world don't live in server rooms, but rather in the hands of end users. In early Unix days, before personal computers, the unix culture defined itself partly as a revolt against the priesthood of the mainframes, the keepers of the big iron. Later, they absorbed the power-to-the-people idealism of the early microcomputer enthusiasts. But today they are the priesthood. They run the networks and the big iron. And the implicit demand is that if one wants to use their software, one must learn to think like them. [^raymond-culture]

There is a deep ambivalence in the unix programmers attitude: A tension between elitism and missionary populism. They want to reach and convert the 92&nbsp;% of the world for whom computing means games and multimedia and glossy GUI interfaces and (at their most technical) light email, word processing and spreadsheets. They are spending major effort on projects like GNOME and KDE designed to give unix a pretty face. But they are still elitists at heart, deeply reluctant and in many cases unable to identify with or listen to the needs of the Aunt Tillies of the world. To non-technical end users, the software the unix people build, tends to be either bewildering and incomprehensible. Or clumsy and condescending. Or both at the same time. Even when the unix people try to do user-friendliness as earnestly as possible, they are woefully inconsistent at it. Many of the attitudes and reflexes they have inherited from old-school Unix are just wrong for the job. Even when they want to listen to and help Aunt Tillie, they don't know how. They give her "solutions" that she finds as daunting as her problems. [^raymond-culture]

The GNU/Linux people can turn aside from this, and remain a priesthood appealing to a select minority, a geek meritocracy focused on their historical role as the keepers of the software infrastructure and the networks. But if they do this, someone else will serve the people. Someone else will put themselves where the power and the money are. Someone else will own the future of 92&nbsp;% of all software. [^raymond-culture]

### Too much distribution(s)

GNU/Linux accounts for a tiny percentage of the overall desktop market share. The perennial one or two percent has been around roughly since 2005, and even if the actual share is higher than that, it's still a small and largely insignificant fraction. And yet, there are hundreds of GNU/Linux distributions populating this narrow, crowded arena (see [Wikipedia - Linux Distributions Timeline](https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg)). For an operating system with less than a few hundred million users worldwide, it's so fragmented, you could build a mosaic. There are a billion GNU/Linux implementations and incarnations, all of which almost entirely privately funded, run by a small team of people, and with uncertain future. [^dedo-2018]

[^dedo-2018]: [Igor Ljubuncic - Linux Fragmentation, published 2018](https://www.dedoimedo.com/computers/linux-fragmentation-sum-egos.html)

#### Volunteer efforts 

Most distributions are just volunteer efforts by passionate people working on what is essentially their hobby. There's absolutely nothing wrong with that. It's actually very cool that people can express themselves in a fun way. The problem is when these efforts are offered to the general public. Most people expect consumer products. Linux distributions are not made as consumer products, and going from a joint fun effort to a serious product takes huge amounts of time and effort. [^dedo-2020]

[^dedo-2020]: [Igor Ljubuncic - Linux Dissatisfaction, published 2020](https://www.dedoimedo.com/computers/linux-year-of-dissatisfaction.html)

#### Little actual variation

While the technology landscape feels big, complex and colorful, the actual variation in creativity and uniqueness is not that huge. Often, ideas build upon other ideas, with small changes and incremental improvements. This is also true of GNU/Linux, with its towering pyramid of distros and forks and still more forks, a whole cutlery division. Lots of stuff but not necessarily variety. [^dedo-ocsmag]

[^dedo-ocsmag]: [Igor Ljubuncic - Magnificent Seven unique Linux projects, published 2018](https://www.ocsmag.com/the-magnificent-seven-unique-linux-projects/)

#### Lack of resources

Lack of resources is always quoted as a big problem in the distro world, when it's almost entirely a self-imposed problem. Distributions are mostly developed by non-professionals (the word amateur is wrong here), who do so mostly in their spare time, to the best of their available abilities (financial, technical, temporal). Most of the projects have 3 to 4 people in the team, in the best case. You often hear about new distros forking, because A didn't get along with B. But how many times do you hear of a distro voluntarily relinquishing its manpower and code in favor of another? How often do distros merge? Imagine what happens if you ax distros 11-100 on DistroWatch list and distribute their resources among the top ten. You now have hundreds of people to work on the same project. [^dedo-2018]

### Too few GUI tools

For serving both casual and expert users, for cooperating with other computer programs, and whether the problem domain is naturally visual or not; Support for both a command language interface (see [Chapter 2, Section: Text interface has retained its utility](02-basic.md#retained-utility)) and a visual interfaces is important. But this not always the case with GNU/Linux. [^browny]

I am amazed that for example looking for a gui to edit the sudoers file (see [Chapter 9, Section: Visudo](09-multi-user.md#visudo)) I find this: A tread where everybody seems to defend the total lack of such a tool. If you have someone using a GUI tool and another of equal competence using CLI and the CLI user takes longer to accomplish that same action, then things are wrong from me. I don't know all the options of the sudoer file, and the format in which it is written, and so far refused to learn it. I do not use the sudoers file enough to justify the time investment. And if I can use a graphical tool, that spares me the effort? And works equally well? Am I a lazy slob because of not memorizing all command line parameters? Maybe. But I think users deserve a choice, because Linux is supposed to be all about choice. <!--And I don't agree with the statement: Who does not know how to use a text editor should just quit Linux. --> [^browny]

Many things can be done with the GUI already. And done well. Maybe these users are more Windows type users than true Linux wizzs, but they still further the proliferation of Linux and the nice perks we enjoy thanks to it (such as hardware drivers for so many products). And in my view it was this restrictive hardcore RTFM philosophy that is killing the Linux desktop. [^browny]

Some admins that I have met in my days are just stuck in the 1980's. They don't believe in choice and think somebody is uneducated if they don't (know how to) use vi (see [Chapter 8, Section: Vi](08-text-editors.md#screen-editor-vi)). I don't. I refused to learn such an archaic P.O.S. I don't see my invested time paying off, the hours and hours to memorize what command does what. I believe that a text editor is not a high tech piece of software, not anymore (we are now in 2020). Going to a four day seminar to learn how to edit text files is a thing that some people enjoy, but should never be forced on others or made mandatory. <!--I always chuckle at the outlandishness of statements of admins saying *Well, vi is the only editor installed.*--> [^browny]

Anyway, I will keep looking for a true visual editor for sudoers, not meaning visudo (see [Chapter 9, Section: Visudo](09-multi-user.md#visudo)), but visuals that actually work with a window manager and KDE or Gnome. Welcome to the 22nd century. In my view Linux has too few GUI tools. Using a CLI tool can be daunting. [^browny]

[^browny]: [User browny_amiga - Comment on linuxquestions.org, published 2011](https://www.linuxquestions.org/questions/linux-software-2/gui-web-interactive-etc-sudoers-editor-556310/)

### Some issues never get fixed

Things don't necesserily get fixed (ever). Something that was an issue in 2001 is still an issue in 2024. [^dedo-2020]

### Lack of consistency

You can run any desktop program in any desktop environment, but ones designed for certain desktop environment may look out of place or drag in other environments. For example, if you tried to run GNOME’s Nautilus file manager on KDE, it would look out of place, require you to install a variety of GNOME libraries, and probably start GNOME desktop processes in the background when you opened it. Or if you tried to use the Nemo file manager
developed by Linux Mint on another distribution such as Solus or Arch, it would lack shortcut icons because the feature is tied to the settings of the surrounding system. [^dedo-2020]

<!-- Saying Linux is all about a choice is rather incorrect. It's a choice in that you can choose the platform you want, but not necessarily be able to do anything you like with it. The inconsistency is everywhere, across the entire stack, both horizontally and vertically. Take any five random distributions, and you will notice the differences in: filesystem layout, boot mechanism, system configuration, desktop environment, packaging format, package management. Then, you cannot trivially port code from one distro to another. You cannot trivially port from one distro release to other releases, both backward and forward due to the intricate system of shared library versioning and dependencies. The commands to get certain actions done are completely different on various distros. Now, the rise of self-contained application formats is a partial attempt to resolve this (see [Chapter 4, Section: Self-contained application formats](04-installing.md#self-contained-application-formats)). -->

### Poor backward compatibility

Backward compatibility is not very good. On Windows, you can run applications created 20 years ago, without any modifications. This is mostly impossible in Linux, for various technological and maintenance reasons. There's work done in this field (see [Chapter 4, Section: Self-contained application formats](04-installing.md#self-contained-application-formats)), but we still haven't reached the level of seamless and transparent usability that ordinary people need and expect. [^dedo-2020]

### Poor graphical user interfaces

There's no pride. The look and feel of most distributions is outdated. Usability and accessibility in most distributions is bad and remains unresolved. Only a handful of distributions have good, legible fonts by default: Kerning, subpixel hinting, font contrast, color, all the fine bits that make reading a joy or a torture. [^dedo-2020] 

Most (cross-platform) frameworks haven't been designed to leverage Linux features. They have been rather designed to just spitt out builds for it. [^dedo-2020]

### Shortcomings in hardware support

It does feel like Linux is leaving old stuff behind. This is a paradox really. On one hand, Linux is well-known for being able to run on ancient low-end hardware, and pride itself for being able to do so. On the other hand, providing and maintaining support for an infinite amount of ancient systems is difficult. If you boot up a ten year old laptop after a long pause, and try using Linux on it yet again you will have problems finding Linux drivers for its graphics card, wifi or what not. While Windows drivers are easily and readily available. [^dedo-pavilion]

From roughly 2000 to 2015, we've observed steady progress and improvement in the overall usability of the Linux desktop. Including hardware support, filesystem, media support, and alike. Installing Nvidia drivers back then required to compiling stuff. MP3 and Flash support were not a given. NTFS write support was not obvious. And tons of things like this, until they were slowly, gradually resolved. [^dedo-2020]

From around 2015 onwards, nothing happened really. The Linux desktop has pretty much the same set of capabilities it had back then. True, the desktop as a platform has not changed much since, but the ecosystem around it has. And the Linux desktop has not caught up. Not only have things plateaued, in some areas there's real degradation of quality, manifesting itself in bugs and regressions. This can be quite disheartening, as you watch something you love and enjoy slowly wither away. [^dedo-2020]

The installation of drivers (like Nvidia) is not trivial. Doing it on say Kubuntu, Fedora, CentOS, or Slackware requires completely different procedures. Support is not trivial, fractional scaling is not trivial, video tearing still affects distros at random, performance is less than Windows, hybrid card support is flaky and nerdy at best. [^dedo-2020]

Linux generally hasn't been as stable as Windows for me. It took a while to get the Wifi drivers working on my laptop, and they only work with kernel 5, not 6. Bluetooth still doesn't work. I sometimes had problems with my package manager, and when tinkering, I almost bricked my whole system. I still dual boot. [^dedo-2020]

[^dedo-pavilion]: [Igor Ljubuncic - Ten year old HP doesn't boot modern distros, published 2021](https://www.dedoimedo.com/computers/hp-pavilion-linux-modern-distros.html)

<a id="why-switch"></a>

## 1.15 Why people switch to GNU/Linux 

### Windows updating at the most inopportune times

- I switched to Windows almost exclusively for a time after I bought a Surface Pro 3 (released 2014). While it is a great piece of hardware, Windows 10 became slow as it updated at the most inopportune times. There are few things more annoying than getting ready to project for a business meeting, and hoping and waiting the update will finish in time. After this happened on a business trip a few weeks ago, I made up my mind to switch back to Linux.
- The forced updates on Windows that sometimes took more than an hour when I needed my computer then and there. Linux doesn't update untill I want. [^redd]

[^redd]: [Comments on Reddit - What were your reasons for switching to linux?, accessed 2024](https://www.reddit.com/r/linuxquestions/comments/1c3mn9m/what_were_your_reasons_for_switching_to_linux/)

### Wanting to extend the life of an old device

- One day I decided to refresh my old laptop, and it ended up with Linux installation. 
- Around the end of the support for Windows 7, I spend like a week testing different Linux distributions and found the one I like. So when the end life for Windows 7 come, I switched to MX Linux.
- Windows stopped supporting my pc of that time and I had no money to buy a new one.
- Couldn't afford the Windows license fee.
- I was broke and pulling computers out of the trash. It’s amazing the amount of decent hardware is thrown away. I even was able to save a couple of Mac's with fried graphics cards, just by installing Linux, after I discovered I could boot the macs into safemode which bypass the gpu. Dumpster computing kept me going for a few years, and taught me how to build pc's. [^redd]

### Pricing

- I'm just tired of having to pay to use Mirosoft Office. Constant upgrades and updates, and their increasing progress toward a subscription model for everything.
- I am able to buy better components because I don't have to pay for Windows.
- The thing that got me started trying Linux back in the days was it feeling wrong to use pirated Windows when there was a totally free alternative that allegedly worked just the same. And even today the main reason that keeps me from using Windows on any of my machines is having to bother with licensing, payment and activation. It's just too much of a hassle. Need to assemble a new machine or VM, quickly? Just grab some spare parts and slap Linux on it. Nobody cares how many Linux systems I run. [^redd]

### Ad-free, usability, privacy

- Ads on the Windows Desktop and Start menu.
- Ever increasing number of mouse clicks to do most things.
- Settings pertaining to privacy reset.
- AI integration to extract even more telemetry from me. [^redd]

### Familiarity from workplace

- I deal with GNU/Linux in my business on a daily basis. [^redd]

### Curiosity

- I wanted something new.
- A mix of boredom and curiosity.
- I was 16 and wanted to be edgy and unique. 
- I played with GNU/Linux for decades before I made the permanent switch.
- I didnt really swtich to GNU/Linux, but more of, learned how to utilize it. [^redd]

### Features

- A lot of ways to do things automatically using things like shell scripts, UDEV rules, services, cron jobs. I can do X, every time Y happens. I am sure though, Windows also has some equivalents to that, I just didn't learn about them.
- I can modify my OS experience to fit my needs so I can work more efficiently. It also allowed me to understand some of the inner workings of my OS.
- Reason is that I am a data professional and I do modelling and deep learning, even though there is support for Windows for some of the libraries, GNU/Linux has a lot of support for all the libraries
- I use Kali, an OS that should only be installed in virtual machines. Not directly on host OS, because you are using semi-trusted tools. Something a DevOps Manager taught me.
- I'm a programmer. A lot of the things we use are either not available on Windows or you have to jump through some hoops to get there. Everything is divided in well defined modules and programs, that do specific things.
- Tiling window managers which organise windows into non-overlapping frames, dependant on mathematical formulas. This is opposed to the more common approach used by stacking window managers, which allow users to drag windows around, instead of windows snapping into a position. This allows for a different style of organization, although it departs from the traditional desktop metaphor. [^redd]
<!-- - There is a learning curve in each OS to be proficient. When you get to this level, I understand that you do not want to let the time investment go away. If you are really efficient with Windows, keep Windows. -->

<a id="suggested-distributions"></a>

## 1.16 Suggested distributions

Recommending the best GNU/Linux distribution is a highly subjective, a biased view based on a person's personal interpretation and perception. But even within the scope of this book we cannot refrain from listing even some GNU/Linux distributions worth considering, such as:
- [Solus Budgie](https://getsol.us/) is good for home users migrating from Windows.
- [Fedora Workstation](https://fedoraproject.org/en/workstation/) is a long standing choice by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds).
- [Trisquel](https://trisquel.info) is a long standing choice by [Richard Matthew Stallman](https://en.wikipedia.org/wiki/Richard_Stallman). [^rms-computing]
- [Ubuntu LTS](https://ubuntu.com/download/desktop) is used by many educational institutions.
- [Debian](https://www.debian.org/) is used by many companies.
- [Clear Linux](https://clearlinux.org/) by Intel Corporation boasts many performance optimizations.
- [Tiny Core Linux](http://www.tinycorelinux.net/) is ultra small and designed to run from RAM.

<!--- [Debian](https://www.debian.org/) and [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) are used by many companies.-->

[^rms-computing]: [Stallman.org - How I do my computing, accessed 2025](https://www.stallman.org/stallman-computing.html)

> [!IMPORTANT]
> Some companies and institutions have their own in-house distribution unavailable to outsiders.

> [!NOTE] 
> Detailed distribution specific installation instructions are beyond the scope of this book. However a high-level overview of an installation process for a generic GNU/Linux is provided in [Chapter 10, Section: Installing GNU/Linux](10-additional.md#installing-gnulinux).

### Important terminology when choosing a distribution

#### Stable

**Stable** means unchanging. As a consequence most packages are dated, even 2-3 years old. Debian is considered one of the stability kings, running very old apps, sometimes even with bugs fixed long ago. Stable does not mean that there are less crashes on the system. Or that the updates are less frequent or smaller in size.

Stable distributions follow a fixed schedule for releasing new major versions. At the beginning of a support period, the software developers impose a **feature freeze**. They can make patches to correct software bugs and vulnerabilities, but do not introduce new features. At the conclusion of the support period, the product reaches end-of-life.

The support period can be long or short. **Long Term Support (LTS)** is primarily aimed at enterprise use, where there may be more resistance to 1) frequent updates and 2) especially agressive plans for adopting new software architecture such as SELinux or Wayland. The point is to build on top of an existing stable release cycle by delivering new versions on a predictable schedule that have a clearly defined support lifecycle. [^wiki-long]

[^wiki-long]: [Wikipedia - Long-term support, accessed 2024](https://en.wikipedia.org/wiki/Long-term_support)

#### Rolling

**Rolling** means continuous delivery of feature updates. Software packages on a rolling system are mostly up to date. Rolling does not mean that there are more crashes on the system. New software packages are usually tested before pushing them out to users.

#### Immutable

**Immutable** is a concept where a base system exists in read-only form, modularized into containers. Critical modules and areas can thus be better protected. Also what you can do is rebase parts of the operating system. You can easily switch a module with a single command, avoiding the need to reinstall and reconfigure the system. Take all the changes that were committed on one branch and replay them on a different branch.

#### Derivative

**Derivative** distributions are essentially the same as their base distributions but with custom configurations that add complexity and may increase the likelihood of issues. Derivative distributions might lack the quality assurance of their upstream counterparts, increasing risk to more frequent problems. Any appealing configuration found in a derivative distribution can usually be implemented on the upstream distribution.

#### Proficient

Every now and then you come across a Linux distribution that is recommended only if you are a proficient Linux user. But what does it mean to be proficient? In my opinion, Linux competence is based on an understanding of Linux-specific vocabulary and concepts, the ability to follow written instructions and the ability to identify outdated instructions or their unsuitability for your environment.

<!-- # References -->

[^raymond-open]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 19<!--. Open Source-->, Section: Unix and Open Source](http://www.catb.org/~esr/writings/taoup/html/ch19s01.html)

[^raymond-best]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 16<!--. Reuse-->, Section: The Best Things in Life Are Open](http://www.catb.org/~esr/writings/taoup/html/ch16s04.html)

[^raymond-origins]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 2<!--. History-->, Section: Origins and History of Unix<!--, 1969-1995-->](http://www.catb.org/~esr/writings/taoup/html/ch02s01.html)

[^raymond-new]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 19<!--. Open Source-->, Section: Programming in the New Unix<!-- Community-->](http://www.catb.org/~esr/writings/taoup/html/opensourcechapter.html)

[^raymond-wars]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 2<!--. History-->, Section: TCP/IP and the Unix Wars<!--: 1980-1990-->](http://www.catb.org/~esr/writings/taoup/html/ch02s01.html)

[^raymond-problems]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 20<!--. Futures-->, Section: Problems in the Environment<!-- of Unix-->](http://www.catb.org/~esr/writings/taoup/html/ch20s04.html)

[^raymond-culture]: [<!--Eric Steven Raymond - -->The Art of Unix Programming 2003, Chapter 20<!--. Futures-->, Section: Problems in the Culture<!-- of Unix-->](http://www.catb.org/~esr/writings/taoup/html/ch20s05.html)





