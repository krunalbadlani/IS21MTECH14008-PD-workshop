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

Every step done by me in this workshop is explained below:- 

### Getting familiar to EDA tools

--- 

- Getting started with openLANE:
1. open terminal
2. redirect to the work directory, then go to tools
3. do a ls and find 2 folders : openlane_working_dir and pdks
4. ``` 
   cd openlane_working_dir
   ls -ltr
   cd openlane
   docker
   ./flow.tcl -interactive
   ```
5. Following will be seen, also follow the commands seen below the openload logo to get the required openlane package and prepare the design picorv32a:

![openLOAD screen](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/Screenshot%202022-08-06%20162200.png)
       
6. The mentioned design can be accessed in the following way from the openlane folder (do this in a new tab of the terminal):

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/accessing%20the%20design%20picorv32a.png)

7. The contents of the design folder will be as follows: 

![k](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/contents%20of%20design%20picorv.png)

8. The input to the openLANE flow is present in the SRC folder as follows:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/src%20before%20flow.png)

9. The config.tcl file looks like this at beginning and we will make changes to it subsequently as we move ahead:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/config.tcl%20initially.png)

### Synthesis for the first time !!

---

1. We are all set and now we get back to our openLANE flow tab and start with synthesis like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/run_synthesis.png)

2. Once it completes we will find a prompt like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/synthesis_successful.png)

3. The prep -design <design_name> command earlier will create a runs folder in the design/picorv32a folder which we accessed steps before, we can verify it by doing a ls in that folder.

4. When we view the contents of the runs folder we will be able to see folders with the name of the date on which that particular design was prepared. It will look like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/runs%20after%20first%20attempt.png)

5. Each of this folder has the following things:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/isnide%20date%20folder%20in%20runs.png)

6. The tmp folder has the following info:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/tmp%20folder.png)

7. The merged.lef file is important here as a lef file or a library exhcange format file is the Library Exchange Format (LEF) is a specification for representing the physical layout of an integrated circuit in an ASCII format. It includes design rules and abstract information about the cells. It looks something like this : 

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/meged_lef%20file.png)

8. The lef file has information on pins and ports of the design like this: 

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/merged_lef2.png)

9. In the runs/<date_of_run> folder we can see the results which contains the folder synthesis, opening it we'll see the files modified by the syntheis process.

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/synthesis%20file%20in%20results.png)

the verilog file on opening using less <name_of_file>:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/synthsis_vfile.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/synthsis_vfileend.png)

10. When we see the reports generated during the run_synthesis in runs/<date_of_run>/reports we can see the following:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/reports.png)

we can open a report from the folder:


![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/timing%20report%20after%20synth.png)

11. We can read the promts generated on the run_synthesis and find:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/chiparea.png)

We can calculate a very important factor called as dflipfloppercentage like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images1/dffpercentage.png)

## Day 2

---

### Beginning with floorplan
---

1. We can go to 
```
        cd openlane
        cd configuration
        less floorplan.tcl
```
and see the defaults set for floorplanning:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/floorplan%20defaults.png)

2. We can now go to the openlane flow and do floorplan:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/run_floorplan.png)

3. We can see the results in various logs in runs/<date_>/tmp/logs and runs/<date_>/config.tcl :

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/4-ioplacer.log.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/configafterFP.png)

4. Floorplanning creats a DEF file or the Data exchange format file (DEF file is used to represent the Physical layout of an Integrated Circuit (IC) in ASCII format. A DEF file is strongly connected with the Library Exchange Format (LEF) file. So both files are needed for a correct display of physical design. DEF file format was developed by Cadence Design System)
Our def file looks like:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/picorv32a_def%20file.png)


5. We can view the output of the floorplan in magic with the following command:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/magic%20to%20read%20stage%20after%20floorplan.png)

6. The outputs are as follows:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/picrorv32a%20in%20magic.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/io%20exploration.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/io%20exploration%20hori.png)

macros are at bottom left:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/marcros%20at%20bottom%20left.png)

7. We can change toggle switches or parameters in the various layout.tcl files in the design folder and see changes in the magic layout like I changed the Metal layers in the following way and saw the changes(but not all changes will get implemented as there is a priority orded in the .tcl files and the default values if some value is set in the most prior file we will only see that in the ouput ) :

changing the config.tcl in picorv32a folder like:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/editing_config_tcl.png)

results:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/metal%20hori%20after%20rectifying.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/metal%20verti%20after%20rectifying.png)

