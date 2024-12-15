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


 
















