# SoC_Design_and_planning
This repository contains the projects and work I completed during the VSD SoC Design and Planning workshop. It includes various aspects of SoC design, such as architecture, RTL design, physical design, DFT, power management, timing analysis, and project planning. These files showcase the skills and techniques I learned.
1) [Day 1-Inception of open-source EDA, OpenLANE and Sky130 PDK](#day-1-inception-of-open-source-eda-openlane-and-sky130-pdk)
2) [Day 2-Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells](#day-2-good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
3) [Day 3-Design library cell using Magic Layout and ngspice characterization](#day-3-design-library-cell-using-magic-layout-and-ngspice-characterization)
4) [Day 4-Pre-layout timing analysis and importance of good clock tree](#day-4-pre-layout-timing-analysis-and-importance-of-good-clock-tree)
5) [Day 5-Final steps for RTL2GDS using tritonRoute and openSTA](#day-5-final-steps-for-rtl2gds-using-tritonroute-and-opensta)

## Day 1-Inception of open-source EDA, OpenLANE and Sky130 PDK
![0](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/756cff7b-7d94-46e7-8389-91f9fd15abb8)

![1](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d7463b0-57cd-4c19-b5da-151a52451b33)

![2](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/c1b2d362-7424-4be8-8cbb-6326b838c369)

![3](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0a173205-a129-41f4-b19e-7bafe3132256)

![4](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/ee66ca0a-833c-4ac1-b97e-e1ce9fc418f8)

![5](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/e9e606fe-930b-4147-a4b9-28cab3f550c5)

![6](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/559bc670-6464-44f7-9810-4db332008a00)

![7](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/f4fe7711-e816-47da-9020-2ee0c5dc5605)


![8](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/0d22997d-726a-4f01-abe6-c5cb96e8f952)


![22](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/cb9d2ac0-62de-458a-a7dd-95d1cc6df1ab)

![23](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/770ed8d6-cc42-465f-89d2-978bdcda33d0)

The run directory is created in the picorv32a file after preparation. Within the folder, the current date is created. Because the synthetic was not run, the run folder is empty.
![23a](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/894143ea-2c48-48d6-ba2c-b93242fb572d)

![24](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/7c6b7ad6-b6d7-494f-9b79-023c6e263023)

![25](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/943ca798-8cb9-44fe-9eb8-060e87c1a599)

![27](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/114d5182-01be-44fd-81ed-4396a8e57bec)
Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

![28](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/01ce9f90-f8b7-4b44-a85f-4479d755ad1f)
```math
Chip\ Area\ for\ Module = 147712.918400 unit
```

## Day 2-Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells
## Day 3-Design library cell using Magic Layout and ngspice characterization
## Day 4-Pre-layout timing analysis and importance of good clock tree
## Day 5-Final steps for RTL2GDS using tritonRoute and openSTA

### new

`cd Desktop/work/tools`

#### old
