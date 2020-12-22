[back](./README.md)

# Setting Up The Whiznium StarterKit Project

Building the Whiznium StarterKit project (developed using WhizniumSBE) is straightforward. It involves cross-compilation of the sources for the C++ SQLite database access library ``dbswzsk`` and the C++ _combined daemon_ ``wzskcmbd``. The compilation results, along with the web-based UI files and a customized preferences file are then deployed on the target.

A single script, ``${WHIZDEVROOT}/setup/wzsk/setup_wzsk_yocto.sh`` performs the required actions for the currently two reference targets, Embedded Linux (Toradex Apalis i.MX6) and FPGA (Digilent Arty Zynq).

Edit the first two lines of ``${WHIZDEVROOT}/setup/wzsk/setup_wzsk_yocto.sh`` to read
```
export set INITPATH=/home/<username>/whiznium_dev/init/ubuntu_tdx_wzsk
export set MCHPOSTFIX=_tdx
```
for the Embedded Linux target and
```
export set INITPATH=/home/<username>/whiznium_dev/init/ubuntu_plnx_wzsk
export set MCHPOSTFIX=_plnx
```
for the FPGA target, respectively.

The setup script can now be executed using:
```
cd ${WHIZDEVROOT}/setup/wzsk
chmod 755 setup_wzsk_yocto.sh
./setup_wzsk_yocto.sh
```

- adapt the ``Wzskcmbd`` preferences file ``${SYSROOT}${WHIZROOT}/bin/wzskcmbd/PrefWzskcmbd.xml``:<br>
	``<StgWzskGlobal.fpgaNotV4l2gpio> = true`` (FPGA target only)<br>
	replace all ``${WHIZROOT}`` by ``/home/root/whiznium``

- copy the updated target SDK folder ``${SYSROOT}${WHIZROOT}`` to the SD card

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
