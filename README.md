# ADVANCED PHYSICAL DESIGN USING OPENLANE/SKY130
# Table Of Contents
## DAY 1
**Inception of Open-Source EDA, OpenLane and Sky130 PDK**
+ [How to Talk to Computers](#how-to-talk-to-computers)
  - Introduction to QFN-48 Package, Chip, Pads, Core, Die and IPs
  - Introduction to RISC-V
  - From Software Applications to Hardware
+ [SoC Design and OpenLane](#soc-design-and-openlane)
  - Introduction to all Components of Open-Source Digital ASIC Design
  - Simplified RTL2GDS Flow
  - Introduction to OpenLane and Strive Chipsets
  - Introduction to OpenLane Detailed ASIC Design Flow
+ [Open-Source EDA Tools](#open-source-eda-tools)
  - OpenLane Directory Structure
  - Design Preparation Step
  - Review Files after Design Prep and Run Synthesis
  - OpenLane Project Git Link Description
  - Steps to Characterize Synthesis Results

 ## DAY 2
 **Good Floorplan vs Bad Floorplan and Introduction to Library Cells
+ [Chip Floorplanning Considerations](#chip-floorplanning-considerations)
  - Utilisation Factor and Aspect Ratio
  - Concept of Pre-placed Cells
  - De-coupling Capacitors
  - Power Planning
  - Pin Placement and Logical Cell Placement Blockage
  - Steps to run Floorplan using OpenLane
  - Review Floorplan Files and Steps to View Floorplan
  - Review Floorplan Layout in Magic
+ [Library Binding and Placement](#library-binding-and-placement)
  - Netlist Binding and intial Place Design
  - Optimise Placement using Estimated Wire-Length and Capacitance
  - Final Placement Optimisation
  - Need for Libraries and Characterization
  - Congestion aware Placement using RePLAce
+ [Cell Design and Characterization Flows](#cell-design-and-characterization-flow)
  - Inputs for cell design flow
  - Circuit Design Step
  - Layout Design Step
  - Typical Characterization Flow
+ [General Timing Characterisation Parameters](#general-timing-characterisation-parameters)
  - Timing Threshold Definitions
  - Propagation Delay and Transition Time

# Day-1
## How to Talk to Computers
<details>
<summary> Introduction to QFN-48 Package, Chip, Pads, Core, Die and IPs </summary>  

**Arduino Board**
+ An Arduino board is a microcontroller-based development platform that allows you to create and prototype a wide range of electronics projects.
<p align='center'>
 <img width="488" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/953e6e1e-3a2d-4dbe-9e26-2a8bde4ea090">
</p>
<p align="center">
  Fig 1. Typical Design of Arduino Board
</p>

**QFN-48 Package**
+ QFN-48 stands for **Quad Flat No-Leads 48**, which is a type of surface-mount integrated circuit (IC) package.
+ QFN packages are commonly used in electronics to house integrated circuits, microcontrollers, and other semiconductor devices.
+ The **48** in QFN-48 refers to the number of pins or leads on the package.
<p align="center">
  <img width="446" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/a089c80c-67e3-4ab6-b034-242aa3c43f17">
</p>
<p align="center">
  Fig 2. QFN-48 Package
</p>

**Chip**
+ In electronics and technology, a **chip** typically refers to a semiconductor device, which is a small piece of silicon that contains integrated circuits.
+ These chips can be microprocessors, memory chips, sensors, or other electronic components. For example, a microprocessor chip is the **brain** of a computer.

<p align="center">
<img width="400" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bbc43d6e-cc64-48ed-93d1-c20b8eaedcf8">
</p>
<p align="center">
  Fig 3. Chip
</p>

**Pads**
+ They refer to the areas on the chip's surface where electrical connections can be made.
+ These pads are typically metalized areas with a specific pattern that allows for the attachment of wires, leads, or other components to create electrical connections.
+ Pads serve as the interface between the internal circuitry of the chip and the external world, such as a printed circuit board (PCB) or other devices.

**Die**
+ It refers to a small, usually rectangular, piece of a semiconductor wafer that contains a single integrated circuit (IC) or microchip.
+ During the manufacturing process, multiple ICs are fabricated on a single semiconductor wafer, and each individual IC is referred to as a "die."
+ After manufacturing, these dies are typically cut from the wafer and then packaged into separate integrated circuits for use in electronic devices.

**Core**
+ It refers to a processing unit within the chip that can independently execute instructions and perform computations.
+ These cores are often referred to as **CPU cores**.
+  A chip may contain one or multiple CPU cores, each capable of running its own set of instructions and performing tasks concurrently.
+  The presence of multiple cores on a single chip is known as **multi-core processing**.

<p align="center">
<img width="466" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/b9231cfb-4caf-407e-a62f-980588abccc3">
</p>
<p align="center">
  Fig 4. Sample RISC-V SoC
</p>

**IPs**
+ It stands for **Intellectual Property** or **IP blocks**.
+ These are pre-designed and pre-verified functional blocks or components that are often licensed or acquired from third-party companies and integrated into a chip's design.
+ IPs help semiconductor companies save time and resources by incorporating well-tested and specialized functionality into their chips, rather than designing everything from scratch.

**Foundry**
+ It refers to a specialized manufacturing facility that produces semiconductor devices, integrated circuits (ICs), and other microelectronic components on behalf of other companies.
+ These facilities are also commonly known as semiconductor fabrication plants or fabs.

**Macros**
+ They refer to pre-designed and pre-verified blocks of logic or functional circuits that are often used for specific tasks within a chip's design.
+ Macros are similar to Intellectual Property (IP) blocks but are typically larger and more complex.
+ They are used to provide standardized, reusable, and well-optimized functionality within a chip.

</details>

<details>
<summary> Introduction to RISC-V </summary> 

**ISA (Instruction Set Architecture)**
+ ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.

**RISC-V (Reduced Instruction Set Computing - Five)**
+ It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
+ RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<p align="center">
  <img width="536" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4eabe0b7-4581-419b-88e7-84c7ac1dac8e">
</p>
<p align="center">
  Fig 5. Design Flow
</p>
</details>

<details>
<summary> From Software Applications to Hardware </summary>  

1. **Apps:** Application software, often referred to simply as **applications** or **apps**, is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.
4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.
5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.
6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.
7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

</details>

## SoC Design and OpenLane
<details>
<summary> Introduction to all Components of Open-Source Digital ASIC Design </summary>  

**PDK**
+ It stands for **Process Design Kit**.
+  It is a collection of files, models, documentation, and tools that are provided by semiconductor foundries to assist integrated circuit (IC) designers in creating and verifying their designs for a specific semiconductor manufacturing process.
+  PDKs are essential for the design and development of semiconductor chips because they provide the necessary information and resources for designers to create circuits that are compatible with the foundry's fabrication process.

**EDA Tools**
+ EDA (Electronic Design Automation) tools are a set of software applications and tools used by electronics engineers and integrated circuit (IC) designers to design, simulate, verify, and analyze electronic circuits and systems.
+ These tools are essential for designing complex electronic devices, ranging from simple integrated circuits to advanced microprocessors and systems-on-chip (SoCs).
<p align="center">
  <img width="317" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/e43d7528-a6a7-4ee4-aacf-b8312364a5e9">
</p>

**130nm**
+ It refers to a semiconductor manufacturing process technology node, which represents the minimum feature size or transistor gate length in that technology.
+ In semiconductor manufacturing, the feature size is a critical metric because it determines the size and performance characteristics of the transistors and other components that make up integrated circuits (ICs).

</details>

<details>
<summary> Simplified RTL2GDS Flow </summary>

**RTL to GDSII**
<p align="center">
  <img width="381" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/0ccd4b81-4965-4194-8d62-ca2b79d761e2">
</p>
<p align="center">
  Fig 1. Simplified RTL to GDS FLow
</p>

+ **Synthesis**
  -  It refers to the process of converting a high-level hardware description into a gate-level representation that can be implemented on a specific hardware technology or semiconductor manufacturing process.
 
+ **Floor and Power Planning**
  - **Chip floor planning** is the process of partitioning the chip die between different system building blocks and place the I/O pads.
  - **Macro floor planning**, also known as block-level floor planning, is a specific aspect of chip floor planning that focuses on the arrangement and organization of large functional blocks or macros within an integrated circuit (IC) design. 
  - **Power planning** also known as power distribution network (PDN) design, focuses on the distribution and management of power and ground connections within the chip. It ensures that all components receive stable power supplies and that power is efficiently distributed throughout the chip.
 
+ **Placment**
  - It refers to the process of determining the physical locations of individual components, such as logic gates, flip-flops, memory cells, and other elements, on the semiconductor die or chip.
  - **Global placement** involves determining approximate positions or locations for major functional blocks, macros, and components on the semiconductor die or chip.
  - **Detailed placement** also known as fine-grained placement, is a critical step in the physical design of integrated circuits (ICs) that follows global placement.
During the detailed placement phase, the positions of individual components, such as logic gates, flip-flops, and memory cells, are determined with high precision within the semiconductor die or chip.

+ **Clock Tree Synthesis**
  - It involves the generation and optimization of a hierarchical tree-like network of clock distribution that ensures synchronized clock signals are delivered efficiently to all flip-flops and other clocked elements within the chip.
  - The primary objectives of clock tree synthesis are to minimize clock skew, reduce clock routing congestion, and meet strict timing requirements.

+ **Routing**
  - It is responsible for establishing the electrical connections (wires or metal traces) that allow signals to flow between different parts of the chip.
  - **Global routing**, also known as channel routing, is the first phase of routing. It determines the general paths for wires that connect different components or blocks on the chip. Global routers aim to minimize the total wirelength while adhering to design rules and constraints.
  - Once the general paths are defined in global routing, detailed routing comes next.
  - **Detailed routing** focuses on individual nets (connections) and determines the specific paths and wires that connect the pins of components or gates. It also resolves any conflicts or overlaps between wires.

+ **Sign-Off**
  - It signifies the point at which a specific design step or aspect has been completed, reviewed, and verified to meet certain criteria or standards.
  - **Physical Verification** sign-off phase covers a range of physical design verification checks, including DRC, LVS, and other manufacturing-oriented checks. It ensures that the design is ready for manufacturing and fabrication.
  - **Timing verification** sign-off specifically focuses on verifying that the chip meets the required timing constraints, such as setup and hold times, clock-to-q delays, and maximum clock frequency. This involves detailed timing analysis and simulation to ensure that the design operates correctly at the specified clock frequencies.
</details>

<details>
<summary> Introduction to OpenLane and Strive Chipsets </summary>

+ **OpenLane**
  - OpenLANE is an opensource tool or flow used for opensource tape-outs.
  - The OpenLANE flow comprises a variety of tools such as Yosys, ABC, OpenSTA, Fault, OpenROAD app, Netgen and Magic which are used to harden chips and macros, i.e. generate final GDSII from the design RTL. The primary goal of OpenLANE is to produce clean GDSII with no human intervention.
  -  OpenLANE has been tuned to function for the Google-Skywater130 Opensource Process Design Kit.

+ **Strive Chipsets**
<p align="center">
  <img width="239" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/2758ce5f-9301-4876-929e-72d93de298f6">
</p>
<p align="center">
  Fig 2. Strive SoC Family
</p>

</details>

<details>
<summary> Introduction to OpenLane Detailed ASIC Design Flow </summary>


<p align="center">
  <img width="584" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8d1647a2-0d27-46a6-b9ad-e9f59984401a">
</p>

<p align="center">
  Fig 3. OpenLane ASIC Flow
</p>

+ **OpenLane Regression Testing**
 - Regression testing in the context of OpenLane refers to the process of running a set of predefined test cases or scripts on the OpenLane design automation framework to ensure that recent changes or updates to the framework have not introduced new bugs or regressions.

+ **Design for Test(DFT)**
  - Scan Insertion
  - Automatic Test Pattern Generation(ATPG)
  - Test Patterns Compaction
  - Fault Coverage
  - Fault Simulation
  
+ **Physical Implementation** (automated PnR(Place and Route)) (OpenRoad)
  - Floor/Power Planning
  - End Decoupling Capacitors and Tap cells insertion
  - Placement : Global and Detailed
  - Post placmnet optimisation
  - Clock Tree synthesis
  - Routing : Global and Detailed

 + **Logic Equivalence Check** (yosys)
   - Everytime the netlist is modified, verification must be performed.
   - LEC is used to formally confirm that the function did not change after modifying the netlist.
  
+ **Dealing with antenna rules violations**
  - When a metal wire segment is fabricated, it can act as an antenna.
  - Reactive ion etching causes charge to accumulate on the wire.
  - Transistor gates can be damaged during fabrication.
  - Two solutions:
    + Bridging attaches a higher layer intermediary.
    + Add antenna diode cell to leak away charges.
  - We took a preventive approach:
    + Add a fake antenna diode next to every cell input after placement.
    + Run the antenna check(**Magic**) on the routed layout
    + If the checker reports a violation on the cell input pin, replace the fake diode cell by a real one.
   
+ **Static Timing Analysis**
  - Static Timing Analysis (STA) is a critical step in the design and verification of integrated circuits (ICs) and other digital systems.
  - It is used to ensure that a digital design meets its required timing constraints and operates correctly within a given clock frequency.
  - STA is performed during the physical design phase of chip development and is crucial for assessing and optimizing the performance and reliability of digital systems.
 
+ **Physical Verification**
  - **LVS (Layout vs Schematic)** is a process that ensures that the physical layout of a chip or circuit matches its intended logical or schematic representation.
  - **DRC (Design Rules Checking)** is a process that ensures that the layout of a chip or circuit adheres to the specific design rules and constraints defined by the semiconductor manufacturing process. 
  - **Magic** is used for design rules checking and SPICE extraction from Layout.
  - **Magic** and **Netgen** are used for LVS

</details>

## Open-Source EDA Tools
<details>
<summary> OpenLane Directory Structure </summary>

+ PDK used in this workshop is Skywater 130nm PDK and OpenLane is built around this PDK.
<p align="center">'
  <img width="580" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8d8a1f07-abbc-46e6-8616-ff13da29ff3b">
</p>
<p align="center">
  Fig 1.
</p>

+ **skywater-pdk** contains all the PDK related files.
+ **open_pdks** contains all the scripts and files that convert these foundry level PDKS to be compatible with the open-source EDA tools
+ **sky130A** is made compatible with our open-source environment.

<p align="center">
  <img width="644" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8dd1e174-9c23-4dcf-a90d-56e5179934be">
</p>
<p align="center">
  Fig 2.
</p>

+ **libs.ref** seems specific to technology.
+ **libs.tech** seems specific to the tool.

<p align="center">
  <img width="744" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/cc73e63f-4629-4b99-8047-e314f9008992">
</p>
<p align="center">
  Fig 3.
</p>

+ **sky130_fd_sc_hd** has all the technology files.
</details>

<details>
<summary> Design Preparation Step </summary>

+ To invoke OpenLane

<p align="center">
  <img width="536" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8b8830dd-7aa4-4e8a-a5ae-51635f8ce4c1">
</p>
<p align="center">
  Fig 4.
</p>

+ Under **Designs** folder, we are going to use **picorv32a**.
+ **src** files contains verilog and sdc file.
<p align="center">
 <img width="697" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4f26eb47-4c0f-4e33-8775-f1144e2cd09b">
</p>
<p align="center">
  Fig 5.
</p>

+ `less config.tcl`

<p align="center">
<img width="763" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/6200069a-9833-4036-80df-4f7d48a42a3a">
</p>
<p align="center">
Fig 6.
</p>

+ We are going to prepare the design.
+ `prep -design picorv32a`.
<p align="center">
  <img width="904" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/81d463c2-4fe6-4a44-b52b-9ac65c54c718">
</p>
<p align="center">
  Fig 7.
</p>
</details>

<details>
<summary> Review Files after Design Prep and Run Synthesis </summary>

<p align="center">
<img width="781" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/d688e5cc-0d8c-47a5-8a98-4ec60a20933c">
</p>
<p align="center">
  Fig 8.
</p>

<p align="center">
<img width="869" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/c69a48e8-1d1a-447e-844d-a349b8f20c38">
</p>
<p align="center">
  Fig 9.
</p>

<p align="center">
<img width="841" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bb4a57cb-a9a1-4ec4-9719-cbab4f6e3b7b">
</p>
<p align="center">
  Fig 10.
</p>

+ `%run_synthesis`

<p align="center">
  <img width="716" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/fdde08ee-bab4-49ba-8c62-7597234aa04c">
</p>
<p align="center">
  Fig 11.
</p>

</details>

<details>
<summary> OpenLane Project Git Link Description </summary>  

+ To know more about openlane

https://github.com/efabless/openlane2

</details>

<details>
<summary> Steps to Characterize Synthesis Results </summary>

+ To calculate the clock ratio, we need
  - the number of D Flipflops = 1613
  - the number of cells = 14876
+ The clock ratio is dff/cells = 0.108
<p align="center">
<img width="311" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/07f50ebb-7621-4f21-a697-d847c1cb4857">
</p>
<p align="center">
  Fig 12.
</p>

+ To view the synthesised netlist

`less picorv32a.synthesis.v`

<p align="center">
  <img width="809" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/f5017424-2fec-4eb6-b89c-1f42982afb80">
</p>
<p align="center">
  Fig 13.
</p>

+ To view the actual statistical synthesis report

`less 1-yosys_4.stat.rpt`
<p align="center">
<img width="223" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/b92a2e88-2ad1-48e1-bb0f-1a972ff6d3cc">
</p>
<p align="center">
  Fig 14.
</p>

</details>

# Day-2
## Chip Floorplanning Considerations
<details>
<summary> Utilisation Factor and Aspect Ratio </summary>

+ Begin with a netlist.
+ Convert the symbols into physical dimensions.
+ Calculate the area occupied by the netlist on a silicon wafer.
+ Place all the logical cells inside the core.
+ If all the logical cells occupy the complete area of the area, then the utilisation is 100%.
+ We can calculate the utilisation factor and the aspect ratio by the formulae given below:

<p align="center">
  <img width="227" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/34bdb376-7176-49e2-a063-f2a4e134c73b">
</p>
<p align="center">
  Fig 1. Formulae
</p>

</details>

<details>
<summary> Concept of Pre-placed Cells </summary>

+ Consider a combinational logic which is converted into netlist
<p align="center">
  <img width="450" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/32a474db-664f-4c2a-a84b-f7274c2470b4">
</p>
<p align="center">
  Fig 2.
</p>

+ Cut the circuit into two parts and separate them out.
<p align="center">
  <img width="530" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/47c738d0-e371-499d-9c5f-1128cdfbce4c">
</p>
<p align="center">
  Fig 3.
</p>

+ Extend the IO pins
<p align="center">
  <img width="287" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4cffdcd0-7b68-4396-bf39-9ffe31a7147c">
</p>
<p align="center">
  Fig 4.
</p>

+ Black box the boxes
<p align="center">
<img width="278" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8e05e87b-e1e4-436f-842b-d348dbb2bdef">
</p>
<p align="center">
  Fig 5.
</p>

+ Separate the black boxes as two different IPs or modules
<p align="center">
<img width="426" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/85fe19b7-05c7-44df-a4f3-a5d3382b850f">
</p>
<p align="center">
  Fig 6.
</p>

+ The arrangement of these IPs in the chip is referred as **Floorplanning**.
+ These IPs/blocks have user-defined locations and hence are placed in the cell before automated placement-and-routing and are called as **pre-placed-cells**.
+ Automated placement and routing tools place the remaining logical cells in the design onto the chip.
</details>

<details>
<summary> De-coupling Capacitors </summary>  

+ Define locations for pre-placed cells.
+ Surround the cells with de-coupling capacitors.
+ Decoupling capacitors, also known as bypass capacitors or noise-reduction capacitors, are electronic components used in electronic circuits to stabilize and improve the performance of integrated circuits (ICs) and other semiconductor devices.
+ They are a vital part of circuit design, especially in digital and mixed-signal electronics.
+ When a circuit is powered, especially in digital circuits where there are rapid transitions between logic states, the current demand can change rapidly. Decoupling capacitors are placed close to the power pins of ICs, such as microcontrollers or processors, to counteract these rapid changes.

<p align="center">
  <img width="413" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/366cbede-bc0a-4a6d-bcc6-f63434adfff7">
</p>
<p align="center">
  Fig 7.
</p>

</details>

<details>
<summary> Power Planning </summary>  
+ Power planning refers to the process of strategically managing and distributing electrical power within a circuit or system to ensure reliable and efficient operation.
+ Effective power planning is essential in modern electronics to meet performance, power consumption, and thermal constraints. 

<p align="center">
  <img width="518" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/a173fa1b-ecf1-49a6-9389-bd8d74cdd340">
</p>
<p align="center">
  Fig 8.
</p>

</details>
