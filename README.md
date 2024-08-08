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
   * [D2 SK2 Library binding and placement](#d2-sk2-library-binding-and-placement)
   * [D2 SK3 Cell design and characterization flows](#d2-sk3-cell-design-and-characterization-flows)
   * [D2 SK4 General timing characterization](#d2-sk4-general-timing-characterization)
 * [Day 3 Design library cells using magic layout and ngspice characterization](#day-3-design-library-cells-using-magic-layout-and-ngspice-characterization)
    * [D3 SK1 Labs for CMOS Inverter and ngspice simulation](#d3-sk1-labs-for-cmos-inverter-and-ngspice-simulation)
    * [D3 SK2 Inception of layout and CMOS fabrication process](#d3-sk2-inception-of-layout-and-CMOS-fabrication-process)
    * [D3 SK3 Sky130 Tech File labs](#d3-sk3-sky130-tech-file-labs)
 * [DAY 4 Prelayout timing analysis and importance of good clock tree](#day-4-prelayout-timing-analysis-and-importance-of-good-clock-tree)
    * [D4 SK1 Timing modelling using delay tables](#d4-sk1-timing-modelling-using-delay-tables)
    * [D4 SK2 Timing analysis using ideal clock using openSTA](#d4-sk2-timing-analysis-using-ideal-clock-using-opensta)
    * [D4 SK3 Clock Tree Synthesis TritonCTS and signal integrity](#d4-sk3-clock-tree-synthesis-tritonCTS-and-signal-integrity)
    * [D4 SK4 Timing analysis with real clocks using openSTA](#d4-sk4-timing-analysis-with-real-clocks-using-opensta)
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
docker
```
```bash

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

  ![1](https://github.com/user-attachments/assets/a075d2b0-be33-483d-8053-aaea3f4efb3e)


![2](https://github.com/user-attachments/assets/5ff5129a-8021-46bb-bf7a-6d937c97e113)

![3](https://github.com/user-attachments/assets/8659235b-e0ed-4e5e-9469-98ca53c333e8)

![4](https://github.com/user-attachments/assets/64febeb7-5607-4ba8-8cc7-8e1f44c27ca5)
### config.tcl contains all the design environment specifications
![5](https://github.com/user-attachments/assets/c0c4869a-2c03-48f4-93c1-3693d412dde5)

![6](https://github.com/user-attachments/assets/633b8548-28ed-4c42-8d89-3e32f153f021)


#### After synthesis is done we will see the results of synthesis both in docker winodw and also in openlane directory under synthesis

![7](https://github.com/user-attachments/assets/b24e9813-a9ea-452e-8410-82dbcfb0357e)

#### RESULTS  
**FLOP RATIO =** $\frac{1613}{14876} = 0.1084$  
**Percentage** = $0.1084 \times 100 = 10.84$

![VirtualBox_vsdworkshop_29_07_2024_15_59_09](https://github.com/user-attachments/assets/b6c74da4-3f14-4a33-adb6-acd7bb58439b)


![VirtualBox_vsdworkshop_29_07_2024_16_10_34](https://github.com/user-attachments/assets/e73f062b-cb9f-476d-bade-01242389da61)


![8](https://github.com/user-attachments/assets/1b05cbce-dd0e-4aca-b327-bce415128c87)

#### In the end we see that the synthesis results in docker window and openlane directory matches
## Day 2 Good floorplan vs bad floorplan and introduction to library cells
### D2 SK1 Chip floor planning considerations
#### Utiliztion factor and aspect Ratio
In this section we will try to cover up the width and height of Core and Die. It is the first step in physical design flow to find out the width and height. Let's begin with a netlist, netlist is two flipflops and have a simple combination logic in between. A netlist describes the connectivity of an electronic design. Here, we dependent on the dimensions of the logic gates(AND & OR) and particular flipflop. Now, let's convert the symbols into physical dimensions. We are interested in the dimensions of the Core and Die not in the dimensions of the wires.

Let's standard cell have dimensions of 1unit*1unit

So, area= 1 Sq. units

Asuume same area for the flipflop as well = 1 Sq. units

with help of these dimensions and netlist let's calculate the area occupied by the netlist on a silicon wafer.
 

![Screenshot 2024-07-14 185039](https://github.com/user-attachments/assets/71c0f3f9-31af-4f8e-b9ea-0830dc8c79e2)  
Befor that will remove all the wires and bring all the flip flops and logic gates in a single plate. So after combining them together width and length will be 2 Sq. units each and if we calculate the total area the it will be 4 Sq. units. So now we have the rough calculation of minimum area occupied by the netlist.  

What is 'Core' and 'Die' section of a chip?

Let's have a silicon wafer on which all the logics are implemented. In thes one section is refered as 'Die' and inside the Die we have the Core.

A Die which consists of core, is small semicondcutor material specimen on which the fundamental circuit is fabricated.

A 'Core is the section of the chip where the fundamental logic of the design is placed.


![Screenshot 2024-07-14 185715](https://github.com/user-attachments/assets/f2bca0e2-ff97-436d-8b25-f0a4a724f2a8)

![Screenshot 2024-07-14 185900](https://github.com/user-attachments/assets/4a615c03-5515-4255-9f17-89c2c9a6f1a2)


![Screenshot 2024-07-14 190020](https://github.com/user-attachments/assets/db93edb1-d8b1-45d2-aa7d-6acf6b273c82)

So, utilization factor = 1 (It means core has utilized all the area and no space left)

Aspect Ratio = Height / width = 2 unit / 2unit = 1

Whenever Aspect Ratio is 1 it signifies that chip is square shaped. When it is not 1 it means the chip is in rectangular shape.  


![Screenshot 2024-07-14 190124](https://github.com/user-attachments/assets/3aa33460-91cf-431d-8f84-8bd793f2c294)

Lets take another example for a square chip wth dimensions 4*4 sq units. We will get utilization factor= 0.25 it means out of the whole chip area only 25% area is utilized by the netlistand 75% is available for additional cells which can be use for routing in which we will have layering. Aspect ratio we get = 1 it means chip is square in shape.

**PREPLACED CELL**:ets take a combinational logic which does some amount of function and assume its a huge circuit having some N Logic gates so let's devide it into some small numbers of gates. We will cut the whole circuit into two parts, and separate both of them into two blocks and both block will be implemented seperately.

![PREPLACED](https://github.com/user-attachments/assets/0255b67b-60ea-44bf-80d0-0b298c8086a9)

![PREPLACED1](https://github.com/user-attachments/assets/e21d2a87-a487-484b-a0f2-b52d0f417ea9)

In both the blocks lets extend the input output pins and now we will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. now will seperate them out as two different IP's or modules.

Advantage of doing this is we can reuse them multiple times after implimenting once only. Similary there are other IP's also available for eg. Memory, Clock-gating cell, Comporator, MUX all of these are part of the top level netlist.They recieve some signals and perform functions and deliver the outputs but the functionality of the cell is implemented only once.

![PREPLACED 2](https://github.com/user-attachments/assets/6a6b746e-b33e-419c-b63f-b762f8266956)
The arrangement of these IP's in a chip is refferd as floorplanning.

These IP's have user-defined locations, and hence are placed in chip before automated placement and routing are called "pre-placed cells".

These cells are placed in such a way that, the placement and routing tool do not touch the location of the cell.
**DE-COUPLING CAPACITORS**:Let consider same circuit, which is the part of the blocks which has been described earlier. When some gate (let consider AND gate) switched from 0 to 1 or 1 to 0, considered amount of the switching current required because of available small capacitance . This capacitor should be completely charged to represent logic 1 and completly discharged to represent logic 0. Consider capacitance to be 0. Rdd,Ldd,and Lss are well defined values. During switching operation, the circuit demands switching current i.e. peak current. Now, due to the presence of Rdd and Ldd, there will be a voltage drop across them and the voltage at Node 'A' would be Vdd' instead of Vdd.

![Decap](https://github.com/user-attachments/assets/eff069ce-0e01-41ae-af22-b0ec4a416168)

![Untitled](https://github.com/user-attachments/assets/146a87ec-3889-4a87-9def-5cdeff10da1e)

So, due to this if ideal logic 1 = 1 volt then here practically it can be less then 1 volt i.e., 0.97 volts (Vdd'). So, for any signal to be considered as Logic '0' and '1' in the NM low and NM high range. It is danger case.


![noise margin](https://github.com/user-attachments/assets/1d1253c5-0f7e-47c7-99c0-2f7cfd738bd2)
To solve this problem,, we have to put De-coupling capacitor in parallel with the circuit. Every time the circuit switches, it draws current from Cd, whereas, the RL network is used to replenish the charge into Cd. And the amount of current needed for the circuit is supplied by the De- Coupling Capacitor.

![decap 2](https://github.com/user-attachments/assets/0dd04fd1-c44b-435c-9475-8de79e9d649b)

In the chip it will look something like shown below Decoupling capacitors are placed in between the block a, block b and block c. So here in this whole block it has been ensured that supply is being done by the de-coupling capacitor. Once we are done with this we have taken care of the local communication.
 **Power planning**:Now let's consider that local circuitory and keep it as a black box and it can be repeat multiple times and there is some logic present at the boundaries also and the problem of current demand was solved by de-coupling capacitor. There is signal which is send from driver to load and the signal is basically logic 0 to logic 1. Here we need to maintain the particular driver to load line with same signal so that the load recieves the same. Now power supply is applied. Now assume 16 bit bus has to retain the same signal from driver to the load. so it should get the sufficient power from the supply. But at this bus, there is no de-coupling capacitor is available because it is not physible to put capacitor at all over the place. now, power supply is far away from the bus, that is why some voltage drop between them will occur definetly.
 
![power planning](https://github.com/user-attachments/assets/6915b809-ca34-4bcf-93bd-48a0f57c8516)

When we say one particular line of 16-bit bus is logic 1 it says that the capacitor is being charged to Vdd, and whenever we say logic 0 it says that the capacitor is discharged to ground.Let consider this 16 bit bus connected to inverter. So, all the capacitor are initially charged will get discharged and vice-versa due to inverter.  

But the problem is occurs due to all capacitor is connected to the single ground. This will cause a bump in 'ground' tap point during discharging. That bump is called as Ground Bounce. If the size of the bump exceeds the noise margin levelit might enter into an undefined state and due to undefined state it can either go to logic 1 or logic 0. So here thing becomes unpredictable
 
![powerplan1](https://github.com/user-attachments/assets/f5e5a0d4-ae27-4b61-a00c-dd821a299747)

Also , all capacitors which were'0' volts will have to charge to 'V'volts through single 'vdd'tap point. This will cause lowering of voltage at Vdd tap point. As long as this voltage drop is in noise margin level we are good enough but if it goes into an undefined region then things become unpredictable.


![powerplan 3](https://github.com/user-attachments/assets/fb35204a-6a68-4ca9-97bd-8caa9903e02f)

The phenomenon we have seen was causing the lowering of the supply voltage,this problem occured because power has applied to one point only. The solution of the problem is use multiple power supply. So, every block will take charge from neartest power supply and similarly dump the charge to the nearer ground. this type of power supply is called mesh.

![powerplan4](https://github.com/user-attachments/assets/ad9105e0-e904-4f0c-a58e-6b69b869675d)
Final layout after powerplaning

![powerplan5](https://github.com/user-attachments/assets/3e8c9aeb-78b1-48a2-b24c-5962c8898236)
**Pin placement and logical placement blockage**:This types of circuits are very much helpful to understand the timing analysis of inter clocks. now complete design becomes like given below which has 6 input ports and 5 output ports. The connectivity information between the gates is coded using VHDL/Verilog language and is called as 'Netlist'.


![placement1](https://github.com/user-attachments/assets/e6984201-2751-44d5-9ab7-2bc9d812a819)

Let's put this netlist in the core which we have designed before and let's try to fill this empty area between core and die with the pin information. The frontend team who decides the netlist connectivity input and output and the backend team who done the pin placements. So according to the pin placements, we have to locate the preplaced blocks nearer to the inputs of the preplaced blocks.
 ![placement2](https://github.com/user-attachments/assets/b1736e81-b1ab-44f6-8eac-210d3052af5c)
 **Section 2 tasks**:-

* Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
* Calculate the die area in microns from the values in floorplan def.
* Load generated floorplan def in magic tool and explore the floorplan.
* Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
* Load generated placement def in magic tool and explore the placement.
  
***Area of die in microns=Die width in microns * Die height in microns***
**Previously we have invoke the OPENLANE using docker method and run the floorplan**
```bash
run_floorplan
```
Before run the floorplanning, we required some switches for the floorplanning.We can get from the configuration from openlane.

![VirtualBox_vsdworkshop_29_07_2024_16_24_48](https://github.com/user-attachments/assets/b2a09723-b496-48e5-ac1a-0d4bdb065ec0)
![VirtualBox_vsdworkshop_29_07_2024_16_25_43](https://github.com/user-attachments/assets/27045311-1c5f-4ad4-80bf-431c949a98ff)

Here we can see that the core utilization ratio is 50% (bydefault) and aspect ratio is 1 (bydefault). similarly other information is also given. But it is not neccessory to take these values. we need to change these value as per the given requirments also.
![VirtualBox_vsdworkshop_29_07_2024_16_28_03](https://github.com/user-attachments/assets/fa865f19-b179-4dc8-a24e-e5a0f6b4e8ad)

![VirtualBox_vsdworkshop_29_07_2024_16_28_03](https://github.com/user-attachments/assets/bb2fabdf-67d4-43ec-90a2-adddd04730de)
Here FP_PDN files are set the power distribution network. These switches are set in the floorplane stage bydefault in OpenLANE.  
Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance.

In the OpenLANE lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

Now we see, with this settings how floorplan run.

![VirtualBox_vsdworkshop_29_07_2024_16_36_12](https://github.com/user-attachments/assets/f2eab3fb-6bd3-48d3-aff9-81e0081fe59f)
![VirtualBox_vsdworkshop_29_07_2024_16_36_32](https://github.com/user-attachments/assets/2d51b5cc-24c4-405e-ae20-4445adef5822)
**Calculate the die are in microns**

![VirtualBox_vsdworkshop_29_07_2024_16_51_49](https://github.com/user-attachments/assets/cec32260-d0b0-4e37-9bed-53e6b95b2ae8)
$$
100 \text{ unit distance} = 1 \text{ micron}
$$

$$
\text{Die width in unit distance} = 660,685 - 0
$$

$$
\text{Die height in unit distance} = 671,405 - 0
$$

$$
\text{Distance in micron} = \frac{\text{Value in unit distance}}{1000}
$$

$$
\text{Die width in micron} = \frac{660,685}{1000}
$$

$$
\text{Die height in micron} = \frac{671,405}{10,000}
$$

$$
\text{Area of die in micron} = 660.685 \times 671.405 = 443,587.212425 \text{ square microns}
$$
**RUNNING floorplan.def in Magic layout in another terminal**
```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-07_10-25/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

![VirtualBox_vsdworkshop_29_07_2024_17_28_51](https://github.com/user-attachments/assets/3a16e30f-45e7-43cd-bfd4-e31d5e7219f2)
![VirtualBox_vsdworkshop_29_07_2024_18_35_54](https://github.com/user-attachments/assets/fba49aad-e412-4441-8673-4a9d4c0311cb)
![VirtualBox_vsdworkshop_29_07_2024_19_15_03](https://github.com/user-attachments/assets/92323cb5-b153-4dfa-878e-1638c99c3597)
![VirtualBox_vsdworkshop_29_07_2024_19_27_26](https://github.com/user-attachments/assets/7d7ba099-ea31-497a-8b86-207430cab598)
![VirtualBox_vsdworkshop_29_07_2024_19_28_21](https://github.com/user-attachments/assets/9fcf975f-1763-47dc-980e-b6ed211d5aeb)
## D2 SK2 Library binding and placement
### Netlist binding and initial place design 
**Build netlist with physical cells**: ets we have the netlist of gates and shape of these gates represents the functionality of this gates. Foe example we have NOT gate as a tringular shape but in reality it is a box with physical dimensions it has width and height.Similarly for AND gate it also has a box shape in reality, Flipfops are also square boxes.So, we have given the physical dimensions to all the gates and flipflops. For everycomponent of the netlist we will give the particular shape with particular dimensions because ir real world the shapes like AND,OR gates does not exists so we make them as square all the blocks also have the width and height and proper shape.

![buildnetlist](https://github.com/user-attachments/assets/d1749ba1-7ece-448d-9bf6-e4db6752eedc)

Now we will remove the wires,all the gates, flipflops and blocks are present in the shelf which is called as Library.

A library is a place where you can find all kind of books all the gates,f/f are books here. Library also has the timing information of the perticular book like delay of the gates. Library can be devides into two sublibraries, One library consist of shape and size and other library might consist only of the delay information. Library has the various flavours of each and every cell. Like same cell can have bigger in size in different self, bigger the size of cell lesser the resestnce path so it will work faster and will have lesser delay. We can pick up from these what we want based on the timing condition and available space on the floorplan.



![buildnetlist2](https://github.com/user-attachments/assets/3bb1daa0-0201-4953-b7aa-1a41f1136dc5)

**Placement**:Once we have given proper shape and size to each and every gates the next step is to take those particular shapes ans sizes and place it on the floorplan. We have the floorplan with inout and output ports, we have particular netlist, and we have particular size given to each component of this netlist. So we have the physical view of the logic gates. Next step is to place the netlist onto the floorplan. We have to take the connectivity information from the netlist and design the physical view gates on the floorplan.


![buildnetlist3](https://github.com/user-attachments/assets/97686f59-0e4c-4024-bf7b-d7ef6c2ee1cd)
Now, we have the floorplan where we have the preplaced cells from the previous slides, Placement will make sure that the pre placed cells locations are not affected they are kept as it as and the second thing which will be taken care of that is no cell should be placed over the pre-placed cells. We need to place the physical view of the netlist onto the floorplan in such a fashion that logical connectivity should be maintained and that particular circuit should interact with their input and output ports to maintain the timing and the delay will be minimal.

![buildnetlist4](https://github.com/user-attachments/assets/3d13f68b-5cc6-414f-a793-a7055d7db72f)
### Optimize placement using estimated wirelength and capacitence
**Optimize Placement**: In optimize placement we will resolve the problem of distancing.Lrt's take the example of FF1 to Din2. There must be a wire going from Din2 to FF1 but before going into routing the desing or wiring we will try to estimate the capacitances. If we lokk the capacitance from Din2 to FF1 it is every huge because wire length is huge in that case even the resutance will also be huge because of that length. If we send the signal from Din2 then it will be difficult for FF1 to catch that input because distance is large. So we can place some intermediate steps to maitain the Signal integrity. By this the input is succesfully driven to the FF1 from Din2. These intermediate steps are called here Repeaters , Repeaters are basically buffers that will recondition the original signal and make a bew signal which replicate the original signal and send it forward this process repeates untill we reach to the actual cell where we want to send the input in this way signal integrity is maintained. By using repeaters we resolve the problem of signal integrity but there will be a loose of area because more and more repeaters are used more area will be used of the particular floorplan.  
![optplace](https://github.com/user-attachments/assets/97a4d26d-105d-4fce-afc7-3e43db445331)

Stage 4 is bit tricky as compared to other stages.Now we have to check that, what we have done is correct or not. For that we need to do Timing analysis by considering the ideal clocks and according to the data of analysis, we will understand that, the placement is correct or not.


![optplace1](https://github.com/user-attachments/assets/11d7b140-1f9b-4624-9e6a-9314e9fddba6)
### Need for libraries and characterization 
Every ICdesign Flow needs to go through the several steps. First step to go through is Logic Synthesis, let's say if we have a functionality which is coded in a form of an RTL so first we need to convert the functionality into legal hardware is refered to as Logic Synthesis. Ouput of the logic synthesis is arrangement of gates that will represent the original functionality that has been described using an RTL. Next step of logic synthesis is Floorplaning, in this we omport the output of logic synthesis and decide the size of the Core and Die. The next step after floorplaning is Placement, in this we take the particular logic cell send place them on the chip in such a fashion that initial timing is better. Next step is CTS(Clock tree synthesis), in this we take care that clk should reach each and every signal at the same time also take care of each clk signal has equal rise and fall.Next step is Routing, routing has to go through the certain flow dependendent on the characterization of the flip flop.And now comes the last step STA(Static timing analysis), in this we try to see the set up time, hold time, maximum achieved frequency of the circuit. One common thing across all stages 'GATES or Cells'.
### Congestion aware placement using RePlAce
In digital design, placement refers to the process of positioning standard cells or blocks on a chip. The RePlAce tool provides a method for congestion-aware placement, focusing on both global and detailed placement stages.

**Global Placement**
Global Placement is the initial stage of placement where the goal is to place cells or blocks approximately in the chip area, ensuring that:

* **Overall Design Constraints**: The cells are roughly placed considering overall area constraints and design rules.
* **Congestion Management**: This stage aims to minimize routing congestion by spreading cells evenly and avoiding high-density regions.
* **Optimization**: The placement is optimized for wirelength, signal delay, and other high-level factors without focusing on precise cell placement.
 **Key Aspects of Global Placement**:

* **Early Estimation of Congestion**: Provides an initial estimate of congestion that helps in further refinement.
* **Algorithmic Approach**: Uses algorithms to approximate optimal cell positions while considering the overall design layout.
 **Detailed Placement**
Detailed Placement follows global placement and focuses on fine-tuning cell positions to achieve the final design goals:

* **Fine Adjustment**: Refines the positions of cells placed during the global placement to meet precise design rules and constraints.
* **Local Congestion**: Reduction: Focuses on reducing local congestion and optimizing the cell arrangement to ensure efficient routing.
* **Final Verification**: Ensures that the final placement meets all the design specifications, including timing, area, and power constraints.
  **Key Aspects of Detailed Placement**:

* **Precise Cell Location**: Adjusts cell positions to optimize local routing and meet specific design rules.
* **Congestion Mitigation**: Addresses local congestion issues identified in the global placement phase by repositioning cells to balance routing density
  **Summary**
Congestion-aware placement using RePlAce involves:

* Global Placement: Rough positioning of cells with an initial focus on congestion.
* Detailed Placement: Fine-tuning of cell positions to optimize local routing and meet design constraints.
* RePlAce: A tool that integrates both global and detailed placement stages with a focus on managing and reducing congestion throughout the placement process.
  ### Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs
  ```bash
  run_placement
  ```
![VirtualBox_vsdworkshop_29_07_2024_20_51_22](https://github.com/user-attachments/assets/796904d8-b85e-4a15-9513-c891725e5524)
### Load placement.def in magic layout
```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-07_10-25/results/placement/
# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![VirtualBox_vsdworkshop_29_07_2024_20_54_40](https://github.com/user-attachments/assets/283ef591-b336-4dbe-af7a-888192fc9422)

![VirtualBox_vsdworkshop_07_08_2024_13_31_27](https://github.com/user-attachments/assets/9a2b31c9-9d4b-45eb-b046-a08a408f2383)
##  D2 SK3 Cell design and characterization flows
### Inputs for cell design flow
In Cell Design Flow, Gates, flipflops, buffers are named as 'Standard Cells'. These standard cells are being placed in the section called as 'Library'.And in the library many other cells are available which have same functionality but the size is different.


![celldesign](https://github.com/user-attachments/assets/b0d61c52-0592-4a12-a826-a9ae56ea0581)
![celldesign1](https://github.com/user-attachments/assets/4af40978-cc92-48dd-9c0c-cab8bfd5d646)

If you look into one of the inverter from the library the cell design flowis as follows

The inverter has to represented in form of the shape, drive strength, power charracteristic and so on. Here cell design flow is devided into three parts.

* Inputs

* Design steps

* Outputs
  
![celldesign2](https://github.com/user-attachments/assets/90dde6df-82a4-40cf-b71e-8d60ae9e723a)
### Circuit design Steps
![circuitdesign1](https://github.com/user-attachments/assets/badc98cc-6aa5-49a5-b1a4-f0ab80fcf010)

In circuit Design there are two steps.

First step is to implement the function itself and second step is to model the PMOS nad NMOS transistor in such a fashion in order to meet the libraray.

**Outputs**

The typical output what we get from the circuit design is CDL(circuit description language) file,GDSII,LEF,extracted spice netlist(.cir).
### Layout design steps


![layoutdesign](https://github.com/user-attachments/assets/91c7eb7a-7fa0-47d9-91da-8405b999fca2)
In Layout Design First step is to get the function implemented through the MOS transistor through a set of PMOS and NMOS transistor and the second step is to get the PMOS network graph and the nNMOS network graph out of the design that has been implemented.

![eulerpath](https://github.com/user-attachments/assets/f336c1a7-9bcc-47bd-85bf-e177302dd5c7)
After getting the network graphs next step is to obtain the Euler's path. Eule's path is basically the path which is traced only once.

![stickdiagram](https://github.com/user-attachments/assets/f525bd4d-f53f-4bb9-bfe0-24e19434f50f)
Next step is to draw stick diagram based on the Euler's path. This stick diagram is derived out of the circuit diagram.
![eulerpath to layout](https://github.com/user-attachments/assets/73680847-e784-47cb-b2d8-6ff7953d5ddf)

Next step is to convert this stick diagram into a typical Layout, into a proper layout and then get the proper rule we have discissed earlier. Once we get the particular layout then we have the cell width, cell length and all the specifications will be there like drain current, pin locations and so on.

Next and Final step is to extract the parasatics of that particular layout and charaterise it in terms of timing. So before that the output of the layout design will be GDSll. Once you get the extracted spice netlist then we characterize it. Characterization helps in getting timing, noise and power information.
### Typical characterization flow

Let's try to build the characterization flow based on the inputs we have,

First step is to read in the model, second step is to read the extracted spice netlist, third step is to define or recognize the behaviour of the buffer, fourth step is to read the subcircuits of the inverter and then in the fifth step need to attach the necessary power supplies, sixth step is to apply the stimulus then in the seventh step we need to provide the necessary output capacitance then in the final eighth step in which we need to provide necessary simulation command for example if we are doing transent simulation so we need to give .tran command , if we are doing DC simulation then we give .dc command.
Next step is to feed in all this inputs from 1 to 8 in a form of a configuration file to the characterization software "GUNA" .

![characterizationflow](https://github.com/user-attachments/assets/b460206e-09f7-4c52-a8e7-03c4cacb263b)
## D2 SK4 General timing characterization
![timing](https://github.com/user-attachments/assets/6be06b3a-4be8-4212-8465-b9b06fb7572f)
* **Slew Low Rise Threshold**: Start point of the rising edge transition.
* **Slew High Rise Threshold**: End point of the rising edge transition.
* **Slew Low Fall Threshold**: Start point of the falling edge transition.
* **Slew High Fall Threshold**: End point of the falling edge transition.
* **Input Rise Threshold**: Voltage level where input is considered 'high'.
* **Input Fall Threshold**: Voltage level where input is considered 'low'.
* **Output Rise Threshold**: Voltage level where output is considered 'high'.
* **Output Fall Threshold**: Voltage level where output is considered 'low'.

![propdelay](https://github.com/user-attachments/assets/e11d8058-d0e0-4978-aca3-af8f53fb924e)
**Propagation Delay**:

Time for a signal to propagate through a circuit element.
Measured at the 50% points of input and output transitions.
Affects circuit speed.




**Transition Time**:

Time for a signal to transition between voltage levels.
Rise time (tr): 10% to 90% transition.
Fall time (tf): 90% to 10% transition.
Affects signal integrity and performance.
## Day 3 Design library cells using magic layout and ngspice characterization
###  D3 SK1 Labs for CMOS Inverter and ngspice simulation
### IO PLACER REVISION
Till now, we have done floor planning and run placement also. But if we want to change the floorplanning, for example, in our floor planning, pins are at equal distance and if we want to change it then we can also make it by ``` Set ``` command.

For that first we have to check the swithes in the configuration and from that we have to take the syntax "env(FP_IO_MODE) 1". and make it to the "env(FP_IO_MODE) 2". then again run the floorplanning.

Then check the changes in the pins location through magic -T.

![VirtualBox_vsdworkshop_31_07_2024_20_13_46](https://github.com/user-attachments/assets/1166a339-3e8a-465e-ad57-c4395f6c3ee4)

![VirtualBox_vsdworkshop_31_07_2024_20_15_27](https://github.com/user-attachments/assets/40c5e5e6-b46c-4481-88ba-03bcf283b8d4)
![VirtualBox_vsdworkshop_31_07_2024_20_20_59](https://github.com/user-attachments/assets/2df1c719-d2a0-4e18-a310-74e1a7f4ba93)
![VirtualBox_vsdworkshop_31_07_2024_20_21_34](https://github.com/user-attachments/assets/5951c7ba-60a5-4900-ad6d-99625863fb1a)
![VirtualBox_vsdworkshop_31_07_2024_20_22_49](https://github.com/user-attachments/assets/cf967777-5ced-44a6-b1ec-42572b79a850)
### SPICE DECK FOR CMOS INVERTER

![ngspice](https://github.com/user-attachments/assets/8345700a-b0d2-4aa4-86f8-1abae27b634d)
**Explaination**
* **Component connectivity**:- In this we need to define the connectivity of the substrate pin. Substrate pin tunes the threshold voltage of the PMOS and NMOS.
* **Component values**:- Values for the PMOS nad NMOS. We have taken the same size of both PMOS and NMOS.
* **Identify the nodes**:- Node mean the points between which there is a component.These nodes are required to define the netlist.
* **Name the nodes**:- Now we wiil name these nodes as Vin, Vss, Vdd, out.
* **CONNECTIONS**:

  * For M1 MOSFET drain is connected to out node, gate is connected to in node, PMOS transistor substrate and Source is connected to Vdd node.
  * For M2 MOSFET drain is connected to out node, gate is connected to in node, NMOS source and substrate are connected to 0.
  * CLOAD It is connected between out and the node 0. And it's value is 10ff
  * Supply voltage(Vdd) which is connected between Vdd and node 0 and value of it is 2.5
  * Similarly we have input voltage which is connected between Vin and node 0 and its value is 2.5.
* **SIMULATION COMMANDS**:
  Now we have to give the simulation commands in which we are swiping the Vin from 0 to 2.5 with the stepsize of 0.05. Because we want Vout while changing the Vin.
* **Final modelling**:
   Final step is to model files. It has the complete description about NMOS and PMOS.
  
 ### SPICE SIMULATION LAB FOR CMOS
 
  
 ![vtc](https://github.com/user-attachments/assets/a8d8aa39-b6b6-4e1a-9cb3-15534ccd6abd)
 ### Switching Threshold Vm


![static](https://github.com/user-attachments/assets/389775be-2fa6-4d41-b42f-613111b6bce3)

Switching thresold, Vm (the point at which the device switches the level) is the one of the parameter that defined the robustness of the Inverter. Switching thresold is a point at which Vin=Vout.

![cmos](https://github.com/user-attachments/assets/ccff5d58-6f19-423f-bf5d-afd9a1207120)

### STATIC AND DYNAMIC BEHAVIOUR OF CMOS

![static](https://github.com/user-attachments/assets/f7117a1b-1bb1-4f2b-86de-73dc030f702f)

![dynamic](https://github.com/user-attachments/assets/80a7ef9f-8bf2-477c-aa44-bc3266083184)


In Dynamic simulation we will know about the rise and fall delay of CMOS inverter and how does it varying with Vout. In this simulation everything else will remian same except the input which is provided will be a pulse and simulation command will be .tran

The graph Time vs Voltage will be plotted here from where we can calculate the rise and fall delay.
### LAB FOR CMOS
Section 3 tasks:-
* Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using openlane flow](https://github.com/nickson-jose/vsdstdcelldesign.git)
* Load the custom inverter layout in magic and explore.
* Spice extraction of inverter in magic.
* Editing the spice model file for analysis through simulation.
* Post-layout ngspice simulations.
* Find problem in the DRC section of the old magic tech file for the skywater process and fix them
**Clone custom inverter standard cell design from github repository**
```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

![VirtualBox_vsdworkshop_01_08_2024_00_31_26](https://github.com/user-attachments/assets/fa408b86-0226-4698-8d0b-8dc54cacb65b)
![VirtualBox_vsdworkshop_01_08_2024_00_41_35](https://github.com/user-attachments/assets/e3b89cd4-052d-433a-afa8-b372b5a906f3)

**Load the custom inverter layout in magic and explore**

![VirtualBox_vsdworkshop_01_08_2024_00_45_14](https://github.com/user-attachments/assets/47c93a7a-8041-4b88-9966-f2658537262b)
![VirtualBox_vsdworkshop_01_08_2024_17_16_05](https://github.com/user-attachments/assets/603f96e9-c00b-4b27-9a77-cbf0fc46c165)
![VirtualBox_vsdworkshop_01_08_2024_17_16_59](https://github.com/user-attachments/assets/108237f3-0752-4703-ad10-a57ebdc342f6)
![VirtualBox_vsdworkshop_01_08_2024_17_33_28](https://github.com/user-attachments/assets/3536373f-4828-46a4-b404-871d48b667b7)  
## D3 SK2 Inception of layout and CMOS fabrication process
**Spice extraction of inverter in magic**
```bash
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

![VirtualBox_vsdworkshop_01_08_2024_17_37_13](https://github.com/user-attachments/assets/fd98cec8-76b7-412c-9d42-0194535ec1ed)
![VirtualBox_vsdworkshop_01_08_2024_17_40_06](https://github.com/user-attachments/assets/8b7c0171-0460-4f37-8f67-6ba8e8962184)
**create spice file and necessary modifications to be made according to our spice deck**

![VirtualBox_vsdworkshop_01_08_2024_17_43_07](https://github.com/user-attachments/assets/cee7a963-9bc1-4ac3-b907-b9e8712ec372)
![VirtualBox_vsdworkshop_01_08_2024_19_59_55-correct correct](https://github.com/user-attachments/assets/bd2c12ec-068b-492d-aac7-9fbc098bbbd3)
**post-layout ngspice simulation**
```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```
![VirtualBox_vsdworkshop_01_08_2024_20_01_26](https://github.com/user-attachments/assets/2cefd190-8555-471c-b709-b24be3350827)
![VirtualBox_vsdworkshop_07_08_2024_19_01_06](https://github.com/user-attachments/assets/0a881800-b855-43ec-b7d3-ff40a2161108)  
**Rise time**
It is time taken to the output waveform to 20% value to 80% value.  
![VirtualBox_vsdworkshop_01_08_2024_20_30_39 -Rise time(2 24-2 18)](https://github.com/user-attachments/assets/61afadca-542a-4277-93c2-95fc8b91b555)  
so, rise time= (2.24609 - 2.18215)e-09 = 63.94 psec.  
**Fall time**  
it is the time take by output for transition from 80% to 20%.  
![fall time 4 095-4 59](https://github.com/user-attachments/assets/675d8253-1006-42eb-91b1-8f7a05f5ccd2)  
so, fall time= (4.09515 - 4.05269)e-09 = 42.46 psec  
**Propagation delay**  
it is the time difference between the 50% of input and 50% of the output.  
![VirtualBox_vsdworkshop_01_08_2024_20_42_57 prop delay(2 21-2 15) - Copy](https://github.com/user-attachments/assets/3bc518c0-aa14-4795-8028-6ab2c5bddda5)  
so, propogation delay =(2.21086 - 2.15)e-09 = 60.86 psec.  
**Cell rise delay**  
Time taken by output to rise to 50% and input to fall to 50%  
![VirtualBox_vsdworkshop_07_08_2024_19_31_06](https://github.com/user-attachments/assets/1e5fdf56-a6e5-42cd-9263-d71209b4c590)  
so,cell rise delay=(2.21078-2.14992)e-09=60.86psec  
**Cell fall delay**  
Time taken by output to fall to 50% and input to rise to 50%    
![VirtualBox_vsdworkshop_07_08_2024_19_32_08](https://github.com/user-attachments/assets/54cd877e-5526-4c80-a552-7533968c8a09)  
so,cell fall delay=(4.07586-4.04914)e-09=26.72psec
## D3 SK3 Sky130 Tech File labs
**Find problem in the DRC section of the old magic tech file for the skywater process and fix them**
To know more about the Magic DRC we can go to the website:-[The Magic Technology File Manual - DRC Section](http://opencircuitdesign.com/magic/Technologyfiles/TheMagicTechnologyFileManual/DrcSection)    
Link to Google_Skywaters Design Rules: -   [SkyWater PDK Documentation - Periphery Rules](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)  
For reference , we can use the github repo of Google-Skywater:[SkyWater PDK GitHub Repository](https://github.com/google/skywater-pdk)  
**Commands used**
```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```
```bash
#IN TKCON WINODW Form a seperate box
paint v2
cif see VIA2
```


![VirtualBox_vsdworkshop_02_08_2024_00_17_51](https://github.com/user-attachments/assets/0bdaa444-6cf3-4e44-a4c7-d2daec109e8b)

![VirtualBox_vsdworkshop_07_08_2024_20_22_50](https://github.com/user-attachments/assets/c769e1fc-af6b-41d0-a486-f0e43082239e)

![VirtualBox_vsdworkshop_02_08_2024_00_30_30](https://github.com/user-attachments/assets/b4bfd00d-d2ef-4949-a5c4-3b22dbb0bbf4)
![VirtualBox_vsdworkshop_02_08_2024_09_55_04](https://github.com/user-attachments/assets/348dec25-ebb7-46b2-ae10-3b579b144bc2)
![VirtualBox_vsdworkshop_07_08_2024_20_54_47](https://github.com/user-attachments/assets/a64f4145-9133-46c2-83dc-bf85e9c0e12c)  
**Incorrectly implemented poly.9**

![Untitled](https://github.com/user-attachments/assets/679e11ca-554e-41e6-ae05-3d0dceffbcee)

![VirtualBox_vsdworkshop_07_08_2024_23_17_10(ip)](https://github.com/user-attachments/assets/aaea6899-11a5-44b8-bbb3-6d30f47dc6ff)
![VirtualBox_vsdworkshop_07_08_2024_23_20_38](https://github.com/user-attachments/assets/28b8c0f0-5616-4e84-87a1-2c2be95509f5)  
**update in sky130a.tech**
```bash
vim sky130A.tech
```
![VirtualBox_vsdworkshop_07_08_2024_23_26_37](https://github.com/user-attachments/assets/b284c39e-9035-452f-9141-c65cb7943328)

![VirtualBox_vsdworkshop_07_08_2024_23_29_35](https://github.com/user-attachments/assets/3172629b-679e-40d8-9aed-6c204bc6c7d3)  
**Commands in tkcon**
```bash
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

![VirtualBox_vsdworkshop_07_08_2024_23_31_28](https://github.com/user-attachments/assets/abb9cb5c-c070-42b3-a3a7-568e5a986f30)
![VirtualBox_vsdworkshop_07_08_2024_23_31_42](https://github.com/user-attachments/assets/d665ff84-b236-43c2-921c-79923fd21adb)
![VirtualBox_vsdworkshop_08_08_2024_01_21_35](https://github.com/user-attachments/assets/4e8952c7-b6a4-4ccf-ad4c-53e1becfad26)  
**Incorrectly implemented difftap2.rule**

![diff](https://github.com/user-attachments/assets/a984e039-6fcb-44b3-92b2-df602569e1a9)
![VirtualBox_vsdworkshop_08_08_2024_01_22_44](https://github.com/user-attachments/assets/67c7b885-3d4f-42f7-ad7e-9155d3263973)  
**Update in sky130A.tech**
```bash
vim sky130A.tech
```

![VirtualBox_vsdworkshop_08_08_2024_01_28_07difftap](https://github.com/user-attachments/assets/2eb31bcf-f1d4-438d-ab27-241008f8a9c6)
![VirtualBox_vsdworkshop_08_08_2024_01_32_20 difftap correct](https://github.com/user-attachments/assets/de2d9859-2a7a-4e8f-867c-7130856f1e99)  
**Commands in tkcon**
```bash
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```
![VirtualBox_vsdworkshop_08_08_2024_01_33_26](https://github.com/user-attachments/assets/9e64de2d-4a1d-4a89-9b66-ce9db6a32f19)  
**Incorrect implementation of nwell.4 rule**


![nwell](https://github.com/user-attachments/assets/8f072b76-49d7-449b-9fd9-79b296a28a08)

![VirtualBox_vsdworkshop_08_08_2024_01_49_27](https://github.com/user-attachments/assets/8b05b6be-285f-4bd4-8141-969ea352285d)  
**Update in sky130A.tech**
```bash
vim sky130A.tech
```
![VirtualBox_vsdworkshop_08_08_2024_01_53_30](https://github.com/user-attachments/assets/17c543ba-3754-4b1a-9578-edeb359a2b90)
![VirtualBox_vsdworkshop_08_08_2024_01_57_18](https://github.com/user-attachments/assets/e27f9942-2eea-40ee-87d0-01b6658b7c97)   
**Commands in tkcon**
```bash
# Loading updated tech file
tech load sky130A.tech

# Change drc style to drc full
drc style drc(full)

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```
![VirtualBox_vsdworkshop_08_08_2024_02_06_51](https://github.com/user-attachments/assets/fb587bbd-fbf1-4acc-8964-a273ad6b301a)
## DAY 4 Prelayout timing analysis and importance of good clock tree
###  D4 SK1 Timing modelling using delay tables
**LAB TASK FOR DAY 4**
* Fix up small DRC errors and verify the design is ready to be inserted into our flow.
* Save the finalized layout with custom name and open it.
* Generate lef from the layout.
* Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
* Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
* Run openlane flow synthesis with newly inserted custom inverter cell.
* Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
* Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
* Do Post-Synthesis timing analysis with OpenSTA tool.
* Make timing ECO fixes to remove all violations.
* Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
* Post-CTS OpenROAD timing analysis.
* Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.<br>
  **LEF(Library Exchange format)**:LEF files describe the physical properties of standard cells, macros, and other library elements. They do not include any information about the actual placement of cells in a design but rather provide the necessary details for placing and routing the design.<br>
   **DEF(Design Exchange format)**:DEF files describe the actual placement and routing of the cells in a specific design. It contains detailed information about how the design has been laid out, including the position of each cell and the routing of interconnections.<br>
  1.**Fix up small DRC errors and verify the design is ready to be inserted into our flow**:<br>
  Condition to be satisfied before making standard cell
  * The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
  * Width of the standard cell should be odd multiples of the horizontal track pitch.
  * Height of the standard cell should be even multiples of the vertical track pitch.
Open the track file from```pdk/sky130/libs.tech /openlane/sky130_fd_sc_hd/track.info```

![1](https://github.com/user-attachments/assets/440b92cf-6ed4-4128-873a-4097e24bd552)
![2](https://github.com/user-attachments/assets/a070a0e9-19f6-477c-b2f4-b38e3e3a9a92)  
**Commands to open custom inverter layout**
```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
**Checking conditions 1,2&3**

![4](https://github.com/user-attachments/assets/faf4a323-88bc-4e98-b650-9eb241d3e1dc)

![5](https://github.com/user-attachments/assets/94f852b7-46dd-407d-9d6f-9c990baf5a4e)

![6](https://github.com/user-attachments/assets/fe205bc2-2bc6-4318-b117-9f23493e69c6)

**Opening newly created inverter and check various port names and its value**
```bash
# Command to save as
save sky130_vsdinv.mag

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```

![7](https://github.com/user-attachments/assets/b3d15096-16aa-498e-91c4-f7445bf1f493)


![VirtualBox_vsdworkshop_04_08_2024_00_19_44](https://github.com/user-attachments/assets/dd9e3054-f492-4482-a6c8-5707fa7932e3)


![8](https://github.com/user-attachments/assets/ec09f98d-42ed-489c-a656-a66daee36cfd)  
**Generating lef from layout**  
```bash
# lef command
lef write
```


![VirtualBox_vsdworkshop_04_08_2024_00_19_36](https://github.com/user-attachments/assets/2523405d-a845-4681-81f8-9005b7eac3b8)
![9](https://github.com/user-attachments/assets/ef0ab4c2-ed83-43ed-9d48-6d001ca5a5ca)
![10](https://github.com/user-attachments/assets/f3b6f92a-2a3d-46c2-ba74-b045e7441b8d)  
**Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory**
```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

![11](https://github.com/user-attachments/assets/74d237fc-fc4f-4793-909c-db212fd91c6f)
![12](https://github.com/user-attachments/assets/0774ef85-57b2-4646-86f7-2f9c65ec232d)
![13](https://github.com/user-attachments/assets/6cd9941a-1b67-46d6-95d2-f5a96258e1bc)
![14](https://github.com/user-attachments/assets/106cf674-4eae-4182-8f76-8d279dbb7b42)  
**Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow**  
**Commands to be added in config.tcl**
```bash
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

![15](https://github.com/user-attachments/assets/ebcd5ed2-c497-4982-b44b-dae58b304dca)
![16](https://github.com/user-attachments/assets/ec41bbf1-e270-4905-bbee-9545654ab3f1)<br>
**Run openlane flow synthesis with newly inserted custom inverter cell**
```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane
docker
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```


![VirtualBox_vsdworkshop_04_08_2024_00_31_30](https://github.com/user-attachments/assets/ab755668-8ce3-4cce-9395-c6cd3f5eb5bc)
![VirtualBox_vsdworkshop_04_08_2024_00_36_00](https://github.com/user-attachments/assets/5b0b86d2-0851-437b-b93f-986469622eb9)
![VirtualBox_vsdworkshop_04_08_2024_00_39_46](https://github.com/user-attachments/assets/8c7b8493-f898-4489-96ff-7f0ec5dd8785)
![VirtualBox_vsdworkshop_08_08_2024_13_34_23](https://github.com/user-attachments/assets/af082b78-cf82-4f36-a7a8-85e01b779553)<br>

#### Introduction to delay tables
**Power aware CTS**:If we make enable pin at logic '1' in the AND gate, then clock will propagate and if we make it 'logic 0' it will block the clock. Similarly in 'OR' gate if we make enable as 'logic 0' it will propagate and on making it 'logic 1' it will block the clock.

So the advantage of this blocking period is that we can save lot of power in clock tree.

![Untitled](https://github.com/user-attachments/assets/4de6a8e8-d4f7-4787-ac68-9407f49df0fa)
**Understanding need and usage of delay tables**<br>
**What Are Delay Tables?**<br>
Delay tables are data structures used in digital integrated circuit design to model and store the delay characteristics of various components, such as gates, interconnects, and cells. They provide information about how long it takes for a signal to propagate through a component under different conditions.<br>

**Need for Delay Tables**<br>
* **Accurate Timing Analysis**: Delay tables are crucial for performing accurate timing analysis of digital circuits. They allow designers to predict the performance of a circuit and ensure that it meets timing requirements.
* **Performance Optimization**: By understanding the delay characteristics, designers can optimize the design for speed, reducing critical path delays and improving overall performance.
* **Design Verification:** Delay tables help in verifying that the design meets the required timing constraints, preventing timing violations that can lead to functional errors.
* **Library Characterization:** Standard cell libraries use delay tables to characterize the delay of each cell under various conditions of load, input slew, voltage, and temperature.<br>
 **Components of Delay Tables**<br>
* **Input Slew Rate**: The rate at which the input signal transitions from low to high or high to low.
* **Output Load**: The capacitance that the output of a cell or gate has to drive.
* **Voltage and Temperature**: Delay can vary based on operating voltage and temperature, so tables often include different conditions.
* **Transition Time (Slew)**: The time it takes for a signal to transition from one logic level to another.
* **Propagation Delay**: The time it takes for a signal to travel from the input to the output of a cell.<br>
**Usage of Delay Tables**<br>

* **Static Timing Analysis (STA)**:

STA tools use delay tables to calculate the timing of each path in the circuit.
They sum the delays of individual components along a path to determine the total path delay.
STA checks the design against timing constraints to ensure that signals arrive within required time windows.
* **Timing Closure**:

During the design process, especially in place-and-route (P&R), delay tables are used to achieve timing closure.
Designers adjust the placement of cells, routing of interconnects, and other parameters to minimize delays and meet timing goals.
* **Simulation**:

Delay tables are used in timing simulations to predict how the circuit will behave under different conditions.
Accurate delay modeling is essential for functional verification and ensuring reliable operation.
* **Library Development**:

When developing standard cell libraries, delay tables are generated for each cell to describe its behavior under various conditions.
These tables are then used by EDA tools for timing analysis and optimization.

![delay tables](https://github.com/user-attachments/assets/28646ec8-7a0d-4705-9d4f-c867f60124cf)
![delay tables1](https://github.com/user-attachments/assets/9f69ba0d-c05f-4bac-87fe-2bbeeba7c421)

**Run openlaneflow synthesis with modified command to improve timing**
```bash

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane


docker
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# overwrite the design
prep -design picorv32a -tag 29-07_10-25 -overwrite 

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) 1

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
# Run_floorplan
run_floorplan
# Run_placement
run_placement

```
```bash
# If floorplan fails
init_floorplan
place_io
tap_decap_or
```


![VirtualBox_vsdworkshop_04_08_2024_00_42_01](https://github.com/user-attachments/assets/d28f4d67-7f28-4e7c-872c-2214e95c211c)

![VirtualBox_vsdworkshop_04_08_2024_00_42_18](https://github.com/user-attachments/assets/ba2841a9-20f2-4b5f-96f6-41da07a5d6e3)


![VirtualBox_vsdworkshop_04_08_2024_00_46_09](https://github.com/user-attachments/assets/952873d5-433d-4ba3-9988-b8c6217de7a5)

![VirtualBox_vsdworkshop_04_08_2024_00_46_25](https://github.com/user-attachments/assets/26951f4a-108e-4194-8c7f-8e487ba78f6d)
![VirtualBox_vsdworkshop_04_08_2024_01_00_55](https://github.com/user-attachments/assets/49271fc5-33fb-4057-a15f-5f9e184e64cc)
![VirtualBox_vsdworkshop_03_08_2024_20_03_46](https://github.com/user-attachments/assets/1577a759-e742-4e05-a759-016b59b5c768)

![VirtualBox_vsdworkshop_03_08_2024_20_03_59](https://github.com/user-attachments/assets/c1e14930-e893-41e7-b778-81f77886d1f6)
![VirtualBox_vsdworkshop_03_08_2024_20_04_36](https://github.com/user-attachments/assets/85857e2c-41f4-4421-ba01-28f6881e7e73)


![VirtualBox_vsdworkshop_04_08_2024_01_07_20](https://github.com/user-attachments/assets/69497bc4-1fb1-4345-a9af-f3f81fc2488e)

![VirtualBox_vsdworkshop_04_08_2024_01_09_37](https://github.com/user-attachments/assets/d2227de2-23a2-49bb-9b76-1c19be6f54db)<br>
**COMMAND TO OPEN MAGIC IN ANOTHER TERMINAL**
```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-07_10-25/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![VirtualBox_vsdworkshop_04_08_2024_01_13_06](https://github.com/user-attachments/assets/58da9098-5e8a-4603-8669-2527461e3d21)


![VirtualBox_vsdworkshop_04_08_2024_01_16_03](https://github.com/user-attachments/assets/66cdc14c-e40b-47f6-9fe1-86da8e2b35dc)<br>

## D4 SK2 Timing analysis using ideal clock using openSTA<br>

**Setup timing Analysis and Introduction to Flipflop setup time**



![setup](https://github.com/user-attachments/assets/b4045b45-7d4f-4460-8aed-3ed143dd3736)<br>
Let's start the setup analysis with the ideal clock(single clock). specifications of the clock is

clock frequency =1 GHz

clock period =1 ns

Now will do the analysis between '0' and 'T' clock period. We sent at edge to the launch flop at '0' clock period and at T=1ns period the second edge reached to capture flop.

Let's say here we have combinatonal delay of theta and set up timing analysis says that this combinational delay should be less than the T for system to work properly.
Now let's open the capture flop and we will see some combinational circuit there it has several MOSFETs , several logics,resistances and capacitances inside it.Also have the time graph for this particular flop
When there is logic '0' or logic '1' of clock 1 the delay of MUX1 and MUX2 will restrict or effect the combinational delay requirement.

So there is some finite amount of time which is required to the D input to settle and this amount of time is reffered to as SET UP TIME.

Hence finite time 's' required before clk edge for 'D' to reach Qm.

So, we can write that the internal delay of the MUX1 = set up time(S).

So, now θ<T becomes θ<(T-S).<br>
**Introduction to clock jitter and uncertainity**


![jitter1](https://github.com/user-attachments/assets/1081967d-3259-4ecf-a7b3-cdf41b2fa0e4)<br>

So in Jitter the clock is being created by PLL(phase-locked loops) and the clk source is expected to sent the clk signal at exactly 0,T,2T,....But that clk source might or might ot be able to generate the clk exactly at 0 or any other certain time because of it's inbuilt variations that is called jitter. Jitter is refered as temporary variation of the clk pulse.
Let's consider this uncertantity time(US) in consideration. So, now equation will become θ<(T-S-US). Now assuming 'S'=0.01ns and 'US'=0.09ns. by taking this, Let's identify the timing path in our circuit stage 1 and stage 3 logic path has single clock.

Now,we have to identify the combinational path delay for the both logics.<br>
**Do post synthesis timing analysis with opensta**<br>
```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

  ![VirtualBox_vsdworkshop_04_08_2024_15_06_14](https://github.com/user-attachments/assets/50663432-cef4-4300-a8ee-c28ee42e5162)<br>
  Newly created ```pre_sta.conf ```for STA analysis in openlane directory
  

![VirtualBox_vsdworkshop_04_08_2024_15_07_03](https://github.com/user-attachments/assets/6aec13fa-f00f-49b6-9fb9-f68afc4a8c0d)

Newly created ```my_base.sdc```for STA analysis in ```openlane/designs/picorv32a/src directory``` based on the file```openlane/scripts/base.sdc```

![VirtualBox_vsdworkshop_04_08_2024_15_11_46](https://github.com/user-attachments/assets/72263eb3-43e2-44a5-9747-1d180f724cc8)

![VirtualBox_vsdworkshop_08_08_2024_16_10_37](https://github.com/user-attachments/assets/6fb2f8e9-a152-4bcd-8354-129d5c117098)<br>
```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```


![VirtualBox_vsdworkshop_08_08_2024_16_15_50](https://github.com/user-attachments/assets/93c3c46b-b3fb-463e-b421-1a174ef0ba10)

![VirtualBox_vsdworkshop_04_08_2024_15_11_22](https://github.com/user-attachments/assets/7749895f-e700-4d4f-83d2-c1377e85657e)<br>
Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

Commands to include new lef and perform synthesis
```bash
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 29-07_10-25 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

![VirtualBox_vsdworkshop_04_08_2024_15_12_54](https://github.com/user-attachments/assets/55183310-2ec8-4f2c-b3af-d75dba8edc95)

![VirtualBox_vsdworkshop_08_08_2024_18_46_36](https://github.com/user-attachments/assets/c9301065-ccb0-45fd-86b2-f42921c746bd)

![VirtualBox_vsdworkshop_04_08_2024_15_13_56](https://github.com/user-attachments/assets/36e9abc5-2168-4c03-b75c-b9df95fec940)
![VirtualBox_vsdworkshop_04_08_2024_15_16_30](https://github.com/user-attachments/assets/b8f5d6c5-2646-4264-8a94-da19ace94b88)<br>
**Make timing ECO FIXES TO REMOVE ALL VIOLATION**<br>
OR gate of driving strength 2 is driving 4 fanouts<br>



![1](https://github.com/user-attachments/assets/57f5159e-03da-43f6-99d6-fc8b26f6e7d9)<br>
**Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4**
```bash
# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

![2](https://github.com/user-attachments/assets/69de151b-f4a7-40e0-914e-f50c8a1151b5)


![3](https://github.com/user-attachments/assets/642862d9-722f-4c17-b264-354a9e5e1f87)

![4](https://github.com/user-attachments/assets/61aaa85a-5883-4ec1-af2e-f73c2797f861)<br>
OR gate of drive strength 2 is driving 4 fanouts


![5](https://github.com/user-attachments/assets/94f2606a-591e-4ac6-bddd-5215654beb6f)<br>
**Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4**
```bash
# Reports all the connections to a net
report_net -connections _11675_

# Replacing cell
replace_cell _14514_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

![6](https://github.com/user-attachments/assets/5704beb9-03e3-4010-a19c-12c393c3a680)


![7](https://github.com/user-attachments/assets/7a672c62-1d6e-430f-bd52-71bd23b48daa)<br>
OR gate of drive strength 2 driving OA gate has more delay

![8](https://github.com/user-attachments/assets/df0eb30b-f35a-471a-b364-14c89b71f024)<br>
 **Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4**
 ```bash
# Reports all the connections to a net
report_net -connections _11643_

# Replacing cell
replace_cell _14481_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

![9](https://github.com/user-attachments/assets/9897b255-c413-4f5d-b247-7dd5a39c1e1c)

![10](https://github.com/user-attachments/assets/d08759d7-b55d-4f37-951e-911a56a40016)<br>

OR gate of drive strength 2 driving OA gate has more delay


![11](https://github.com/user-attachments/assets/4d749d2c-59ac-4524-ad53-df92ea2d8adc)<br>
**Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4**
```bash

# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

![12](https://github.com/user-attachments/assets/9588846a-47ce-44a0-8289-1e023e2f2b0a)
![13](https://github.com/user-attachments/assets/465304ba-12c7-4678-b92b-8eb9f87a8d48)<br>
**We see that the overall slack is reduced**<br>
## D4 SK3 Clock Tree Synthesis TritonCTS and signal integrity<br>
**Clock Tree routing and buffering Using H-tree algorithm**


![clock tree](https://github.com/user-attachments/assets/c30ea7b7-d33f-464e-a5d7-a8ef0e49413d)<br>
**Clock tree synthesis**:Let's connect clk1 to FF1 & FF2 of stage 1 and FF1 of stage 3 and FF2 of stage 4 with physical wire.Now let's see what is the problem with this? Let's consider some physical distance from clk to FF1 and FF2 , so due to this t2>t1.

Skew= t2-t1, and skew should be 0ps.Previously we have build bad tree now we will try to modify that in a smarter way. Hrre clk will come in somewhere mid points with this clk will reach to every flip flop at almost same time. In the same way we will connect the clk2 with flip flops like midpoint manner.Now will see clock tree synthesis(Buffering), Let's we have some clock route through which it has to reach to particular locations and clock end points and in the path many capacitance, resitors are there.<br>


![clock tree 1](https://github.com/user-attachments/assets/73ceea05-5fd3-4e9e-9e96-d7d33a6266fe)<br>
Because of the wire length we did not get the same wave form at ouput as input and bcz of RC networks , so to resolve this problem we use repeaters. The only difference between the repeaters we use for clock or for data path is that clock repeaters repeaters will have equal rise and fall time.

First step is we will remove the clock route and place 2 repeaters and allow the clock to go through this particular repeater, in this case whatever wave form is generated here will go to the output. So we can as many as repeaters we want to make the continuous flow of th clock till the output.

![clocktree2](https://github.com/user-attachments/assets/30c0ac94-fe64-4d64-9057-b3b158c5258d)<br>
#### Cross talk and Clock Net Shielding
**Clocknet shielding**:Is a technique used in digital integrated circuit (IC) design to minimize the effects of noise and crosstalk on the clock signal. The clock signal is one of the most critical signals in a chip, and its integrity is vital for the proper functioning of the circuit. Shielding helps ensure that the clock signal remains clean and consistent by reducing interference from neighboring signals.<br>
**Crosstalk**:Crosstalk refers to the unwanted interference caused by a signal in one circuit or wire influencing a signal in an adjacent circuit or wire. In the context of integrated circuits (ICs), crosstalk primarily occurs when a signal in one net induces noise in a neighboring net due to capacitive or inductive coupling.<br>

![cross talk](https://github.com/user-attachments/assets/850ab9af-eb9a-49a7-8369-d1b8a41c4793)

![cosstalk1](https://github.com/user-attachments/assets/e37e64d0-e734-4d17-a964-d0f04d9ba837)<br>
**Lab steps to run CTS using triton**<br>
**Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts**
```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-07_10-25/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls
```

![VirtualBox_vsdworkshop_08_08_2024_18_59_41](https://github.com/user-attachments/assets/3b97bf7f-15d8-410f-993e-8a29d85cbe30)<br>
Command to write verilog
```bash

# Check syntax
help write_verilog

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-07_10-25/results/synthesis/picorv32a.synthesis.v

# Exit from OpenSTA since timing analysis is done
exit
```

![VirtualBox_vsdworkshop_04_08_2024_16_28_17](https://github.com/user-attachments/assets/68bb08ec-2ef1-4bdf-9686-5e628d205caf)<br>
Verified that the netlist is overwritten by checking that instance``` _14506_``` is replaced with ```sky130_fd_sc_hd__or4_4```

![VirtualBox_vsdworkshop_04_08_2024_16_29_38-replacement successful](https://github.com/user-attachments/assets/a495367e-a364-451b-87ac-d97509b64d80)<br>
Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages
```bash
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 29-07_10-25 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```
![VirtualBox_vsdworkshop_04_08_2024_17_46_04](https://github.com/user-attachments/assets/b5932cd2-25a4-4d19-8159-da6fcc69db88)

![VirtualBox_vsdworkshop_04_08_2024_17_46_47](https://github.com/user-attachments/assets/533cf13c-a690-46c7-bfd7-ad6bbadbbfed)

![VirtualBox_vsdworkshop_04_08_2024_18_10_31](https://github.com/user-attachments/assets/e0875ad1-4e6b-4a08-85e8-9c082ce202cf)
![VirtualBox_vsdworkshop_04_08_2024_18_11_46](https://github.com/user-attachments/assets/e78b1b35-b6bf-42e4-a1bf-3bf154f97c22)
## D4 SK4 Timing analysis with real clocks using openSTA
**Setup analysis with real clock**


![setup with real](https://github.com/user-attachments/assets/8160aead-5e62-4151-8324-d643b67fd7c3)<br>
**Hold analysis with real clock**



![hold analysis](https://github.com/user-attachments/assets/07c222b4-64a0-4a0a-a9d7-051f8ee69977)
![hold real](https://github.com/user-attachments/assets/ebbc6d54-2f9d-4fb7-b5fc-2fc587572c88)<br>
**Post cts OPENROAD TIMING analyis**
```bash
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/29-07_10-25/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/29-07_10-25/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/29-07_10-25/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```


![VirtualBox_vsdworkshop_04_08_2024_19_51_05](https://github.com/user-attachments/assets/478def47-e87c-4087-ae99-35d71cd699fc)

![VirtualBox_vsdworkshop_04_08_2024_19_56_48](https://github.com/user-attachments/assets/8272d640-0f3c-43a0-a136-0cac50ce8c72)



![VirtualBox_vsdworkshop_04_08_2024_20_02_42](https://github.com/user-attachments/assets/e9366bdf-f754-4106-b532-e81d79bae1d3)


![VirtualBox_vsdworkshop_04_08_2024_20_03_41](https://github.com/user-attachments/assets/d2590de4-ffa5-4f0c-a8fb-e89f5c665e54)<br>
**Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'**
```bash
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/29-07_10-25/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/29-07_10-25/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/29-07_10-25/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/29-07_10-25/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```
![VirtualBox_vsdworkshop_04_08_2024_23_07_15](https://github.com/user-attachments/assets/52ca802f-3cb4-45fc-a8bb-0eaea80fbbd8)

![VirtualBox_vsdworkshop_04_08_2024_23_16_20](https://github.com/user-attachments/assets/420254f6-d525-4ce4-bdbd-645bba916eca)

![VirtualBox_vsdworkshop_04_08_2024_23_24_31](https://github.com/user-attachments/assets/fc0e229d-118f-4ea0-90d0-7a72792b3640)

![VirtualBox_vsdworkshop_04_08_2024_23_31_23](https://github.com/user-attachments/assets/fa078dc7-1722-4453-b6bb-7a6bb95b6134)

![VirtualBox_vsdworkshop_04_08_2024_23_34_00](https://github.com/user-attachments/assets/486ae600-2a7c-449d-aec4-fa53c0d192d8)


