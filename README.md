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
### Define Width and Height of Core and Die
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
```math
  Total Area=(Number of Flip-Flops×Area of Each Flip-Flop)+(Number of AND Gates×Area of Each AND Gate)+(Number of OR Gates×Area of Each OR Gate)
```
```math
Total Area=(2×1 sq. unit)+(1×1 sq. unit)+(1×1 sq. unit)
```
```math
Total Area=2+1+1=4 sq. units
```
![32](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f90d020a-500d-4888-be5c-ec9464620987)

![33](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5e3e61f4-5852-42ec-a186-b8c964909526)


![34](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/10b02ad8-ee0d-49d9-84da-3413620bded6)

![35](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9717b790-f6ca-4d1a-bb0c-c0c9ba725ea1)

![36](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8980382e-5e48-4b4a-a114-95200cb92f78)

![37](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/46064baf-3bba-4161-bccd-a9c915d9e24a)

![38](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b248bc65-3f29-4eaf-9197-6a294224f8ef)

![39](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/be807d2a-cb70-412f-a31d-9ba15fa163bc)

![40](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/84ec243f-7a98-4831-b9a1-a6bf46c88758)

![41](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/00b20f77-b345-437a-854f-18e5cd4c21e8)

![42](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dcc0ae04-3765-4378-ba77-0952cf21d3b3)

![43](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/562d1671-62d6-482a-b3ed-7b98cc8d0959)

![44](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/5f6cae0a-1b46-4110-af2b-d8487968207b)

![45](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/349e52ca-5592-4105-bc45-99dff960fad1)

![46](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/4a5ebd30-a6e5-4271-b9f7-71c8912cbc3d)

![47](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1a46add3-bac1-4170-b916-199b6db93886)

![48](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/23f29ef8-7467-4b26-a579-8c7a3661c7a7)

![49](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/9861c48a-3397-4517-b77c-f9448502c859)

![50](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d04dab76-87a4-49cf-9f59-407e2e9d2e9e)

![51](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fb0a99e6-e5b7-4ded-9906-320d5d0da83f)

![52](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/d95e2479-7228-490a-bc8a-289c55c5875d)

![53](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6e1749f2-6dd2-4295-9b02-d7ca891fc71d)


![54](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/21e807fc-2503-4fdd-8c2e-f613bdc914e9)

![55](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/dea0d1e7-f865-4155-a3b6-f40238164708)



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


![58](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/51fed000-69ff-41bf-98f1-a8f4de3ccd8f)

![59](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/35d65ebf-1959-4fa2-9b7a-e2fd3ba33712)

![60](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/1d5424b1-f99c-4d3b-9a4a-228b85d69490)

![61](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/320367be-1666-48a5-89e6-9888343ca817)

![62](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b46080f9-7805-4c69-816a-6ac07207a524)

![63](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/205d1a70-da96-4aea-8bb8-3d6003611245)

![64](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/546ee348-1c3e-4507-b8e7-b70552288c9f)

![65](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/da4aa11d-cca3-4150-acb7-586c6219462f)

![66](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/68539627-8f88-4df2-8052-c3b94b5d5d55)

![67](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fceb1408-4219-4373-832d-c544d9e6e577)

![68](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/538d02d8-0ecb-4e34-8235-4d49a5e42edb)

![69](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/03b24ff7-4ddc-4996-b707-c6333dd3a275)

![70](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/85d7cfb0-83de-48a3-a749-c39e641f45cf)

![71](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/6f8a2d83-121c-444b-a136-82603b3d0c75)

![72](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/904a6acf-7cea-483e-88b4-ee106955f7c5)

![73](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/00c21afc-e901-43e8-aaf0-1246ee8fc4d8)

![74](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/92ac81f0-1048-4af1-a1ee-816c9ddf211a)

![75](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cf4d6357-96c7-419b-9b88-7e925211e8db)

![76](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0503f9e1-0509-447f-8310-45a6eec3d69c)

![77](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/2cccad14-3901-4f84-a86e-729a4d60a7ed)

![78](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/33ebce2e-52cb-4467-a391-eb05ae4e7964)

![79](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/bab11107-65d9-4bcb-bda4-f33d7f0d983e)

![80](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c4db52c8-e252-4e28-94c8-718b93b9171e)

![81](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fc6596cd-5e87-489f-9c3d-228165972aa7)

![82](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/92f7fcd0-9124-4869-a3f8-aac28c345fd2)

![83](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e331b3d3-335e-41fb-b793-98927312bcaf)

![84](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ddcf5431-f789-4e26-9441-c01a2394309c)

![85](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e8ac6337-9473-420d-9b79-d1afb3a6cfcb)

![86](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7b7c732a-e819-425b-b8b1-3918c907f79e)

![87](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/fdffcc49-8a7e-40f5-a8fc-9b9b260c23ba)







## Day 3-Design library cell using Magic Layout and ngspice characterization

![88](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/b0cb042d-44cb-4213-ad43-b918d603535b)

![89](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0c1d1b38-075d-4ad9-8ccc-1f5d111c5d9f)

![90](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/16472b9e-ad60-481c-9c04-3a9b0a769365)

![91](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/971b6fed-1324-4002-bd43-cc077127a693)

![92](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8a6730c7-1447-4a24-8cf8-c5ee26ae0e3b)

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


