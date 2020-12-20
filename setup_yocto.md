- install prerequisites
sudo apt-get install device-tree-compiler
from yocto manual at https://www.yoctoproject.org/docs/current/brief-yoctoprojectqs/brief-yoctoprojectqs.html
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
     build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
     xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
     pylint3 xterm

- set up tdx sdk
(roughly following https://developer.toradex.com/knowledge-base/board-support-package/openembedded-core)

mkdir emb
mkdir emb/tdx
mkdir emb/tdx/wzsk
mkdir emb/tdx/wzsk/oe-core
cd emb/tdx/wzsk/oe-core

curl https://storage.googleapis.com/git-repo-downloads/repo > ./repo
chmod 755 repo
git config --global user.email "aw@mpsitech.com"
git config --global user.name "Alexander Wirthmueller"

./repo init -u https://git.toradex.com/toradex-manifest.git -b dunfell-5.x.y -m tdxref/default.xml
./repo sync
. export

- edit build/local.conf (for reference, check setup/tdx/resources/local.conf, last lines marked (mpsi))
uncomment line MACHINE ?= "apalis-imx6"

- run first complete build
bitbake -k tdx-reference-minimal-image
bitbake -k console-tdx-image -c populate_sdk

(TBD: add mpsi layer for OV5640 patch)
(TBD: .dtb execrise starting out from build directory)
(+ create SD card)
(+ ln ...)
