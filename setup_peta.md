[back](./README.md)

# Setting Up A New PetaLinux SDK For Use With Whiznium

The following instructions have been tested on a Linux workstation running ubuntu 20.04. Xilinx's PetaLinux version was 2020.1.

## Preparation

As also PetaLinux is based on the Yocto project, the first two sections of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md), "Enabling WhizniumSBE to provide an SDK-specific initialization script" and "Installing prerequisites", need to be performed before proceeding.

In addition, PetaLinux needs to be installed, its download location can be found [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-design-tools/2020-1.html). On the reference system, the install location was chosen to be ``/opt/Xilinx/petalinux-v2020.1``.

## Building the image

The Embedded Linux image to be built is intended for Digilent's Cora Z7 development board. This is one of the reference targets of MPSI Technologies' starter kit. As of December 2020, Yocto 3.0 (code name zeus) is used which corresponds to the Linux kernel 5.4.

- starting from ``/home/<username>``, prepare the folder structure
```
mkdir emb
mkdir emb/plnx
mkdir emb/plnx/wzsk
cd emb/plnx/wzsk
source /opt/Xilinx/petalinux-v2020.1/settings.sh
```

- create a PetaLinux project and configure it with the current Whiznium StarterKit Device (_wskd_) FPGA bit file:
```
petalinux-create --type project --template zynq --name Arty-Z7-10
cd Arty-Z7-10
petalinux-config --get-hw-description ${WHIZDEVROOT}/setup/plnx
```

- in Kconfig showing up change the file root file system to SD card, by following _Image Packaging Configuration_ -> _Root filesystem type_ and selecting _EXT3_. _Save_ and _Exit_.

To conform to the target board and to provide additional needed packages for Whiznium projects and Whiznium StarterKit in particular, it is required to overwrite ``project-spec/meta-user/recipes-bsp/device-tree/files/system-user.dtsi`` and 
``project-spec/meta-user/conf/user-rootfsconfig`` by the respective counterparts in ``${WHIZDEVROOT}/setup/plnx``.

The changes are applied by invoking ``petalinux-config -c rootfs``, and selecting all _User packages_, followed by _Save_ and _Exit_.

A custom driver, providing 32bit transfers across the AXI interconnect between Linux processing system (PS) and programmable logic (PL) needs to be integrated in the Linux kernel. This is achieved by generating a corresponding Kernel module
```
petalinux-create -t modules --name arty --enable
````

The driver file ``project-spec/meta-user/recipes-modules/arty/files/arty.c`` needs to be replaced with the provided file ``${WHIZDEVROOT}/setup/plnx/arty.c``.

- run the first complete image build
```
petalinux-build
```

The procedure may take several hours with the final output reading something like this:

```
mpsitech@josh:~/emb/plnx/wzsk/Arty-Z7-10$ petalinux-build
INFO: sourcing build tools
[INFO] building project
[INFO] sourcing build environment
[INFO] generating user layers
[INFO] generating workspace directory
INFO: bitbake petalinux-image-minimal
WARNING: Host distribution "ubuntu-20.04" has not been validated with this version of the build system; you may possibly experience unexpected failures. It is recommended that you use a tested distribution.
Parsing recipes: 100% |###############################################################################################################| Time: 0:02:20
Parsing of 2962 .bb files complete (0 cached, 2962 parsed). 4231 targets, 189 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies
NOTE: Fetching uninative binary shim from file:///home/mpsitech/emb/plnx/wzsk/Arty-Z7-10/components/yocto/downloads/uninative/9498d8bba047499999a7310ac2576d0796461184965351a56f6d32c888a1f216/x86_64-nativesdk-libc.tar.xz;sha256sum=9498d8bba047499999a7310ac2576d0796461184965351a56f6d32c888a1f216
WARNING: Your host glibc verson (2.31) is newer than that in uninative (2.30). Disabling uninative so that sstate is not corrupted.
Initialising tasks: 100% |############################################################################################################| Time: 0:00:03
Checking sstate mirror object availability: 100% |####################################################################################| Time: 0:00:21
Sstate summary: Wanted 1096 Found 760 Missed 336 Current 0 (69% match, 0% complete)
NOTE: Executing Tasks
NOTE: Setscene tasks completed
NOTE: Tasks Summary: Attempted 3840 tasks of which 771 didn't need to be rerun and all succeeded.

Summary: There were 2 WARNING messages shown.
INFO: Failed to copy built images to tftp dir: /tftpboot
[INFO] successfully built project
````

Subsequent runs will execute much faster with only the modified sections being rerun.

## Installing the SDK

The Yocto SDK is a folder structure on the workstation resembling the root file system on the target machine. It is produced using the following commands:
```
petalinux-build --sdk
cd images/linux
./sdk.sh
Enter target directory for SDK (default: /opt/petalinux/2020.1): /home/<username>/emb/plnx/wzsk/sdk
```

By selecting the target directory as ``/home/<username>/emb/plnx/wzsk/sdk``, the setup is consitent with the reference location of ``${WHIZROOT}`` and ``${WHIZSDKROOT}`` of the _machine_ ``any;yocto;armv7;plnx;ubuntu_plnx_wzsk``.

## Preparing an SD card

Please follow the instructions provided in the same section of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md).

## Writing the boot partition

These commands will generate a boot binary file and copy it - along with a u-boot bootloader - to the boot partition:
```
petalinux-package --boot --force --format BIN --fsbl images/linux/zynq_fsbl.elf --fpga images/linux/system.bit --u-boot
sudo cp images/linux/BOOT.BIN /mnt/emb_boot/
sudo cp images/linux/boot.scr /mnt/emb_boot/
sudo cp images/linux/image.ub /mnt/emb_boot/
```

The Cora Z7 board does not come with an EEPROM to store its MAC address. Rather, the address can be found printed on a sticker on its backside. To make sure the board presents its correct MAC address to the network, it needs to be specified in the file ``${WHIZDEVROOT}/setup/plnx/uEnv.txt`` before being copied to the boot partition using
```
sudo cp ${WHIZDEVROOT}/setup/plnx/uEnv.txt /mnt/emb_boot/
```

## Writing the root file system

In analogy to the boot partition, these commands populate the (larger) root file system partition:
```
cd images/linux
sudo tar xf rootfs.tar.gz --no-same-owner -C /mnt/emb_rootfs
```

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
```

## Building the Whiznium specifics

Please follow the instructions provided in the same section of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md) - with the differences that now the path to the initialization script folder becomes ``/home/<username>/whiznium_dev/init/ubuntu_plnx_wzsk`` and the machine postfix becomes ``_plnx```.

## Bulk-copying the Whiznium folder to the SD card

While later during development there are multiple options of downloading executables to the target, it is advisible to perform the initial fill by a direct copy operation to the SD card. The required commands are:
```
sudo mount /dev/sdb2 /mnt/emb_rootfs
cp ${WHIZDEVROOT}/setup/plnx/init.sh ${SYSROOT}/home/root
cd ${SYSROOT}/home/root
sudo cp init.sh /mnt/emb_rootfs/home/root/
sudo cp -r whiznium /mnt/emb_rootfs/home/root/
sync
sudo umount /mnt/emb_rootfs
```

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
