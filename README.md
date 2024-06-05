# SoC_Design_and_planning
This repository contains the projects and work I completed during the VSD SoC Design and Planning workshop. It includes various aspects of SoC design, such as architecture, RTL design, physical design, DFT, power management, timing analysis, and project planning. These files showcase the skills and techniques I learned.
1) [Day 1-Inception of open-source EDA, OpenLANE and Sky130 PDK](#day-1-inception-of-open-source-eda-openlane-and-sky130-pdk)
2) [Day 2-Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells](#day-2-good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
3) [Day 3-Design library cell using Magic Layout and ngspice characterization](#day-3-design-library-cell-using-magic-layout-and-ngspice-characterization)
4) [Day 4-Pre-layout timing analysis and importance of good clock tree](#day-4-pre-layout-timing-analysis-and-importance-of-good-clock-tree)
5) [Day 5-Final steps for RTL2GDS using tritonRoute and openSTA](#day-5-final-steps-for-rtl2gds-using-tritonroute-and-opensta)

## Day 1-Inception of open-source EDA, OpenLANE and Sky130 PDK
![0](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/756cff7b-7d94-46e7-8389-91f9fd15abb8)
## Introduction to QFN-48 Package, chip, pads, core, die and IPs
![1](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d7463b0-57cd-4c19-b5da-151a52451b33)
- **Die:** it denotes the dimensions of the complete chip located at the corner.
- **Core:** This area is designated for placing the logic gates. It includes all the combinational circuits, soft and hard IPs, and nets.
- **Pads:** This area is utilized for transmitting signals from inside the chip to the outside, or vice versa.
- **IPs:** Foundry IPs necessitate manual design or human intervention for their definition and creation, including SRAM, ADC, DAC, and PLLs.
- **PDK:** PDKs act as a bridge between foundries and design engineers. They encompass a collection of files that simulate the fabrication process for the design tools employed in IC design, encompassing device models, DRC, LVS, physical extraction, layers, LEF, standard cell libraries, timing libraries, etc. In this workshop, the SkyWater 130nm PDK, particularly sky130_fd_sc_hd, is utilized, and openLANE is constructed around this PDK.



![2](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c1b2d362-7424-4be8-8cbb-6326b838c369)


![3](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0a173205-a129-41f4-b19e-7bafe3132256)
### RISC V
RISC-V is a computer language used for communication with the computer. The name abbreviation indicates that "five" refers to the number of generations of RISC architecture developed at the University of California, Berkeley. The chip is positioned in the center, as depicted in the figure, and is connected to all other components via wiring, as illustrated below.
![4](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ee66ca0a-833c-4ac1-b97e-e1ce9fc418f8)

![5](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e9e606fe-930b-4147-a4b9-28cab3f550c5)
Example of a RISC-V SoC: It includes elements such as SRAM, SoC, ADC, DAC, PLL, and SPI. The components PLL, SRAM, ADC, and DAC are referred to as foundry IPs.

![6](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/559bc670-6464-44f7-9810-4db332008a00)

![7](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f4fe7711-e816-47da-9020-2ee0c5dc5605)

### Software Application to Hardware Execution:
Upon opening an application, the process unfolds across three distinct stages: Application Software, System Software, and Hardware chip. Initially, the user's interaction triggers the execution of the application. As the application code delves into the System Software layer, a series of sophisticated operations commence. Here, the code undergoes a pivotal transformation, transitioning from its human-readable form into machine language, specifically binary instructions. This intricate conversion process is essential, as it ensures compatibility with the underlying Hardware chip. As the converted binary instructions are relayed to the Hardware chip, a cascade of intricate operations ensues. The Hardware chip interprets these instructions, orchestrating a symphony of electronic signals and computations to execute the desired functionalities encapsulated within the application. This seamless interaction between software and hardware culminates in the seamless presentation of the application's features to the user, embodying the synergy between technology's abstract and tangible realms.
![8](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d22997d-726a-4f01-abe6-c5cb96e8f952)
Within the system software, three layers are present:
- **Operating System (OS):**
(1) Manages overall system operation.
(2) Handles input/output (IO) operations, memory allocation, and low-level system functions.
- **Compiler:**
(1)Translates high-level programming languages (e.g., C, C++, Java) into machine-readable instructions.
(2)Generates instructions based on hardware architecture.
- **Assembler:**
(1)Converts compiler-generated instructions into machine-executable binary code.
(2)Translates assembly language into binary representations understood by hardware.

Together, these layers enable software execution on computer systems by managing resources, translating code, and facilitating communication with hardware.

Steps to start the OpenLANE process and carry out synthesis:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```
```tcl
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
![22](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cb9d2ac0-62de-458a-a7dd-95d1cc6df1ab)

![23](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/770ed8d6-cc42-465f-89d2-978bdcda33d0)

The runs directory is created in the picorv32a file after preparation. Within the directory, the current date is created. Because the sythesis was not run, the run folder is empty.
![23a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/894143ea-2c48-48d6-ba2c-b93242fb572d)

![24](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7c6b7ad6-b6d7-494f-9b79-023c6e263023)

![25](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/943ca798-8cb9-44fe-9eb8-060e87c1a599)

![27](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/114d5182-01be-44fd-81ed-4396a8e57bec)
Calculation of Flop Ratio and DFF % from synthesis statistics report file
```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```
```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

![28](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/01ce9f90-f8b7-4b44-a85f-4479d755ad1f)
```math
Chip\ Area\ for\ Module = 147712.918400 sq. unit
```

## Day 2-Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells
### Define Width and Height of Core and Die:
![29](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/55a63d32-ba1d-4fa5-afba-57585c3ce2a8)
Consider two flip-flops: a launch flop and a capture flop, with simple combinational logic between them. A netlist outlines the connections among all components in an electronic design. Here, we depend on the sizes of the logic gates (AND & OR) and the specific flip-flops used.
![30](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8b42c546-aabb-4547-8f43-fdda11703c9c)
To convert the symbols into physical dimensions and calculate the area occupied by the netlist on a silicon wafer, we'll consider the following:
- Standard Cell Dimensions: Each standard cell has dimensions of 1 unit x 1 unit, resulting in an area of 1 square unit.
- Flip-Flop Dimensions: Each flip-flop also has an area of 1 square unit.
Now, let's assume the netlist includes:
- 2 flip-flops (launch and capture).
Combinational logic gates (AND, OR) in between.
- For simplicity, let's assume:
- There are 1 AND gates and 1 OR gates in the combinational logic.
Components and Their Areas:
- Flip-Flops: 2 (launch and capture), each with an area of 1 square unit.
- AND Gate: 1, with an area of 1 square unit.
- OR Gate: 1, with an area of 1 square unit.
```math
  Total\ Area= (Number\  of\ FFs ×Area\ of\ Each\ FF)+(Number\ of\ AND\ Gates×Area\ of\ Each\ AND\ Gate)+(Number\ of\ OR\ Gates×Area\ of\ Each\ OR\ Gate)
```
```math
Total \ Area=(2×1 sq. unit)+(1×1 sq. unit)+(1×1 sq. unit)
```
```math
Total \ Area=2+1+1=4 sq. units
```
![32](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f90d020a-500d-4888-be5c-ec9464620987)

![33](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5e3e61f4-5852-42ec-a186-b8c964909526)


![34](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/10b02ad8-ee0d-49d9-84da-3413620bded6)
Consider a silicon wafer where the logic circuits are implemented. The small square within the silicon wafer is known as the Die. Inside the Die, there is a section called the Core.
*Placement of Logic Inside the Core*
Now, let's place the specific logic inside the Core. Given that the netlist will occupy the entire area of the Core, it implies a 100% utilization of the Core. From this, we can calculate the utilization factor.
*Utilization Factor Calculation*
The utilization factor is defined as the ratio of the area occupied by the logic to the total area of the Core.
```math
Utilization\ Factor = \frac{Area\ Occupied\ by\ Logic}{Total\ Area\ of\ Core}
```

Given:
- The total area occupied by the netlist (logic) is 4 square units (as calculated earlier).
- Assume the Core's total area is exactly 4 square units to match the logic placement for 100% utilization.
*Utilization Factor*
```math

Utilization\ Factor = \frac{4 sq.\ units}{4 sq.\ units}
```
```math
Utilization\ Factor=1×100%=100%
```
Thus, the utilization factor is 100%, indicating that the logic completely occupies the Core area
*Aspect Ratio*
The aspect ratio is defined as the ratio of the width to the height of a rectangular area. 
Core is a square with each side being 2 units
```math
Aspect\ Ratio\ of\ Core = \frac{Width}{Height}
```
```math
Aspect\ Ratio\ of\ Core = \frac{2}{2} = 1
```
![35](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9717b790-f6ca-4d1a-bb0c-c0c9ba725ea1)

![36](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8980382e-5e48-4b4a-a114-95200cb92f78)

![37](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/46064baf-3bba-4161-bccd-a9c915d9e24a)

*Locations of Preplaced Cells*
Consider a large combinational logic circuit with 𝑁 logic gates performing a significant function. To manage its complexity, we divide the circuit into smaller segments. Specifically, we split the circuit into two parts, placing each into separate blocks, Block A and Block B. These blocks are then implemented independently.
- This approach allows for effective management of complexity, optimal performance, and better utilization of chip area by handling each block independently.


![38](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b248bc65-3f29-4eaf-9197-6a294224f8ef)
*Extending Input/Output Pins and Black Boxing :*
After dividing the circuit into Block A and Block B, we proceed with extending the input and output pins for each block. Then, we black box these blocks, making their internal details invisible to anyone looking at the main netlist. This process involves the following steps:


- *Extend Input/Output Pins:*
- Extend the input and output pins for both Block A and Block B to facilitate connections with other parts of the circuit.

  
- *Black Box the Blocks:*
- Encapsulate Block A and Block B as black boxes. This means the internal logic of each block is hidden, and only the input and output interfaces are visible.
- This abstraction makes the upper portion of each block invisible from the top-level view or to anyone examining the main netlist.

  
- *Separate into Different IPs or Modules:*
- Once black-boxed, Block A and Block B can be treated as independent Intellectual Property (IP) blocks or modules.
- These IPs can now be integrated separately into different designs or reused in other projects.

By extending the input and output pins, black boxing the blocks, and separating them into distinct IPs or modules, we achieve a modular design approach. This method simplifies the main netlist, enhances reusability, and allows for easier integration and management of complex circuits.
![39](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/be807d2a-cb70-412f-a31d-9ba15fa163bc)
One significant advantage of black boxing and using pre-placed cells is the ability to reuse these blocks multiple times after a single implementation. This approach simplifies the design process and ensures consistency across multiple projects. Besides the combinational logic blocks, other common IPs include memory, clock-gating cells, comparators, and multiplexers (MUX). These components are part of the top-level netlist, where they receive input signals, perform their designated functions, and deliver outputs. Notably, each IP's functionality is implemented only once, contributing to design efficiency.

The process of arranging these IPs on a chip is known as floorplanning. In this phase, IPs are given specific, user-defined locations on the chip. These designated positions ensure optimal performance and efficient use of space. Before automated placement and routing, these strategically positioned IPs are referred to as "pre-placed cells." By fixing their locations, we ensure that the placement and routing tools do not alter their positions, maintaining the integrity of the design.


![40](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/84ec243f-7a98-4831-b9a1-a6bf46c88758)
### De-coupling capacitors
To address the switching current demands of pre-placed cells, we incorporate decoupling capacitors into the circuit. Consider a scenario where a gate, such as an AND gate, transitions from Logic 0 to Logic 1 or vice versa. During this transition, the gate requires a certain amount of current, known as the peak current, to charge or discharge the capacitor representing the logic state.

The decoupling capacitor acts as a reservoir of charge, ensuring a stable and adequate supply of current during these transitions. When the gate switches from Logic 0 to Logic 1, the capacitor is charged from the supply voltage VSS. Conversely, when the gate switches from Logic 1 to Logic 0, the capacitor discharges, and the excess charge is collected by VSS.

However, due to the presence of resistance (Rdd) and inductance (Ldd) in the circuit, there will be a voltage drop across them during switching operations. As a result, the voltage at Node 'A' may deviate from the ideal supply voltage Vdd, denoted as Vdd'. This deviation can impact the performance and reliability of the circuit, underscoring the importance of carefully selecting decoupling capacitors and managing the parasitic effects of resistance and inductance.

The deviation in voltage, denoted as Vdd', from the ideal logic 1 voltage (1 volt) can pose a challenge, especially if it falls below a certain threshold. For instance, if Vdd' measures at 0.97 volts, it may fall within an undefined range between the voltage levels corresponding to logic 0 and logic 1. In digital circuits, voltage ranges are defined to distinguish between logic 0 and logic 1 states, ensuring reliable signal interpretation. Typically, any voltage below the input low voltage (Vil) threshold is considered logic 0, while voltages above the input high voltage (Vih) threshold are considered logic 1. The region between Vil and Vih is regarded as an undefined region, where the voltage levels may lead to ambiguous signal interpretation. Therefore, careful consideration of voltage thresholds and signal ranges is essential for ensuring the proper operation and reliability of digital circuits.
![41](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/00b20f77-b345-437a-854f-18e5cd4c21e8)

![42](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dcc0ae04-3765-4378-ba77-0952cf21d3b3)
To address the voltage drop issue and ensure stable operation of the circuit, a decoupling capacitor (Cd) is introduced in parallel with the circuit. This capacitor serves as a reservoir of charge, providing the necessary current to the circuit during switching operations. When the circuit switches, it draws current from Cd, mitigating the voltage drop across the RL network. The RL network, in turn, replenishes the charge in Cd to maintain its voltage level. Additionally, when Cd discharges, it takes charge from the power supply to recharge itself, ensuring a continuous and stable supply of current to the circuit. By effectively managing the charge and discharge cycles of the decoupling capacitor, the voltage drop issue can be mitigated, enhancing the reliability and performance of the circuit.
![43](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/562d1671-62d6-482a-b3ed-7b98cc8d0959)
Within the chip layout, the strategic placement of decoupling capacitors between Block A, Block B, and Block C ensures a stable and continuous power supply for each block. This arrangement effectively manages local communication within the blocks, mitigating voltage drops and ensuring reliable operation. By integrating decoupling capacitors in this manner, the overall performance and stability of the chip design are enhanced.
![44](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5f6cae0a-1b46-4110-af2b-d8487968207b)
### Power planning
Let's take a closer look at the local circuitry, treating it as a black box with repeatable logic at its boundaries. Thanks to the integration of decoupling capacitors, the issue of current demand has been effectively resolved. Now, as signals transition from logic 0 to logic 1 and propagate from the driver to the load, it's crucial to maintain signal integrity along specific driver-to-load lines. With the power supply now activated, ensuring reliable signal transmission across the 16-bit bus becomes paramount. However, due to physical constraints, decoupling capacitors cannot be placed directly at the bus. This presents a challenge, as the power supply and the bus are positioned at a distance, leading to an anticipated voltage drop between them.
![45](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/349e52ca-5592-4105-bc45-99dff960fad1)
Consider a specific 16-bit bus line where a logic 1 signal indicates that the capacitor is charging to Vdd, while a logic 0 signal indicates discharge to ground. Now, let's examine this bus line connected to an inverter. With the inverter's operation, the capacitors initially charged will discharge, and vice versa. This reversal happens as the inverter alters the logic level of the signals on the bus line, thereby changing the state of each capacitor accordingly.
![46](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/4a5ebd30-a6e5-4271-b9f7-71c8912cbc3d)
The issue arises because each capacitor is connected to a single ground point. When discharge occurs, the "ground" tap point becomes uneven, resulting in a phenomenon known as "ground bounce." This bounce may cause the voltage to enter an indeterminate state, transitioning between logic 1 and logic 0 if its magnitude exceeds the noise margin level. Consequently, unpredictability arises, leading to uncertain outcomes in the circuit's behavior.
![47](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1a46add3-bac1-4170-b916-199b6db93886)
Furthermore, with a single "Vdd" tap point, all capacitors previously at "0" volts need to be charged to "V" volts. This charging process causes a drop in voltage at the Vdd tap point. As long as this voltage drop remains within the noise margin threshold, the system operates normally. However, if the drop exceeds this threshold and enters an unknown region, the behavior of the circuit becomes unpredictable.
![48](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/23f29ef8-7467-4b26-a579-8c7a3661c7a7)

The observed phenomena, characterized by a drop in supply voltage, stems from the concentration of electricity at a single point. The solution to this issue lies in employing multiple power supplies. By doing so, each block can draw power from the nearest power source and discharge it to the nearest ground. This distribution of power and ground connections forms a mesh topology, ensuring more uniform and efficient power distribution throughout the circuit.
![49](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9861c48a-3397-4517-b77c-f9448502c859)
*The power planning for the top view is depicted below:*
![50](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d04dab76-87a4-49cf-9f59-407e2e9d2e9e)
## Pin placement 

Let's consider the following designs for implementation. The first circuit is driven by clk1, while the second circuit is driven by clk2. Both circuits have different inputs, Din1 and Din2 respectively, and outputs Dout1 and Dout2. Additionally, we have some preplaced cells, such as Block A, which receives inputs from Din1 and Din2, processes them, and provides an output to one of the inputs of the combinational gates. Another preplaced cell, Block B, receives inputs from clk1 and clk2 and generates a clk output. So, in total, we have 4 input ports: Din1, Din2, Clk1, and Clk2, and 3 output ports: Dout1, ClkOut, and Dout2. This setup serves as the circuit for explaining the concepts of placement and routing.

- Let's introduce another design that needs to be implemented. This section includes FF1 and FF2, highlighted in a different color (blue). FF1 is driven by Din3 and Clk1 as inputs, while the clock port of FF2 is clk2. Such circuits are particularly useful for understanding the timing analysis of inter-clock scenarios, where two flip-flops are driven by different clock inputs.

- Now, let's incorporate one more design, represented by FF1 and FF2 highlighted in a different color (green). In this configuration, FF1 is driven by Din4 and Clk2 as inputs, while the clock port of FF2 is clk1. This setup also helps in exploring timing analysis, specifically for inter-clock scenarios.

- Thus, in total, we now have 2 input ports: Din3 and Din4, and 3 output ports: Dout3, ClkOut, and Dout4. Additionally, we have some preplaced cells and Block C, which receives inputs from Din3 and Din4, processes them, and provides an output to one of the inputs of the combinational gates.
![51](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fb0a99e6-e5b7-4ded-9906-320d5d0da83f)
The completed design now consists of 6 input ports and 5 output ports. The connectivity information between the gates is encoded using VHDL/Verilog language and is referred to as the 'Netlist'. Below is a summary of the design:
*Input Ports:*
Din1, Din2, Clk1, Clk2, Din3 & Din4 
*Output Ports:*
Dout1, Dout2, Dout3, ClkOut, Dout4
The netlist describes how these input and output ports are connected to the various gates and flip-flops within the design, defining the interconnections and logic functionality of the entire circuit.

- Let's proceed with placing the netlist into the core design that we have previously created. We'll then fill the empty area between the core and the die with pin information. This process involves collaboration between the frontend team, responsible for determining the netlist connectivity, and the backend team, responsible for pin placements. Based on the pin placements, preplaced blocks should be located closer to the inputs of the preplaced blocks for optimal performance.

It's important to note that clock-in and clock-out pins are typically larger in size compared to data ports (input and output pins). This size difference is due to the critical nature of clock signals. Input clocks continuously provide signals to all elements of the chip, while output clocks need to propagate signals as quickly as possible. Therefore, larger-sized clock pins are preferred to minimize resistance and ensure efficient signal transmission.
![52](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d95e2479-7228-490a-bc8a-289c55c5875d)



Another critical consideration is the blocking of the pin placement area for routing and cell placements. Logical cell placement blockage is necessary to ensure that this area remains reserved exclusively for pin placement and is not occupied by routing or cell placement activities. This blockage is depicted in the floor plan image provided, delineating the space between the pins for exclusive pin placement purposes.

With these preparations completed, the floor plan is now ready for the Placement and Routing step of the design process. This step involves placing the logic cells and routing connections according to the established floor plan, ensuring efficient signal flow and optimal performance of the chip design.
![53](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6e1749f2-6dd2-4295-9b02-d7ca891fc71d)

*To initiate the OpenLANE flow and execute floorplan operations, utilize the following commands*

```bash

cd Desktop/work/tools/openlane_working_dir/openlane


docker
```
```tcl

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

run_synthesis

run_floorplan
```
![54](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/21e807fc-2503-4fdd-8c2e-f613bdc914e9)
The config.tcl file, located in the runs folder, contains all configurations necessary for the flow. It houses parameters and settings crucial for the execution of the workflow. By referring to this file, users can access a comprehensive list of acceptable arguments and their respective values within the current flow, enabling precise customization of the OpenLANE flow to achieve desired outcomes.

![55](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dea0d1e7-f865-4155-a3b6-f40238164708)

The floorplan.tcl file, situated within the runs folder, outlines the physical layout of the chip design. It specifies parameters like area allocation, power distribution, and pin placement constraints, guiding the optimization of chip layout for efficient routing and signal integrity.

![56](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a4616d7c-fe50-49f6-a3eb-ca2363dd9d29)

![57](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8ebc0d58-782a-4726-a306-478742aaf0e1)
According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

*To load the floorplan definition in Magic from another terminal, execute the following commands.*

```bash

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![58](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/51fed000-69ff-41bf-98f1-a8f4de3ccd8f)

![59](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/35d65ebf-1959-4fa2-9b7a-e2fd3ba33712)

![60](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1d5424b1-f99c-4d3b-9a4a-228b85d69490)

![61](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/320367be-1666-48a5-89e6-9888343ca817)

### Netlist binding and initial place design:

Associate the netlist with physical cells: Let's examine the netlist comprising gates, noting that each gate's shape reflects its function. For instance, consider the gate represented by a rectangular box rather than a triangular shape. Flip-flops are depicted as square boxes, resembling the AND gate, which also appears as a box. Thus, we've assigned physical dimensions to all flip-flops and gates. Since certain shapes like AND and OR gates don't exist physically, we'll designate specific shapes and measurements for each netlist component. Additionally, all blocks will be assigned appropriate width, height, and shape attributes.
![62](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b46080f9-7805-4c69-816a-6ac07207a524)
We'll proceed by removing the wires from the design. Within the Library, all the gates, flip-flops, and blocks are stored for reference. This Library serves as a repository of these components, allowing easy access and reuse during the design process. By organizing these elements in the Library, designers can efficiently manage the design components and streamline the implementation process.

![63](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/205d1a70-da96-4aea-8bb8-3d6003611245)
The library is akin to a collection of books, housing gates and flip-flops. It contains timing information and is subdivided into shape and delay sub-libraries. Each component exists in multiple flavors, offering different sizes and configurations. Designers select components based on timing requirements and floorplan space availability for optimal chip design.
![64](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/546ee348-1c3e-4507-b8e7-b70552288c9f)
*Placement:* Placement is a critical step in chip design, involving the strategic positioning of gates and flip-flops on the floorplan in accordance with their specified shapes and sizes. The floorplan, complete with input and output ports and dimensions assigned to each gate, serves as the foundation for this process. Guided by the netlist, which provides crucial connection information, placement ensures that every component is physically positioned to establish the necessary connections. It's crucial that preplaced cells maintain their positions to prevent overlap and preserve logical connectivity. The netlist circuit is exclusively utilized for creating connections on the floorplan, ensuring that the physical layout aligns with the logical connections defined in the netlist. This meticulous arrangement enables seamless interaction between the circuit and its input/output ports, crucial for maintaining timing and minimizing delays. Any remaining components are arranged based on the floorplan blueprint, with optimization employed to address any distance discrepancies, ultimately striving for an optimal layout conducive to efficient circuit operation.
![65](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/da4aa11d-cca3-4150-acb7-586c6219462f)
*Optimize placement:*
In optimizing placement, the issue of distancing is addressed, as exemplified by the distance between FF1 and Din2. Before proceeding to routing or wiring, capacitances are estimated to gauge signal integrity. The capacitance from Din2 to FF1 can be significant due to the lengthy wire, resulting in high resistance. This lengthy distance poses challenges for FF1 to receive the input signal effectively. To mitigate this, intermediate steps known as Repeaters are introduced. Repeaters act as buffers, reconditioning the original signal and generating a new signal that replicates the original, which is then forwarded. This process continues until reaching the target cell, maintaining signal integrity throughout. While repeaters effectively resolve signal integrity issues, they result in increased area consumption within the floorplan, as more repeaters are added.
- In Stage 1, the signal transmission does not necessitate the use of repeaters due to the manageable distances involved. However, in Stage 2, the increased distance leads to longer wire lengths, causing signal degradation beyond a certain range. Consequently, repeaters are essential to boost and maintain signal integrity over these extended distances.
- Similar to Stage 2, in Stage 3, a buffer is necessary between gate2 and FF2 to ensure signal integrity. This buffer helps to maintain the signal's strength and integrity over the distance between the two components, ensuring reliable communication between them.
- Stage 4 presents a heightened challenge compared to previous stages. Now, the imperative is to verify the correctness of our actions. This involves conducting timing analysis, considering the optimal clocks. By scrutinizing the analysis results, we can ascertain the suitability of the placement. This meticulous examination is crucial for ensuring that the design meets performance requirements and operates as intended.

![66](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/68539627-8f88-4df2-8052-c3b94b5d5d55)

*Command to run placement:*

```tcl
run_placement
```

![67](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fceb1408-4219-4373-832d-c544d9e6e577)
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![68](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/538d02d8-0ecb-4e34-8235-4d49a5e42edb)
*Standard cells are placed in accordance with legal standards to ensure compliance with design regulations and constraints:*
![69](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/03b24ff7-4ddc-4996-b707-c6333dd3a275)
## Inputs for cell design flow:

In the cell design flow, components like gates, flip-flops, and buffers are termed "standard cells." These are pre-defined units representing specific logic functions or storage elements in integrated circuit design. Standard cells are optimized for performance, power, and area, facilitating efficient design implementation.
![70](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/85d7cfb0-83de-48a3-a749-c39e641f45cf)

Standard cells, including gates, flip-flops, and buffers, are housed within a section known as the "Library" in the IC design flow. Similar to a traditional library storing various types of books, the IC design library contains different standard cells tailored for specific logic functions. Moreover, within the library, variations in cell sizes are categorized based on their drive strength. These varying sizes cater to different design requirements and performance considerations. Furthermore, the library encompasses cells with diverse functionalities, sizes, and threshold voltages, offering designers a range of options to optimize their designs.
![71](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6f8a2d83-121c-444b-a136-82603b3d0c75)
When delving into the design process of an inverter from the library, the cell design flow typically comprises three main segments: Inputs, Design Steps, and Outputs.

In the Inputs stage, specifications such as shape representation, drive strength, power characteristics, and other design parameters are defined. These inputs provide the foundation for the subsequent design steps.

The Design Steps phase involves the actual creation and refinement of the inverter. This includes tasks such as layout design, circuit simulation, optimization, and verification. Each step is meticulously executed to ensure the final design meets the specified requirements.

Finally, in the Outputs stage, the completed inverter design is generated. This includes the layout of the inverter, simulation results, timing analysis data, and any other relevant output information. These outputs serve as the deliverables of the cell design process, ready for integration into larger IC designs.
![72](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/904a6acf-7cea-483e-88b4-ee106955f7c5)
*Inputs:* Essential inputs for cell design include Process Design Kits (PDKs), DRC and LVS rules, SPICE models, libraries, and user-defined specifications. PDKs provide fabrication process details, while DRC and LVS rules ensure design compliance. SPICE models offer insight into transistor behavior, crucial for accurate circuit simulation. These inputs collectively guide the design process, enabling the creation of robust cell designs.
![73](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/00c21afc-e901-43e8-aaf0-1246ee8fc4d8)

![74](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/92ac81f0-1048-4af1-a1ee-816c9ddf211a)
### *Circuit design steps:* 
*Design Steps:* The design process unfolds in three main steps: circuit design, layout design, and characterization. Within circuit design, the process commences with implementing the desired function. This is followed by modeling the PMOS and NMOS transistors to conform to the library standards. Cell height is determined by the separation between the power and ground rails, while cell width is influenced by factors such as timing, drive strength, supply voltage, and metal layers. These parameters collectively guide the design specifications and inform subsequent design stages.
![75](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cf4d6357-96c7-419b-9b88-7e925211e8db)
*Euler path:* An Euler path is a sequence of edges in a graph that connects all the vertices, visiting each edge exactly once.
![76](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0503f9e1-0509-447f-8310-45a6eec3d69c)

![77](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2cccad14-3901-4f84-a86e-729a4d60a7ed)

![78](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/33ebce2e-52cb-4467-a391-eb05ae4e7964)
The subsequent stage involves transforming the stick diagram into a conventional layout, ensuring adherence to the appropriate design rules discussed earlier. Upon obtaining the finalized layout, various parameters such as cell length, width, pin placements, and drain current are determined. This process ensures that the layout meets the required specifications and design constraints, facilitating the accurate fabrication of the integrated circuit.
### *Layout Design:*
![79](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bab11107-65d9-4bcb-bda4-f33d7f0d983e)
The characterization flow begins by reading the model and the extracted SPICE netlist. Subsequently, the behavior of the buffer is defined or recognized, followed by the reading of the subcircuits of the inverter. Once these initial steps are completed, the required power supplies are connected, and the stimulus is applied to the circuit. Additionally, the output capacitance is provided to ensure accurate simulation results. Finally, the necessary simulation commands are issued, such as ".trans" for transient simulation or ".dc" for DC simulation, depending on the type of analysis being performed. This comprehensive approach ensures that the circuit is accurately characterized and validated for its intended functionality.
![80](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c4db52c8-e252-4e28-94c8-718b93b9171e)
The typical outputs obtained from circuit design include a Circuit Description Language (CDL) file, GDSII file, LEF file, and an extracted SPICE netlist (.cir).


### Timing threshold definitions: 
As seen in the previous section, a series of inverters are interconnected alongside power sources and stimulus inputs, forming the foundation for the concept of "timing threshold definitions." These definitions delineate critical threshold points within waveforms. In the provided figure, 'Slew_low_rise-thr' signifies a value proximal to zero, typically set at 20%, albeit sometimes at 30%. This parameter crucially impacts waveform transition characteristics, exerting a significant influence on overall circuit timing behavior.
![81](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fc6596cd-5e87-489f-9c3d-228165972aa7)

Now, by examining the waveform of the input stimulus, which serves as the input to the initial buffer, alongside the output of the first buffer, we can identify thresholds for delay analysis. Similar to slew thresholds, delay thresholds are determined by selecting specific rise and fall points from the waveforms. These thresholds typically correspond to approximately 50% of the signal's amplitude. By pinpointing these critical points, we gain insight into the delay characteristics of the circuit, facilitating comprehensive timing analysis and optimization.
![82](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/92f7fcd0-9124-4869-a3f8-aac28c345fd2)

![83](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e331b3d3-335e-41fb-b793-98927312bcaf)
### *Propagation delay and transition time:*
The values mentioned serve as pivotal references for computing parameters like propagation latency, current, and signal swings. Calculating delay involves subtracting the out_rise_thr from the in_rise_thr, typically set at 50%. This formula, Time delay = Time(out_thr) - Time(in_thr), provides a straightforward method to gauge the time delay between threshold points in the waveform. Such analysis offers crucial insights into circuit performance, aiding in optimization and troubleshooting efforts.
![84](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ddcf5431-f789-4e26-9441-c01a2394309c)
In the provided example, a consistent threshold of 50% was maintained for both in_rise_thr and out_fall_thr. However, negative delays are prohibited when the threshold point rises, and the output precedes the input. Thus, careful selection of the threshold point is imperative, as it directly influences the possibility of negative delays. This consideration underscores the importance of meticulous threshold determination to avoid such discrepancies in delay analysis
![85](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e8ac6337-9473-420d-9b79-d1afb3a6cfcb)
Transition time, a crucial parameter in waveform analysis, is determined by subtracting the time at the slew_high_rise_thr from the time at the slew_low_rise_thr, or alternatively, by subtracting the time at the slew_high_fall_thr from the time at the slew_low_fall_thr. These calculations enable us to quantify the duration of signal transitions within a waveform, providing essential insights into circuit behavior. Let's examine a waveform to illustrate the process of slew calculation.
![86](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7b7c732a-e819-425b-b8b1-3918c907f79e)
![87](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fdffcc49-8a7e-40f5-a8fc-9b9b260c23ba)







## Day 3-Design library cell using Magic Layout and ngspice characterization
### SPICE deck creation for CMOS inverter:
*VTC-SPICE simulations:* VTC-SPICE simulations commence with the generation of a SPICE deck, akin to a netlist, containing essential connectivity information. This deck includes specific points designated for output and input connections required for the simulation.

*Component connectivity:* Component connectivityplays a crucial role in this process, necessitating the provision of substrate pin connections. Adjustments to the threshold voltages of PMOS and NMOS components are facilitated through the substrate pin connection. This step ensures accurate modeling and simulation of component behavior within the circuit.

*Component values:* Component values, particularly those for PMOS and NMOS, are crucial considerations in VTC-SPICE simulations. Here, both PMOS and NMOS components are assigned identical sizes, ensuring uniformity in their characteristics and behaviors. By maintaining consistency in component sizes, accurate simulations can be conducted, facilitating comprehensive analysis of the circuit's performance and behavior across varying input conditions.

*Identify the nodes:* Identifying nodes is a fundamental aspect of circuit analysis, referring to the points between which components are connected. These nodes play a vital role in defining the netlist, providing essential connectivity information for the circuit simulation. By accurately identifying and labeling nodes, the netlist can effectively represent the circuit's topology, enabling comprehensive analysis and simulation of its behavior. Now we wiil name these nodes as Vin, Vss, Vdd, out.

*Let's proceed with drafting the SPICE deck following the format outlined below:*

*For the M1 MOSFET:*
- The drain is connected to the out node.
- The gate is connected to the in node.
- The PMOS transistor's substrate and source are linked to the Vdd node.

*For the M2 MOSFET:*
- The drain is connected to the out node.
- The gate is linked to the in node.
- The NMOS source and substrate are both connected to 0.
![88](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b0cb042d-44cb-4213-ad43-b918d603535b)
### SPICE simulation lab for CMOS inverter:
Having reviewed the CMOS inverter's connectivity thus far, we'll now explore the connections of other components, like the load capacitor and source. Let's delve into the connectivity of the output load capacitor. It's associated with both node 0 and out, with a capacitance value of 10ff. Similar to the supply voltage (Vdd), positioned between Vdd and node 0 with a value of 2.5, we have an input voltage (Vin) bridging Vin and node 0. Next, we proceed to input the simulation commands, where Vin is swept with a step size of 0.05 from 0 to 2.5, corresponding to our desire for Vout while modifying Vin. The final step entails incorporating the model files, which furnish comprehensive descriptions of the NMOS and PMOS components.
![89](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0c1d1b38-075d-4ad9-8ccc-1f5d111c5d9f)
Now, we will execute the SPICE simulation with the specified values and generate the corresponding graph.
![90](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/16472b9e-ad60-481c-9c04-3a9b0a769365)
### Switching Threshold Vm:
Each model, characterized by its unique width, fulfills a specific purpose. Despite varying voltage levels, both models exhibit the same waveform shape, showcasing the robustness of CMOS technology. Regardless of changes in NMOS or PMOS sizes, CMOS logic maintains consistency across all sizes, with production peaking when Vin is low and dipping when Vin is high. This uniform behavior underscores CMOS logic's widespread use in gate design. The switching threshold, denoted as Vm, plays a crucial role in determining the inverter's robustness. When Vin equals Vout, the switch occurs, marking the transition point between levels.
![91](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/971b6fed-1324-4002-bd43-cc077127a693)
The figure indicates that Vin equals Vout at approximately Vm~0.9v. This is a critical juncture for CMOS devices as both PMOS and NMOS transistors may be activated concurrently, posing a risk of current leakage (direct flow from power to ground). Comparing these two graphs aids in understanding the concept of switching threshold voltage. By examining the graph, we can discern the regions where the PMOS and NMOS transistors operate. Notably, the direction of current flow differs for NMOS and PMOS.
![92](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8a6730c7-1447-4a24-8cf8-c5ee26ae0e3b)
*Static and dynamic simulation of CMOS inverter:*
In our exploration of the CMOS inverter, we'll delve into its rise and fall delays, examining how they vary with Vm using dynamic simulation. Everything else in this simulation will remain consistent, except for the input, which will be a pulse, and the simulation command, which will be .trans. This will enable us to generate a Time vs. Voltage graph, facilitating the calculation of rise and fall delays.
![93](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/36310ebd-dd20-409e-874f-27f2cc8f589e)

![94](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7e2663a2-92e2-48ae-b25d-3851f745faf9)

![95](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1f5635f5-0858-428c-a805-893c1bed3999)

![96](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2169914f-fe9a-42a5-a2c0-86772eaa255d)

![97](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f32343e9-8701-4990-ab8f-033499ae0d38)

![98](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bb877696-9757-4215-a11d-1694dc4ee970)

![99](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/15b75693-5d87-47d5-9248-64b2b0626920)

![100](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/eba30bd5-475d-480f-b751-e5362186feb9)

![101](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e7a4bf80-1d21-4765-af63-2d0e993e0f59)

![102](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/455836f5-f50e-4543-b1d0-1cb6cc89aa56)


![103](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f7ed0926-c19b-4492-b9e8-3491fa2994b1)

![104](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/db4d6385-f187-4703-a7f1-4411735246c1)

![105](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9d9acb84-f11f-4b8d-ab2c-723603a49779)

![106](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dcf330c4-93cb-4b6d-ac5d-27a72ea2782f)

![107](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1766493b-e779-4585-a9ef-260538451bb0)

![108](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d4d2027e-80aa-45ec-bb58-fc015d40b455)

![109](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e64293ef-68c7-4ff6-b311-6d49cb0b66ec)

![110](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3c236f67-2404-4641-a91f-38b511c049c2)

![111](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5419fe24-3deb-4a0c-852d-a7a2c4ab2320)

![112](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f2bbf740-d564-4e34-8ebc-9f5261a1fa09)

![113](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2666187e-0a20-4d5a-8054-55ddc827f446)

![114](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/15e0e4f1-b685-4935-8309-6a7c1caba97f)

![115](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3e48d68d-d5ad-47d6-87d7-7d2125fc2547)

![116](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/074507d0-c8ab-428f-9226-c91a4711dbe0)

![117](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d277c2d5-98ce-4335-9f15-18dfc3466839)

![118](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0df2ba0c-43b5-4bf4-bda5-61e4b339fb46)

![119](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1e0f5de1-3771-4831-9a1b-f7d730a72c05)

![120](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/53316a16-9739-4fe2-b113-cec67aa76b4a)

![121](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/630099b8-8074-4aa1-bf3d-18e9fdcfed51)

![122](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b88a28e1-fd89-44c8-8a30-699f8bc9fb00)

![123](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/22641b98-486e-4b44-8104-e112828ced7b)

![124](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/24a615b2-e1d9-48d4-9187-82123f18831f)

![125](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/44bb4e0f-817d-4e74-bc73-54911fee50c2)

![126](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f2db9dd0-4421-4e9b-8401-22347f6d2397)

![127](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1ea9eb21-de6a-4930-a713-5364783669cf)

![128](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/35f01c5d-7e06-4d0b-b460-08a50f84774b)

![129](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dfd9da5d-c539-42b6-bf68-e6b73bf9fe60)

![130](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/442890db-2afd-4141-91a9-10a3773e25f5)

![131](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/90c138b5-ce3d-4b88-b4f3-7f58bbad3002)

![132](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3f3f2a4e-59e2-407a-9219-df855692c5ea)

![133](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d5b599bd-974c-49d6-8590-5c4f6e7d1491)

![134](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/66acc44f-ae3d-4fb0-bb28-9b1b3b8396a4)

![135](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/95231d64-ba9e-478b-bae1-4eb62e1d9cd3)

![136](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9ebe0e33-9af7-4998-9ff0-7c2b2eecba8e)

![137](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/929bb87c-5699-4ae1-819a-426cd748fa66)

![138](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3d35adb2-844b-40a7-b600-2c639a293895)

![139](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c1806688-1930-41d4-95b1-85d521f2a3f0)

![140](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/85b83ad0-ec49-4cf4-90ae-c5393b807dd9)

![141](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/33a3511f-cf20-43f0-9f64-1c72f0446fc1)

![142](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d662af90-750a-4327-abff-fe3028a30f80)

![143](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7dbba132-9658-4849-a7a5-8772ccdb6276)

![144](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/97f55d44-4450-4b7f-bd3c-8409b3c7088a)

![145](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d6bb7b28-dfb7-4ddd-8849-c962784780d9)

![146](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/21bd5682-c00c-4b30-8192-614cbac28956)

![147](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6c948ab8-3443-4b0a-9b1e-3a5a8d636b95)

![148](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3571f96e-574b-43d5-bca3-a9240b93ffd1)

![149](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bb227ffa-8e24-47e2-8f6d-0d41c60572e2)

![150](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/33e653c5-6ab4-4746-9539-c6966c915bb2)

![151](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/28c09e11-f566-4be6-ba34-da89f2b2ffe8)

![152](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6065db19-d7b6-4ffa-951d-3ed01a9f89bc)

![153](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c3476735-ed6e-4416-a71e-81dbd24d06ee)

![154](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6092c3a0-1541-4525-a96b-393d46fed15a)

![155](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/03d24991-9a09-4bec-9c77-b1bb3920609c)

![156](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/07ba14bc-9010-4d2d-a927-02670e4a55fa)

![157](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/14ecda51-4ec6-4cfe-839c-c0535c7cd0dc)

![158](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/84be91b1-ce55-4888-bfef-22fb82415217)
Maximum Vdd Value:
![max vdd value](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7f91c262-e719-4083-922a-f4587202d776)

Voltages at 20% and 80% of maximum voltage:
```math
20\%\ of\ output = 0.66\ V
```
```math
80\%\ of\ output = 2.64\ V
```
### Rise Time
20%
![20% vtc](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/babf7212-6e45-4bd9-b095-11badacdf06e)
![20% value](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e1cf6261-7b5b-4984-8e8a-c03943411f13)

80%
![80% vtc](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ddedcd74-9432-4222-b017-b3c611c0b76b)
![80% value](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/35ba19b6-07d1-450d-a157-80a62eb1d1f3)

### Fall Time
20%
![164](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/60fbe637-a539-44be-a958-96c76f452ef2)
![165](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/98aeeb13-1399-4114-8c18-4defcece8335)

80%
![166](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b235f006-4844-4794-981e-af13975c9188)
![167](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9b59854f-2bcd-4ca2-b658-eb14c0093889)


### Cell Rise delay
![168](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5f1987b6-f73d-48d6-a3d5-71dc5e2db910)
![169](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e18c2e0e-e56e-4cb8-9710-5669ce0a36cb)

### Cell Fall delay

![170](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/66a083d4-7587-4830-a515-0ea4b4e6247b)
![171](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f57c666f-f3dc-4436-a008-a2f8396e3b07)


![172](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/45768272-ab7e-47a4-99d5-2f6011d94ee0)
![173](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bbb829d0-f97f-439e-a8e5-7b8ebc2e2522)
![174](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/55ac2331-c031-4917-8c95-da61abedf4f5)
![175](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e56c7540-eeda-4503-967d-bc5523e95c0a)
![176](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/59056dae-e747-42a4-a776-dedccddc8228)
![177](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/613608c9-aefa-437b-8a9b-171d93602713)
![178](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9c4ef9a7-5106-40dd-905a-b0cd25269a03)
![179](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7e1d263a-2684-47d0-959d-52468e890a12)
![180](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/889591b2-197b-4c97-9943-ac6c18b990f6)
![181](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/03e1a25c-b945-4b3a-b22b-c9760953bc78)
![182](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/97d98166-621c-4c42-8258-4d79695677fa)
![183](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/46d5ebb8-74cc-49cb-9b18-8d1a04775403)
![184](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6eac334c-2106-4e36-acf8-d4e5250e8cdd)
![185](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/86306eae-5209-4fe4-b0b7-6b1560bc488d)

![186](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/072a12e9-b6a4-45b4-bf03-e9bf083d9b4d)
![187](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/24ddcec4-ce37-4071-a40e-0e793432a167)
![188](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cdd1e8cf-7a02-48c9-9ff0-fc026ebd350b)
![189](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bf1e0997-c90e-4828-b0eb-950d2471117a)
![190](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/16fbe121-e4f9-4832-9482-38ff78979fae)
![191](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f34d40f6-dc6c-4cd3-896b-3898f77e1332)
![192](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/10d68e72-5119-43a5-a8e3-4944b098ccd0)

## Day 4-Pre-layout timing analysis and importance of good clock tree

![193](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c2914292-f787-4eed-9b61-a9969aad4f60)
![194a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/03aaba6e-e8c6-417d-9c3c-cc6a05e606d6)
![194](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/33bd3aef-01d4-43f8-9c80-8fd1a2dbf318)


![195](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/108f737f-10be-4120-952b-f9ade09cd5e1)
![196](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/474fb9dc-7a8d-4dc5-b1c9-6d1e90995441)
![197](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/758c6a4e-768b-466b-990c-2b45974a19a5)
![198](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9bdeab41-5fe6-4438-a3f4-81206ff9734e)
![199](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ff3a1fb4-0c83-4604-9ef3-e9e3cf12873e)
![200](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2e6fde51-1fce-41de-97a0-f41e3e4da7c5)
![201](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2ab96628-fb23-46bc-b6e6-fb6864d66aff)

![202](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d7f689ac-fd13-4875-87c4-49cf00d931b3)
![203](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3a051aa0-bd86-48ac-b92a-2a8241394a45)
![204](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d6e056c9-4d01-4160-9f39-44ea2faaa140)
![205](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e916aa5d-896d-40d5-8c6b-3f27cef60fe1)
![206](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/795c4510-b20d-426f-a97f-8323cdc9e532)
![207](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d3d9e86a-adcb-4b35-97a1-ff5f8e43391b)
![208](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1070323e-5e22-4b6c-ba3e-ff76d429bb07)
![209](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/473e9189-a1f9-499f-b431-0b92d06d1b3d)
![210](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/22827b9b-fde8-483b-9f9c-15ba808b3b4c)
![211](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/448868e7-c4be-4896-a192-c4f2a719edcd)
![212](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3c35d575-119e-499a-9705-d6ec002daab0)
![213](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/76e3100c-2fdb-4334-b993-a0d634ff50bc)
![214](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/da912964-3cc5-4315-a745-c699b0ab4c54)

![215](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/01967145-34cf-413a-bdb4-b95995cdfb26)
![216](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0dbc57c8-c742-4bc5-9bc7-cae85f65e102)
![217](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d472c215-88a4-47eb-a535-d68c47081015)
![218](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/31927f20-9046-4453-8a88-ddaa098515eb)
![219](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9d9e15ae-7d75-4d37-8275-b4df1913fb83)
![220](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e4ad2400-7039-458b-b141-68c750b55c42)

![221a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/238e5752-92c5-45fd-b7d8-2f5e6895d77c)
![221](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2ad91ca3-df41-46af-93c0-b11e3ae104f9)
![222](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8f7661b4-f0af-4f39-979f-3e2716ec4edc)
![223](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5b0adcd1-811f-412f-a629-2c6840d87c6e)
![224](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e21377a8-2788-463c-bd9d-aecb1348e5b3)
![225](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/64702e87-5e95-433f-9394-a52ab46b4f46)
![226](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a711589d-bfac-489c-9b41-0f08df2a4f90)
![227](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cfea8f78-23cd-4e86-8e98-7701d8d890de)
![228](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d00923f3-5aec-4a0a-84ab-6586fc34ff25)


## Day 5-Final steps for RTL2GDS using tritonRoute and openSTA
![229](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a4955daf-e730-4651-b5f0-df224d6335a2)
![230](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/4c0fdd6a-7334-43b4-bfdb-1440d7223fd2)
![231](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/3d8769d8-d792-406e-9d6f-d24f2ca7f519)
![232](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/194b86de-cd66-4373-88ef-3654b2a5706b)
![233](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a2c593d3-2e88-4af8-8d37-4e3f430f7c9d)
![234](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a48d01ae-823b-4846-9e04-a780c233913c)
![235](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/039825bf-2f52-4923-b276-5c11103bf5b4)
![236](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/de987e85-65b8-450c-ad61-c9615361f231)
![237](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1a59b98a-45dc-473d-b6ab-8f584407e0eb)
![238a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/353ada51-67df-4763-a781-6c876cca5097)
![238](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6c0dbe84-3567-49e3-a6d4-5c4d7b515553)
![239](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/77e307c5-5e47-4da3-963d-ca8774dc8ce1)
![240](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cde6fdb9-40f0-4d48-bf5c-ee2fb228800e)
![241](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d493f55-8735-41b1-9752-6239aed3c36b)
![242](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/a24d230b-777d-475a-a5d6-f7a78a9d9e7b)
![242a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/db7f7e9a-d06d-4f80-b0d3-2241deac0a47)
![243](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/635d2ed4-cb8e-47a7-8b00-8d7ec60734e0)
![244](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/de39d893-be8d-4565-a523-071289b971ed)
![245](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d194eaf-4e57-4dbd-a632-bb99aadebea7)
![246](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e2a0d32f-46b4-408e-aa9c-4892863142b7)
![247](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8c058db9-5952-4dfb-9961-36e08a1ad986)
![248](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ab356d8e-87ea-4525-9042-2650c33b59e4)
![249](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/719bfa90-6681-4730-9689-7e992587b8b2)
![250](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fe2dbabe-0169-4b9c-9405-c52f56add230)
![251](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/300f0045-323f-4113-bf40-c47526757e4f)
![252](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/14c78ec9-a893-44cb-8391-d9772d71d950)


