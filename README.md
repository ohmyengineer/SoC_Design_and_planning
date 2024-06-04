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

The run directory is created in the picorv32a file after preparation. Within the directory, the current date is created. Because the sythesis was not run, the run folder is empty.
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
![29](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/55a63d32-ba1d-4fa5-afba-57585c3ce2a8)

![30](https://github.com/ohmyengineer/SoC_Design_and_planning/assets/91957013/8b42c546-aabb-4547-8f43-fdda11703c9c)

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






## Day 3-Design library cell using Magic Layout and ngspice characterization


## Day 4-Pre-layout timing analysis and importance of good clock tree


## Day 5-Final steps for RTL2GDS using tritonRoute and openSTA


### new

`cd Desktop/work/tools`

#### old
