# ADVANCED PHYSICAL DESIGN USING OPENLANE/SKY130
# Table Of Contents
## DAY 1
**Inception of Open-Source EDA, OpenLane and Sky130 PDK**
+ [How to Talk to Computers](#how-to-talk-to-computers)
+ [SoC Design and OpenLane](#soc-design-and-openlane)
+ [Open-Source EDA Tools](#open-source-eda-tools)
  
## DAY 2
**Good Floorplan vs Bad Floorplan and Introduction to Library Cells**
+ [Chip Floorplanning Considerations](#chip-floorplanning-considerations)
+ [Library Binding and Placement](#library-binding-and-placement)
+ [Cell Design and Characterization Flows](#cell-design-and-characterization-flow)
+ [General Timing Characterisation Parameters](#general-timing-characterisation-parameters)

## DAY 3
**Design Library Cell using Magic Layout and Ngspice Characterisation**
+ [Labs for CMOS Inverter Ngspice Simulations](#labs-for-cmos-inverter-ngspice-simulations)
+ [Inception of Layout](#inception-of-layout)
+ [Sky130 Tech File Labs](#sky130-tech-file-labs)
  
## DAY 4
**Pre-Layout Timing Analysis and importance of Good CLock Tree**
+ [Timing Modelling Using Delay Tables](timing-modelling-using-delay-tables)
+ [Timing Analysis with Ideal Clocks using openSTA](#timing-analysis-with-ideal-clocks-using-opensta)
+ [Clock Tree Synthesis TritonCTS and Signal Integrity](#clock-tree-synthesis-tritoncts-and-signal-integrity)
+ [Timing Analysis with Real Clocks using OpenSTA](#timing-analysis-with-real-clocks-using-opensta)

## DAY 5
**Final Steps for RTL2GDS**
+ [Routing and DRC](#routing-and-drc)
+ [Power Distribution Network and Routing](#power-distribution-network-and-routing)

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

<details>
<summary> Pin Placement and Logical Cell Placement Blockage </summary>

**Pin Placment**
+ Pin placement, also known as I/O (Input/Output) placement, is a crucial step in the physical design of an integrated circuit (IC).
+ It involves determining the locations and positions of input and output pins on the chip's package or die.
+ Proper pin placement is essential to ensure that the IC can interface with the external world effectively, meet performance requirements, and adhere to manufacturability constraints.

<p align="center">
  <img width="342" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1f7b19e7-addd-4188-b7d7-98bdc9b9a50e">
</p>
<p align="center">
  Fig 9. Circuit Example
</p>

<p align="center">
  <img width="419" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/aab16f1d-6deb-4619-8a14-4311f916b872">
</p>
<p align="center">
  Fig 10. Pin placement for the Circuit
</p>

**Logical Cell Placement Blockage**
+ Logical cell placement blockage, often referred to as blockage constraints or blockage regions, is a concept used in the physical design of integrated circuits (ICs).
+ Blockage constraints are used to restrict or reserve specific areas of the chip's layout for various purposes, such as accommodating specialized circuitry, ensuring signal integrity, or meeting manufacturing requirements.

<p align="center">
  <img width="446" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/07e33231-302b-47eb-a400-d7796c51adb8">
</p>
<p align="center">
  Fig 11. Logical Cell Placement Blockage for the Circuit
</p>

</details>

<details>
<summary> Steps to run Floorplan using OpenLane </summary>

+ `less floorplan.tcl`
<p align="center">
<img width="230" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/882a9fd5-5338-43f8-8395-0de6aec6669a">
</p>
<p align="center">
  Fig 12.
</p>

+ `less config.tcl`
<p align="center">
<img width="780" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/906d421d-ef8f-4ed3-88eb-fea7e6911146">
</p>
<p align="center">
  Fig 13.
</p>

+ `%run_floorplan`
<p align="center">
<img width="908" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/05a0ed9e-1673-4904-b7b5-69f2ed8a5e4c">
</p>
<p align="center">
  Fig 14.
</p>

</details>

<details>
<summary> Review Floorplan Files and Steps to View Floorplan </summary>

<p align="center">
<img width="886" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/85df9627-fb26-436c-9f23-6fc653fd564f">
</p>
<p align="center">
  Fig 15.
</p>

<p align="center">
<img width="496" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/90a8e19b-9d4e-4894-81ca-13058b6d90ae">
</p>
<p align="center">
  Fig 16.
</p>

<p align="center">
<img width="910" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/068120f1-4d43-4de4-b33a-2d1fd7d773c0">
</p>
<p align="center">
  Fig 17.
</p>

<p align="center">
<img width="395" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/04010e78-508a-4a2f-a5aa-975688049236">
</p>
<p align="center">
  Fig 18.
</p>

</details>

<details>
<summary> Review Floorplan Layout in Magic </summary>
  
 `magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &`

<p align="center">
<img width="711" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/5cb06161-be66-4d66-a48b-447ff645608f">
</p>
<p align="center">
  Fig 19.
</p>

+ When viewed the horizontal metal layer
<p align="center">
<img width="734" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/88b24fe9-0b63-4cff-8630-b35be1ef1d8b">
</p>
<p align="center">
  Fig 20.
</p>

+ When viewed the vertical metal layer
<p align="center">
<img width="736" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/eb472d5a-269b-43cf-b97f-a8e8cfc62d07">
</p>
<p align="center">
  Fig 21.
</p>

</details>

## Library Binding and Placement
<details>
<summary> Netlist Binding and Initial Place Design </summary>

**Netlist Binding**
+ Netlist binding is a crucial step in the process of transforming a high-level design description into a representation that can be physically implemented on a chip or printed circuit board (PCB).
+ This step involves associating the logical components and connections described in the netlist with physical components, such as gates, flip-flops, and interconnections, that will be used in the actual implementation.

<p align="center">
  <img width="584" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4778d23c-a1cf-4368-9993-bfc2c9a3cb78">
</p>
<p align="center">
  Fig 1.
</p>

</details>

<details>
<summary> Optimise Placement using Estimated Wire-Length and Capacitance </summary>

+ We need to estimate the wire length and capacitance, and based on that insert repeaters.

<p align="center">
  <img width="406" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/dbe73423-c63e-440d-88ce-ac2d9c72a11c">
</p>
<p align="center">
  Fig 2.
</p>

</details>

<details>
<summary> Need for Libraries and Characterization </summary>

**Library Characterisation**
+ Library characterization is the process of creating a comprehensive and accurate characterization model for a library of standard cells.
+ These standard cells serve as the fundamental building blocks for designing digital circuits.
+ The goal of library characterization is to provide designers with essential information about how these cells behave under various operating conditions, allowing for accurate timing analysis and optimization.

</details>

<details>
<summary> Congestion aware Placement using RePLAce </summary>

+ `%run_placement`
<p align="center">
<img width="320" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/2257f078-126d-4627-aafa-3343a07709bf">
</p>
<p align="center">
  Fig 3.
</p>

+`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

<p align="center">
<img width="695" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/51f8adf9-436f-49c1-ab07-6eb3467e0dd4">
</p>
<p align="center">
Fig 4.
</p>

</details>

## Cell Design and Characterization Flows
<details>
<summary> Inputs for Cell Design Flow </summary> 

**Cell Design Flow**
<p align="center">
  <img width="189" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/97b725b8-ee8d-42fa-9659-17d2e014343d">
</p>
<p align="center">
  Fig 1.
</p>

**Inputs:**
+ PDKs (Process Design Kits):
- PDKs are essential resources provided by semiconductor foundries.
- They contain information about the fabrication process, including the available semiconductor technology, transistor models, and design rules.
- PDKs enable IC designers to create layouts and perform simulations that are compatible with the specific manufacturing process of the foundry.

+ DRC (Design Rule Checking) and LVS (Layout vs. Schematic) Rules:
- DRC rules are a set of guidelines that ensure that the physical layout of a chip adheres to the foundry's manufacturing process requirements.
- LVS rules ensure that the electrical characteristics of the layout match the intended schematic design.
- Both DRC and LVS checks are crucial for identifying and rectifying design errors and ensuring manufacturability and functionality.

+ SPICE Models:
- SPICE (Simulation Program with Integrated Circuit Emphasis) models are mathematical representations of electronic components (transistors, resistors, capacitors, etc.).
- They describe how these components behave electrically under different conditions.
- SPICE models are used for circuit simulation to analyze the performance of an IC design and predict its behavior.

+ Library:
- A library in IC design contains a collection of pre-designed, standardized components (e.g., logic gates, flip-flops, analog blocks) that can be used to build more complex circuits.
- Libraries save time and effort by providing readily available building blocks for designing ICs.
- Libraries often include SPICE models for each component, allowing for accurate simulation.

+ User-Defined Specifications:
- User-defined specifications are custom requirements and constraints set by the IC designer for a specific design project.
- These specifications can include performance goals (e.g., speed, power consumption), design constraints (e.g., area, power budget), and unique functionality requirements.
- User-defined specifications guide the entire IC design process, influencing choices made in terms of circuit design, layout, and simulation.

</details>

<details>
<summary> Circuit Design Step </summary>

+ Circuit design involves creating the logical and functional representation of digital or analog circuits using hardware description languages (HDLs) like Verilog or VHDL.
+ This step defines the behavior of the circuit without specifying its physical layout.
+ Key tasks include defining circuit functionality, specifying input and output behaviors, selecting components like logic gates or transistors, and optimizing for desired performance metrics.

</details>

<details>
<summary> Layout Design Step </summary>

+ Layout design is the process of creating the physical arrangement of components, such as transistors, interconnections, and metal layers, on the silicon substrate to implement the circuit designed in the previous step.
+ Layout designers adhere to design rules and guidelines specific to the semiconductor process technology to ensure manufacturability.
+ Key tasks include transistor placement, routing of metal layers, ensuring signal integrity, and minimizing area while meeting performance requirements.

</details>

<details>
<summary> Typical Characterization Flow </summary>

+ Characterization involves the comprehensive evaluation and modeling of the circuit's behavior under various conditions, ensuring that it meets design specifications and performance goals.
+ This step generates timing models, power models, and other characterization data to describe how the circuit performs under different operating conditions (e.g., voltage, temperature, process variations).
+ Characterization data is crucial for accurate static timing analysis, power estimation, and integration of the circuit into larger designs.

</details>

## General Timing Characterisation Parameters
<details>
<summary> Timing Threshold Definitions </summary>

<p align="center">
  <img width="520" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/fbb86265-278e-4ece-b4b9-12184a5fb7e5">
</p>
<p align="center">
  Fig 1.
</p>

<p align="center">
  <img width="289" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/f88636f1-87c1-4eae-ba89-736ea5b5bd9f">
</p>
<p align="center">
  Fig 2.
</p>

**Slew Low Rise Threshold (slew_low_rise_thr):**
+ This parameter defines the minimum input signal slope (rate of change) required to trigger a rising transition in the output signal.
+ It helps characterize how fast an input signal must rise to initiate a change in the output signal from low to high.

**Slew High Rise Threshold (slew_high_rise_thr):**
+ Similar to the slew_low_rise_thr, this parameter defines the minimum input signal slope required to trigger a rising transition in the output signal, but for signals that are already at a high logic level.

**Slew Low Fall Threshold (slew_low_fall_thr):**
+ This parameter defines the minimum input signal slope required to trigger a falling transition in the output signal.
+ It specifies how fast an input signal must fall to initiate a change in the output signal from high to low.

**Slew High Fall Threshold (slew_high_fall_thr):**
+ Like the slew_low_fall_thr, this parameter defines the minimum input signal slope required to trigger a falling transition in the output signal, but for signals that are already at a high logic level.

**Input Rise Threshold (in_rise_thr):**
+ This parameter represents the threshold voltage level at which an input signal is considered to be transitioning from low to high.
+ It is essential for accurate timing analysis and helps determine when inputs trigger changes in the circuit.

**Input Fall Threshold (in_fall_thr):**
+ Similar to in_rise_thr, this parameter represents the threshold voltage level at which an input signal is considered to be transitioning from high to low.

**Output Rise Threshold (out_rise_thr):**
+ This parameter defines the threshold voltage level at which an output signal is considered to be transitioning from low to high.
+ It is used to specify the timing behavior of the circuit's outputs.

**Output Fall Threshold (out_fall_thr):**
+ Similar to out_rise_thr, this parameter defines the threshold voltage level at which an output signal is considered to be transitioning from high to low.

</details>

# Day-3
## Labs for CMOS Inverter Ngspice Simulations
<details>
<summary> IO Placer </summary>

+ In order to change the distance between the IO pins:

  ` % set ::env(FP_IO_MODE) 2`
  `% run_floorplan`

<p align="center">
<img width="371" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/19090a7e-cfae-4fa4-9660-3dbc2adc7ddb">
</p>
<p align="center">
  Fig 1.
</p>

+ We can see that they are no more equidistant.

</details>

<details>
<summary> SPICE Deck Creation for CMOS Inverter </summary> 

**SPICE Deck**
+ Component connectivity
+ Component values
+ Identify nodes
+ Name nodes

<p align="center">
<img width="259" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/46e02f1a-2708-4ca0-956f-83bbd08c7c92">
</p>
<p align="center">
  Fig 2.
</p>

CMOS_INVERTER.cir
```
*** MODEL DESCRIPTIONS ***
*** NETLIST DESCRIPTION ***
M1 out in vdd vdd pmos W=0.375u L=0.25u
M2 out in 0 0 nmos W=0.375u L=0.25u

cload out 0 10f

Vdd vdd 0 2.5
Vin in 0 2.5
*** SIMULATION Commands ***

.op
.dc Vin 0 2.5 0.05
*** include tsmc_025um_model.mod ***
.LIB "tsmc_025um_models.mod" CMOS_MODELS
.end
```

</details>

<details>
<summary> SPICE Simulation Lab for CMOS Inverter </summary>

+ Simulation steps
 - `cd <folder where the .cir file is present>`
 - `source CMOS_INVERTER.cir`
 - `run`
 - `setplot`
 - `dc1`
 - `display`
 - `plot out vs in`

<p align="center">
<img width="364" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8a5eb330-8c2b-4675-a977-257d343c8db3">
</p>
<p align="center">
Fig 3.
</p>

+ The output should be symmetric ie., the threshold voltage should be at vdd/2.
+ If it isnt, try to increase the PMOS width and run the simulation again.

</details>

<details>
<summary> Switching Threshold Vm </summary>

+ CMOS as a circuit itself is a very **Robust** device.
+ **Switching threshold** defines the robustness of CMOS.
+ **Vm** is the point where Vin=Vout.

</details>

<details>
<summary> Lab Steps to Gitclone vsdstdcelldesign </summary>

+ `git clone https://github.com/nickson-jose/vsdstdcelldesign.git`

<p align="center">
<img width="661" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/c0a4f88c-51c3-48d6-84a0-10c295b035be">
</p>
<p align="center">
  Fig 4.
</p>

+ ` cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign`

<p align="center">
<img width="901" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4b789488-6dd8-4631-b6aa-45a8707f9c8d">
</p>
<p align="center">
  Fig 5.
</p>

+ We can see that the tech file is added.

<p align="center">
<img width="669" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/799e1d19-41ad-49ba-87c4-4d2d88d574c9">
</p>
<p align="center">
Fig 6.
</p>

</details>

## Inception of Layout
<details>
<summary> Create Active Regions </summary>

+ Fabrication of CMOS is a 16 Mask process.

**Selecting the Substrate**
+ We go for a p-type substrate with
  - resistivity around : 5-50 ohm
  - doping level : 10^15 cm^-3
  - orientation : 100

**Creating Active region for transistors**

+ Grow a layer of SiO2(~40nm) on Psub.
+ Deposit a layer of ~80nm Si3N4 on SiO2.
+ Deposit 1um layer of photoresist(used to define regions).
+ Photolithography.
+ Etch out Si3N4 and SiO2 using a suitable solvent.
+ Place the obtained structure in oxidation furnace due to which field oxide is grown.This process is called LOCOS ( Local oxidation of silicon).
+ Etch out Si3N4 using hot phosphoric acid.

</details>

<details>
<summary> Formation of n-well and p-well </summary>

+ Deposit a layer of photoresist.
+ Apply mask to cover NMOS.
+ Expose to UV light, wash away the area which is exposed and remove mask.
+ Deposit Boron using ion implementation at an energy of 200keV.
+ Repeat the same steps for other half using phosphorous at an energy of 400keV.
+ Wells have been created but the depth is low, hence subject it to high temperature furnace which increases the well depth.

</details>

<details>
<summary> Formation of Gate Terminal </summary>
  
+ Deposit a layer of photoresist.
+ Apply mask to cover NMOS.
+ Expose to UV light, wash away the area which is exposed and remove mask.
+ Deposit Boron using ion implementation at an energy of 200keV cause we need boron at the surface.
+ Repeat the same steps for other half using arsenic.
+ Original oxide etched/stripped using hydroflouric solution.
+ Then re-grown again to give high quality oxide (~10nm thin).
+ Deposit ~0.4um polysilicon layer.
+ Dope N-type (phosphorous/ arsenic) ion implants for low gate resistance.
+ Deposit a layer of photoresist and repeat the same steps till removing the mask.

</details>

<details>
<summary> Lightly Doped Drain Formation </summary>

+ The doping profile near n-well is P+, P-, N.
+ Near p-well is N+, N-, P.
+ 2 reasons to do this:
  - hot electron effect
  - short cahnnel effect
+ On the surface of SiO2, near N-well, deposit a layer of photoresist, and mask it.
+ Expose to UV light, wash away the area which is exposed and remove mask.
+ Apply phosphorous to form N- implant on p-well.
+ Similarly do it on the other half, but apply boron to form P- implant on n-well.
+ LDD needs to be protected, hence deposit 0.1um thick SiO2 on full structure and etch out using plasma anisotropic etching.
+ This results in the formation of side-wall spacers.

</details>

<details>
<summary> Source and Drain Formation </summary>

+ On the surface of SiO2, near N-well, deposit a layer of photoresist, and mask it.
+ Expose to UV light, wash away the area which is exposed and remove mask.
+ Deposit arsenic at 75KeV that forms an N+ implant on Pwell.
+ Similarly do it on the other half, but apply boron to form P+ implant on n-well.
+ Subject it to high temperature furnace that results in required thickness of N+,P+,N-,P- implants.

</details>

<details>
<summary> Local Interconnect Formation </summary>

+ Etch thin SiO2 oxide in HF solution.
+ Deposit Titanium of wafer surface using sputtering.
+ Wafer heated at 650-700 degree celsius in N2 ambient for 60 sec.
+ Results in low resistant TiSi2.
+ At the other places, TiN is formed which is used only for local communication.
+ TiN is etched off using RCA cleaning.

</details>

<details>
<summary> Higher Level Metal Formation </summary>

+ Deposit 1um of SiO2 with phosphorous or boron (known as phosphoborosilicate glass) on wafer surface.
+ Use CMP (chemical mechanical polishing) technique for planarizing wafer surface.
+ TiN and blanket Tungsten layers are deposited and subjected to CMP.
+ An aluminum (Al) layer is added and subjected to photolithography and CMP.
+ Deposit a layer of Si3N4 that acts as dielectric to protect the chip.

<p align="center">
  <img width="413" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/6c433da2-3e8c-4072-9abe-576e442ea492">
</p>

</details>

<detailS>
<summary> Lab Introduction to Sky130 Basic Layers Layout and LEF using Inverter </summary>

+ `magic -T sky130A.tech sky130_inv.mag &`

<p align="center">
<img width="719" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/c75dc309-03ef-4b5b-968a-62d4438b1943">
</p>
<p align="center">
Fig 7.
</p>

+ Click on the component and type `what` in the tkcon window.

<p align="center">
<img width="648" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/995400e6-dbb6-4940-beb1-4581d7415656">
</p>
<p align="center">
Fig 8.
</p>

</detailS>

<details>
<summary> Lab Steps to Create std cell Layout and Extract SPICE Netlist </summary>

+ DRC errors in magic will be highlighted with white dotted lines.
<p align="center">
<img width="541" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/25877323-e6ff-4289-83cb-0159ef9e07ec">
</p>
<p align="center">
  Fig 9.
</p>

+ To identify DRC errors select `DRC find next error`.
+ It will be displayed on the tkcon window.

<p align="center">
<img width="551" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/3fb71982-e469-424c-a463-3b53d561a846">
</p>
<p align="center">
  Fig 10.
</p>

+ Extracting to SPICE Command
  - `extract all`
  - `ext2spice cthresh 0 rthresh 0`
  - `ext2spice`
+ cthresh and rthresh are used to extract all parasatic capacitances.

<p align="center">
<img width="589" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8ed214bb-d45a-417b-991c-520fb5bf34ea">
</p>
<p align="center">
  Fig 11.
</p>

+ We can see that the spice file is created in the folder.

<p align="center">
<img width="551" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1262ad1d-1591-4769-8eda-56d2ddd0e60e">
</p>
<p align="center">
  Fig 12.
</p>

+ Spice File

<p align="center">
<img width="622" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1c8795c8-5704-4b4e-be02-7b89d538e4d3">
</p>
<p align="center">
Fig 13.
</p>

</details>

## Sky130 Tech File Labs
<details>
<summary> Lab Steps to Create Final SPICE Deck using Sky130 Tech </summary>

+ Grid size.
<p align="center">
<img width="620" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bc81ff12-1b6a-4c89-bc89-63cbd3e6be74">
</p>
<p align="center">
  Fig 1.
</p>

+ We modified the spice file.
<p align="center">
<img width="476" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/76803aae-5b91-478a-b4ca-a5789c5bd6e9">
</p>
<p align="center">
  Fig 2.
</p>

 - `ngspice sky130_inv.spice`
 - `plot y vs time a`

<p align="center">
<img width="881" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/a50792a4-3ac7-421f-9d19-2952bdc69bf0">
</p>
<p align="center">
  Fig 3.
</p>

</details>

<details>
<summary> Introduction to Magic Options and DRC rules </summary>
+ For reference : http://opencircuitdesign.com/magic/

**Magic**
+ Magic is a venerable VLSI layout tool, written in the 1980's at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl. 
+ Due largely in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies.
+ The open-source license has allowed VLSI engineers with a bent toward programming to implement clever ideas and help magic stay abreast of fabrication technology.
+ However, it is the well thought-out core algorithms which lend to magic the greatest part of its popularity.
+ Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.

**DRC rules**
+ DRC (Design Rule Check) rules are a set of guidelines and constraints used in the field of semiconductor and integrated circuit (IC) design to ensure that the physical layout of a chip or circuit adheres to the manufacturing process's design rules.
+ These rules are essential for maintaining manufacturability and ensuring that the final ICs can be fabricated without defects.
+ The design rules used by Magic's design rule checker come entirely from the technology file.

</details>

<details>
<summary> Introdcution to Sky130 PDKs and Steps to Download Labs </summary>

**Sky130 PDK**
+ SKY130 is a mature 180nm-130nm hybrid technology developed by Cypress Semiconductor that has been used for many production parts.
+ SKY130 is now available as a foundry technology through SkyWater Technology Foundry.

+ `wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz`

<p align="center">
<img width="758" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/abd377f1-d5df-4639-bbe6-7a5237bc1f97">
</p>
<p align="center">
  Fig 4.
</p>

</details>

<details>
<summary> Lab Introduction to Magic and Steps to Load Sky130 Tech-Rules </summary>

+ To open Magic
  - `magic -d XR`
 
+ Go to files then open `met3.mag` file.

<p align="center">
<img width="835" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/ba236cb5-4769-4e81-a801-0467d545f2fa">
</p>
<p align="center">
  Fig 5.
</p>

+ To check which DRC rule is being violated select area.
+ Type `drc why` in tkcon.

<p align="center">
<img width="770" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/ae1e9b82-8b02-48ed-be75-10ab6b43b68e">
</p>
<p align="center">
  Fig 6.
</p>

+ To add contact cuts add met3 contact by selecting area and clicking on m3contact using middle mouse button.
+  Type  `cif see VIA2` in tkcon prompt.

<p align="center">
<img width="726" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/13f6db17-0d5c-48cb-95c7-6221f5a7089b">
</p>
<p align="center">
  Fig 7.
</p>

</details>

<details>
<summary> Lab Exercise to fix poly.9 error in Sky130 Tech File </summary>

+ Type `load poly` in the tkon prompt.

<p align="center">
<img width="735" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1d4ac890-5bbd-4630-b124-a23f795baa04">
</p>
<p align="center">
  Fig 8.
</p>

<p align="center">
<img width="182" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/cf6d4ecd-44c1-4c5b-86ec-1653d7a3d62b">
</p>
<p align="center">
  Fig 9.
</p>

+ The error is:
<p align="center">
<img width="611" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1d709337-9601-4541-bda2-4cce6d787d17">
</p>
<p align="center">
  Fig 10.
</p>

+ To fix the error open the sky130A.tech file using a editor and search for poly.9 and make the changes.
<p align="center">
<img width="662" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/32d10f95-bec7-4278-a870-5bac048f7c29">
</p>
<p align="center">
  Fig 11.
</p>

<p align="center">
<img width="496" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/384efd39-5077-4bfa-943a-d12b10be7536">
</p>
<p align="center">
  Fig 12.
</p>

+ Now load the sky130A.tech file `tech load sky130A.tech`.
+ Type the command `drc check`.
+ We can see that the error is fixed.

<p align="center">
<img width="356" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bf3227a0-056e-499f-91d6-e31d230fd23d">
</p>
<p align="center">
  Fig 13.
</p>

</details>

<details>
<summary> Lab Challenge Exercise to Describe DRC Error as Geometrical Construct </summary>

+ Open the nwell.mag file in magic.
+ Select the nwell.6
+ Type the following commands in tkon prompt:
  - `cif ostyle drc`
  - `cif see dnwell_shrink`
  - `cif see dnwell_missing`

<p align="center">
<img width="891" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/300cf7b8-302e-42a8-8340-3ba25163e1bd">
</p>
<p align="center">
Fig 14.
</p>

+ To find missing or incorrect rules and fix them.

<p align="center">
<img width="403" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4dc02e55-9192-45b2-bac7-2431441cee34">
</p>
<p align="center">
Fig 15.
</p>

+ Error is :

<p align="center">
<img width="611" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/7a002a41-51b8-4018-9d0a-7ee8195359fe">
</p>
<p align="center">
Fig 16.
</p>

+ To fix the error open the sky130A.tech file using a editor.

<p align="center">
<img width="575" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/ee2e7173-7af3-4906-8286-c5f0a1e34b82">
</p>
<p align="center">
Fig 17.
</p>

<p align="center">
<img width="506" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/823aceec-1182-44d1-8d85-ce98499da3e0">
</p>
<p align="center">
fig 18.
</p>

+ Now load the sky130A.tech file `tech load sky130A.tech`.
+ Type the command `drc check` for both normal and drc fast.

<p align="center">
<img width="760" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/eab2681e-e063-4d01-888d-2df4c2c84c65">
</p>
<p align="center">
Fig 19.
</p>

<p align="center">
<img width="371" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/e6a0ce8b-3454-438f-a68c-2d613857623a">
</p>
<p align="center">
Fig 20.
</p>

</details>

# Day-4
## Timing Modelling Using Delay Tables
<details>
<summary> Lab steps to convert Grid info into Track info </summary>

+ ` ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130fd_sc_hd/tracks.info`
+ `less tracks.info`

<p align="center">
<img width="167" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/8289365c-c2c7-4a3e-99de-1889d106a431">
</p>
<p align="center">
Fig 1.
</p>

+ The 'tracks.info' file is used during the routing stage.
+ Routes are the metal traces.
+ Since the PNR is an automated flow, we need to specify where all we want the routes to go.

+ Now we converge the grid definition in the layout to track definition.

<p align="center">
<img width="823" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/882256d8-28cc-46ee-8c63-2a798b87e6d8">
</p>
<p align="center">
Fig 2.
</p>

+ The next requirement is that the width of the cell should be the odd multiple of xpitch which is '0.46' as seen in the 'tracks.info' file.
+ As we can see it encloses two full boxes and two halves of one box, totally making three boxes as indicated by the white line.

<p align="center">
<img width="678" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/381783f2-7ad4-4a01-9982-260a0ba61a67">
</p>
<p align="center">
Fig 3.
</p>

</details>

<details>
<summary> Lab steps to convert Magic Layout to Std Cell LEF </summary>

+ In the tkcon window, type `save sky130_vsdinv.mag`.
+ This is to make our own .mag file.
+ `lef write` to make .lef file
<p align="center">
<img width="854" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/6f2d7ace-30df-4e29-b786-b4269ec9385c">
</p>
<p align="center">
Fig 4.
</p>

+ `less sky130_vsdinv.lef`.
<p align="center">
<img width="517" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/00eeb26b-21af-4ca8-b3db-395dd850477c">
</p>
<p align="center">
Fig 5.
</p>

</details>

<details>
<summary> Introduction to Timing Libs and Steps to include New cell in Synthesis </summary>

+ We copy the lef file and the libraries.

<p align="center">
<img width="905" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/d91ccfe2-057f-41a6-857e-7f011f2d0a63">
</p>
<p align="center">
Fig 6.
</p>

<p align="center">
<img width="713" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/9b9901c4-f07d-4514-8016-87be96adfbd6">
</p>
<p align="center">
Fig 7.
</p>

+ Next we modify the 'config.tcl' file in the picorv32a folder.

<p align="center">
<img width="866" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/6c01a5df-2ae5-431d-9636-9c8762e1e94c">
</p>
<p align="center">
Fig 8.
</p>

+ Open the OpenLANE interactive window and retrieve the 0.9 package.
 - `prep -design picorv32a -tag 14-09_10-42 -overwrite`
 - `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`
 - `add_lefs -src $lefs `
 - `run_synthesis`
<p align="center">
<img width="905" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/9b7bdfb2-9c0f-432b-84e0-9c7dd7a4c2a6">
</p>
<p align="center">
Fig 9.
</p>

<p align="center">
<img width="353" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/37319c15-7f05-4642-a2dd-ff5e9cb845f3">
</p>
<p align="center">
Fig 10.
</p>


<p align="center">
<img width="167" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/a09b259e-6bcf-42d0-97b9-4c4b8d0fe0bf">
</p>
<p align="center">
Fig 11.
</p>

+ `%init_floorplan`
+ `%run_placement`
+ `magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

<p align="center">
<img width="709" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/078de7cd-80c9-4001-b709-7c6d14a556cc">
</p>
<p align="center">
Fig 12.
</p>

+ We can see that We have plugged in our custom cell in the OpenLANE flow.
<p align="center">
<img width="693" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/c5d78355-e056-4f0f-a2ad-393a7df6ae03">
</p>
<p align="center">
Fig 13.
</p>

+ VLSI engineers will obtain system specifications in the architecture design phase. These specifications will determine a required frequency of operation. To analyze a circuit's timing performance designers will use static timing analysis tools (STA). When referring to pre clock tree synthesis STA analysis we are mainly concerned with setup timing in regards to a launch clock. STA will report problems such as worst negative slack (WNS) and total negative slack (TNS). These refer to the worst path delay and total path delay in regards to our setup timing restraint. Fixing slack violations can be debugged through performing STA analysis with OpenSTA, which is integrated in the OpenLANE tool. To describe these constraints to tools such as In order to ensure correct operation of these tools two steps must be taken:

+ Design configuration files (.conf) - Tool configuration files for the specified design
+ Design Synopsys design constraint (.sdc) files - Industry standard constraints file

</details>

<details>
<summary> Delay Tables </summary>

**Introduction**
+ Delay tables, often referred to as delay models or delay tables in the context of digital integrated circuit design, are data structures that provide information about the propagation delay of digital logic gates or cells under various conditions.
+ These tables are a fundamental component of static timing analysis (STA) and are used to predict the signal arrival times and meet timing constraints in digital designs.

**Purpose of Delay Tables:**
+ Delay tables are used to estimate the time it takes for a signal to propagate through a digital logic gate or cell.
+ This information is crucial for ensuring that signals meet their setup and hold time requirements and for calculating the overall timing behavior of a digital circuit.

**Types of Delay Tables:**
+ There are two main types of delay tables:
   - Library Delay Tables: These tables are part of a standard cell library and provide information about the delays of individual logic gates (AND, OR, XOR, flip-flops, 
    etc.) under various operating conditions (input transitions, voltage, temperature, etc.). Library delay tables are used to estimate the delays associated with 
    different gate types.
   - Interconnect Delay Tables: These tables describe the delay associated with routing signals between logic gates or cells on a chip. They account for wire resistance, 
   capacitance, and other physical properties that affect signal propagation.

**Data in Delay Tables:**
+ Delay tables typically include information such as:
   - Input conditions: Input transition times or slew rates.
   - Process corners: Variations in process technology, including worst-case and best-case scenarios.
   - Operating conditions: Voltage and temperature conditions.
   - Delay values: Delays for signal propagation through the gate or interconnect, often specified for different output loading conditions.

**Timing Analysis:**
+ Delay tables are used by STA tools to perform timing analysis on digital designs.
+ These tools use the delay tables to estimate the critical path delays, setup times, hold times, and other timing parameters.

**Corner Analysis:**
+ Corner analysis involves using delay tables for various process corners (e.g., slow, typical, fast) to account for manufacturing process variations.
+ This ensures that the design meets timing under a range of conditions.

**Clock Domain Crossing (CDC) Analysis:**
+ Delay tables are also used in CDC analysis to analyze signals that cross between different clock domains.
+ Understanding signal arrival times is crucial in preventing metastability issues.

**Optimization:**
+ Designers use delay tables to optimize their designs by selecting gates with appropriate delays to meet performance, power, and area goals.

**Iterative Process:**
+ During the design process, delay tables are used iteratively.
+ Designers may make adjustments to the design and rerun timing analysis to ensure that the design meets its timing constraints.

</details>

## Timing Analysis with Ideal Clocks using openSTA
<details>
<summary> Configure OpenSTA for Post-Synth Timing Analysis </summary>

+ We must create two files.
+ The first one must be in the openlane directory
+ This file is known as the 'pre_sta.conf' file.
<p align="center">
<img width="908" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/f9ca3695-1128-4a3b-8d11-c50e27deab47">
</p>
<p align="center">
  Fig 1.
</p>

+ The second is the my_base.sdc file.
+ This should be in the 'src/sky130' directory under the picorv32a directory.
<p align="center">
<img width="715" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/e19cfd30-3f5b-4cfd-b554-eea5649ac686">
</p>
<p align="center">
  Fig 2.
</p>

<p align="center">
<img width="649" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/4739e25b-f179-492f-863d-ab208dbbbccc">
</p>
<p align="center">
  Fig 3.
</p>

+ To run the timing analysis we type
+ `sta pre_sta.conf`

<p align="center">
<img width="533" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1a027fbc-9465-46ea-a4a4-9c2f83cba62b">
</p>
<p align="center">
  Fig 4.
</p>

+ There is a slack violation.
</details>

<details>
<summary> Optimise synthesis </summary>

+ Setting MAX_FANOUT value to 4 reduces the slack violation.
+ `set ::env(SYNTH_MAX_FANOUT) 4`
+ Then `run_synthesis`

<p align="center">
<img width="541" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bc32754a-dc6c-4651-a4c8-f6da5db4fd64">
</p>
<p align="center">
  Fig 5.
</p>

+ Since we have synthesised the core using our vsdinv cell too and as it got successfully synthesized, it should be visible in layout after `run_placement` stage which is followed after `run_floorplan` stage.

<p align="center">
<img width="725" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/1e14c8f4-54bc-4723-8652-1db5258048e5">
</p>
<p align="center">
  Fig 6.
</p>

</details>

## Clock Tree Synthesis TritonCTS and Signal Integrity

<details>
<summary> CTS </summary>

+ To run CTS we need to type the command.
+ `run_cts`
+ New .v is created.

<p align="center">
<img width="883" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/9ae4df75-3a0a-4ee0-b335-dd28dd4baa3e">
</p>
<p align="center">
  Fig 7.
</p>

</details>

## Timing Analysis with Real CLocks using OpenSTA

<details>
<summary> Lab steps to analyse Timing with Real CLocks</summary>

+ `openroad`
+ `read_lef /openLANE_flow/designs/picorv32a/runs/14-09_10-42/tmp/merged.lef`
+ `read_def /openLANE_flow/designs/picorv32a/runs/14-09_10-42/results/cts/picorv32a.cts.def`
+ `write_db pico_cts.db`
+ `read_db pico_cts.db`
+ `read_verilog /openLANE_flow/designs/picorv32a/runs/14-09_10-42/results/synthesis/picorv32a.synthesis_cts.v`
+ `read_liberty -max $::env(LIB_SLOWEST)`
+ `read_liberty -max $::env(LIB_FASTEST)`
+ `read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`

<p align="center">
<img width="763" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/477f4146-c8cb-440d-bffc-9087c4b2be7f">
</p>
<p align="center">
  Fig 8.
</p>

+ `set_propagated_clock [all_clocks]`
+ `report_checks -path_delay min_max -format full_clock_expanded -digits 4`

<p align="center">
<img width="536" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/0359e82d-9757-4992-a5e4-e50706fe45c2">
</p>
<p align="center">
  Fig 9.
</p>

<p align="center">
<img width="664" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/5803494c-a24e-4c1e-a72d-b36f61f25794">
</p>
<p align="center">
  Fig 10.
</p>

+ We perform it again for a more accurate result.

<p align="center">
<img width="481" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/5bdb83b0-e614-4b62-a936-26a6de2f301a">
</p>
<p align="center">
  Fig 11.
</p>

<p align="center">
<img width="496" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/69e32947-27d1-43d7-b0c1-9fa731180fee">
</p>
<p align="center">
  Fig 12.
</p>

</details>

<details>
<summary> Lab steps to Observe Setup and Hold Timing </summary>

+ `report_clock_skew -hold`

<p align="center">
<img width="216" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/bc82d3ba-7733-41c6-8fdc-da1dfbfa8a1f">
</p>
<p align="center">
  Fig 13.
</p>

+ `report_clock_skew -setup`

<p align="center">
<img width="273" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/6eac4399-094b-458e-bf3e-1346965d4668">
</p>
<p align="center">
Fig 14.
</p>

</details>

# Day-5
## Routing and DRC
<details>
<summary> Maze routing </summary>

+ Maze routing is a method used in electronic design automation (EDA) and integrated circuit (IC) design to determine efficient paths for interconnecting various components, such as logic gates, on a chip's layout. The goal is to find a path through a maze-like grid of obstacles while optimizing for factors like wire length, signal delay, and area utilization.

+ Lee's algorithm, also known as Lee's breadth-first search (BFS) algorithm, is a graph traversal and pathfinding algorithm that is commonly used in maze routing, maze solving, and other grid-based problems. Named after its creator, C. Y. Lee, the algorithm is particularly useful for finding the shortest path between two points in a grid while exploring the grid layer by layer.

</details>

<details>
<summary> DRC </summary>
  
Lambda rules are process-specific design rules used in semiconductor manufacturing to ensure that integrated circuit (IC) layouts adhere to the capabilities and constraints of a particular semiconductor process. These rules are expressed in terms of lambda (λ), a normalized unit of measurement relative to the process technology. Lambda rules can vary between semiconductor foundries and process nodes, but they typically cover various aspects of IC design. Here's a list of common lambda rules and design considerations:

+ Minimum Feature Size: Specifies the minimum allowed width and spacing for features such as transistors, metal tracks, and vias, often expressed as multiples of λ.
+ Aspect Ratio: Defines the acceptable aspect ratio (width-to-height ratio) for rectangular structures, ensuring manufacturability.
+ Metal Layer Constraints: Specifies minimum metal track widths, metal-to-metal spacings, and via sizes on metal layers.
+ Poly Pitch: Defines the minimum pitch (spacing between features) for the poly-silicon (poly) layer, which affects the size of transistors and gates.
+ Active Area Constraints: Specifies minimum active area dimensions, ensuring that transistors meet process requirements.
+ Well and Substrate Taps: Covers the placement and size of well and substrate taps for connecting to power and ground planes.
+ Gate Length: Specifies the minimum gate length for transistors, affecting their performance characteristics.
+ Contact and Via Rules: Defines the minimum size and spacing of contacts and vias used to connect different layers in the IC.
+ Local Interconnects: Provides rules for local interconnects, which are used for routing within a cell or macro.
+ Minimum Metal to Active Spacing: Sets the minimum separation between metal tracks and active areas.
+ Minimum Metal to Contact Spacing: Specifies the minimum distance between metal tracks and contacts.
+ Edge Exclusion Zones: Defines exclusion zones near the chip's edge, where certain design elements are not allowed.
+ Density Rules: Enforces limits on the density of features in different regions of the chip to ensure proper manufacturing and avoid over-congestion.
+ Well Proximity Rules: Governs the proximity of different well types (e.g., n-well and p-well) to prevent undesirable interactions.
+ Metal Layer Ordering: Specifies the order in which metal layers should be used in the design hierarchy.
+ Metal Filling: Addresses requirements for metal fill patterns to ensure planarity and manufacturability.
+ Antenna Rules: Addresses the issue of charge buildup (antenna effect) during manufacturing, providing guidelines for mitigating this effect.
+ Variation-Aware Rules: Accounts for process variations, statistical timing, and other variations in critical design rules.
+ Electromigration Constraints: Specifies limits on current densities to prevent electromigration issues in metal tracks.
+ Supply Voltage Constraints: Sets design guidelines for supply voltage levels and power distribution.
  
</details>

## Power Distribution Network and Routing

<details>
<summary> Power Distribution Network </summary>

+ After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network `gen_pdn` in OpenLANE:

<p align="center">
<img width="649" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/e1ce1d33-1b5a-4140-9edf-39d33130198d">
</p>
<p align="center">
  Fig 1.
</p>

<p align="center">
<img width="503" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/ac918898-3556-4737-b23c-5d299bbb4392">
</p>
<p align="center">
  fig 2.
</p>

+ The PDN feature within OpenLANE will create:
   - Power ring global to the entire core
   - Power halo local to any preplaced cells
   - Power straps to bring power into the center of the chip
   - Power rails for the standard cells
+ We see that there is a change in the DEF.

<p align="center">
<img width="569" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/10725da7-4122-456e-b69c-31c8b4215ec3">
</p>
<p align="center">
  Fig 3.
</p>

</details>

<details>
<summary> Global and Detailed Routing </summary>

+ OpenLANE uses TritonRoute as the routing engine for physical implementations of designs. Routing consists of two stages:
   - Global Routing - Routing guides are generated for interconnects on our netlist defining what layers, and where on the chip each of the nets will be reputed.
   - Detailed Routing - Metal traces are iteratively laid across the routing guides to physically implement the routing guides.

+ To run routing in OpenLANE:
  `run_routing`

<p align="center">
<img width="433" alt="image" src="https://github.com/Veda1809/pes_pd/assets/142098395/d559ab2c-9d22-4bd8-aa5c-d0084a5f77c4">
</p>
<p align="center">
  Fig 4.
</p>

+ If DRC errors persist after routing the user has two options:
  - Re-run routing with higher QoR settings.
  - Manually fix DRC errors specific in tritonRoute.drc file.
  
</details>

<details>
<summary> SPEF Extraction </summary>

+ After routing has been completed interconnect parasitics can be extracted to perform sign-off post-route STA analysis. The parasitics are extracted into a SPEF file.
+ The SPEF extractor is not included within OpenLANE as of now.

</details>
