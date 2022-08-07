# **Advance Physical Design Workshop using openLANE/sky130pdk**
This repository contains the whole summary of khowledge acquired and hands on done by Krunal Badlani (IS21MTECH14008) during the workshop "Advance Physical Design Workshop using openLANE and Google - skywater 130 nm pdk" organised by VSD.

## *Contents*

  * [DAY 0](#day-0)
  * [Day 1](#day-1)
    + [Talking to Computers](#talking-to-computers)
    + [SoC design and openLANE](#soc-design-and-openlane)
    + [ASIC flow](#asic-flow)
    + [Getting familiar to EDA tools](#getting-familiar-to-eda-tools)
    + [Synthesis for the first time !!](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/README.md#synthesis-for-the-first-time-)
* [Day 2](#day-2)
    + [Beginning with floorplan](#beginning-with-floorplan)
    * [Lets do the Placement now](#lets-do-the-placement-now)
* [Day 3](#day-3)
    + [Changing parameters of the flow on the fly from the openLANE flow](#changing-parameters-of-the-flow-on-the-fly-from-the-openlane-flow)
    + [Spice model of the cmos inverter and its characterization using ngspice:](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/README.md#spice-model-of-the-cmos-inverter-and-its-characterization-using-ngspice)
 + [Day 4](#day-4)
   * [Merging our inverter with the design](#merging-our-inverter-with-the-design)
   * [Running CTS](#running-cts)
   * [We Do STA here:](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/README.md#we-do-sta-here)
  * [DAY 5](#day-5)
    + [The PDN:](#the-pdn-)
     * [Finally we do Routing:](#finally-we-do-routing-)
     * [Thanking VSD And team for such a great workshop](#thanking-vsd-and-team-for-such-a-great-workshop)
  * [Acknowledgement](#acknowledgement)




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
The 3 important factors in ASIC design process are, 
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

(We can select in magic by selecting a region by left click followed by right, pressing s and then z for zooming into it)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/picrorv32a%20in%20magic.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/io%20exploration.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/io%20exploration%20hori.png)

standard cells are at bottom left:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/marcros%20at%20bottom%20left.png)

7. We can change toggle switches or parameters in the various layout.tcl files in the design folder and see changes in the magic layout like I changed the Metal layers in the following way and saw the changes(but not all changes will get implemented as there is a priority orded in the .tcl files and the default values if some value is set in the most prior file we will only see that in the ouput ) :

changing the config.tcl in picorv32a folder like:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/editing_config_tcl.png)

results:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/metal%20hori%20after%20rectifying.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/metal%20verti%20after%20rectifying.png)

The background of the terminal in the given platform can be edited like following:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/editing%20background.png)

## Lets do the Placement now
---

1. We run the placement command in similar way to synthesis and floorplan :

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/run_placement.png)

2. The placement done! prompt:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/placement%20done.png)

3. Viewing placement in magic

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/magic%20placement.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/magic%20placement%20result.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images2/zooming%20placement.png)

## Day 3
---
### Changing parameters of the flow on the fly from the openLANE flow
---
1. Go to:
```
        cd configurations
        less README.md
```
Here we find all parameters which we can tweak :

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/readme%20of%20switches%20in%20floorplan.png)

2. We can set parameters to new values form the openLANE  flow on the fly like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/setting%20parameters%20on%20the%20fly%20in%20openlane.png)

3. We can see the results, the io placement has changed now as per our new setting:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/change%20in%20io%20orientation.png)

### Spice model of the cmos inverter and its characterization using ngspice:
---
1. Git cloning the required files from [Nickson Jose's github](https://github.com/nickson-jose/vsdstdcelldesign)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/gitcloning%20vsdstdcelllib%20from%20nickson.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/vsdstdcell%20showing%20up.png)

2. Copying the sky130a.tech file to the folder to enable magic to view the inverter's layout:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/copying%20sky130atech%20file%20to%20vsdstdcell.png)

3. Opening the inverter in magic:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/opening%20inv%20in%20magic.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/inv%20in%20magic.png)


![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/identifying%20nmos%20in%20layout.png)

![o](    https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/identifying%20pmos%20in%20layout.png)    

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/veryifying%20the%20connections%20in%20inv%20layout.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/veryifying%20the%20connections%20in%20inv%20layout2.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/veryifying%20the%20connections%20in%20inv%20layout3.png)

We can check any DRC errors like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/drc%20error%20check.png)

4. We can extract the file and its spice deck to our folder like this:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/extraction%20of%20inv%20in%20vsdstdcell%20lib.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/extraction%20of%20spice%20file%20in%20vsdstdcell%20lib.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/extraction%20of%20spice%20file%20in%20vsdstdcell%20lib2.png)

5. The spice deck looks like this: (less sky130_inv.spice)
and the dimensions of the one inv are in the tkcon window:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/spice%20file%20details.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/size%20x%20size%20in%20tkcon%20.png)

6. We modify the spice file as per our design to see its response in ngspice:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/modified%20spice%20file.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/running%20ngspice.png)



![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/op%20in%20ngspice.png)

plotting y vs time vs a: 

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/ngop1.png)


We modify the cap values in spice deck to get better waveforms:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/modify%20cap%20to%20get%20good%20op.png)

We obtain the following results


![o](  https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/ngop2.png)

Rise time at 0.660 v (20%) and 2.64 v(80%)

![o](  https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/ngop2660.png)

Diff of these values gives rise time (0.06281ns):

![o](  https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/rise%20time.png)

Values at 1.65 V (50% to calculate propagation delay)

![o](  https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/ngop3.png)

DIff of these two values gives propagation delay(0.06096ns):

![o](  https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images3/propdelay.png)

### Day 4

## Merging our inverter with the design
---
1. We should look at the tracks.info (dependent on the PDK) file to set the grid size of our inverters layout so that we can get perfect merger of our inverters with the standard cells present in the design already:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/tracksinfo.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/tracks%20info%20less.png)

2. We have to set the grid size of our inv with respect to the design tracks.info , we use g to make the grid visible and the subsequent steps to change it etehn we save it to our folder:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/grid%20in%20magic.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/size%20of%20grid.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/sizing%20the%20grid%20as%20per%20tracks%20info.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/resized%20grid%20.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/resized%20grid%201.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/saving%20with%20our%20name.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/our%20saved%20cell%20in%20vsdstdcell.png)

3. We now write the lef file of our inverter and send it to our folder and see whats inside it and also sending it to src of the picorv32a folder to later merge it to the lef of the design:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/writing%20lef%20for%20vsdinv.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/seeing%20the%20new%20lef%20in%20vsd%20std%20cell.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/inside%20lef%20file%20of%20vsdinv.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/copyinglef%20to%20src%20of%20picorv32a.png)

4. We transfer the lib files of the inverter to the src of the design:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/copying%20these%20libs%20to%20src.png)

