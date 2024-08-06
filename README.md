# NASSCOM-VSD-DIGITAL-SOC-DESIGN-FROM-RTL-TO-GDSII
Here I have demonstrated the process of converting a RTL to GDS II.This is a two weeks workshop organized by VSD in association with NASSCOM
## CONTENTS
* [Day 1 - Inception of open-source EDA OpenLANE and sky130 PDK](#day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
   * [D1 SK1 How To Talk to Computers](#d1-sk1-how-to-talk-to-computers)
       * [SKY L1 Introduction to QFN-48 Package chip pads core die and IPs](#sky-l1-introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
       * [SKY L2 Introduction to RISC-V](#sky-l2-introduction-to-risc-v)
       * [SKY L3 From software applications to Hardware](#sky-l3-from-software-applications-to-hardware)
   * [D1 SK2 SOC Design and OPENLANE](#d1-sk2-soc-design-and-openlane)
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
Application Software (Top Left): Our journey begins with the software applications we use daily. These applications, written in languages like C++, Java, or Python, interact with the underlying system through a defined set of instructions.
System Software and Compilation (Top): The Operating System (OS) acts as an intermediary, managing system resources and providing an interface for applications to interact with the hardware. Compilers translate high-level code (e.g., C++) into lower-level assembly language instructions specific to the target CPU architecture.
Assembly and Machine Code (Middle): The Assembler further converts assembly code into binary machine code (0s and 1s) that the hardware can directly understand and execute. The Instruction Set Architecture (ISA) serves as the abstract interface between software and hardware, defining the set of instructions a processor can execute.
Hardware Implementation (Bottom): Register Transfer Level (RTL): This stage describes the hardware behavior using a Hardware Description Language (HDL) like Verilog or VHDL. RTL defines the flow of data between registers and the logical operations performed.
Netlist Synthesis: The RTL description is synthesized into a netlist, a detailed representation of the circuit's interconnected components (gates, flip-flops).

Physical Design: Finally, the netlist guides the physical placement and routing of transistors and wires on the silicon die, resulting in the tangible hardware that executes the original software instructions.

Key Takeaways: This diagram highlights the layered abstraction involved in bridging the gap between software and hardware. It emphasizes the crucial role of compilers, assemblers, and hardware design tools in translating abstract instructions into physical circuits. Understanding this flow provides valuable insights into the relationship between software, hardware, and the underlying computer architecture.
