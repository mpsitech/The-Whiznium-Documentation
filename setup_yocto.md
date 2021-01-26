[back](./README.md)

# Setting Up A New Yocto SDK For Use With Whiznium

The following instructions have been tested on a Linux workstation running ubuntu 20.04.

## Enabling WhizniumSBE to provide an SDK-specific initialization script

All WhizniumSBE/DBE-generated Makefiles make use of environment variables to facilitate placing SDK's anywhere in the file system. By making changes to the WhizniumSBE initialization file at ``${WHIZDEVROOT}/projects/wznm/ini/IexWznmIni.xlsx``, WhizniumSBE gets all information it needs to writing out scripts containing these environment variables.

A new SDK is added by adding a new _machine_ to the initialization file. For use with the Whiznium StarterKit project, both with Toradex/Yocto and Xilinx/PetaLinux SDK's, two machines are already pre-configured, which provide the correct pathes with minor adaptations:

- in the section ``// IP machines --- BEGIN/END``, only for the ``any;ubuntu;default``, ``any;yocto;armv7;plnx;ubuntu_plnx_wzsk`` and ``any;yocto;armv7;tdx;ubuntu_tdx_wzsk`` machines, replace ``username`` in the paths by your user name

- save the initialization file as tab-separated text ``${WHIZDEVROOT}/projects/wznm/ini/IexWznmIni.txt``

- re-run the WhizniumSBE Bootstrap procedure described in the [WhizniumSBE Development Workflow](./sbe.md) document

- log into WhizniumSBE as any user
- in the menu _Navigation_, choose _Machines ..._
- for both ``ubuntu_plnx_wzsk`` and ``ubuntu_tdx_wzsk`` machines, select them in the list view
- in the _Machine_ menu, choose _Write initialization scripts ..._
- on the _Writing_ tab, hit _Execute_
- on the _File archive_ tab, hit _Download_
- unpack the downloaded archives into ``${WHIZDEVROOT}/init/ubuntu_plnx_wzsk`` and ``ubuntu_tdx_wzsk``, respectively

## Installing prerequisites

