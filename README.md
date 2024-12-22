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

# Library building and Placement

## Netlist binding and initial place design
**Bind netlist with physical cells** 
![Screenshot 2024-12-18 182533](https://github.com/user-attachments/assets/96ada0a6-8512-4198-beb0-2d0dfa59d8fe)

 This is the Netlist circuit that have different types of gate and flip flops and many more logical circuits repersented using different blocks. But in actual circuit these do not looks like the shape they are having in the Netlist. In actual physical cell they are converted into either a square or rectangular cell.
 
![Screenshot 2024-12-18 183309](https://github.com/user-attachments/assets/7cd478cd-954b-4af1-b49e-f61d4071e899)

Here in the above image each and ever netlist components have been converted into a square shape box and this how they looks like in real worlds

**Library** : In library we will get each of these blocks with its specifications like, size of blocks,delay time, required condition for the particular blocks. Otherthan that we can also get some blocks with same working specifications of different size.
![Screenshot 2024-12-18 184127](https://github.com/user-attachments/assets/8978a023-d9f6-4af6-881d-974a7b5cefcc)


**Placement**:  Once we have given proper shape and size to each and every gates the next step is to take those particular shapes ans sizes and place it on the floorplan. We have the floorplan with inout and output ports, we have particular netlist, and we have particular size given to each component of this netlist. So we have the physical view of the logic gates. Next step is to place the netlist onto the floorplan. We have to take the connectivity information from the netlist and design the physical view gates on the floorplan.



![Screenshot 2024-12-18 184318](https://github.com/user-attachments/assets/f70d1bb0-fde8-4712-bace-72522398ca2b)

# Optimize placement using estimated wire-length and capacitance
 In optimize placement we will resolve the problem of distancing.Lrt's take the example of FF1 to Din2. There must be a wire going from Din2 to FF1 but before going into routing the desing or wiring we will try to estimate the capacitances. If we lokk the capacitance from Din2 to FF1 it is every huge because wire length is huge in that case even the resutance will also be huge because of that length. If we send the signal from Din2 then it will be difficult for FF1 to catch that input because distance is large. So we can place some intermediate steps to maitain the Signal integrity. By this the input is succesfully driven to the FF1 from Din2. These intermediate steps are called here Repeaters , Repeaters are basically buffers that will recondition the original signal and make a bew signal which replicate the original signal and send it forward this process repeates untill we reach to the actual cell where we want to send the input in this way signal integrity is maintained. By using repeaters we resolve the problem of signal integrity but there will be a loose of area because more and more repeaters are used more area will be used of the particular floorplan.



![Screenshot 2024-12-18 185436](https://github.com/user-attachments/assets/5aa82419-3cd8-48be-bdaa-433e5c867d7d)

Since in this step distance between two blocks are not much, that's why we dont need repeaters here  we can directly connect the blocks with each other.


![Screenshot 2024-12-18 185807](https://github.com/user-attachments/assets/7aedc2a0-797b-4b4c-88f9-ec2b1614a59c)

But here in 2nd stage since blocks are far away from each other, so we need to put repeaters between those two blocks which has much distance between them.

# # Need for libraries and characterization
 Every ICdesign Flow needs to go through the several steps. First step to go through is Logic Synthesis, let's say if we have a functionality which is coded in a form of an RTL so first we need to convert the functionality into legal hardware is refered to as Logic Synthesis. Ouput of the logic synthesis is arrangement of gates that will represent the original functionality that has been described using an RTL. Next step of logic synthesis is Floorplaning, in this we omport the output of logic synthesis and decide the size of the Core and Die. The next step after floorplaning is Placement, in this we take the particular logic cell send place them on the chip in such a fashion that initial timing is better. Next step is CTS(Clock tree synthesis), in this we take care that clk should reach each and every signal at the same time also take care of each clk signal has equal rise and fall.Next step is Routing, routing has to go through the certain flow dependendent on the characterization of the flip flop.And now comes the last step STA(Static timing analysis), in this we try to see the set up time, hold time, maximum achieved frequency of the circuit. One common thing across all stages 'GATES or Cells'.

 # # Congestion aware placement using RePlAce

    [image required]
## (c) Cell design and characterization flows

**Inputs for cell design flow** 
In Cell Design Flow, Gates, flipflops, buffers are named as 'Standard Cells'. These standard cells are being placed in the section called as 'Library'.And in the library many other cells are available which have same functionality but the size is different.



![Screenshot 2024-12-19 091540](https://github.com/user-attachments/assets/4af6ce64-34a4-4a41-a08a-9e966bbba44d)

If you lokk into one of the inverter from the library the cell design flowis as follows

The inverter has to represented in form of the shape, drive strength, power charracteristic and so on. Here cell design flow is devided into three parts.

**Inputs**

**Design steps**

**Outputs**

**1)Inputs**:- Inputs required for cell design is PDKs, DRC and LVS rules SPICE models, library and user defined specs. In DRC& LVS rules tech file is provided which contains design rules and actual values. Rules can be converted in to code. SPICE MODEL tells about threshold voltage equation.





![Screenshot 2024-12-19 091942](https://github.com/user-attachments/assets/bb90c17b-796c-4586-9081-96b46ba1982b)

## Circuit Design Steps

The seperation between the power rail and the ground rail defines the cell height. Cell width depends upon the timing and drive strength.

**2)design steps**:- Design involves three steps which are circuit design, layout design, characterization.

In circuit Design there are two steps.

First step is to implement the function itself and second step is to model the PMOS nad NMOS transistor in such a fashion in order to meet the libraray.

**3)Outputs**

The typical output what we get from the circuit design is CDL(circuit description language) file,GDSII,LEF,extracted spice netlist(.cir).




![Screenshot 2024-12-19 093127](https://github.com/user-attachments/assets/520e70b6-7f4d-4162-aa3c-a17a89fede78)

## Layout design step
 So in layout design first we implement the given function using MOS transistor, it needs some set of NMOS and PMOS transistors to implement the function. Second step is to get PMOS network graph and NMOS network graph.

 
![Screenshot 2024-12-19 093359](https://github.com/user-attachments/assets/3845f0c1-b362-49a2-9444-c08c4c2b7c07)

After getting the network graphs next step is to obtain the Euler's path. Eule's path is basically the path which is traced only once.


![Screenshot 2024-12-19 093509](https://github.com/user-attachments/assets/e102938e-6c50-4395-bc27-2399efc0cb0d)

After this we will draw the stick diagram and it will be purely based on Euler's path. This stick diagram is derived from the circuit diagram.


![Screenshot 2024-12-19 093523](https://github.com/user-attachments/assets/0d3d94bd-0708-4525-b6a1-810e6910d0e0)

Next step is to convert this stick diagram into a typical Layout, into a proper layout and then get the proper rule we have discissed earlier. Once we get the particular layout then we have the cell width, cell length and all the specifications will be there like drain current, pin locations and so on.



![Screenshot 2024-12-19 094355](https://github.com/user-attachments/assets/0255f6bc-f52e-4733-b165-fd996c75ba5c)

## Typical characterization flow
Let's try to build the characterization flow based on the inputs we have,

First step is to read in the model, second step is to read the extracted spice netlist, third step is to define or recognize the behaviour of the buffer, fourth step is to read the subcircuits of the inverter and then in the fifth step need to attach the necessary power supplies, sixth step is to apply the stimulus then in the seventh step we need to provide the necessary output capacitance then in the final eighth step in which we need to provide necessary simulation command for example if we are doing transent simulation so we need to give .tran command , if we are doing DC simulation then we give .dc command.



![Screenshot 2024-12-19 100420](https://github.com/user-attachments/assets/ab963bdf-ee17-4d2b-b3ce-10919010f583)

In the next step we will feed all those 1-8 inputs to the **GUNA** software for time,power,noise,.lib function analysis


![Screenshot 2024-12-19 101654](https://github.com/user-attachments/assets/835433b7-dcdc-4135-895f-9474430f8beb)

# (d) General timing characterization parameters
## Timing threshold definitions
As seen in the previous section we have inverter connected back to back, we have power sources, we have the stimulus applied to the inverter all these things brings a very important point of understanding differenet threshold points of a waveform itself and it is called as "Timing threshold definitions'.

in the figure below the term 'Slew_low_rise-thr' depicts the value close to 0. and the typically value of this is about 20% it could be 30% as well.


**'Slew_low_rise-thr'**

![Screenshot 2024-12-19 102908](https://github.com/user-attachments/assets/ace60107-c49d-4628-9ba1-9141a2b5c1af)


**Slew_high_rise_thr**




![Screenshot 2024-12-19 103310](https://github.com/user-attachments/assets/6d4f4ca4-b99d-45ad-b444-3a814d60539c)


**Slew_low_fall_thr**


![Screenshot 2024-12-19 103453](https://github.com/user-attachments/assets/24b18aa2-0e59-48ee-b69d-d199b4ec6fad)


**Slew_high_fall_thr**

![Screenshot 2024-12-19 103607](https://github.com/user-attachments/assets/71d5a018-ad19-4015-9153-848ec9101fe3)


## Propagation delay and transition time

Based on these above values we are going to calculate the further values like propogation delay, current,slews etc.

If we want to calculate the delay of anything we need to subtract the out_rise_thr from in_rise_thr. Here let's take typical value 50%, let's see on the particular waveform how does it works Time delay = Time(out_thr)-time(in_thr)




![Screenshot 2024-12-19 104438](https://github.com/user-attachments/assets/dd24d2c8-22f4-4262-a13d-5d0681d371da)

In the above example in_rise_thr and out_fall)thr was kept at 50%. But if the threshold ponit moves to the top the the output comes before the input and we see negative delay and negative delays are not accepted. So the reason behind having this negative delay is poor choice od threshold point so thr choice of the threshold point is really important.



![Screenshot 2024-12-19 104536](https://github.com/user-attachments/assets/607c7818-483b-43ef-aaf2-50dffadf83b9)


Let's take another example where we have choosed threshold point correctly but still can get a negative delay. Because uotput comes before the input that's why we are getting negative delay here, which is not accepted


![Screenshot 2024-12-19 104703](https://github.com/user-attachments/assets/2b298c70-9cc7-4a9d-94c1-a6137712a7ec)

Transition time= time(slew_high_rise_thr)- time(slew_low_rise_thr)

or

**transition time**  = time(slew_high_fall_thr)- time(slew_low_fall_thr)

Let's say we have the waveform to understand the slew calculation.


![Screenshot 2024-12-19 104833](https://github.com/user-attachments/assets/578828e0-2a46-48a6-8174-9cdd48ea4602)

<div class="toc">
  <ul>
    <li><a href="#header-1">Day 3- Design library cell using Magic Layout and ngspice characterization
</a></li>
	<ul>

# (a)Labs for CMOS inverter ngspice simulations

**IO Placer Version**

Till now, we have done floor planning and run placement also. But if we want to change the floorplanning, for example, in our floor planning, pins are at equal distance and if we want to change it then we can also make it by Set command.

For that first we have to check the swithes in the configuration and from that we have to take the syntax "env(FP_IO_MODE) 1". and make it to the "env(FP_IO_MODE) 2". then again run the floorplanning.

Then check the changes in the pins location through magic -T.

          [image required]

   ## SPICE deck creation for CMOS inverter

   **VTC- SPICE simulations**:-Here first part is to create SPICE deck, it's the connectivity information about the netlist so basically it's a netlist.It has input that are provided to the simulation and the deck points which will take the output.

**Component connectivity**:- In this we need to define the connectivity of the substrate pin. Substrate pin tunes the threshold voltage of the PMOS and NMOS.


![Screenshot 2024-12-19 123315](https://github.com/user-attachments/assets/647939b0-1f2f-4839-af2d-42e24ba5a51c)

**Component Values** : Althoug the size of PMOS is two times of NMOS, but for the simplicity we have taken here it as equal to NMOS. And the values of load capacitor 10fF



![Screenshot 2024-12-19 124846](https://github.com/user-attachments/assets/50753e8a-1ce5-454f-9267-1c90db780c18)

**Identify the nodes**:  Nodes are the points where two or more two branches are connected. Here we use nodes to repersents the component connected between them.



![Screenshot 2024-12-19 125242](https://github.com/user-attachments/assets/841784e8-e48d-4803-9146-b79622f2dadd)

**Name the nodes**:- Now we wiil name these nodes as Vin, Vss, Vdd, out.




![Screenshot 2024-12-19 125830](https://github.com/user-attachments/assets/c9b9ca28-f526-45a8-a929-10f97f3419cc)

Now we will start writing the SPICE deck. It's written like shown below

Drain- Gate- Source- Substrate

For **M1 MOSFET** drain is connected to out node, gate is connected to in node, PMOS transistor substrate and Source is connected to Vdd node.

For **M2 MOSFET** drain is connected to out node, gate is connected to in node, NMOS source and substrate are connected to 0.



![Screenshot 2024-12-19 130031](https://github.com/user-attachments/assets/5d57d4b4-d9b7-4cca-9dc0-3f8b915923bc)

## SPICE simulation lab for CMOS inverter

Till now we have described the connectivity information about CMOS inverter now we will describe the other components connnectivity information like load capacitor, source. Let's seee the connectivity of output load capacitor.

It is connected between out and the node 0. And it's value is 10ff. Supply voltage(Vdd) which is connected between Vdd and node 0 and value of it is 2.5 , Similarly we have input voltage which is connected between Vin and node 0 and its value is 2.5.


![Screenshot 2024-12-19 132659](https://github.com/user-attachments/assets/f1288b05-8c16-49d8-ac17-80bec227e3af)

Now we will do the SPICE simulation for the particular values. And will get the graph.


![Screenshot 2024-12-19 133250](https://github.com/user-attachments/assets/ca3c04d1-2be0-48ef-a10a-9a60a5a8a845)

## Switching Threshold Vm

These both model of different width has their own application. By comparing this both waveform, we can see that the shape of the both waveform is same irrespective of the voltage level.It tells that CMOS is a very roboust device. when Vin is at low, output is at high and when Vin is at high, the output is at low. so the charactoristic is maintain at all kind of CMOS with different size of NMOS or PMOS. That is why CMOS logic is very widely used in the design of the gates.

Switching thresold, Vm (the point at which the device switches the level) is the one of the parameter that defined the robustness of the Inverter. Switching thresold is a point at which Vin=Vout.




![Screenshot 2024-12-19 134320](https://github.com/user-attachments/assets/513b6097-e33e-484c-abc1-4b563a3432cf)

In the graph below we can identify that the PMOS and NMOS are in which region. The direction of current flowing is different for NMOS nad PMOS.


![Screenshot 2024-12-19 134523](https://github.com/user-attachments/assets/9fc001e0-0a61-445a-a436-e04b756dd707)

## Static and dynamic simulation of CMOS inverter

In Dynamic simulation we will know about the rise and fall delay of CMOS inverter and how does it varying with Vm. In this simulation everything else will remian same except the input which is provided will be a pulse and simulation command will be .tran

The graph Time vs Voltage will be plotted here from where we can calculate the rise and fall delay.


![Screenshot 2024-12-19 165035](https://github.com/user-attachments/assets/9592264a-c88f-4217-8d5c-497668f8ab7f)


![Screenshot 2024-12-19 165312](https://github.com/user-attachments/assets/d6aacefc-1167-41a1-b5b7-551e9e96e46b)

## Lab steps to git clone vsdstdcelldesign 

To get the clone, copy the clone address from reporetery and paste in openlane terminal after the command git clone. this will create the folder called "vsdstdcelldesign" in openlane directory.


![open8](https://github.com/user-attachments/assets/5a2527eb-3072-4ba3-9475-a2b0cb479da5)

now, if we open the openlane directory, we find the vsdstdcelldesing folder in the openlane directory.


![Screenshot 2024-12-19 172222](https://github.com/user-attachments/assets/8db4ecc9-831d-4c99-8305-b802c0daf2f4)

Now if we goe to the vsdstdcelldesign folder and open it, we get the .mag file,libs file etc.


![Screenshot 2024-12-19 172612](https://github.com/user-attachments/assets/d1d929d5-2067-4ae4-bf08-2995744c7d2f)

Now, here to see the layout in magic, we don't need to write the whole address because we copy the tech file here.Now, we can see the layout of CMOS inverter in the magic like this.



![Screenshot 2024-12-19 173933](https://github.com/user-attachments/assets/6e7c2154-c247-41b0-b8ec-d4beb3ba4e3d)


## (b) Inception of layout ̂A CMOS faabrication process

**Create Active regions** 
**1) selecting a substrate**:- we have a p-type silicon substrate having high resistivity(5-50ohm) well dopped, and orintation(100).

**2) creating active region for transistor**:- Region where you see PMOS and NMOS. On p-type substrate we are going to create some small pockets which will be called as active region and in these pockets we are going to create PMOS and NMOS transistor. Will cretae isolation between each and every pockets.

We create the isolation layer by depositing the Sio2 layer (~40nm) on the substrate. Now, we are depositing the Si3N4 layer (~80 nm) on the Sio2 layer.



![Screenshot 2024-12-19 185817](https://github.com/user-attachments/assets/910a3c3e-6853-477b-b83d-a6f21ea6ab11)


Before creating the pocket identify the region where we need to crete the pocket. Now will deposite a layer of photoresist(~1um) on which we will create some mask1 using UV light.

![Screenshot 2024-12-19 190127](https://github.com/user-attachments/assets/e51b2201-3ede-4a66-adb5-4e3f23dc2371)

Here exposed area will soften using UV rays and then later on it will be washed out


![Screenshot 2024-12-19 190218](https://github.com/user-attachments/assets/50292f41-a6b5-4148-9d5d-f8a14255c81b)

In the next step we will remove the mask and then will do etching to remove the unwanted area

![Screenshot 2024-12-19 190536](https://github.com/user-attachments/assets/735d3fde-757c-4a55-afa9-ae9ad2517682)


**Formation of N-well and P-well**

**3) N-well and P-well formation**:- we can not form P-well and N-well at a same time. we have to protect a region while forming one of the region by photoresist. And then using mask 2 and UV light, we will do patterning of photoresist to form P-well


![Screenshot 2024-12-19 191158](https://github.com/user-attachments/assets/2b703ff9-b67c-45fc-8ff6-2d0f700ab6d1)



![Screenshot 2024-12-19 191318](https://github.com/user-attachments/assets/e6b06a33-7b42-4d1c-8d06-5787c77cd90e)

Here in N-well we will fabricate PMOS transistor and in P-Well we will fabricate NMOS transistor.

**(4) Formation of Gate Terminal**

To form the gate terminal for PMOS and NMOS we repeate all the process ,like masking the surface, exposing to the UV rays and then etching out the unwanted area etc.


![Screenshot 2024-12-19 192313](https://github.com/user-attachments/assets/e0cb09f2-cc9c-4085-8476-3b30b10ac2ce)

## Lightly doped drain (LDD) formation

**5) LDD formation**:- Here, we actully want P+,P-,N doping profile in the PMOS and N+,N-,P doping profile for NMOS. Reason for that is

Hot electron effect

short channel effect

For the formation of LDD, we again do ion implantation in P-well by using mask 7 and here we use phosphoros as a ion for light doping.

![Screenshot 2024-12-19 193536](https://github.com/user-attachments/assets/ae5cbd7d-8629-4e02-879a-9eea7d3486fd)



![Screenshot 2024-12-19 193845](https://github.com/user-attachments/assets/e673af2d-a64e-4537-a404-e882d4b96a64)



## Source and Drain Formation 

Now to form the drain and source, again we do the ion implantation of arsenic at 75kev to create the N+ implant by using mask 9 in the P-well to form PMOS.


![Screenshot 2024-12-19 194241](https://github.com/user-attachments/assets/2b95c03a-9848-4c7f-8b52-2538b16b1b18)

Same process we will repeat for NMOS by using the mask 10 and boron ion in the N-well at 50kev to creat P- implant.



![Screenshot 2024-12-19 194442](https://github.com/user-attachments/assets/5077927e-62fb-4bf3-b03b-1d3d86e389e1)


And then after all these process we put them into high temperature analeaing 


![Screenshot 2024-12-19 194712](https://github.com/user-attachments/assets/250cbe57-af67-4292-a3dc-76833acc726c)

## Local interconnect formation

**7)steps tp form contacts and local interconnects**:- First step is remove the thin screen oxide layer by etching. Then deposite the titanium (Ti) using sputtering. here Ti is used because Ti has very low resistivity.


![Screenshot 2024-12-19 195506](https://github.com/user-attachments/assets/da58a49f-c60d-4682-9ea1-b54f0e1f605b)

Next step is to create the reaction between Ti layer and source, gate, drain of CMOS. For that wafer is heated at about 650-700 degree temparature in N2 ambient for about 60 seconds. and after reaction, we can see the titanium siliside over the wafer. One more reaction is heppend there between Ti and N. and it results the TIN which is used for local communication.


![Screenshot 2024-12-19 195641](https://github.com/user-attachments/assets/64e84a0d-87ed-4a37-bdde-0610c6fee0ea)

Now by using mask 11 and photoresist, we will etched out the TIN and make perticular contacts. TIN is etched out by using RCA cleaning.



![Screenshot 2024-12-19 195909](https://github.com/user-attachments/assets/bc3f4f50-f428-44d4-bad5-65e474241a32)

## Higher level metal formation

**8)Higher level metal formation**:- These steps are very semilar like previous steps. First thing that we are noticing is that the surface is non planner. it is not good to use this type of non planner serface for matel interconnects because of the problems regarding the metal disconinuty. so, we have to plannerize the surface by depositing the thick layer of sio2 with some impurity to make less resistive layer. and then we used CMP (chemical mechanical polishing) technique to plannerise the surface.


![Screenshot 2024-12-20 133958](https://github.com/user-attachments/assets/f6adace5-3469-4197-a266-89f2dd1a8de9)

Now again we will use previous steps to get metal contact done like masking , lithography and all, and then we will deposit a thin layer of titanium metal and then we will do again Chemical Mechanical polishing process to planarizing the surface.


![Screenshot 2024-12-20 135002](https://github.com/user-attachments/assets/226d1a10-1ede-4a56-8074-099f537e6626)

## Lab introduction to Sky130 basic layers layout and LEF using inverter


![Screenshot 2024-12-19 173933](https://github.com/user-attachments/assets/e4cd9ec2-9935-479e-bbbf-41e53c1bda91)


In sky130, every color is showing the different layer. here the first layer is for local interconnect shown by blue_purple color, then second layer is metal 1 which is shown by light purple color, and the metal 2 is shown by pink color. N-well is shown by solide das line. green is N-diffusion region. and red is for polysilicon gate. similarly the brown color is for P-diffusion.

In tckon window, we can see that the selected area is NMOS and similarly we can chech PMOS also. and that is how we can check that the CMOS is working or not.



![open1](https://github.com/user-attachments/assets/b36f1348-a293-42b2-8bfd-de584e956f75)

In similar way we can identify the PMOS of the inverter


![open2](https://github.com/user-attachments/assets/d8970282-3076-4f09-a4e8-a9ad8764069d)

we will use this .ext file to create the spice file to be use with our ngspice tool. for that we have apply the command ext2spice cthresh 0 rthresh 0. this will not create anything new. now again we have to type ext2spice command in tckon window.


![open4](https://github.com/user-attachments/assets/0bcb5de6-222d-4d62-8999-6388db57617a)

## (c) Sky130 Tech File Labs

**Lab steps to create final SPICE deck using Sky130 tech** 

Let's see what is inside spice file 



![eopen](https://github.com/user-attachments/assets/17da6a93-01f0-4f0d-b1af-2ca0681a8abf)


<div class="toc">
  <ul>
    <li><a href="#header-1">Day 4 - Pre-layout timing analysis and importance of good clock tree
</a></li>
	<ul>

 ## (a) Timing modeling using delay tables

 **Lab steps to convert grid info to track info**


 **Lab steps to convert magic layout to std cell LEF**

 **Introduction to timing libs and steps to include new cell in synthesis**


 **Introduction to delay tables**

 **Power Aware CTS**:- If we make enable pin at logic '1' in the AND gate, then clock will propagate and if we make it 'logic 0' it will block the clock. Similarly in 'OR' gate if we make enable as 'logic 0' it will propagate and on making it 'logic 1' it will block the clock.

So the advantage of this blocking period is that we can save lot of power in clock tree.


![Screenshot 2024-12-22 114835](https://github.com/user-attachments/assets/ff50a0d5-d94e-4ea4-bd7b-697b6959eb0b)



Let's say we have a clock tree, The buffer present at the first input is driving the load of second two buffers. We have splited the buffer and in clock gating technique we have just swaped the buffer with and gate so now will all the other characteristic will be same or will get changed will see in coming steps.


![Screenshot 2024-12-22 115242](https://github.com/user-attachments/assets/58bbdc70-2ebc-4f55-bc24-02b613910f20)

Before swaping the buffer with gate we have made some assumptions which are follows


![Screenshot 2024-12-22 115606](https://github.com/user-attachments/assets/a310ea26-f9b5-441e-bf21-deebfaff046f)

**How delay tables are prepared?**

For this purpose we have carried out the one buffer from the circuit and and seperately varying its input transition within some range of let's say 10ps-100ps than the output load will also vary so we willl characterise the delay and put the data in tabular format.



![Screenshot 2024-12-22 120129](https://github.com/user-attachments/assets/4e96f064-5db4-45a0-878f-fee4bb440276)

**Delay table usage Part 1**

Let's take the example for other buffers.


![Screenshot 2024-12-22 120802](https://github.com/user-attachments/assets/890f8398-ea21-43f6-9211-1b533d36894c)


For practical example let's say we have the input transition of 40ps of buffer1 the output capacitance of this particular buffer is 60ff. The delay of the cell in this case is lies between x9-x10.

So the values which are not available in the delay table those are extrapolated from the given data so we can take the range in that case.

**Delay table usage Part 2**
Now we have to calculate the delay of buffer 2 and after that we can find the latency at the 4 clock end points.

Here input transition is common for both the buffers. now assuming that the transition is around the 60psec and load at both the buffers is 50fF. so it will give the delay of y15.

The total delay from input to the output is= x9' + y15.(here we are ignoring the delay of the wires). that means the skew at the any output point is zero.

If load is not same at the every nodes, the skew will not be the zero.

**Lab steps to configure synthesis settings to fix slack and include vsdinv** 

We will try to modify the parameters of our cell by referring the README.md file in the configuration folder in openlane directory

The README.md file contains information about the parameters of the cell.



## (b)Timing analysis with ideal clocks using openSTA

**Setup timing analysis and introduction to flip-flop setup time**


**Timing analysis (with ideal clock)**:- Let's start the setup analysis with the ideal clock(single clock). specifications of the clock is

clock frequency =1 GHz

clock period =1 ns

Now will do the analysis between '0' and 'T' clock period. We sent at edge to the launch flop at '0' clock period and at T=1ns period the second edge reached to capture flop.

Let's say here we have combinatonal delay of theta and set up timing analysis says that this combinational delay should be less than the T for system to work properly.


![Screenshot 2024-12-22 130600](https://github.com/user-attachments/assets/ff76e1fa-22e9-4ba8-a9da-caa934e26a50)

Now let's open the capture flop and we will see some combinational circuit there it has several MOSFETs , several logics,resistances and capacitances inside it.Also have the time graph for this particular flop



![Screenshot 2024-12-22 131040](https://github.com/user-attachments/assets/9dd7e85e-68a4-4577-9f79-04f4400d382e)

When there is logic '0' or logic '1' of clock 1 the delay of MUX1 and MUX2 will restrict or effect the combinational delay requirement.

So there is some finite amount of time which is required to the D input to settle and this amount of time is reffered to as SET UP TIME.

Hence finite time 's' required before clk edge for 'D' to reach Qm.

So, we can write that the internal delay of the MUX1 = set up time(S).

So, now θ<T becomes θ<(T-S).

**Introduction to clock jitter and uncertainty**

So in Jitter the clock is being created by PLL(phase-locked loops) and the clk source is expected to sent the clk signal at exactly 0,T,2T,....But that clk source might or might ot be able to generate the clk exactly at 0 or any other certain time because of it's inbuilt variations that is called jitter. Jitter is refered as temporary variation of the clk pulse.


![Screenshot 2024-12-22 131450](https://github.com/user-attachments/assets/f0e86da7-ad8f-42dd-bc9f-dd30e4cc95e9)

Let's consider this uncertantity time(US) in consideration. So, now equation will become θ<(T-S-US). Now assuming 'S'=0.01ns and 'US'=0.09ns. by taking this, Let's identify the timing path in our circuit stage 1 and stage 3 logic path has single clock.

Now,we have to identify the combinational path delay for the both logics.


Let's consider this uncertantity time(US) in consideration. So, now equation will become θ<(T-S-US). Now assuming 'S'=0.01ns and 'US'=0.09ns. by taking this, Let's identify the timing path in our circuit stage 1 and stage 3 logic path has single clock.

Now,we have to identify the combinational path delay for the both logics.


![Screenshot 2024-12-22 131827](https://github.com/user-attachments/assets/bd03ef9a-e93b-4c59-a965-73c1d36a40f4)




![Screenshot 2024-12-22 132033](https://github.com/user-attachments/assets/b65f7d7f-5e64-464d-961d-152f590f3c56)



![Screenshot 2024-12-22 132159](https://github.com/user-attachments/assets/f6a22cda-c62e-45c5-a1f5-095487252d5e)



**Lab steps to configure OpenSTA for post-synth timing analysis**


**Lab steps to optimize synthesis to reduce setup violations**

## (c)Clock tree synthesis TritonCTS and signal integrity


**Clock tree routing and buffering using H-Tree algorithm**

Clock tree synthesis:- Let's connect clk1 to FF1 & FF2 of stage 1 and FF1 of stage 3 and FF2 of stage 4 with physical wire.


![Screenshot 2024-12-22 160547](https://github.com/user-attachments/assets/2cb9b678-6e43-48c0-b721-97a958594cd6)

Now let's see what is the problem with this? Let's consider some physical distance from clk to FF1 and FF2 , so due to this t2>t1.

Skew= t2-t1, and skew should be 0ps


![Screenshot 2024-12-22 160639](https://github.com/user-attachments/assets/84c4b2af-3c4f-4b43-892a-f6d81fbf607d)

Previously we have build bad tree now we will try to modify that in a smarter way. Hrre clk will come in somewhere mid points with this clk will reach to every flip flop at almost same time. In the same way we will connect the clk2 with flip flops like midpoint manner.



![Screenshot 2024-12-22 160852](https://github.com/user-attachments/assets/cb6156d0-19b3-4028-88e8-8ac998d6e695)
Now will se clock tree synthesis(Buffering), Let's we have some clock route through which it has to reach to particular locations and clock end points and in the path many capacitance, resitors are there.



![Screenshot 2024-12-22 161121](https://github.com/user-attachments/assets/408ceb74-d44c-4615-9789-01a071e25173)

Because of the wire length we did not get the same wave form at ouput as input and bcz of RC networks , so to resolve this problem we use repeaters. The only difference between the repeaters we use for clock or for data path is that clock repeaters repeaters will have equal rise and fall time.

First step is we will remove the clock route and place 2 repeaters and allow the clock to go through this particular repeater, in this case whatever wave form is generated here will go to the output. So we can as many as repeaters we want to make the continuous flow of th clock till the output.




![Screenshot 2024-12-22 161304](https://github.com/user-attachments/assets/04cb0e49-a3d6-431f-93fb-090d514de4a1)



**Crosstalk and clock net shielding**
**Clock Net Shielding** :- Till now we have built the clk tree in such a fashion that the skew between the launch flop and capture flop is 0. Skew means the latency difference between clk ports of the flop pins. Clk net shielding is the critical net scene in the design. We take the particular clk net and shield it means we protect the clk from the outside world, it's like house for tha clk.


![Screenshot 2024-12-22 161640](https://github.com/user-attachments/assets/75a423a7-94d6-492c-87a3-0d79730721e8)

If we do not protect the clk then two types of problem we can face Glitch and Delta delay

Let's consider on of the clk net. So whenever there is switching activity happening at the aggraser because of the coupling capacitance between the wires and this capacitance is so strong that any activity happening at the aggraser will directly impact the net which is close.


![Screenshot 2024-12-22 161857](https://github.com/user-attachments/assets/e2339ffc-3f9d-438e-83e1-4eb545992562)

The shielding is the technique, by which we can protect the net from these problems. In a shielding, we put wire between the either two wire where coupling capacitance is generate. This extra wire is grounded or connected to VDD.

We see the amount of delta delay because of the bump when we are switching from logic '1' to logic '0'. And skew is not anymore 0 here. So the impact of crosstalk delta delay is that it make the skew value non-zero.


![Screenshot 2024-12-22 162112](https://github.com/user-attachments/assets/364d9845-c35d-4915-89c6-ce56bbde040c)



**Lab steps to run CTS using Triton**


**Lab steps to verify CTS runs**

## (d) Timing analysis with real clock using openSTA


**Setup timing analysis using real clocks**

Circuit tree looks little bit different than ideal clock with real clock here we have buffers,wires etc Clock reach to launch flop and capture flop through a set of buffers.So clock signal will not reach to the buffer at t=0 time due to these buffers. So the combinational circuit equation will be (θ+1+2)<(T+1+3+4). Initially it was θ<T.


![Screenshot 2024-12-22 163435](https://github.com/user-attachments/assets/eda86697-6956-4f76-9236-aa77ceec3015)

Let's called "1+2"=∆1 and "1+3+4"=∆2 and (∆1-∆2)=skew


![Screenshot 2024-12-22 164021](https://github.com/user-attachments/assets/bb500495-4bc8-4667-a9e8-ab3d103afce0)


![Screenshot 2024-12-22 164143](https://github.com/user-attachments/assets/6b03c238-1912-475e-89f2-0ac6c32f84cd)

And here also, we have to consider the propogation skew (s) and uncertainty delay (US). so final equaltion becomes like, (θ+∆1)<(T+∆2-S-US).

we can also say that (θ+∆1)= data arrival time and (T+∆2-S-US)=data required time. If (Data required time)- (Data arrival time) = +ve then it is fine. If it is -Ve then it is called 'slack'.

**Hold timing analysis**:- It is littel bit different then setup timing analysis. here we are sending the first pulse to the both launch FLop and capture flop.

Hold condition state that, Hold time (H)< combinational delay (θ). So, (θ>H). And for real clock Hold time (H)< combinational delay (θ). So, (θ+1+2>H+1+3+4)




![Screenshot 2024-12-22 164745](https://github.com/user-attachments/assets/b676371c-b59f-408f-94be-384bfc1caf73)






**Hold timing analysis using real clocks**

Combinational delay should be grater then the hold time of the capture flip flop. Once the clk reaches the launch flop it takes ariund 2buffer delay(∆1) and when it reaches to the capture flip flop it takes around 3 buffer delay(∆2). Uncertainity will be same for both the flip flops becaiuse clock applied to both the flops from the same edge only. Now let's add the uncertainity value to it.



![Screenshot 2024-12-22 215742](https://github.com/user-attachments/assets/a2e26680-cc44-4219-b5b5-33a54a16ff32)

Let's identify the timing paths from design, with single clock


![Screenshot 2024-12-22 221827](https://github.com/user-attachments/assets/da11b9de-cabe-406e-80b5-78bc0473181b)



![Screenshot 2024-12-22 222013](https://github.com/user-attachments/assets/7faf4e17-621d-4286-83bd-c7e2998c6d6e)


![Screenshot 2024-12-22 222123](https://github.com/user-attachments/assets/7a4c38ec-7730-4480-87ca-a0e5d51983ee)


![Screenshot 2024-12-22 222158](https://github.com/user-attachments/assets/09c8e210-f19a-459f-a993-2ea5077b3917)



**Lab steps to analyze timing with real clocks using OpenSTA**

Lab steps to analyze timing with real clocks using OpenSTA
Now we can execute the following commands,

To load the created db file in Openroad

read_db pico_cts.db

To read the netlist post CTS

read_verilog /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/synthesis/picorv32a.synthesis_cts.v

To read the library for design

read_liberty $::env(LIB_SYNTH_COMPLETE)

To link the design and library

link_design picorv32a

To read the custom sdc we have created

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

To setting all clocks as propagated clocks

set_propagated_clock [all_clocks]

To Generate the custom timing report

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

To exit from Openlane flow

exit
 

