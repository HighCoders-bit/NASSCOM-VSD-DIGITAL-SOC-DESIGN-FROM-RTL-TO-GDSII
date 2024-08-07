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
