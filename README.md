# Digital-VLSI-SoC-design-and-planning
<div class="toc">
  <ul>
    <li><a href="#header-1">Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK</a></li>
	<ul>
		
##  (a) How to talk to Computers 

**FPGA/ Aurdino Board** =>  An FPGA is an integrated circuit that can be programmed by the user after manufacturing to implement custom hardware functionality. It consists of an array of configurable logic blocks (CLBs) connected through programmable interconnects, allowing users to create custom digital circuits. FPGAs are highly flexible and are used in a variety of applications such as telecommunications, automotive systems, and aerospace, where custom hardware is needed for high-speed data processing, parallel computing, and real-time systems.

The picture shown below is an aurdino board, the chip circled is the picture is nothing, but the processor/SoC which is the heart of the this aurdino board, it has many pins coming outside to connect other peripharals devices with it or get signal in and out.

![ordino board](https://github.com/user-attachments/assets/c3c04add-854b-4d81-a32f-a31f3e6dc102)
	    

## Block Diagram of Above Aurdino Board


![Screenshot 2024-12-14 201734](https://github.com/user-attachments/assets/be7dfb3f-85cc-4cd7-9811-588259a32674)

Here SDRAM is an external component that we have shown in the block diagram and remaining all blocks are from aurdino board and the rectangle block is nothing, but processor/SoC that has been circled in the actual aurdino board 

## This is how Processor/SoC looks like inside 

![Screenshot 2024-12-14 204127](https://github.com/user-attachments/assets/ac569f40-3854-48b6-9c61-04abc24041b0)

This is called package, this is one of the package that we have in the market, there multiples pins available in the package that all are driven by the aurdino board

## This is how all pins are connected to the chip

![Screenshot 2024-12-15 010435](https://github.com/user-attachments/assets/c0de9e63-c966-499c-a31f-ba019d1e3f65)

These threads like wires are called wire bonds, these are used to connect the package to pins of the chip, and in this way we transfer the signals that are coming from the outer world to the proccessor 

## If we open the chip how it will look like ?

 **Let's See**

 ![Screenshot 2024-12-15 011621](https://github.com/user-attachments/assets/da6f1665-e592-478d-896f-db1755fc7c68)

 Inside of the chip there are many components available, some important components are given below

 **PADS** :- PADS are somthing through which any signal comes inside the chip and vice-versa


 **DIE** :- Dies are the square/rectangular shape area that are manufactured on silicon wafer, and later on we implement the different logic blocks on these DIES
 

 **CORE** :- Core is the central area of the chip that are used to place the different logic blocks.

 ![Screenshot 2024-12-15 022809](https://github.com/user-attachments/assets/9d22c573-e143-40cd-8313-68c27a3b7a03)

**Foundary IP's** :- Foundry IPs (Intellectual Properties) refer to pre-designed, verified, and reusable circuit blocks or modules provided by semiconductor foundries for use in integrated circuit (IC) design. These IPs are typically optimized for the specific manufacturing processes of the foundry, allowing IC designers to incorporate them into their designs without needing to develop certain functionalities from scratch.

**Macros** :- Macros are somthing which is a pure digital circuit logic blocks that are there inside the chip.


## Introduction to RISC-V:-    

This is nothing but the language of the computer, this is the way we are going to talk with the computer.

**Ex:-** If we want to run the C- program to specific hardware then there is certain flow through which it has to pass through as given below. That C-level program is first compile into assembly language program, which is nothing but the RISC-V assembly language program.

![Screenshot 2024-12-15 123842](https://github.com/user-attachments/assets/449dd6d7-a501-47cf-a3f3-ae43a3b6c5ce)


## From Software Applications to Hardware:-

![Screenshot 2024-12-15 131105](https://github.com/user-attachments/assets/10801c99-495b-4abd-ad6c-65d04f69b77c)

So here applications runs on the hardware of the our computer with the help of the intermediate stage "system software". So here application program enters into the system software and then system software interns converts the application program into binary language. 
The major components of system softwares are **Operating system (OS), Compiler, Assembler** 

**Operating System** :- It performs multiples job like, it handles input-output operations, it allocates memory , it manages low level memory functions. Other than this it converts the application program into assembly language program and then binary language program, so that it is to be understood by hardware.

**Compiler** :- Compiler converts the different types of programs written in different languages into the set of instructions, now these set of instructions are specific to the hardware that we are using, for example if given hardware belongs to ARM then set of instructions will be in ARM format.

**Assembler** :- Once complier is converted the different program into set of instructions then job of assembler is to convert these set of instructions into binary language or machine level language. Now these binary language is given to the hardware and it gives output as per its function and input.


##  (b) SoC Design and OpenLANE 

# Introduction to all open-source digital asic design

  For digital ASIC design we need **RTL IP's**, **EDA Tools**, **PDK DATA** all these things we need from the day one.

  **What is RTL IP's** :- RTL stands for "Register Transfer Level" At the RTL level, a circuit is modeled as a combination of registers (which store data) and combinational logic (which processes data). RTL is often used during the design and simulation of digital circuits before they are synthesized into a lower-level gate or transistor implementation.

  *Open Source for RTL IP's*: librecores.org, opencores.org, github.com etc

  **What is EDA Tools** :- EDA tools (Electronic Design Automation tools) refer to a set of software applications that are used to design, verify, and simulate electronic systems, including integrated circuits (ICs) and printed circuit boards (PCBs). These tools help automate and optimize various stages of the electronics design process, from concept and architecture through to detailed design, verification, and final production.

  *Open Source for EDA Tools*:  Qflow, OpenROAD, OpenLANE etc.


**What is PDK Data** :- Collection of files used to model a fabrication process for the EDA tools used to design an IC 

*Process Design Rules*: DRC,LVS,PEX
*Device Models*
*Digital standard cell libraries*
*I/O Libraries*

*Open Source for PDK Data*:  github.com/google/skywater-pdk

## Simplified RTL2GDS Flow

![Screenshot 2024-12-15 182733](https://github.com/user-attachments/assets/ac00e61d-7ec9-4b58-83fb-df613ec9892a)

**(1)Synthesis** :- It is the process in which we converts the RTL to a circuits out of components from the "Standard cell library" (SCL), the resultant circuit is describe in HDL and usualy refered to the gate level netlist. the gate level netlist is functionaly equivelent to the RTL. "standard Cells" have regular layouts like Electrical. HDL,SPICE

**(2)Floor/Power Planning** :- Floor planning depends on whether your implementing single components of the design or whole chip, the objective here is to plan the silicon area and creats robust power distribution network 

![Screenshot 2024-12-15 185242](https://github.com/user-attachments/assets/d3954d86-99d9-4316-aa46-e26ba70fdac5)

In power planning the power network is constructed,typically this network is connected by multiple power supplies such as VDD,VSS and these are supplied through the power pads. Power pads are conncted to all vertical and horizontal metals and rings.

**Chip-Floor Planning**:-  In chip-floor planning we partioned the chip die between different system building blocks and place the I/O Pads.


**(3)Placements** :- In this step we place gate level netlist into the floor of silicon wafer, here we represents each gate or filp-flop with a quare or rectangle and then we put them in such a way so that we can minimize the connecting wires among them. If we alling each square close to each other then, it reduces the connecting wires and hence delay is reduced. 

Usually placements done in two step - **Global placement followed by the Detailed placement** 


**Global Placement**:- Global placement tries to find optimal position for all cells such position may not be legal,and that's why may overlap or go off rules.

**Detailed Placement**:- In detail placement the position obtained from global placements are minimally altered to be legal

**(4)Clock Tree Synthesis(CTS)**:- In clock synthesis we create a clock distribution network, to deliver the clock to all sequencial elements like FF with minimum skew and in a good shape usually a tree (H,X)

![Screenshot 2024-12-15 193703](https://github.com/user-attachments/assets/ee10762d-06ee-4848-a4b1-4ba0b2902abf)

**(5)Routing** :- After routing the clock, the signal routing comes. Making physical connections between signal pins using metal layers are called Routing. Routing is the stage after CTS and optimization where exact paths for the interconnection of standard cells and macros and I/O pins are determined. There are two types of nets in VLSI systems that need special attention in routing:

Clock nets Power/Ground nets The sky130 PDK defines the 6 routing leyers. the lowest leyer is called local interconnect layer (titanium nitride layer). Other five layers are alluminium layersIn the proccess of routing, metal trackes forms a routing grids and these grids are huge. so, devide and conquer approach is use for routing. The two types of routing is used:

**Global routing**: Generates the routing guides

**Detailed Routing**: Uses the routing guides to implement the actual wiring.

![Screenshot 2024-12-15 194312](https://github.com/user-attachments/assets/e7a11ae6-fbef-43c2-b1f9-bd7c01aefcbb)

**(6)Sign off**:- Once done with routing, we can construct the final layout which undergoes physical verifications and time verifications.

**Physical Verifications**: Design Rules Checking (DRC), Layout vs Schematics (LVC)

  **Time verifications**: Static time analysis (STA)


  ## Introduction to OpenLANE and Strive chipset :- 

  OpenLANE is an open-source end-to-end digital ASIC (Application-Specific Integrated Circuit) design flow that leverages multiple tools in the open-source domain to automate and streamline the process of designing integrated circuits (ICs). Developed by Efabless, it integrates various tools from the open-source Electronic Design Automation (EDA) ecosystem to offer a complete workflow for chip design. It is particularly focused on RTL-to-GDSII flow, where the high-level RTL (Register Transfer Level) description of a circuit is converted into a physical layout ready for fabrication.

The goal of OpenLANE is to make it easier for engineers, researchers, and students to create designs, perform optimizations, and generate layouts that can be physically manufactured. The platform supports various design stages such as synthesis, placement, routing, and verification, ensuring compatibility with the SkyWater 130nm process node.


 **Strive SoC Family**

![Screenshot 2024-12-15 230526](https://github.com/user-attachments/assets/a321a130-4ef8-4a9a-9743-93ac8ade0d60)


The main goal of OPENLANE is to produce a clean GDSII with no human intervation (no-human-in-the-loop). here the meaning of clean is that:

No LVS violations

No DRC Violations

No timing Violations

OPENLANE is tuned for skyWter130nm open PDK. it can be used to harden Macros and chips.there is two mode of operation Autonomus : it is the push botton flow. with the push botton , it is a some time base design and due to this push botton, we get final GDSII

interactive : here we can run comamds and steps one by one.

It has large number of design examples(43 designs with their best configurations).

## Introduction to OpenLANE detailed ASIC design flow 


![Screenshot 2024-12-16 123725](https://github.com/user-attachments/assets/8344a5ed-1cdb-4a98-9ec3-7b8cebb2df8a)

The design exploration utility is also used for regression testing(CI). we run OpenLANE on ~ 70 designs and compare the results to the best known ones.

DFT(Design for Test) it perform scan inserption, automatic test pattern generation, Test patterns compaction, Fault coverage, Fault simulation.After that physical implementation is done by OpenROAD app. physical implementation involves the several steps:

Floor/Power Planning

End Decoupling Capacitors and Tap cells insertion

Placements: Global and Detailed

Post Placement Optimization

Clock Tree synthesis (CTS)

Routing: Global and Detailed

**Dealing with Antenna rules violation**

Every time the netlist is modified.(CTS modifies the netlist and Post Placements optimization also modifies the netlist).so for that verification must be performed. The LCE(yosys) is used to formally confirm that the function did not change after modifying the netlist. ### Dealing with antenna rules Violation: when a metal wire segment is fabricated, it can act as antenna.as an antenna, it collect charges which can demaged the transister gates during the fabrication.


![Screenshot 2024-12-15 234117](https://github.com/user-attachments/assets/2e12641d-4270-4459-98a8-60121317899e)

To address this issue, we have to limit the lenght of the wire. usually this is the job of the router. If router fails to do this, then there are two solutions: Bridging attaches a higher layer intermediary.Add antenna diode cell to leak away charges.(Antenna diodes are provided by the SCL)




![Screenshot 2024-12-15 234643](https://github.com/user-attachments/assets/ac137da0-ffd2-4c9d-b118-54fa55464563)

With OpenLANE, we took a preventive approach. here we add fake antenna diode next to every cell input after placement. Then run the Antenna checker on the routed layout. If the checker reports a violation on cell input pin, replace the fake diode cell by a real one.


![Screenshot 2024-12-15 234902](https://github.com/user-attachments/assets/6d7ccb14-f16c-4eb6-9f88-ba691580dc33)


**Static Timing analysis(STA)**:- It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. resulting report will shows the timing violations if any violations is there.

**Physical Verification (DRC and LVS)**:- Magic is used for design Rules checking and SPICE Extraction from Layout. Magic and Netgen are used for LVS.

# Get familiar to open-source EDA tools

# OpenLANE Directory structure in detail

**Basic Linux Commands**

**cd** : opens the particular folder

**ls** : lists the content of the folder

**pwd** : shows the present working directory

**mkdir** : to make a new directory

**command** --help : shows the complete use that command

**clear** : clears the terminal screen

Here we are working in Sky130_fd_sc_hd PDK varient. where, "sky130" is process name or node name."fd" is a foundary name (skyWater foundary)."sc" means standerd cell librery files and the last one "hd" stands for high density(basically one type of varient).

Sky130_fd_sc_hd varient contains many technology files like verilog, spice, techlef, meglef,mag,gds,cdl,lib,lef,etc. (techlef file contains the layer information).

# Design Preparation Step

when we enter in the OpenLANE, we have to use flow.tcl because as a name says, it will goes with the flow using the script. And by using interactive switch, we will do step by step process. without interactive switch, it will run complete flow from RTL to GDSII. Now OpenLANE is open and we can see that prompt will change now.

![openlane1](https://github.com/user-attachments/assets/d645ec47-c278-4171-b0fb-bf3a0c0c337e)

Now we have to input all the packages which required to run the flow.

![openlane2](https://github.com/user-attachments/assets/f17cf7f9-9814-44ab-9dc2-8d8340557089)

Now, here we are ready to execute the command.

Now, if we are going into the design folder in openlane, there are nearly 30-40 designs are already builted. Out of them we can open any of the design. for example, here we are opening the picorv32a.v design. In this design we can see many files are available. i.e., scr, config.tcl, etc. This config.tlc file contains every details about the design. for example, details about enrollment, clock period, clock period port etc.




![openlane2](https://github.com/user-attachments/assets/56d77755-6f72-4c0d-a001-f291eb72876d)

Here we can see that the time period is set to the 5.00 nsec. but is we see in the openlane sky130_fd_sc_hd folder, the period is set about 24 nsec. so it is not override to the main file. If it override then give first priority to the main folder.

Now, in openlane, we are going to run the synthesis, but before synthesis, we have to prepare design setup stage. for that command is  prep -design picorv32a


 ![openlane1](https://github.com/user-attachments/assets/f122a583-a970-4847-a287-14e7aae19108)

 Here in the above screenshoot we can see that from preparation start to completion all the steps are completed 

 # Review files after design prep and run synthesis

 After completing the preparation, in the picorv32a file, the run terictory is created. Inside the folder, Today's date is created. so in this terictory some folders are available which is required for openlane.

In the temp file, merged.lef file is available which was created in preparation time. if we open this merged.lef file, we get all the wire or layer level and cell level information.


 


  















 
















