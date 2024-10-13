# CDTux

> ![WARNING]
> This repository is no longer maintained and has been archived.
>
> Please consider using [rrpi](https://github.com/CDSoft/rrpi) or [fu](https://github.com/CDSoft/fu) instead.

CDTux is my GNU/Linux "distribution"...
In fact a set of scripts to install some useful softwares
for programmers on Ubuntu and Raspbian.

[CDTux]: http://cdsoft.fr/cdtux
[Post Install]: http://cdsoft.fr/pi

[CDTux] is a set of scripts to complete the installation of several Linux
devices for my personal needs (programming oriented).
It can be in some way tuned for other situations.

It configures a fresh 64 bit Ubuntu or Raspbian installation with I3,
some programming languages and a few other things...

**Caution**: make backups,
read carefully and understand the source code before running this script.
You have been warned ;-)

CDTux is based on my outdated [Post Install] script
but I made some different choices:

- Ubuntu based to have richer and more up-to-date repositories
- 64 bits because I don't have 32 bit machine anymore
- also Raspbian to play with my Raspberry Pi

Installation
============

Currently this script has been tested on
Ubuntu 16.10 (Qemu, desktop computer and laptop)
and Raspbian (Raspberry Pi 3).

## Quick procedure

1. Install Ubuntu, Raspbian...

2. Execute `cdtux`:

~~~~~~~~~~ sh
sudo apt update
sudo apt install git
git clone https://github.com/CDSoft/cdtux
cd cdtux
./cdtux
~~~~~~~~~~

3. Edit `~/.cdtuxrc` and restart `cdtux` if necessary

4. Need to know more about CDTux? *Use the source, Luke!*

## Longer procedure

### Ubuntu on a regular PC

[Ubuntu]: https://www.ubuntu.com/download
[CDKey]: http://cdsoft.fr/cdkey

This should be pretty easy.

If you have a CD reader on your computer, just download [Ubuntu],
burn the ISO and boot it.

If you want to install Ubuntu from a USB key,
you can try my [CDKey] script to build a bootable key.

### Raspbian on a Raspberry Pi

[Raspbian]: https://www.raspberrypi.org/downloads/raspbian/

This may be a little bit trickier.
I describe here a way to install and configure [Raspbian]
without any keyboard or screen connected to the Raspberry Pi.
You will need an other computer to connect to the Raspberry Pi with `ssh`.
If you have a screen and a keyboard it should be easier.

#### Download and extract [Raspbian].

The lite version is enough for me.

~~~~~~~~~~ sh
wget https://downloads.raspberrypi.org/raspbian_lite_latest
unzip *-raspbian-*-lite.zip
~~~~~~~~~~

#### Flash the image on a SD card

Reference: <https://www.raspberrypi.org/documentation/installation/installing-images/linux.md>

Let's assume the SD card is `/dev/sdc`.
Be very careful not to destroy one of your hard disk!

~~~~~~~~~~ sh
sudo dd bs=4M if=$(ls *-raspbian-*.img) of=/dev/sdc
~~~~~~~~~~

#### Prepare the SD card for the first boot

SSH is not enabled by default for security reasons (<https://www.raspberrypi.org/blog/a-security-update-for-raspbian-pixel/>).
Let's enable it (remember that the SD card is still assumed to be `/dev/sdc`).

~~~~~~~~~~ sh
mkdir /tmp/sdcard
sudo mount /dev/sdc1 /tmp/sdcard
sudo touch /tmp/sdcard/ssh
sudo umount /tmp/sdcard
sync
~~~~~~~~~~

This will create a file named `ssh` on the boot partition.

#### First boot

1. Put the SD card in the Raspberry Pi SD card reader.
2. Plug the power supply as well as an ethernet cable.
3. Connect to the Raspberry Pi with `ssh`.

Well, you need to know the IP address of the Raspberry Pi.
Your home network is probably configured to give IP addresses
in a classical subnetwork (`192.168.0.0/24`).

You can use `nmap` (*on your desktop or laptop*)
to discover the Raspberry Pi IP address:

~~~~~~~~~~ sh
sudo apt install nmap
nmap -sP 192.168.0.0/24
sudo nmap -sS -p 22 192.168.0.0/24
~~~~~~~~~~

Hopefully you see something like a Raspberry Pi...
Just connect and configure it with `raspi-config`:

~~~~~~~~~~ sh
ssh -X pi@192.168.0.XX
raspi-config
~~~~~~~~~~

The default password is `raspberry`.

In `raspi-config` you can:

- expand the filesystem to use the whole SD card (you will need to reboot)
- change the password
- enable ssh permanently (otherwise you will have to recreate the `ssh` file as before)
- enable everything you want

### Install CDTux

You are now ready to execute the `cdtux` script
on your new Ubuntu or Raspbian installation.

Just install `git` and download `cdtux`:

~~~~~~~~~~ sh
sudo apt update
sudo apt install git
git clone https://github.com/CDSoft/cdtux
cd cdtux
./cdtux
~~~~~~~~~~

You will have sometimes to provide your password to gain `root` privileges.

### Some specificities for Raspbian on Raspberry Pi

**Erlang/Elixir**: When asked for a distribution name, enter `jessie`

Configuration
=============

The configuration file `.cdtuxrc` is a single bash script used to configure [CDTux].

No more documentation written yet. *Use the source, Luke!*
