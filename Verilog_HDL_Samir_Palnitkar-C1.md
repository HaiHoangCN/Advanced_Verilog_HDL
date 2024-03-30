# Chapter 1: Overview of Digital Design with Verilog HDL

## 1.1. Evolution of Computer-Aided Digital Design
- Vacuum tubes => Transistors => ICs (Logic gates on a single chip)
- First ICs are SSI (Small Scale Integration) chips ~ gate count small => MSI (Medium) => LSI (Large) ~ EDA (Electronic Design Automation).
- CAD (Computer-Aided Design) tools ~ back-end tools (function related to route, place, chip layout).
- CAE (Computer-Aided Engineering) tools ~ front-end processes like HDL simulation, logic synthesis, timing analysis...
- Today, EDA is used for both CAD & CAE interchangeably => For simplicity, all design tools are EDA tools.
- VLSI (Very-large) more than 100,000 transistors.

## 1.2. Emergence of HDLs
- HDLs allow designers to model the concurrency of processes in hardware elements.
- Verilog HDL and VHDL are popular. Verilog HDL originated in 1983 at Gateway Design Automation. Later, VHDL was developed under contract from DARPA. Both simulates large digital circuits.
- Designers still have to manually translate HDL-based design into a schematic circuit with interconnections between gates.
- Digital circuits could be described at a RTL (register transfer level) by HDL.
- Details of gates and interconnections are automatically extracted by logic synthesis tools from RTL description.
- HDLs used for system-level design, simulation of system boards, interconnect buses, FPGAs (Field Programmable Gate Arrays) and PALs (Programmable Array Logic).
- Verilog HDL accepted by IEEE standard (IEEE 1364 - 2001).

## 1.3. Typical Design Flow
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/8ed7ef86-8cb8-4e1e-8c09-2e88dda304a0" height="600">

- Figure: Design VLSI IC circuits (Unshaded blocks - level of design representation, Shaded blocks - processes in design flow).
- ***SPECs*** describe abstractly functionality, interface, overall architecture of digital circuit to be designed, don't care how to implement this circuit.
- A behavioral description: 
