- set up plnx sdk

- download and install PetaLinux 2020.1
https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-design-tools/2020-1.html
	in this example, to /opt/Xilinx/petalinux-v2020.1

mkdir emb/plnx
mkdir emb/plnx/wzsk/
cd emb/plnx/wzsk
source /opt/Xilinx/petalinux-v2020.1/settings.sh

petalinux-create --type project --template zynq --name Arty-Z7-10
cd Arty-Z7-10
petalinux-config --get-hw-description setup/plnx/resources

- in Kconfig showing up, Image Packaging Configuration -> Root filesystem type -> EXT4
	Save -> Exit

petalinux-create -t modules --name arty --enable

overwrite project-spec/meta-user/recipes-modules/arty/files/arty.c
overwrite project-spec/meta-user/recipes-bsp/device-tree/files/system-user.dtsi
overwrite project-spec/meta-user/conf/user-rootfsconfig

petalinux-config -c rootfs
user packages -> select all
	Save -> Exit

petalinux-build
