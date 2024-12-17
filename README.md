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

# (c) Get familiar to open-source EDA tools

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

![openlane3](https://github.com/user-attachments/assets/4a595bde-6122-45b9-8338-42414b7c0284)
While, in the result folder is empty because till we have not run anything and in the report folder all the folders are there about synthesis, placement, floorplanning,cts,routing,magic,lvs.

now here also one config.tcl file is available similar like design folder. But this config.tcl file contains all default parameter taken by the run.

when we make some change in the origional configuration and then we run, for example if we make a change in core utilization in the floorplanning and then we run the floorplanning, at this time in the congig.tcl file, the core utility will change and by cross checking it we can check that the modification is reflected in the exicution or not.

Now coming to the openlane, we are going to run the synthesis. for that command is run_synthesis It will take some 3-4 mnts to run the synthesis and finally synthesis will complited.
![openlane4](https://github.com/user-attachments/assets/06b8ed2a-1e87-490a-912f-91f66b1a497b)

# Steps to characterize synthesis results



 
![openlane5](https://github.com/user-attachments/assets/6c715807-64ef-4711-a027-55d9237a7b98)


From the above synthesis we can see that 

 Number of flip flop = 1613  


 Number of  cell = 14876


 So Flop Ratio = [Number of Flip Flop / Number of cell]*100 = [1613]/[14876] *100 = 10.84%

 Before we had ran the synthesis we had seen these folders were empty, now once synthesis is done, we can see that these folders are now full

![openlane1](https://github.com/user-attachments/assets/fc131ca1-c44e-4936-9fc6-6b8706e95732)


And in the report, we can see when the actual synthesis has done. and the actual statistics synthesis report is showing below, which is same as what we have seen before.




 ![openlane6](https://github.com/user-attachments/assets/238c2d78-c1e8-4c1e-ae85-1cd5e7163487)

  

<div class="toc">
  <ul>
    <li><a href="#header-1">Day 2 - Good floor planning considerations</a></li>
	<ul>

 # (a)  Chip Floor planning consideration

 **Utilization factor and aspect ratio** 

In this section we will try to cover up the width and height of Core and Die. It is the first step in physical design flow to find out the width and height. Let's begin with a netlist, netlist is two flipflops and have a simple combination logic in between. A netlist describes the connectivity of an electronic design. Here, we dependent on the dimensions of the logic gates(AND & OR) and particular flipflop. Now, let's convert the symbols into physical dimensions. We are interested in the dimensions of the Core and Die not in the dimensions of the wires.

Let's standard cell have dimensions of 1unit*1unit

So, area= 1 Sq. units

Asuume same area for the flipflop as well = 1 Sq. units

with help of these dimensions and netlist let's calculate the area occupied by the netlist on a silicon wafer.

![Screenshot 2024-12-17 163429](https://github.com/user-attachments/assets/f078fdb5-a54d-4ae5-bc55-39b65affce30)

Before that will remove all the wires and bring all the flip flops and logic gates in a single plate. So after combining them together width and length will be 2 Sq. units each and if we calculate the total area the it will be 4 Sq. units. So now we have the rough calculation of minimum area occupied by the netlist.

![Screenshot 2024-12-17 163711](https://github.com/user-attachments/assets/6f3cbbd2-e1f1-4d28-bc6d-3e72f3d59c10)


**Core**:- In the context of digital IC design, "core" can also refer to a pre-designed, reusable block of logic or functionality, such as a CPU core, memory controller core, etc., integrated into a larger IC design.

**Die**:- The die refers to the actual piece of semiconductor material (usually silicon) on which the integrated circuit is fabricated. It is the small, rectangular or square slice of silicon wafer that contains the core circuitry and all other components of the IC.

![Screenshot 2024-12-17 164439](https://github.com/user-attachments/assets/159b8e09-4b85-47e6-8b6c-ac8441625f60)


 Utilization Factor = Area occupied by netlist / Total area of the core
   
 lets put the dimensions we have, we get
 
 Utilization factor = 4*1sq.unit / 2unit *2unit
 
		= 4sq unit /  4sq unit
So, utilization factor = 1 (It means core has utilized all the area and no spane left)

Aspect Ratio = Height / width = 2 unit / 2unit = 1


From above formula we can say that, if aspect ratio is unity it signifies that chip is in square shape. Other than unity it will be always rectangular shape.


## Concept of Pre-Placed cells

Lets take a combinational logic which does some amount of function and assume its a huge circuit having some N Logic gates so let's devide it into some small numbers of gates. We will cut the whole circuit into two parts, and separate both of them into two blocks and both block will be implemented seperately.

![Screenshot 2024-12-17 165337](https://github.com/user-attachments/assets/0a72441e-5401-4e39-ad17-4f52ca7347e1)

In both the blocks lets extend the input output pins and now we will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. now will seperate them out as two different IP's or modules.
![Screenshot 2024-12-17 165600](https://github.com/user-attachments/assets/50993692-ae76-419c-ad72-719fca8c788c)
Advantage of doing this is we can reuse them multiple times after implimenting once only. Similary there are other IP's also available for eg. Memory, Clock-gating cell, Comporator, MUX all of these are part of the top level netlist.They recieve some signals and perform functions and deliver the outputs but the functionality of the cell is implemented only once.

The arrangement of these IP's in a chip is refferd as floorplanning.

These IP's have user-defined locations, and hence are placed in chip before automated placement and routing are called "pre-placed cells".

These cells are placed in such a way that, the placement and routing tool do not touch the location of the cell.

**De-Coupling Capacitors**

surround pre-placed cells with Decoupling capacitor:- Let consider some circuit, which is the part of the blocks which has been described earlier. When some gate (let consider AND gate) switched from 0 to 1 or 1 to 0, considered amount of the switching current required because of available small capacitance . This capacitor should be completely charged to represent logic 1 and completly discharged to represent logic 0. Consider capacitance to be 0. Rdd,Ldd,and Lss are well defoned values. During switvhing operation, the circuit demands switching current i.e. peak current. Now, due to the presence of Rdd and Ldd, there will be a voltage drop across them and the voltage at Node 'A' would be Vdd' instead of Vdd.

![Screenshot 2024-12-17 173936](https://github.com/user-attachments/assets/5be77d1e-df13-443f-bf90-f0017118745d)

In the chip it will look something like shown below Decoupling capacitors are placed in between the block a, block b and block c. So here in this whole block it has been ensured that supply is being done by the de-coupling capacitor. Once we are done with this we have taken care of the local communication.

![Screenshot 2024-12-17 174342](https://github.com/user-attachments/assets/65a1dde3-d4ea-4a7b-837b-f8905fc445b3)

**Power Planning** :

Now let's consider that local circuitory and keep it as a black box and it can be repeat multiple times and there is some logic present at the boundaries also and the problem of current demand was solved by de-coupling capacitor. There is signal which is send from driver to load and the signal is basically logic 0 to logic 1. Here we need to maintain the particular driver to load line with same signal so that the load recieves the same. Now power supply is applied. Now assume 16 bit bus has to retain the same signal from driver to the load. so it should get the sufficient power from the supply. But at this bus, there is no de-coupling capacitor is available because it is not physible to put capacitor at all over the place. now, power supply is far away from the bus, that is why some voltage drop between them will occur definetly.


![Screenshot 2024-12-17 175824](https://github.com/user-attachments/assets/23d14dfa-a40e-4dbb-b91d-968ac548e473)

If all capacitors dischared at the same time then ground potential will rise above 0V, and if it is above noise margin then then it may creats problem. 
and this rise in voltage called as "Groun Bounce"

![Screenshot 2024-12-17 180411](https://github.com/user-attachments/assets/ae03bd4f-cbb3-49aa-a07c-c19b3c68753e)


If all the capacitors chagred at the same time then this will lower down the Vdd of the supply, and if it will be in the range of noise margin then it will create problem.


![Screenshot 2024-12-17 180818](https://github.com/user-attachments/assets/f8e93949-8c51-4d7d-a6ef-060778071773)

The phenomenon we have seen was causing the lowering of the supply voltage,this problem occured because power has applied to one point only. The solution of the problem is use multiple power supply. So, every block will take charge from neartest power supply and similarly dump the charge to the nearer ground. this type of power supply is called mesh.

![Screenshot 2024-12-17 180955](https://github.com/user-attachments/assets/be26a386-f14b-4391-b192-bfe6e4079980)

This is how final power planning looks like 


![Screenshot 2024-12-17 181227](https://github.com/user-attachments/assets/3d431d18-04d7-43fe-a8ec-5a11cf8d62da)


## Pin placement and logical cell placement blocks :
Lets take below designs for example that needs to be implemented. Here first circuit is driven by clk1 and second circuit is driven by clk2 and both has different inputs Din1 and Din2 respectively and outputs as Dout1 and Dout2.Along with that we have some preplaced cells as well as Blocka which recieves inputs from Din1 second input from Din2. We have another preplced cell as Blockb Which recieves input from clk1 and clk2 and provides a clk output. So currently we have 4 input ports Din1,Din2,Clk1,Clk2 and 3 output ports Dout1,ClkOut,Dout2


![Screenshot 2024-12-17 184117](https://github.com/user-attachments/assets/92455003-7d93-4f41-85d5-3e47418f2428)
let's have one more design that needs to be implemented. this types of circuits are very much helpful to understand the timing analysis of inter clocks. now complete design becomes like given below which has 6 input ports and 5 output ports. The connectivity information between the gates is coded using VHDL/Verilog language and is called as 'Netlist'.



![Screenshot 2024-12-17 184506](https://github.com/user-attachments/assets/9c211adf-9707-4400-9539-ac38f829b87b)



Let's put this netlist in the core which we have designed before and let's try to fill this empty area between core and die with the pin information. The frontend team who decides the netlist connectivity input and output and the backend team who done the pin placements. So according to the pin placements, we have to locate the preplaced blocks nearer to the inputs of the preplaced blocks.


 
![Screenshot 2024-12-17 184931](https://github.com/user-attachments/assets/ec055d4a-f876-4dee-badc-b2bb0de8129f)

Here one thing that we noticed is that clock-in and clock-out pins are bigger in size as compared to input and output pins. reason behind this is that, input clocks are conntinuously provides the signal to the every elements of the chip and output clock should out the signal as fast as possible. So, we need least resistance path for the clocks inputs and clocks outputs. So, bigger the size, lower the resistance.

One more thing is need to take care about is that, this pin placement area is blocked for routing and cell placements. so we nned to do logical cell placement blockage. this blockage is shoown in above image in between pins.

So, floor plan is ready for Placement and Routing step.


## Steps to run floorplan using OpenLANE

Before we run floorplane we will be needed with some switches, which we can get from the openlane configuration 


![open1](https://github.com/user-attachments/assets/a8fd3b9e-bda3-4623-b1ff-beccddd09fae)
Here we can see that the core utilization ratio is 50% (bydefault) and aspect ratio is 1 (bydefault). similarly other information is also given. But it is not neccessory to take these values. we need to change these value as per the given requirments also.

Here FP_PDN files are set the power distribution network. These switches are set in the floorplane stage bydefault in OpenLANE.


![open2](https://github.com/user-attachments/assets/d830b745-8387-4139-97f9-f277fa69aafc)
Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance.

In the OpenLANE lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

Now we see, with this settings how floorplan run.

## Review floorplan files and steps to view floorplan

In the run folder, we can see the connfig.tcl file. this file contains all the configuration that are taken by the flow. if we open the config.tcl file, then we can see that which are the parameters are accepted in the current flow.
![open3](https://github.com/user-attachments/assets/34bf2145-30e2-4c35-9758-4d5a02d3985c)


To watch how floorplane looks, we have to go in the results. in the result, one def( design exchange formate) file is available. if we open this file, we can see all information about die area (0 0) (660685 671405), unit distance in micron (1000). it means 1 micron means 1000 databased units. so 660685 and 671405 are databased units. and if we devide this by 1000 then we can get the dimensions of chips in micrometer.

![open4](https://github.com/user-attachments/assets/bc318511-ae62-4220-b6a9-da19121ca128)
so, the width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer.

To see the actual layout after the flow, we have to open the magic file by adding the command magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

And then after pressing the enter, Magic file will open. here we can see the layout.


![open5](https://github.com/user-attachments/assets/e32507fa-c196-4f88-bf16-4b2d31e7bb68)
# Review floorplan layout in Magic
In the layout we can see that, input output pins are at equal distance.

![open7](https://github.com/user-attachments/assets/d9d37a04-7a3d-4ed1-83f1-93d10c61aa1b)
after selecting (To select object, first click on the object and then press 's' from keyboard. the object will hight lited. to zoom in the object, click on the object and then press 'z' and for zoom out press 'sft+z') one input pin, if we want to check the location or to know at on which layer it is available, we have to open tkcon window and type "what". it will shows all the details about that perticular pin.

![open6](https://github.com/user-attachments/assets/0536ec40-a342-4c2c-a931-5aad17a83405)


