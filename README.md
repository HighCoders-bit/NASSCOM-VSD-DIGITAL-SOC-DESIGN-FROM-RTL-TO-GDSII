# NASSCOM-VSD-DIGITAL-SOC-DESIGN-FROM-RTL-TO-GDSII
Here I have demonstrated the process of converting a RTL to GDS II.This is a two weeks workshop organized by VSD in association with NASSCOM
## CONTENTS
* [Day 1 - Inception of open-source EDA OpenLANE and sky130 PDK](#day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
   * [D1 SK1 How To Talk to Computers](#d1-sk1-how-to-talk-to-computers)
       * [SKY L1 Introduction to QFN-48 Package chip pads core die and IPs](#sky-l1-introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
       * [SKY L2 Introduction to RISC-V](#sky-l2-introduction-to-risc-v)
       * [SKY L3 From software applications to Hardware](#sky-l3-from-software-applications-to-hardware)
   * [D1 SK2 SOC Design and OPENLANE](#d1-sk2-soc-design-and-openlane)
       * [SKY L1 Introduction to all components of an open-source digital ASIC design](#sky-l1-introduction-to-all-components-of-an-open-source-digital-asic-design)
       * [SKY L2 simplified RTL TO GDSII MODEL](#sky-l2-simplified-rtl-to-gdsii-model)
       * [SKY L3 Introduction to openlane and strive chipsets](#sky-l3-introduction-to-openlane-and-strive-chipsets)
       * [SKY L4 Introduction to OPENLANE and detailed ASIC designed flow](#sky-l4-introduction-to-openlane-and-detailed-asic-designed-flow)
   * [D1 SK3 Get Familiar with Open Source EDA Tools](#d1-sk3-get-familiar-with-open-source-eda-tools)
* [Day 2 Good floorplan vs bad floorplan and introduction to library cells](#day-2-goodfloorplan-vs-bad-floorplan-and-introduction-to-library-cells)
   * [D2 SK1 Chip floor planning considerations](#d2-sk1-chip-floor-planning-considerations)
   * [D2 SK2 Library binding and placement](d2-sk2-library-binding-and-placements)
   * [D2 SK3 Cell design and characterization flows](d2-sk3-cell-design-and-charaterization-flows)
   * [D2 SK4 General timing characterization](D2-sk4-general-timing-characterization)
 * [Day 3 Design library cells using magic layout and ngspice characterization](day-3-design-library-cells-using-magic-layout-and-ngspice-characterization)
    * [D3 SK1 Labs for CMOS Inverter and ngspice simulation](d3-sk1-labs-for-cmos-invereter-and-ngspice-simulation)
    * [D3 SK2 Inception of layout and CMOS fabrication process](d3-sk2-inception-of-layout-and-CMOS-fabrication-process)
    * [D3 SK3 Sky130 Tech File labs](d3-sk3-sky130-tech-file-labs)
 * [DAY 4 Prelayout timing analysis and importance of good clock tree](day-4-prelayout-timing-analysis-and-importance-of-good-clock-tree)
    * [D4 SK1 Timing modelling using delay tables](d4-sk1-timing-modelling-using-delay-tables)
    * [D4 SK2 Timing analysis using ideal clock using openSTA](d4-sk2-timing-analysis-using-ideal-clock-using-opensta)
    * [D4 SK3 Clock Tree Synthesis TritonCTS and signal integrity](d4-sk3-clock-tree-synthesis-tritonCTS-and-signal-integrity)
    * [D4  SK4 Timing analysis with real clocks using openSTA](d4-sk4-timing-analysis-with-real-clocks-using-open-sta)
  * [DAY 5 Final steps for RTL2GDS using Tritronroute and openSTA](day-5-final-steps-for-rtl2gds-using-tritronroute-and-opensta)
     * [D5 SK1 Routing and design rule check](d5-sk1-routing-and-design-rule-check)
     * [D5 SK2 Power distribution network and routing](d5-sk2-power-distribution-network-and-routing)
     * [D5 SK3 Tritron route features](d5-sk3-tritron-route-features)
  ##  Day 1 - Inception of open-source EDA OpenLANE and sky130 PDK
  ### D1 SK1 How To Talk to Computers
  ## SKY L1 Introduction to QFN-48 Package chip pads core die and IPs
  
  ![Screenshot 2024-07-13 095151](https://github.com/user-attachments/assets/fe5f6945-5a50-4bef-bb30-09e41b7620be)
  ### Arduino Board 
  This is an arduino microcontroller board. The encircled area shows the chip(microprocessor) which is interfaced with other components of the board. The designing of this chip from abstract level all the way down to the fabrication is done by RTL to GDSll flow.Arduino consists of both a physical programmable circuit board (often referred to as a microcontroller) and a piece of software, or IDE (Integrated Development Environment) that runs on the computer, used to write and upload computer code to the physical board.
  ### RISC-V SOC
  

![Screenshot 2024-07-13 095251](https://github.com/user-attachments/assets/4586126a-86a6-4234-bf5c-0961a8ffaebc)
 It consist of SRAM,SOC,ADC,DAC,SPI these all are called foundary IP's.All devices depends upon foundary where all chips are fabricated using deposition and lithography techniques and so on.
 ### INSIDE A MICROCONTROLLER BOARD 
 
![Screenshot 2024-07-13 095935](https://github.com/user-attachments/assets/e5d67db0-74fa-4c2a-9d94-967bccf3421c)
![inside die](https://github.com/user-attachments/assets/02cf2094-608b-4567-8c2f-f2a576f7e8e1)
### Microcontroller Board Components
#### Core:

Definition: The central processing unit (CPU) of the microcontroller that executes instructions.
Example: ARM Cortex-M, RISC-V core.
Die:

Definition: The physical silicon chip on which the microcontroller’s circuitry is fabricated.
#### Pad:

Definition: The physical connection points on the microcontroller chip where external components are connected.
#### GPIO (General-Purpose Input/Output):

Definition: Pins on the microcontroller that can be programmed to either input signals (e.g., sensors) or output signals (e.g., LEDs).
#### Bank:

Definition: A grouping of I/O pins or memory segments used for organization within the microcontroller. For GPIO, it refers to a set of pins grouped together.
#### Foundries:

Definition: Facilities where the microcontroller chips are manufactured. Examples include TSMC, Intel.
#### IPs (Intellectual Properties):

Definition: Pre-designed blocks of logic that can be integrated into the microcontroller. Examples include UART, SPI, and I2C controllers.
#### SRAM (Static Random-Access Memory):

Definition: A type of volatile memory used for temporary data storage within the microcontroller. Fast but more expensive and power-consuming than DRAM.
#### DRAM (Dynamic Random-Access Memory):

Definition: A type of volatile memory used for larger, temporary data storage. Requires periodic refreshing to maintain data.
#### ADC (Analog-to-Digital Converter):

Definition: Converts analog signals (e.g., sensor outputs) into digital values that can be processed by the microcontroller.
#### DAC (Digital-to-Analog Converter):

Definition: Converts digital values into analog signals (e.g., to drive speakers or analog displays).
#### RISC-V SoC (System on Chip):

Definition: A microcontroller or microprocessor incorporating a RISC-V core along with additional integrated components such as memory, peripherals, and communication interfaces.
#### Macros:

Definition: Predefined sequences of code or hardware configurations used to simplify and automate repetitive tasks in programming or hardware design.
#### Connecting All Components
Core: Executes instructions and processes data.
Die: Houses the core and other integrated components.
Pad: Connects the die to external components via GPIO.
GPIO: Interfaces with external devices, configured via macros.
Bank: Organizes GPIO and other resources.
Foundries: Manufacture the microcontroller with the integrated core, SRAM, DRAM, ADC, DAC, and IPs.
IPs: Provide specialized functions like UART and SPI, integrated into the SoC.
SRAM & DRAM: Store data temporarily for processing and operation.
ADC & DAC: Enable analog signal processing and generation.
This layout ensures a microcontroller can interact with the external world and perform complex tasks by integrating various components into a single, functional chip.
## SKY L2 Introduction to RISC-V
![Screenshot 2024-07-13 100329](https://github.com/user-attachments/assets/6d9f3f2e-9156-401a-9163-5e4cbc871820)
### Visualizing a RISC-V CPU Core: From Code to Silicon Layout
RISC-V Assembly Code (Left): We start with a snippet of assembly code written for the RISC-V architecture. Each line represents a low-level instruction, demonstrating the fundamental operations the CPU is designed to execute.
Implementation in Hardware Description Language (Bottom): This section displays the implementation of the picorv32 CPU core using a Hardware Description Language (likely Verilog or SystemVerilog). It demonstrates how the assembly instructions are translated into logical operations and register transfers within the CPU's architecture. Parameters for configuring the core's features (like enabling counters or cache) are also visible.
Physical Layout (Right): This represents the actual physical layout of the picorv32 CPU core, visualized using a tool like "qflow." Different colors and labels represent various circuit elements like logic gates (AND2X2, BUFX2), flip-flops (DFFPOSx1), and interconnections. This layout dictates how the transistors and wires are arranged on the silicon die to implement the CPU's functionality. Key Takeaways: The image illustrates the intricate link between software and hardware in CPU design. Starting from high-level code, we traverse down to the physical realization of a RISC-V core, showcasing the different levels of abstraction involved. This visual representation helps in understanding how CPU design choices in the hardware description language translate into the physical layout of the silicon chip.
## SKY L3 From software applications to Hardware

![Screenshot 2024-07-13 104219](https://github.com/user-attachments/assets/985e037b-30cd-44d9-b04c-503eb2927901)
![Screenshot 2024-07-13 104157](https://github.com/user-attachments/assets/b25abdc7-c9b4-4960-8872-355d84aafbec)
* Application Software (Top Left): Our journey begins with the software applications we use daily. These applications, written in languages like C++, Java, or Python, interact with the underlying system through a defined set of instructions.
* System Software and Compilation (Top): The Operating System (OS) acts as an intermediary, managing system resources and providing an interface for applications to interact with the hardware. Compilers translate high-level code (e.g., C++) into lower-level assembly language instructions specific to the target CPU architecture.
* Assembly and Machine Code (Middle): The Assembler further converts assembly code into binary machine code (0s and 1s) that the hardware can directly understand and execute. The * * * 
* Instruction Set Architecture (ISA) serves as the abstract interface between software and hardware, defining the set of instructions a processor can execute.
* Hardware Implementation (Bottom): Register Transfer Level (RTL): This stage describes the hardware behavior using a Hardware Description Language (HDL) like Verilog or VHDL. RTL defines the flow of data between registers and the logical operations performed.
Netlist Synthesis: The RTL description is synthesized into a netlist, a detailed representation of the circuit's interconnected components (gates, flip-flops).

* Physical Design: Finally, the netlist guides the physical placement and routing of transistors and wires on the silicon die, resulting in the tangible hardware that executes the original software instructions.

Key Takeaways: This diagram highlights the layered abstraction involved in bridging the gap between software and hardware. It emphasizes the crucial role of compilers, assemblers, and hardware design tools in translating abstract instructions into physical circuits. Understanding this flow provides valuable insights into the relationship between software, hardware, and the underlying computer architecture.
### D1 SK2 SOC Design and OPENLANE
## SKY L1 Introduction to all components of an open-source digital ASIC design

![Screenshot 2024-07-13 120549](https://github.com/user-attachments/assets/7d58721f-1fb1-4b61-80c0-a62b4cc2935e)
Introduction to All Components of a Digital ASIC Design
### RTL Design (Register Transfer Level Design):

Definition: Describes the logic and behavior of a digital circuit using registers and the data transfers between them.
Purpose: Defines the functionality and operations of the circuit.
### EDA Tools (Electronic Design Automation Tools):

Definition: Software tools used for designing, simulating, and verifying electronic systems and integrated circuits.
### Open-Source Tools:
QROad: Focuses on routing within digital ASIC designs.
OpenROAD: Provides a comprehensive tool suite for placement, routing, and design rule checking.
OpenLane: Offers an end-to-end RTL-to-GDSII flow, integrating with other open-source tools.
### PDK (Process Design Kit):

Definition: Contains files and information from semiconductor foundries describing the manufacturing process and design rules.
Purpose: Ensures designs are manufacturable and provides parameters for accurate simulation.
### Google Skywater 130nm PDK:

Definition: An open-source PDK for the SkyWater 130nm process technology.
Features: Includes libraries, design rules, and models specific to the 130nm technology node.
## SKY L2 simplified RTL TO GDSII MODEL

![Capture1](https://github.com/user-attachments/assets/28aa102c-c1b6-48a9-b779-84b4926f9b0c)
* #### RTL Design: Create a high-level description of the circuit.
* #### Synthesis: Convert RTL code to a gate-level netlist.
* #### Floorplanning and Power Planning: Arrange blocks and plan power distribution.
* #### Clock Tree Synthesis: Design the clock distribution network.
* #### Routing: Connect the gates and flip-flops.
* #### Signoff: Verify design with DRC, LVS, and ERC.
* #### GDSII File Generation: Generate the final layout file for manufacturing.
 ## SKY L3 Introduction to openlane and strive chipsets
![Capture](https://github.com/user-attachments/assets/8744bc7f-5d48-4e61-ad8a-c397ddfe62ea)

Strive SoC is an open-source System on Chip (SoC) project aimed at providing a comprehensive platform for learning, experimentation, and development in digital design. Here’s a brief overview:

#### Strive SoC Overview
##### Purpose:

Strive SoC is designed to offer a practical, educational platform for understanding SoC design principles and techniques.
It provides a reference design that can be used for academic purposes, prototyping, and as a starting point for custom SoC development.
##### Components:

**Processor Core**: Includes a basic RISC-V or other open-source CPU core.
**Peripherals**: Features standard peripherals such as UART, GPIO, timers, and memory interfaces.
**Interconnects**: Uses a bus or network-on-chip (NoC) architecture to connect various components.
**Memory**: Includes SRAM and/or DRAM for storage and cache.
##### Design Tools:

**EDA Tools**: Utilizes open-source EDA tools like OpenROAD, OpenLane, and QROad for design, synthesis, and layout.
**Simulation**: Integration with simulation tools for verification of design functionality.
Process Technology:

The SoC can be designed using various process technologies, often utilizing open-source PDKs like the Google Skywater 130nm PDK.
Features:

**Educational Focus**: Designed to help users understand the complete SoC design flow from RTL to GDSII.
Customizability: Allows users to modify and extend the design to suit specific needs or experimental purposes.
Applications:
## SKY L4 Introduction to OPENLANE and detailed ASIC designed flow


![Capture (1)](https://github.com/user-attachments/assets/580ae3fe-e7a1-4d54-825a-98b82c998319)
**Illustrates the comprehensive OpenLANE flow, encompassing design exploration, physical implementation, and sign-off. Key stages include:**

* **RTL Synthesis**: Converting Register Transfer Level (RTL) code into a gate-level netlist.
* **Floorplanning & Placement**: Planning the chip layout and placing standard cells.
* **CTS & Routing**: Clock Tree Synthesis and interconnecting placed cells with metal layers.
* **Static Timing Analysis (STA)**: Verifying timing closure.
* **Physical Verification**: Ensuring design rule compliance (DRC) and layout vs. schematic (LVS) correctness.
* **DFT(Design for Test)**: it perform scan inserption, automatic test pattern generation, Test patterns compaction, Fault coverage, Fault simulation.After that physical implementation is done by OpenROAD app
* **Static Timing analysis(STA)**: It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. resulting report will shows the timing violations if any violations is there.
* **Physical Verification(DRC and LVS)**: Magic is used for design Rules checking and SPICE Extraction from Layout. Magic and Netgen are used for LVS.

Every time the netlist is modified.(CTS modifies the netlist and Post Placements optimization also modifies the netlist).So for that verification must be performed. The LCE(yosys) is used to formally confirm that the function did not change after modifying the netlist. 
  
![Capture1 (1)](https://github.com/user-attachments/assets/aeb32125-4582-45ab-88ee-0a147486ba47)

 **Dealing with antenna rules Violation**: When a metal wire segment is fabricated, it can act as antenna.As an antenna, it collect charges which can damaged the transister gates during the fabrication.
 ![Capture2](https://github.com/user-attachments/assets/56658377-62ad-4058-9e61-d97f3c669b31)
 To address this issue, we have to limit the lenght of the wire. usually this is the job of the router. If router fails to do this, then there are two solutions: Bridging attaches a higher layer intermediary.Add antenna diode cell to leak away charges.(Antenna diodes are provided by the SCL)


![Screenshot 2024-07-13 150323](https://github.com/user-attachments/assets/dfed294c-36d8-4de1-8daa-a4a1be766e52)

With OpenLANE, we took a preventive approach. here we add fake antenna diode next to every cell input after placement. Then run the Antenna checker on the routed layout. If the checker reports a violation on cell input pin, replace the fake diode cell by a real one.
## D1 SK3 Get Familiar with Open Source EDA Tools
**Commands to start Openlane using a docker and run synthesis**  
**After synthesis we have to calculate**  
**FLOP RATIO =** $\frac{\text{No of D flipflop}}{\text{Total Number of cells}}$  
**Percentage** = $\text{Flop Ratio} \times 100$
```bash
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

                                      