5. We find some errors in preparing the design after adding the inverter:

![o]( https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/errors%20in%20preping%20design%20after%20including%20std%20cell.png)

So we change the config file like this: 

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/changes%20to%20the%20config_tcl%20file%20to%20include%20our%20vsdiat.png)

we then run these commands:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/commands%20from%20nicksons%20git%20to%20merge%20lefs.png)

6. We then run the synthesis and see the results and find our inverter cell merged!

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/run_synthesis%20with%20our%20cell.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/we%20can%20see%20our%20design%20yay.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/successfull%20synthesis%20with%20tns%20and%20wns.png)

We now tinker the switches to bring that wns and tns down to 0 , ( keep in mind to prep the design overwriting the previous run using prep -design name -tag date_runs -overwrite to let your synthesize everytime and not skip it):

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/tinkering%20synth%20switches.png)

We choose the following strategy and see the subsquent results:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/delay%203%20buffer%204.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/delay%203%20area%20and%20vsdinv.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/delay%203%20wns%20and%20tns.png)

We can see the merged.lef with our inverter !

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/meged%20lef%20with%20vsd.png)

We will now follow the flow of subsequent steps but theres a tweak, to avoid the following error we use the flow mentioned below it:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/error%20in%20floorplan%20.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/new%20flow.png)

Following new flow mentioned above we go on like this:



![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/init_floorplan.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/place_io.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/global_placement_or.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/detailed_placement.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/detailed_placement%20result.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/tap_decap_or.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/tap_decap_orresults.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/detailed_placement%201.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/detailed_placement%20result%201.png)

Placement result in magic:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/placement_result%20in%20magic.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/finding%20our%20cell%20and%20using%20command%20to%20highlight%20ports.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/ourcell_placed.png)

## Running CTS 
---
We run cts here and take a look at the results:


![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/run_cts.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/trion_cts.png)

#### We Do STA here:
---
We start openROAD to give a platform to the openSTA:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/running%20openroad%20to%20implement%20opensta.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/reading%20lef%20in%20openroad.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/read%20def%20in%20or.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/read%20write%20db%20in%20or.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/reading%20insts%20or%20and%20error.png)

solving error by adding my_base.sdc:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/my_base_sdc.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/solved%20and%20subsequent%20steps.png)

Hence we get the delays:

setup delay:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/setup%20delay.png)

hold delay:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/hold%20delay.png)

This delay is not right because of limitations of TrionCTS:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/to%20get%20real%20analysis.png)


![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/slack%20met%20yay.png)

The TrionCTS 2.0 used in this workshop gives the slack analysis and the skew analysis:

Setup_slack:

![o]( https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/setup_slack.png)

Hold_slack:
![o]( https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/hold_slack.png)

Skew_analysis:
![o]( https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images4/skew%20report%20post%20cts.png)

## DAY 5
---
### The PDN:
---
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/gen_pdn.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/pdn%20report.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/pdn%20finished.png)

## Finally we do Routing:
---
1. the defaults:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/routing%20defaults.png)

2. One error we get while tweaking the defaults:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/routing%20error.png)

3. We run routing now and see the following results:

 ![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/routing%20finished.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/routing%20finished.png)

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/routing%20report.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/preroute_file.png)
4. opening the final result in magic:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/post%20route%20magic%20.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/post%20route%20magic%20vsdinv.png)
![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/post%20route%20magic%20vsdinv%20expanded.png)

5. openLANE now integrates SPEC formation in the flow so we dont need any different steps for it, we can see it in the results:

![o](https://github.com/krunalbadlani/IS21MTECH14008-PD-workshop/blob/main/images5/spef%20file%20present%20in%20runs%20by%20default.png)
 



## Thanking VSD And team for such a great workshop
---

## Acknowledgement
---
- Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)
- Nickson Jose, VLSI Engineer
