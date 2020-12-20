[back](./README.md)

# WhizniumDBE glossary

Expressions and abbreviations which are commonly used in WhizniumDBE models and WhizniumDBE-generated code.

expression|context|description|
---|---|---|
AXI|RTL code, C++ code|Advanced eXtensible Interface conceived by ARM as an interconnect for SoC's ; used by Xilinx to link its Zynq's ARM-based processing system (PS) to programmable logic (PL)|
buffer transfer|RTL code, C++ code|bulk read or write data transfer from/to a inter-module buffer connected to the host interface - as opposed to parameter passing in commands|
command invocation buffer|RTL code|in the full model, this on-FPGA buffer ensures non-blocking transmission of command invocations from the host|
command return buffer|RTL code|in the full model, this on-FPGA buffer ensures non-blocking transmission of commend returns from controllers|
controller|RTL code, C++ code|module for which commands can be defined|
core|RTL code|template, either manufacturer (Xilinx) supplied or as part of the WhizniumDBE parametric module generation|
device|project definition|grouping entity for systems|
easy model|project definition|low-FPGA-footprint implementation of a WhizniumDBE device, with blocking command invocation/return and buffer transfers. Cascades systems are not possible|
forwarding controller|RTL code|in the full model, this type of controller serves as virtual host, allowing to cascade units|
FSM|RTL code|finite state machine, a sub-category of a VHDL process|
full model|project definition|high-throughput and -performance implementation of a WhizniumDBE device, with non-blocking command invocation/multiuple returns and step-wise buffer transfers|
host interface|RTL code|automatically generated module which connects the host via SPI/UART/AXI/PCIe to controllers and inter-module buffers|
inter-module buffer|RTL code|dual-port RAM in FPGA to perform directional data transfers, e.g. from a processing module to the host interface|
machine|C++ code|computer or deployment target|
project|project definition|topmost entity for a WhizniumDBE project - a project has multiple versions|
release|project definition|results in a makefile set for a device, specific to a machine|
RTL|RTL code|register-transfer level, logic based on clock edge-triggered manipulation of physical 0's and 1's, described in VHDL|
system|C++ code|grouping entity for targets|
target|C++ code|definition of the cascaded arrangement of units|
tixV...|RTL code, C++ code|index referring to a byte-vector, e.g. tixVCommand is the variable used to refer to the vector CtrMsddZedbTrigger::VecVCommand|
unit|RTL code, C++ code|one unit represents one (FPGA-based or µC-based) hardware board|
vector|RTL code, C++ code|enumerated non-extensible list of identifiers, used e.g. to set up an address space for a unit's controllers|
version|project definition|technically the topmost entity when working with WhizniumDBE, as each version comprises the full project model definition|
