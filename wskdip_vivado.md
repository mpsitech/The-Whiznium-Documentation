[back](./README.md)

# Creating The Whiznium StarterKit Device Vivado IP From Scratch

In preparation for the following instructions, clone the [Whiznium StarterKit Device Git repository](https://github.com/mpsitech/wskd-Whiznium-StarterKit-Device). If your development workstation is set up with Whiznium StarterKit, this step may have taken place already and the location is ``${WHIZDEVROOT}/rep/wskd``.

## Creating the project and importing sources

Launch Vivado and perform the following steps for setting up the IP project:

- in __Quick Start__, select __Create Project >__, then click __Next >__ on the __New Project__ dialog
- on the __Project Name__ tab, choose "wskd_core" as __Project name__ and ``/home/mpsitech/fpgacode`` as __Project location__; hit __Next >__ twice
- on the __Add Sources__ tab, click __Add Files__ and navigate to ``${WHIZDEVROOT}/rep/wskd/fpgawskd/arty``, then select all (.vhd) files, click __OK__, then __Next >__ twice
- on the __Default Part__ tab, either select the __Part__ "xc7z020clg400-1" or the __Board__ "Arty Z7-20", hit __Next >__ then __Finish__

## Configuring modules from the IP catalog

Some VHDL modules are instantiated as black boxes and require configuration from the Xilinx IP catalog. For this, navigate to __Window__ -> __IP Catalog__.

The mixed-mode clock manager for use in ``Top.vhd`` is configured as follows:

- select __FPGA Features and Design__ -> __Clocking__ -> __Clocking Wizard__
- set __Component Name__ to "Mmcm_div2"
- in __Output Clocks__, set "clk_out1" __Output Freq (MHz)__ -> __Requested__ to 50
- also de-dselect the __locked__ optional output
- finalize by hitting __OK__

The MIPI-CSI receiver for use in ``Camacq.vhd`` is configured as follows:

- select __FPGA Features and Design__ -> __IO Interfaces__ -> __SelectIO Interface Wizard__
- set __Component Name__ to "Mipirx_w2"
- in __Data Bus Setup__, choose __Data Rate__ "DDR", select __Serialization Factor__ and set it to 8
- additionally, choose __External Data Width__ 2 and __Type__ "Differential" with __Standard__ "LVDS 25"


The dual-port BlockRAM's for use in ``Camacq.vhd`` and ``Featdet.vhd`` are configured as follows:

Spbram_size2kB_w8
Spbram_size4kB_w8

Dpbram_size2kB_a8b8

- select __Memories & Storage Elements__ -> __RAMs & ROMs & BRAM__ -> __Block Memory Generator__
- set __Component Name__ to "Dpbram_size58kB_a8b32"
- in __Basic__, set the __Memory Type__ to "True Dual Port RAM"
- in __Port A Options__, set __Write/Read Width__ to 8 and __Write/Read Depth__ to 59392
- additionally, select __Primitives Output Register__
- in __Port B Options__, set __Write/Read Width__ to 32
- additionally, de-select the __Primitives Output Register__
- finalize by hitting __OK__

Repeat the procedure for "Dpbram_size96kB_a8b32":

- in __Port A Options__, set __Write/Read Depth__ to 98304
- additionally, de-select __Primitives Output Register__
- else, as above

A large number of math functions are required for the pipelined algorithm in ``Featdet.vhd``. They are preferentially implemented using dedicated DSP48 primitives.

Adders are configured as follows:

- select __Math Functions__ -> __Adders & Subtracters__ -> __Adder/Subtracter__
- set __Component Name__ to "Add_a23b23s24"
- in __Basic__, change __Implement using__ to "DSP48", __A/B Input Width__ to 23 and __Output Witdh__ to 24
- furthermore, change __Latency Configuration__ to "Automatic" which should calculate __Latency__ to be 2
- finalize by hitting __OK__

Repeat the procedure for the remaining three adder types of the project:

- for "Add_a23b21s23", in __Basic__, __A Input Width__ to 23, __B Input Width__ to 21 and __Output Witdh__ to 23; else, as above
- for "Add_a21b21s22", in __Basic__, __A/B Input Width__ to 21 and __Output Witdh__ to 22; else, as above
- for "Add_a22b22s23", in __Basic__, __A/B Input Width__ to 22 and __Output Witdh__ to 23; else, as above

Multipliers are configured as follows:

- select __Math Functions__ -> __Multipliers__ -> __Multiplier__
- set __Component Name__ to "Mult_a23b23p46"
- in __Basic__ -> __Input Options__, set __A/B Width__ to 23
- furthermore, change __Multiplier Construction__ to "Use Mults"
- in __Output and Control__, select __Use Custom Output Width__ and set __Output MSB__ to 45
- also, set __Pipeline Stages__ to 4 and enable __Clock Enable__
- finalize by hitting __OK__

Repeat the procedure for "Mult_a24b24p48":

- in __Basic__ -> __Input Options__, set __A/B Width__ to 24
- in __Output and Control__, set __Output MSB__ to 47
- else, as above

The single product module is configured as:

- select __Basic Elements__ -> __DSP48 Macro__
- set __Component Name__ to "Prod_a9b9p18"
- in __Instructions__, set "A*B" for __0__
- in __Pipeline Options__, switch to "By Tier" and select __Tier__ 5
- furthermore, enable the __Control port__ "CE/Global"
- in __Implementation__, set __Input Port Properties__ A/B to 9
- finalize by hitting __OK__

Subtracters are configured as follows:

- select __Math Functions__ -> __Adders & Subtracters__ -> __Adder/Subtracter__
- set __Component Name__ to "Sub_a46b46s47"
- in __Basic__, change __Implement using__ to "DSP48", __A/B Input Width__ to 46, __Add Mode__ to "Subtract" and __Output Witdh__ to 47
- furthermore, change __Latency Configuration__ to "Automatic" which should calculate __Latency__ to be 2
- finalize by hitting __OK__

Repeat the procedure for "Sub_a47b44s48":

- in __Basic__, change __A Input Width__ to 47, __B Input Width__ to 44 and __Output Witdh__ to 48
- else, as above

Three-input adders are configured as follows:

- select __Basic Elements__ -> __DSP48 Macro__
- set __Component Name__ to "Threesum_a18c20d18p21"
- in __Instructions__, set "(A+D)+C" for __0__
- in __Pipeline Options__, switch to "By Tier" and select __Tier__ 4 and 6
- furthermore, enable the __Control port__ "CE/Global"
- in __Implementation__, set __Input Port Properties__ D/A to 18 and C to 20
- finalize by hitting __OK__

Repeat the procedure for "Threesum_a18c18d18p20":

- in __Implementation__, set __Input Port Properties__ D/A/C to 18
- in addition, switch __Output Properties__ to "User Defined" and __Width__ to 20
- else, as above

## Test-synthesizing and publishing the IP

Synthesizing the design ensures no errors are present, simplifying debugging of the parent design:

- click on __Run Synthesis__, a step which will take several minutes on first execution

Finally package the IP for re-use in the parent design, for this, navigate to __Tools__ -> __Create and Package New IP__. Perform the following steps:

- click __Next >__ then select "Package your current project" under __Packaging Options__, hit __Next >__ again
twice, then __Finish__
- the __Package IP__ tab opens, where with __Review and Package__ -> __Re-Package IP__, the relevant output can be generated.

During this last step, the folder ``wskd_core.srcs/sources_1/imports/arty`` is written which can subsequently be imported into the parent design.

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
