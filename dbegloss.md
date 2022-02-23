[back](./README.md)

# WhizniumDBE glossary

Expressions and abbreviations which are commonly used in WhizniumDBE models and WhizniumDBE-generated code.

expression|context|description|
---|---|---|
AXI|RTL code, C++ code|Advanced eXtensible Interface conceived by ARM as an interconnect for SoC's; used e.g. by Xilinx to link its Zynq's ARM-based processing system (PS) to programmable logic (PL)|
buffer transfer|RTL code, C++ code|bulk read or write data transfer from/to a inter-module buffer connected to the host interface - as opposed to parameter passing in commands|
command|RTL code, C++ code|triggered by the host, invokes action on, or retrieves information from the device; invocation/return parameters may be added. Bytecode representation derived by WhizniumDBE|
command invocation buffer|RTL code|in the full model, this on-FPGA buffer ensures non-blocking transmission of command invocations from the host|
command return buffer|RTL code|in the full model, this on-FPGA buffer ensures non-blocking transmission of commend returns from controllers|
controller|RTL code, C++ code|module for which commands can be defined|
core|RTL code|template, either manufacturer supplied or as part of the WhizniumDBE parametric module generation|
device|project definition|grouping entity for systems (full model) or units (easy model)|
easy model|project definition|low-FPGA-footprint implementation of a WhizniumDBE device, with blocking command invocation/return and buffer transfers. Cascaded systems are not possible|
error|RTL code, C++ code|in the full model, used for abnormal rtermination of a command, optionally including parameters|
family|RTL code|grouping entity for silicon devices|
forwarding controller|RTL code|in the full model, this type of controller serves as virtual host, allowing to cascade units|
FSM|RTL code|finite state machine, a sub-category of a RTL process|
full model|project definition|high-throughput and -performance implementation of a WhizniumDBE device, with non-blocking command invocation/multiuple returns and step-wise buffer transfers|
host interface|RTL code|automatically generated module which connects the host via SPI/UART/AXI/PCIe to controllers and inter-module buffers|
insertion point|RTL code, C++ code|comment in source code, short form IP, indicating a spot into which code can be inserted manually|
inter-module buffer|RTL code|dual-port RAM in FPGA to perform directional data transfers, e.g. from a processing module to the host interface|
iteration|project definition|the process of letting WhizniumDBE generate a new version based on the previous version's source code tree and updated model files|
machine|C++ code|computer or deployment target with common e.g. compiler flags and library paths; hierarchical structure with parameter inheritance|
peripheral|RTL code|hard-wired functionality block in MCU devices|
project|project definition|topmost entity for a WhizniumDBE project - a project has multiple versions|
release|project definition|results in a makefile set for a device, specific to a machine|
RTL|RTL code|register-transfer level, logic based on clock edge-triggered manipulation of physical 0's and 1's, described in VHDL; WhizniumDBE also writes equivalent C code for MCU projects|
silicon device|RTL code|packaged FPGA or MCU device which can be used as template for units by specifying its pinout|
system|C++ code|in the full model, grouping entity for targets|
target|C++ code|definition of the cascaded arrangement of units|
tixV...|RTL code, C++ code|index referring to a byte-vector, e.g. tixVCommand is the variable used to refer to the vector CtrMsddZedbTrigger::VecVCommand|
unit|RTL code, C++ code|one unit represents one (FPGA-based or MCU-based) hardware board|
vector|RTL code, C++ code|enumerated non-extensible list of identifiers, used e.g. to set up an address space for a unit's controllers|
version|project definition|technically the topmost entity when working with WhizniumDBE, as each version comprises the full project model definition|
