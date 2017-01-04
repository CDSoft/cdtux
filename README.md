# CDTux

My GNU/Linux "distribution"... In fact a set of scripts to install useful softwares for programmers on Ubuntu and Raspbian.

[CDTux]: http://cdsoft.fr/cdtux
[Post Install]: http://cdsoft.fr/pi

[CDTux] is a set of scripts to complete the installation of several Linux
devices for my personal needs (programming oriented).
It can be in some way tuned for other situations.

It configures a fresh 64 bit Ubuntu or Raspbian installation with I3,
some programming languages and a few other things...

**Caution**: make backups, read carefully and understand the source code before running this script.
You have been warned ;-)

CDTux is based on my outdated [Post Install] script but I made some different choices:

- Ubuntu based to have richer and more up-to-date repositories
- 64 bits because I don't have 32 bit machine anymore
- also Raspbian to play with my Raspberry Pi

Installation
============

Installation from GitHub:

    git clone https://github.com/CDSoft/cdtux
    cd cdtux
    ./cdtux

Configuration
=============

The configuration file `.cdtuxrc` is a single bash script used to configure [CDTux].

Documentation
=============

No documentation written yet. *Use the source, Luke!*

TODO
====

- Test on my desktop
- Test on my laptop
- Test on my Raspberry Pi

Currently these scripts have been tested on Ubuntu 16.10 on Qemu.
