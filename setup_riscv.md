[back](./README.md)

# Setting Up A New PolarFire SoC Yocto SDK For Use With Whiznium

The following instructions have been tested on a Linux workstation running ubuntu 20.04.

## Preparation

The first two sections of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md), "Enabling WhizniumSBE to provide an SDK-specific initialization script" and "Installing prerequisites", need to be performed before proceeding.

## Building the image

The Embedded Linux image to be built is intended for Microchip's PolarFire SoC Icicle kit. This is one of the reference targets of MPSI Technologies' starter kit. As of July 2021, Yocto 3.1 (code name dunfell) is used along with the Linux kernel 5.6.16.

The instructions roughly follow Microchip's [BSP repository README](https://github.com/polarfire-soc/meta-polarfire-soc-yocto-bsp).

- starting from ``/home/<username>``, prepare the folder structure
```
mkdir emb
mkdir emb/icicle
mkdir emb/icicle/wzsk
mkdir emb/icicle/wzsk/oe-core
cd emb/icicle/wzsk/oe-core
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
./repo init -u https://github.com/polarfire-soc/meta-polarfire-soc-yocto-bsp.git -b master -m tools/manifests/riscv-yocto.xml
./repo rebase
source ./meta-polarfire-soc-yocto-bsp/polarfire-soc_yocto_setup.sh
```

- edit the local build configuration in ``build/local.conf``: append the sections marked ``(mpsi)`` from the end of the file ``${WHIZDEVROOT}/setup/riscv/local.conf``

- apply a kernel patch which adds NFS client functionality and which also adds a custom driver, providing 32bit transfers across the AXI interconnect between Linux processing system (PS) and programmable logic (PL)
```
bitbake-layers create-layer meta-mpsi
rm -rf meta-mpsi/recipes-example
cp -r ${WHIZDEVROOT}/setup/riscv/meta-mpsi/recipes-kernel meta-mpsi/
```

- add the new layer by including ``emb/icicle/wzsk/oe-core/meta-mpsi \`` at the end of the file ``build/conf/bblayers.conf``

- run the first complete image build
```
MACHINE=icicle-kit-es bitbake mpfs-dev-cli
````

The procedure may take several hours with the final output reading something like this:

```
mpsitech@josh:~/emb/icicle/wzsk/oe-core/build$ MACHINE=icicle-kit-es bitbake mpfs-dev-cli
NOTE: Reconnecting to bitbake server...
Loading cache: 100% |#################################################################################################################| Time: 0:00:00
Loaded 3568 entries from dependency cache.
Parsing recipes: 100% |#################################################################################################################| Time: 0:00:00
Parsing of 2329 .bb files complete (2328 cached, 1 parsed). 3569 targets, 144 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION           = "1.49.0"
BUILD_SYS            = "x86_64-linux"
NATIVELSBSTRING      = "universal"
TARGET_SYS           = "riscv64-oe-linux"
MACHINE              = "icicle-kit-es"
DISTRO               = "nodistro"
DISTRO_VERSION       = "nodistro.0"
TUNE_FEATURES        = "riscv64"
meta                 = "HEAD:ea6f27e35b6cac4db9e1ab0d9a888d15daba6c09"
meta-oe              
meta-python          
meta-multimedia      
meta-networking      = "HEAD:69bae2a2360643805de2ae1cd9ebc4202cd5a2fb"
meta-riscv           = "HEAD:94ec885cec6f15bab5bc3bc617b8250b9aaf1b45"
meta-polarfire-soc-yocto-bsp = "HEAD:71caa6716459c57f24f9d5a9fd57d9585cf6305e"
meta-mpsi            = "<unknown>:<unknown>"

Initialising tasks: 100% |#################################################################################################################| Time: 0:00:03
Sstate summary: Wanted 0 Found 0 Missed 0 Current 1926 (0% match, 100% complete)
NOTE: Executing Tasks
NOTE: Tasks Summary: Attempted 5587 tasks of which 5587 didn't need to be rerun and all succeeded.
NOTE: Writing buildhistory
NOTE: Writing buildhistory took: 1 seconds
```

Subsequent runs will execute much faster with only the modified sections being rerun.

## Installing the SDK

The Yocto SDK is a folder structure on the workstation resembling the root file system on the target machine. It is produced using the following commands:
```
MACHINE=icicle-kit-es bitbake mpfs-dev-cli -c populate_sdk
cd build/tmp-glibc/deploy/sdk
./oecore-x86_64-riscv64-toolchain-nodistro.0.sh
Enter target directory for SDK (default: /usr/local/oecore-x86_64): /home/<username>/emb/icicle/wzsk/sdk
```

By selecting the target directory as ``/home/<username>/emb/icicle/wzsk/sdk``, the setup is consitent with the reference location of ``${WHIZROOT}`` and ``${WHIZSDKROOT}`` of the _machine_ ``any;yocto;riscv64;ubuntu_riscv64_wzsk``.

## Preparing an SD card

Please follow the instructions provided in the same section of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md).

## Writing the boot partition

These commands copy the u-boot bootloader packaged e.g. with the device tree information onto the boot partition:
```
cd build/tmp-glibc/deploy/images/icicle-kit-es
sudo cp boot.scr.uimg /mnt/emb_boot
sudo cp fitImage /mnt/emb_boot
```

## Writing the root file system

This command populates the (larger) root file system partition; here, an archive is extracted:
```
sudo tar xf core-image-minimal-dev-icicle-kit-es.tar.gz --no-same-owner -C /mnt/emb_rootfs
````

Finally, the SD card can be ejected like this:
```
sync
sudo umount /mnt/emb_boot
sudo umount /mnt/emb_rootfs
````

## Building the Whiznium specifics

Please follow the instructions provided in the same section of [Setting Up A New Yocto SDK For Use With Whiznium](./setup_yocto.md) - with the differences that now the path to the initialization script folder becomes ``/home/<username>/whiznium_dev/init/ubuntu_riscv64_wzsk`` and the machine postfix becomes ``_riscv``.

## Bulk-copying the Whiznium folder to the SD card

While later during development there are multiple options of downloading executables to the target, it is advisible to perform the initial fill by a direct copy operation to the SD card. The required commands are:
```
source ${WHIZDEVROOT}/init/ubuntu_riscv64_wzsk/init.sh
sudo mount /dev/sdb2 /mnt/emb_rootfs
cp ${WHIZDEVROOT}/setup/riscv/init.sh ${SYSROOT}/home/root
cd ${SYSROOT}/home/root
sudo cp init.sh /mnt/emb_rootfs/home/root/
sudo cp -r whiznium /mnt/emb_rootfs/home/root/
sync
sudo umount /mnt/emb_rootfs
```

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
