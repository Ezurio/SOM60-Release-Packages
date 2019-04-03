# SOM60-Release-Packages
SOM60 Development Kit and Source Releases.  For source release instructions and a getting started guide, jump to the intoduction. For binary development kit images and a prebuilt SDK, see the releases page linked below. Source releases require binaries from the development kit binary releases.  For these binaries and the development kit binary images, also see the link below:

<https://github.com/LairdCP/SOM60-Release-Packages/releases>

# Introduction
## Purpose
The reference guide is intended to provide an embedded developer with the information needed to start evaluating and integrating the 60 Series SOM for their connectivity and embedded Linux processing needs.  The guide is designed to walk the developer integrating the 60 Series SOM though the same process Laird developers use to develop our own boxed products. This allows multiple levels of Laird's customer support team to assist with customer integrations.
## Product Overview
Laird’s 60 Series SOM, based on the Microchip SAMA5D36 processor, brings all of Laird’s industry competence and capabilities into one solution. The SOM provides superior enterprise-class Wi-Fi connectivity with full support for 2x2 MU-MIMO 802.11ac WLAN, plus Bluetooth 4.2 dual-mode. This solution is equipped with a power efficient Cortex A5 applications processor, wireless and wired connectivity, enterprise-grade security, LCD support, and comprehensive Linux board support package (BSP). The 60 SOM is the ideal system on module for devices that require superior connectivity. Complete with the Sterling 60 series module and Summit Software Stack, the SOM provides superior wireless connectivity in harsh RF environments. For wired connectivity, it supports dual-Ethernet and CAN bus. The 30mm x 30mm form factor and variety of interfaces allow the 60 Series SOM to be used as a wireless bridge, main processing unit, or IoT gateway.
# Hardware Information
## 60 Series SOM
For full hardware specifications, please see [Datasheet - 60 Series SOM](https://connectivity-staging.s3.us-east-2.amazonaws.com/2019-02/CS-DS-60-SOM%20v1_2.pdf) on our website.
## 60 Series SOM Development Kit
The DVK-SU60-SOMC development kit is intended for evaluating the features and software of the 60 Series SOM module.  The 60 Series SOM module is soldered to the development board and all its relevant hardware interfaces have been brought out onto the DVK-SU60-SOMC. An optional DVK-SU60-SOMC-LCD board is available to enabled evaluation of the graphics and touchscreen capabilties of the 60 Series SOM module.
### Kit Contents
The development kit contains the following:
* DVK-SU60-SOMC development board
* External dipole antenna (2) – LSR 001-0009
* Stand-offs (4)
* Nuts (4)
* Power supply – 12V 2A (1)
* SMA to IPEX pigtail cable – 110 mm (2)
* USB A to Micro USB – 1200 mm (1)
* Product insert card (1)

### Specifications
![SOM60 DVK Spec](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_kit_spec.jpg?raw=true)
### Block Diagram
![SOM60 Block Diagram](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_block_diagram.jpg?raw=true)
### Board Overview
![SOM60 Labeled](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_labeled.jpg?raw=true)
### Board Components
![SOM60 Interface Con](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_board_interface_con.jpg?raw=true)
### Pin Header Definition
![SOM60 Pin Headers](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_pin_headers.jpg?raw=true)
### Powering Up the Board
To power up the board, follow these steps:
1. Unpack the board. Be careful to avoid electrostatic discharge.
2. Ensure VDDIOP0 and VDDIOP1 is configured to 3.3V by adjusting the slide switch SW3 and jumper SW4.
3. Unpack the power supply, select the right power plug adapter corresponding to that of your country, and plug it into your AC outlet.
4. Connect the power supply's DC barrel plug to the DC jack (CON8) on the DVK-SU60-SOMC.

### Using the Debug Console
Connect the USB-to-Micro USB cable from your computer to the Debug UART (USB1) on the DVK-SU60-SOMC. During development and evaluation, a serial console program is required.  Laird recommends the use of minicom on Linux or PuTTY on Windows. If using the recommended Ubuntu operating system for evaluation or development, you can install minicom as follows:

* `sudo apt install minicom`


### Booting From SD Card
### Booting From Embedded NAND Flash
### Booting From SAMBA
![SOM60 NAND Deselect](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_nand_deselect.jpg?raw=true)
### Using UART Directly Without FDTI Converter
![SOM60 UART Wire Out](https://github.com/LairdCP/content_imgs/blob/master/som60/dvk_som60_uart_wire_out.jpg?raw=true)
# Software Information
## Prerequisites
### Linux Development Environment Setup
These are Laird's recommendation for setting up a development environment for use with Laird's Buildroot based Linux board support package.
#### Ubuntu
Laird recommends Ubuntu 16.04 as the base operating system for your development. All instructions in this reference guide assume a developer on an Ubuntu 16.04 system.
#### SSH
Laird makes extensive use of GitHub and having proper Secure Shell (SSH) access to our repositories on GitHub. If you haven't set up SSH, you can use the instructions below to enable SSH for use with GitHub.
1. Check whether your private key (~/.ssh/id_rsa) and public key (~/.ssh/id_rsa.pub) files exist
  1. `$ ls -1 ~/.ssh/id_rsa*`
2. If they do not, generate them
  1. `$ ssh-keygen`
    1. Accept default file paths
    2. Accept no passphrase
3. View your public key
  1. `$ cat ~/.ssh/id_rsa.pub`

#### git
Laird delivers the Laird Linux board support package using git repositories. If you haven't set up git, you can use the instructions below to enable git for use with GitHub.
* Install and configure the "git" package
  1. `$ sudo apt install git`
  2. `$ git config --global user.name "John Doe"`
  3. `$ git config --global user.email "john.doe@yourcompany.com"`
  4. `$ git config --list`
    1. Expect user.name=John Doe
    2. Expect user.email=john.doe@yourcompany.com

#### repo
Laird uses the repo tool from the Android project to pull down and correctly layout the git repositories that comprise the Laird Linux board support package. To install repo on Ubuntu, use the instructions below.
* `$ sudo apt install repo`

You can also get it by following the instructions here:
* (https://source.android.com/source/downloading.html#installing-repo)

#### Github Account
Laird Linux board support packages are availabe on GitHub. The most seamless workflow throughout a integration is to set up a GitHub account (https://github.com/) and add your SSH public key to you GitHub account. Instructions for setting up a GitHub account and adding an SSH key are below.
1. Go to (https://github.com/join) and follow the instructions.
2. Once you have a GitHub account add your public SSH key generated previously.
  1. View your public key
    1. `$ cat ~/.ssh/id_rsa.pub`
  2. This should be similar to:
    1. `ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDW5HxCJe56MZKkGxtHU2hkb1uyuJ3i+AFZNnSIApiDe1l1H9Y40YjBF+sE47GKgNuzQIMqKZ6xjRdb8KxvtjQIE/VcSiz9KIaFtKce/wKKxy0vOXbskSLzELlA9ovY9AJmp3qUaW+BEChnggERjPvq+1oyiKGRJzo51j/CQr+Yx8c2MtKubjHknKkQ2Th8kxL1bQj4lVgyfqNGj3DXUz9S+kTm+dLnmmOXlUfxx8Khrb7j0Dg+lk1lqeolqt6aFwpMnb8V2h5lDevJ0YSSyId01OnaAnIlx1lc+zauctsgtZf5Htl9cXS7Cp3OCMfSa+IKFeFL9/ku9C25EdA5zOnt your@email.com`
  3. Copy the contents of the above output to you clipboard
  4. Follow the instructions at
	 (https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) starting with Step 2.

## Laird Linux
### Overview
Laird Linux is Laird's board support package specifically tailored for Laird's SOMs and customer's connectivity driven use cases. Laird regularly updates Laird Linux by merging in the upstream Linux kernel and Buildroot. We merge in major long-term support kernel releases which allow our SOMs to utilize the latest in drivers and kernel space functionality, performance enhancements, security, and bug fixes.  Also, we merge in major long-term support Buildroot releases which provide for the latest in over 2200 user space applications and libraries. Laird Linux takes this solid upstream heritage and integrates our custom platform enhancements for connectivity, security, and power consumption.

### Buildroot
The core piece of Laird Linux is [Buildroot](https://buildroot.org/). Buildroot is a from source build system designed to allow the customer to create a customized Linux image for a target embedded computing module. Buildroot is capable of configuring and building the toolchain, bootloader, kernel, and rootfs for Laird's SOMs. Buildroot's core build system technologies are the well-known and easy to understand [make](https://en.wikipedia.org/wiki/Make_(software)) build tool and [kconfig](https://www.kernel.org/doc/Documentation/kbuild/kconfig-language.txt) configuration tool. This enables easy build customization through the user interface tools [menuconfig](https://en.wikipedia.org/wiki/Menuconfig) or xconfig and Buildroot make commands. The [Linux kernel](https://www.kernel.org/), [U-Boot bootloader](http://www.denx.de/wiki/U-Boot/WebHome), and [Busybox core userspace ulilities toolkit](https://en.wikipedia.org/wiki/BusyBox) all use make, Kconfig, and menuconfig. Build and configuration concepts found in one translate nicely to another. Buildroot has easy to read and extensive documentation available at (https://buildroot.org/docs.html) in pdf, html, and ascii form.  If time permits, Laird highly recommends following the Training section of the documentation landing page.

Laird's Buildroot is a fork of the upstream [Buildroot stable](https://git.busybox.net/buildroot/). Starting with and merging upstream allows Laird to know the authenticity of Buildroot's source code and better verify the security of our fork. Laird targets [long-term support releases (LTS)](https://buildroot.org/download.html) for merging into our Buildroot fork.

### Linux Kernel
Laird's kernel is a fork the upstream [Linux stable kernel](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/). Starting with and merging upstream allows Laird to know the authenticity of the kernel's source code and better verify the security of our fork. Laird targets [long-term support releases (LTS)](https://www.kernel.org/category/releases.html) for merging into our kernel fork.

### Versioning
Laird Linux releases follow an A.B.C.D versioning scheme. Rolling the A.x.x.x digit indicates we have merged a new major LTS kernel version and created a new git branch. Once we merge the new LTS kernel, B.C.D go to 0.0.0.0. For example the 6.0.0.x releases are based on the 4.14.x LTS kernel and the 7.0.0.x releases are based on the 4.19.x LTS kernel. All new A.0.0.x releases also merge the latest LTS Buildroot. For example the 6.0.0.x releases are based on the 2018.02.x LTS Buildroot and the 7.0.0.x releases are based on the 2019.02.x LTS Buildroot. Laird rolls the x.B.x.x digit to indicate that a new major LTS Buildroot has been merged on a specific A.x.x.x LTS kernel after its initial Buildroot release. The x.x.C.x digit is reserved for future use. The x.x.x.D digit indicates the build number for that A.B.C.x release.

### Release Types
Laird Linux has two branch and release types. Every A.0.0.x branch of Laird Linux will have at minimum two releases, one release (R1) in Q2 and another (R2) in Q4 of the first year it is released. Certain Laird Linux branch will be declared long-term support branches. These long-term support branches will consist of 5 releases instead of the standard 2. The LTS branches will have the normal Q2 (R1) and Q4(R2) releases in their first calendar year, a Q2 (R3) and Q4 (R4) release in their second calendar year, and a final Q2 (R5) release in their third calendar year. This will allow for 2 years of support on LTS branch from the first year's Q2 release to the final year's Q2 release.

## Getting started with a Developer's SD Card Image and a SDK
This section will walk a developer through following:

* [Downloading a developer's SD card image](#downloading-a-developers-sd-card-image)
* [Flashing a developer's SD card image](#flashing-a-developers-sd-card-image)
* [Using a prebuilt SDK](#using-a-prebuilt-sdk)
* [Downloading the board support package source code](#downloading-the-board-support-package-source-code)
* [Building the developer's SD card image](#building-the-sd-card-developers-image)
* [Creating a custom SDK](#create-a-custom-sdk)

### Downloading a developer's SD card image
Laird Linux releases include a prebuilt SD card image as a starting point for evaluating and integrating a Laird Linux release on a Laird SOM. For the 60 SOM, these prebuilt images are found on at [60 SOM release page](https://github.com/LairdCP/SOM60-Release-Packages/releases). These releases are named som60sd-laird-A.B.C.D.tar.bz2. These prebuilt SD card images are good for quickly testing a SOM running the latest software.

### Flashing a developer's SD card image
Once the image is downloaded. Extract the image:
```
~/Downloads/som60sd$ tar -xvf som60sd-laird-7.0.0.38.tar.bz2 
som60sd-laird-7.0.0.38/
som60sd-laird-7.0.0.38/som60sd-target-sbom-20190222
som60sd-laird-7.0.0.38/som60sd-host-sbom-20190222
som60sd-laird-7.0.0.38/u-boot-spl.bin
som60sd-laird-7.0.0.38/u-boot.itb
som60sd-laird-7.0.0.38/rootfs.tar
som60sd-laird-7.0.0.38/som60sd-sdk.tar.bz2
som60sd-laird-7.0.0.38/legal-info-20190222.tar.bz2
som60sd-laird-7.0.0.38/kernel.itb
som60sd-laird-7.0.0.38/mksdcard.sh
som60sd-laird-7.0.0.38/mksdimg.sh

```
To flash the image to an SD card use the mksdcard.sh script. The mksdcard.sh script takes the target device as an argument and will ask if you'd like to proceed with removing all data on your SD card and flashing a new image.  This is shown below:
```
~/Downloads/som60sd-laird-7.0.0.34$ sudo ./mksdcard.sh /dev/sdc
[sudo] password for user: 
*************************************************************************
WARNING: All data on /dev/sdc now will be destroyed! Continue? [y/n]
*************************************************************************
[Partitioning /dev/sdc...]
1024+0 records in
1024+0 records out
1048576 bytes (1.0 MB, 1.0 MiB) copied, 0.653846 s, 1.6 MB/s
DISK SIZE - 1967128576 bytes
Checking that no-one is using this disk right now ... OK

Disk /dev/sdc: 1.9 GiB, 1967128576 bytes, 3842048 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

>>> Created a new DOS disklabel with disk identifier 0x59c337f4.
Created a new partition 1 of type 'W95 FAT16 (LBA)' and of size 48 MiB.
/dev/sdc2: Created a new partition 2 of type 'Linux' and of size 1.8 GiB.
/dev/sdc3: 
New situation:

Device     Boot  Start     End Sectors  Size Id Type
/dev/sdc1  *      2048  100351   98304   48M  e W95 FAT16 (LBA)
/dev/sdc2       100352 3842047 3741696  1.8G 83 Linux

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
[Making filesystems...]
[Copying files...]
[Done]
```
You can now insert your SD card into the SOM hardware development kit and press the reset button to boot into the new SD card image.

### Using a prebuilt SDK

Laird Linux releases include a prebuilt SDK to start doing application development for a Laird SOM. For the 60 SOM, this prebuilt SDK is called som60sd-sdk-A.B.C.D.tar.bz2 and can be found with each release at the [60 SOM release page](https://github.com/LairdCP/SOM60-Release-Packages/releases). The prebuilt SDK includes the toolchain and all development files of the software packages used to generate the prebuilt SD card image from that release. The SDK can set up for use with an IDE to allow application developers to not need a full BSP on their system. To use the SDK, extract the SDK tarball then run the script relocate-sdk.sh (located at the top directory of the SDK), to make sure all paths are updated with the new location. For more information on using SDKs generated from Laird's Buildroot fork, see the [Buildroot manual's section on the SDK](https://buildroot.org/downloads/manual/manual.html#_advanced_usage).

### Downloading the board support package source code

First step, pick which release you want. Odds are you want the most recent of your release.

Next, use repo to initalize and fetch your release. This is a two-step process: first you tell repo which manifest to use and then you tell it to fetch everything.

    mkdir som60_6.0.0.132_source
    cd som60_6.0.0.132_source
    repo init -u git@github.com:LairdCP/SOM60-Release-Packages.git -m som60_6.0.0.132.xml
    repo sync

_Note: Repo will initialize a .repo directory and then place all files directly in the directory that you are in when you run the `repo` command. So we recommend making a subdirectory and working in there._

#### Buildroot cache
In order to speed up builds, set up a Buildroot cache to store sources that Buildroot will download. Off your home directory:

    mkdir ~/.br2_dl_dir

Then add it to your build environment:

    export BR2_DL_DIR="${HOME}/.br2_dl_dir"

### Building the SD Card developer's image
Once your repo sync is finished, you are ready to build your own SD card image. This can be achieved by the following:

    cd wb
    make som60sd

Once your build completes, you will find the output similar to below:
```
~/git/lrd-7.0.0.x/wb$ cd buildroot/output/som60sd/images/
~/git/lrd-7.0.0.x/wb/buildroot/output/som60sd/images$ ls -al
som60sd-target-sbom-20190222
som60sd-host-sbom-20190222
u-boot-spl.bin
u-boot.itb
rootfs.tar
som60sd-sdk.tar.bz2
legal-info-20190222.tar.bz2
kernel.itb
mksdcard.sh
mksdimg.sh

```
You can see that the SD card image and the mksdcard.sh script are included.

### Create a custom SDK
If you'd like to create a custom SDK from your customized source build, while in the target's output directory, issue a `make sdk`:
```
~/git/lrd-7.0.0.x/wb/buildroot/output/som60sd$ make sdk
```