The build system requires some packages to be installed, the corresponding list was copied from the [Yocto project homepage](https://www.yoctoproject.org/docs/current/brief-yoctoprojectqs/brief-yoctoprojectqs.html):
```
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
     build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
     xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
     pylint3 xterm
```
On top, these packages are required to perform Whiznium (StarterKit) specific changes to the Embedded Linux image:
```
sudo apt-get install device-tree-compiler sqlite3
```

## Building the image

The Embedded Linux image to be built is intended for Toradex's Apalis i.MX6 compute module, mounted on an Ixora carrier board. This is one of the reference targets of MPSI Technologies' starter kit. As of December 2020, Yocto 3.1 (code name dunfell) is used which corresponds to the Linux kernel 5.4.

The instructions rougly follow Toradex's [knowledge base article](https://developer.toradex.com/knowledge-base/board-support-package/openembedded-core).

- starting from ``/home/<username>``, prepare the folder structure
```
mkdir emb
mkdir emb/tdx
mkdir emb/tdx/wzsk
mkdir emb/tdx/wzsk/oe-core
cd emb/tdx/wzsk/oe-core
```
- download the repo script and - if not already done so - set the local Git coordinates
```
curl https://storage.googleapis.com/git-repo-downloads/repo > ./repo
chmod 755 repo
git config --global user.email "yourname@yourcompany.com"
git config --global user.name "Firstname Lastname"
````
- run repo
```
./repo init -u https://git.toradex.com/toradex-manifest.git -b dunfell-5.x.y -m tdxref/default.xml
./repo sync
. export
```
- edit the local build configuration in ``build/local.conf``: uncomment the line ``MACHINE ?= "apalis-imx6"`` and append the sections marked ``(mpsi)`` from the end of the file ``${WHIZDEVROOT}/setup/tdx/local.conf``

- apply a kernel patch which adds functionality to the OV5640 camera driver
```
cd layers
bitbake-layers create-layer meta-mpsi
rm -rf meta-mpsi/recipes-example
cp -r ${WHIZDEVROOT}/setup/tdx/meta-mpsi/recipes-kernel meta-mpsi/
cd ..
```

- add the new layer by including ``${TOPDIR}/../layers/meta-mpsi \`` at the end of the file ``oe-core/build/conf/bblayers.conf``

- run the first complete image build
```
bitbake -k tdx-reference-minimal-image
````

The procedure may take several hours with the final output reading something like this:

```
mpsitech@josh:~/emb/tdx/wzsk/oe-core/build$ bitbake -k tdx-reference-minimal-image
Loading cache: 100% |#################################################################################################################| Time: 0:00:00
Loaded 3874 entries from dependency cache.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION           = "1.46.0"
BUILD_SYS            = "x86_64-linux"
NATIVELSBSTRING      = "universal"
TARGET_SYS           = "arm-tdx-linux-gnueabi"
MACHINE              = "apalis-imx6"
DISTRO               = "tdx-xwayland"
DISTRO_VERSION       = "5.1.0-devel-20201218083935+build.0"
TUNE_FEATURES        = "arm armv7a vfp thumb neon callconvention-hard"
TARGET_FPU           = "hard"
meta-toradex-nxp     = "HEAD:4087b01cd5c70f4656cdff26a4e7d7ecc73bf41f"
meta-freescale       = "HEAD:46f54fdc5ad854a22bf759aac7fd65db1d1bb574"
meta-freescale-3rdparty = "HEAD:05b1746a4adc240b690fe965ac5b8a043d9b9d03"
meta-toradex-tegra   = "HEAD:b5179b050062a29c2fe0bdfc1717b616c4f1630e"
meta-toradex-bsp-common = "HEAD:cab1ac409fa532c22f64c570f1b5c2350b570f94"
meta-oe              
meta-filesystems     
meta-gnome           
meta-xfce            
meta-initramfs       
meta-networking      
meta-mpsi      
meta-multimedia      
meta-python          = "HEAD:f2d02cb71eaff8eb285a1997b30be52486c160ae"
meta-freescale-distro = "HEAD:5d882cdf079b3bde0bd9869ce3ca3db411acbf3b"
meta-toradex-demos   = "HEAD:b962519c754bd918e99ff08e583f63ffb10757b0"
meta-qt5             = "HEAD:0d8eb956015acdea7e77cd6672d08dce18061510"
meta-toradex-distro  = "HEAD:48913ab629a231913e3e147e93e57f7cf6019ac6"
meta-poky            = "HEAD:c1c79c1a122b053fb3ce0187b3cc89df1bb3bdd6"
meta                 = "HEAD:b885888df67eb5cdb3b82f4f0a07369a449e223b"

Initialising tasks: 100% |############################################################################################################| Time: 0:00:04
Sstate summary: Wanted 2524 Found 0 Missed 2524 Current 0 (0% match, 0% complete)
NOTE: Executing Tasks
WARNING: htop-2.2.0-r0 do_fetch: Failed to fetch URL http://hisham.hm/htop/releases/2.2.0/htop-2.2.0.tar.gz, attempting MIRRORS if available
NOTE: Tasks Summary: Attempted 6902 tasks of which 1 didn't need to be rerun and all succeeded.
NOTE: Writing buildhistory
NOTE: Writing buildhistory took: 5 seconds

Summary: There was 1 WARNING message shown.
```

Subsequent runs will execute much faster with only the modified sections being rerun.

## Installing the SDK

The Yocto SDK is a folder structure on the workstation resembling the root file system on the target machine. It is produced using the following commands:
```
bitbake -k tdx-reference-minimal-image -c populate_sdk
cd build/deploy/sdk
./tdx-xwayland-glibc-x86_64-Reference-Minimal-Image-armv7at2hf-neon-apalis-imx6-toolchain-5.1.0.sh
Enter target directory for SDK (default: /opt/tdx-xwayland/5.1.0): /home/<username>/emb/tdx/wzsk/sdk
```

By selecting the target directory as ``/home/<username>/emb/tdx/wzsk/sdk``, the setup is consitent with the reference location of ``${WHIZROOT}`` and ``${WHIZSDKROOT}`` of the _machine_ ``any;yocto;armv7;tdx;ubuntu_tdx_wzsk``.

## Preparing an SD card

The typical SD card setup for Embedded Linux consists of a small FAT32 boot partition and a larger ext3 partition for the root file system. The following procedure can be followed to this end:

- insert an empty SD card into your workstation, possibly using a USB adapter
- find which block device the SD card is associated with using ``ls -l /dev/sd*``; in this example it is ``/dev/sdb``
- run ``sudo fdisk /dev/sdb`` to generate the two partitions; the result (``p`` command) should look something like
```
Device     Boot  Start      End  Sectors  Size Id Type
/dev/sdb1  *      2048   133119   131072   64M  b W95 FAT32
/dev/sdb2       133120 31116287 30983168 14,8G 83 Linux
```
- use e.g. GParted to format both partitions
- mount the partitions
```
sudo mkdir /mnt/emb_boot
sudo mkdir /mnt/emb_rootfs
sudo mount /dev/sdb1 /mnt/emb_boot
sudo mount /dev/sdb2 /mnt/emb_rootfs
```

## Writing the boot partition

These commands will extract a suitable u-boot bootloader along with all configuration files onto the boot partition:
```
cd build/deploy/images/apalis-imx6
sudo tar xf Apalis-iMX6_Reference-Minimal-Image.rootfs.bootfs.tar.xz --no-same-owner -C /mnt/emb_boot
```

In the default configuration, a PWM signal needed for driving the Whiznium StarterKit turntable is occupied by the display backlight. As a quick fix removing that dependency, the device tree binary generated by BitBake can be adapted by de- and re-compiling it:
```
dtc -I dtb -O dts imx6q-apalis-ixora-v1.2.dtb > imx6q-apalis-ixora-v1.2.dts
```
- in ``imx6q-apalis-ixora-v1.2.dts``, remove block ``backlight``, in the ``symbols`` block remove the line ``backlight``.
- re-compile and copy to the boot partition
```
dtc imx6q-apalis-ixora-v1.2.dts -o imx6q-apalis-ixora-v1.2.dtb
sudo cp imx6q-apalis-ixora-v1.2.dtb /mnt/emb_boot/
```

## Writing the root file system

In analogy to the boot partition, this command populates the (larger) root file system partition:
```
sudo tar xf Apalis-iMX6_Reference-Minimal-Image.rootfs.tar.xz --no-same-owner -C /mnt/emb_rootfs
````

An important missing link is added by executing
```
cd /mnt/emb_rootfs/lib/
sudo ln -s ld-linux-armhf.so.3 ld-linux.so.3
```

Finally, the SD card can be ejected like this:
```
sync
sudo umount /mnt/emb_boot
sudo umount /mnt/emb_rootfs
````

## Building the Whiznium specifics

Setting up Whiznium within a newly-built SDK is mostly equivalent to the procedure for the workstation as described in [Setting Up Whiznium On Your Workstation](./setup.md), section "Obtaining and setting up the folder structure". The key difference is that now, cross-compilation instead of native compilation takes place. The build results again comprise the sbecore and dbecore libraries along with the WhizniumSBE Engine Monitor project.

A single script, ``${WHIZDEVROOT}/setup/base/setup_base_yocto.sh`` performs the required actions for both reference targets currently supported, Embedded Linux (Toradex Apalis i.MX6) and FPGA (Digilent Arty Zynq).

Edit the first two lines of ``${WHIZDEVROOT}/setup/base/setup_base_yocto.sh`` to read
```
export set INITPATH=/home/<username>/whiznium_dev/init/ubuntu_tdx_wzsk
export set MCHPOSTFIX=_tdx
```

The setup script can now be executed using:
```
cd ${WHIZDEVROOT}/setup/base
chmod 755 setup_base_yocto.sh
./setup_base_yocto.sh
```

## Bulk-copying the Whiznium folder to the SD card

While later during development there are multiple options of downloading executables to the target, it is advisible to perform the initial fill by a direct copy operation to the SD card. The required commands are:
```
sudo mount /dev/sdb2 /mnt/emb_rootfs
cp ${WHIZDEVROOT}/setup/tdx/init.sh ${SYSROOT}/home/root
cd ${SYSROOT}/home/root
sudo cp init.sh /mnt/emb_rootfs/home/root/
sudo cp -r whiznium /mnt/emb_rootfs/home/root/
sync
sudo umount /mnt/emb_rootfs
```

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
