#### INTRODUCTION

Let’s cut the bullshit, this project is based on Arch Linux and designed with Pentest, Security and Development in mind for the best experience. This installation script of Arch Linux is based on the excellent work of [picodot.dev](https://github.com/picodotdev). The main purpose of this script is to make the Arch Linux installation process easier with a special touch for the Arch Linux Lovers with the aim to promote the culture of pentest and security IT environment.

* * *

#### KEYS FEATURES

Before you try these alternative Arch Linux installation method, I highly recommend installing Arch Linux in the traditional way from the command line, step-by-step using this [tutorial](https://cybsploit.com/2020/02/23/how-to-install-arch-linux-with-lvm-and-luks-disk-encryption-YzZyRVdDUVZDeHV4MEZYYXBWZU44Zz09) in order for you to gain a deeper understanding of your system and and what goes into installing a desktop Linux operating system.


**What exactly does this script do?**

This method of installing Arch Linux automates the entire installation process of Arch Linux.

**Keys Features**

- System support for UEFI and BIOS Mode
- HDD support for SATA NVMe and MMC Disk
- SSD TRIM support compatibility
- Disk SWAP support enable/disable
- Logical Volume Management on LUKS
- Encrypted Root Partition
- File system formats EXT4, BTRFS and XFS
- Arch Mirror Optimization using Reflector
- Support for "mkinitcpio" Ramdisk Environment
- GRUB bootloader installation and configuration
- Detect and install "Intel processors microcode"
- Enable Arch Linux "Multilib"
- Install advanced linux sound architecture (ALSA)
- Graphical Drivers Installation (Radeon, Nvidia, Intel)
- Install Gnome Desktop Environment
- Install GDM Display managers
- Install VirtualBox Guest Utils
- Full user creation process along with "sudoers" configuration
- Common packages installation

* * *

#### INSTALLATION

**Download a Copy of Arch Linux ISO**

To start in the right order, you'll have to visit the [official Arch download](https://www.archlinux.org/download/) page to copy the most recent Arch Linux ISO link as well as the sha1sum text file link. As soon as you have them, simply open your terminal to execute the following commands, without forgetting to replace the links present in the below example by the one you just grab from the Arch Linux website.

```bash
cd /tmp/

# Replace the ISO link and filename if needed
wget -O archlinux-2020.02.01-x86_64.iso http://mirrors.evowise.com/archlinux/iso/2020.02.01/archlinux-2020.02.01-x86_64.iso

# Replace the sha1sum link and filename if needed
wget -O sha1sums.txt http://mirrors.evowise.com/archlinux/iso/2020.02.01/sha1sums.txt
```

**Verify the ISO Signature**

It is recommended to verify the image signature before to move further, especially when downloading from an HTTP mirror. To do this, we'll simply compare the "sha1sum" from the text file we downloaded previously with a generated "sha1sum" of our ISO.

```bash
sha1sum=$(cat "sha1sums.txt" | head -n1 | awk '{print $1;}')
echo "${sha1sum}" /tmp/archlinux-2020.02.01-x86_64.iso | sha1sum -c
```

**Creating a Bootable Arch Linux USB Drive**

Creating a bootable Arch Linux USB key in a Linux environment is easy. Once you've downloaded and verified your Arch Linux ISO file, you can use the "`dd`" command to copy it over to your USB stick using the following procedure. Plug your USB drive into an available USB port on your system, and run the following command to write the ISO image to your USB drive.

```bash
sudo fdisk -l
```

Once you identified the path of your USB drive, run the below command to create your bootable Arch Linux USB key.

```bash
dd if=/tmp/archlinux-2020.02.01-x86_64.iso of=/usb/path status=progress bs=4M && sync
```

The block size parameter "`bs`" can be increased, and while it may speed up the operation of the "`dd`" command, it can occasionally produce unbootable USB drives, depending on your system and a lot of different factors. The recommended value, "`bs=4M`", is conservative and reliable.

**Boot from the Live USB**

Once you are ready with your bootable Arch Linux USB drive, shut down your system. Plugin your USB and boot your machine again.

<a class="gallery-item" href="https://cybsploit.com/uploads/posts/2020/02/how-to-install-arch-linux-with-lvm-and-luks-disk-encryption-1.png" data-fancybox="How to Install Arch Linux with LVM and LUKS Disk Encryption" data-options="{'caption':'How to Install Arch Linux with LVM and LUKS Disk Encryption'}"><img src="https://cybsploit.com/uploads/posts/2020/02/how-to-install-arch-linux-with-lvm-and-luks-disk-encryption-1.png" alt="How to Install Arch Linux with LVM and LUKS Disk Encryption"/></a>

**Important:** You may be unable to boot from live USB if **secure boot** is enabled on your system. In such a case you must first disable the secure boot option from your BIOS panel.

**Configure Default Keyboard**

The default keyboard layout in the live session is US. You can list out all the supported keyboard layout using the below command:

```bash
ls /usr/share/kbd/keymaps/**/*.map.gz
```

If you need to change the keyboard layout, you can do it using "`loadkeys`" command. For example, if we want a French keyboard, this is what you'll use:

```bash
loadkeys fr-latin1
```

**Connect to the internet using Ethernet Cable**

Ensure your network interface is listed and enabled invoking the "`ip`" command:

```bash
ip link
```

If your network interface is not yet enabled, you can enable it using:

```bash
# Replace "interface" with your current Ethernet adapter name for example "eth0"
ip link set "interface" up
dhcpcd
```

You can now verify the connection doing a simple ping as follow:

```bash
ping archsploit.org -c 3
```

Or

**Connect to the Internet using Wireless Connection**

Like the above method, you must ensure your network interface is listed and enabled. Once you are done with this step, you can connect to your WiFi network using the following command:

```bash
# Replace "passphrase" with the password of your WiFi network and "SSID" with your network name
wpa_passphrase "passphrase" | wpa_supplicant -B -i "SSID" -c /dev/stdin
dhcpcd
```

In the same way as above, we'll verify the connection using the ping command:

```bash
ping archsploit.org -c 3
```

**Launch The Installation Script**

When you are ready, you will need to grab and configure the installation script. In order to do it, simply use the following command:

```bash
# Download the script and configuration file using wget
wget -O - https://archsploit.org/download.sh | bash

# Edit the archsploit.conf script with nano
nano archsploit.conf

# Execute the script
./archsploit.sh
```

For more information on how this automated script works, I encourage you to watch the video below.

[![Video](https://img.youtube.com/vi/tmGLHk2-rBE/maxresdefault.jpg)](https://www.youtube.com/watch?v=tmGLHk2-rBE)

**Installation of the Pentest Packages**

Designed to be fast, easy to use and provide a minimal yet complete desktop environment. Archsploit let's you choice which Pentest Packages you want to install on your target system. Once you have completed the installation, you will be able to select which packages category you want to setup in your environment. In order to do it, simply log into your machine, open your terminal and use the following commands.

```bash
# List all available Pentest Packages
archsploit-packages -h

# Install specific packages category
archsploit-packages -i <category>

# Install all packages categories
archsploit-packages -i all
```
