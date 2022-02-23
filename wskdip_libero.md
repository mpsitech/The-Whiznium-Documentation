[back](./README.md)

# Creating The Whiznium StarterKit Device Libero SoC IP From Scratch

In preparation for the following instructions, clone the [Whiznium StarterKit Device Git repository](https://github.com/mpsitech/wskd-Whiznium-StarterKit-Device) into an auxiliary folder, e.g. to ``C:\Users\mpsitech\temp\wskd``.

## Creating the project and importing sources

Launch Libero SoC and perform the following steps for setting up the IP project:

- click on __Projects__ -> __New...__
- choose __Project name__ "wskd_core", __Project location__ ``C:\Users\mpsitech\fpgacode`` and select VHDL as __Preferred HDL type__, as well as __Enable block creation__
- click __Next >__
- select the "MPFS250T-FCVG484E" part and hit __Next >__ twice
- in __Add HDL Sources__, choose __Import file__, navigate to ``C:\Users\mpsitech\temp\wskd\fpgawskd\iccl`` and select all .vhd files
- click __Open__, then __Finish__
- in __Design Hierarchy__, click on __Build hierarchy__, then select "Iccl_ip_v1_0_S_AXI" as top module by right-clicking on it and selecting __Set as root__

## Configuring modules from the IP catalog

Some VHDL modules are instantiated as black boxes and require configuration from the Microchip IP catalog. All configuration in this section takes place in the __Catalog__ tab.

The MIPI stuff:

TBD

The clock conditioning circuit for use in ``Top.vhd`` is configured as follows:

- select __Clock & Management__ -> __Clock Conditioning Circuitry (CCC)__
- in the __Create Component__ dialog, set __Name__  to "Ccc_div2_5" and click __OK__
- in __Clock Options PLL__, set __Input Frequency__ to 125MHz
- in __Output Clocks__ -> __Output Clock 0__, set __Requested Frequency__ to 50MHz
- finalize by hitting __OK__

The dual-port SRAM blocks for use in ``Camacq.vhd``, ``Camif.vhd`` and ``Featdet.vhd`` are configured as follows:

- select __Memory & Controllers__ -> __PF Dual-Port Large SRAM__
- in the __Create Component__ dialog, set __Name__  to "Dpsram_size2kB_p8" and click __OK__
- in __Parameter settings__, choose "Rising edge" (for 'p')
- in __Port settings__ -> (both) __PortA/PortB Settings__ set __Depth__ to 2048 and __Width__ to 8
- furthermore enable __Block Select (A/B_BLK)__
- finalize by hitting __OK__

Repeat the procedure for the remaining three memory layouts of the project:

- for "Dpsram_size2kB_n8", in __Parameter settings__, choose "Falling edge" (for 'n'); else, as above
- for "Dpsram_size4kB_n8", in __Parameter settings__, choose "Falling edge"; in __Port settings__ -> (both) __PortA/PortB Settings__ set __Depth__ to 4096; else, as above
- for "Dpsram_size96kB_p8", in __Port settings__ -> __PortA Settings__ set __Depth__ to 98304; in __Port settings__ -> __PortB Settings__ set __Depth__ to 24576 and __Width__ to 32; else, as above

The two-port SRAM blocks for use in ``Camacq.vhd`` are configured as follows:

- select __Memory & Controllers__ -> __PF Two-Port Large SRAM__
- in the __Create Component__ dialog, set __Name__  to "Tpsram_size2kB_rn8_wp8" and click __OK__
- in __Parameter settings__, choose "Independent read/write clocks", then "Falling edge" (for 'n') for __Read clock (R_CLK)__ and "Rising edge" (for 'p') for __Write clock (W_CLK)__
- in __Port settings__ -> (both) __Write/Read Port Settings__ set __Depth__ to 2048 and __Width__ to 8
- furthermore select  __Write enable (W_EN)__ and __Read enable (R_EN)__
- finalize by hitting __OK__

Repeat the procedure for "Tpsram_size58kB_rp32_wp8":

- in __Parameter settings__, choose "Independent read/write clocks", then "Rising edge" for both __Read clock (R_CLK)__ and __Write clock (W_CLK)__
- in __Port settings__ -> __Write Port Settings__, set __Depth__ to 59392 and __Width__ to 8
- in __Port settings__ -> __Read Port Settings__, set __Depth__ to 14848 and __Width__ to 32
- else, as above

## Test-synthesizing and publishing the IP

Synthesizing the design ensures no errors are present, simplifying debugging of the parent design:

- in __Design Flow__, click on __Synthesize__, a step which will take several minutes on first execution

Make sure the many AXI-related ports are identified as one single bus:

TBD: first invocation is __Create Core from HDL ...__
- in __Design Hierarchy__, right-click on the topmost "Iccl_ip_v1_0_S_AXI" module and select __Edit Core Definition__
- click __Add/Edit bus interfaces ...__
- click __Add Bus Interface...__, select "AXI4, slave" and click __OK__
- re-name the "Bus interface (AXI4)" from "BIF_1" to "S_AXI" and automatically map the core signals by entering "S_AXI_" in the __Map by Name Prefix__ field and hitting __Map by Name__
- click __OK__ twice to close the dialogs

Finally publish the core for re-use in the parent design:

- in __Design Flow__, click on __Publish Block__ 
- de-select __Publish Placement__ and __Publish Region__, click __OK__
- save and close the projet

During the last step, the file ``designer\Iccl_ip_v1_0_S_AXI\Iccl_ip_v1_0_S_AXI.cxz`` is written which can subsequently be imported into the parent design.

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
