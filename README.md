# **Advance Physical Design Workshop using openLANE/sky130pdk**
This repository contains the whole summary of khowledge acquired and hands on done by Krunal Badlani (IS21MTECH14008) during the workshop "Advance Physical Design Workshop using openLANE and Google - skywater 130 nm pdk" organised by VSD.

## *Contents*

## DAY 0
We are introduced to the platform and the flow of the workhop was explained. The Platform ( lab_instance 1 ) is a remote Linux based system hosted on a server on the cloud.

## Day 1
---

The day starts off with few sessions on:-
### Talking to Computers
---
- We are introduced to the internal structure of a computer using an example of a microcontroller board. 
- Terms like Board and chip design, Integrated circuits, die,packaging, IP and Foundry IP, and macros are explained.
- RISC-V instruction set architecture is introduced along with the mention of other popular architectures like ARM and x86. This is done because the design on which we are gonna work is RISC-V based picorv32a CPU core.
- An introduction to SoC is given i.e. what is a SoC, how is it laid out is explained using examples of processors, memories and IPs.

### SoC design and openLANE
---
-- The 3 important factors in ASIC design process are, 
1. RTL designs 
2. EDA tools 
3. Process design Kits (PDKs) 

And openLANE has made them OPENSOURCE !

### ASIC flow
- Specification
- RTL design
- Verification
- Synthesis 
- Floorplanning and power planning
- Placement
- Clock Tree Synthesis (CTS)
- Routing
- Sign-off 

Or in short the ASIC flow is the RTL to GDSII flow.

The flow can be divided into 2 parts the front end (Specifications to Verification) and the back end ( Synthesis to Sign-off). The openLANE flow is the biggest open-source automated facilitator of the Back end flow, taking input as the RTL, SDC (constraint file) and the technology files (in this case the skywater 130nm PDK) and giving GDSII as the output which can be send to the foundry for physical implementation.
The *striVe* SoC is the example of an open source flow producing a fully funtional chip.

The openLANE flow differs slightly from the conventional ASIC flow, it can be seen below: 

![openlane_flow](https://github.com/krunalbadlani/IS21MTECH14008-AdvancePDworkshopusingopenLANE-sky130pdk/blob/main/images/openlane_flow.png)


- openLANE works in either autonomous or interactive mode, we will use the interactive one here to tweak something or other on each and every stage of the flow. 

More data on openLANE can be found on its original github page [openLANE](https://github.com/efabless/openlane).
