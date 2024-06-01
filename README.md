# Contents covered in the Workshop:

# Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK
- How to talk to computers
- Introduction to QFN-48 Package, chip, pads, core, die and IPs
- Introduction to RISC-V
- From Software Applications to Hardware
- Soc design and OpenLANE
- Introduction to all components of open-source digital asic design
- Simplified RTL2GDS flow
- Introduction to OpenLANE and Strive chipsets
- Introduction to OpenLANE detailed ASIC design flow
- Get familiar to open-source EDA tools
- OpenLANE Directory structure in detail
- Design Preparation Step
- Review files after design prep and run synthesis
- OpenLANE Project Git Link Description
- Steps to characterize synthesis results
# Day 2 - Good floor planning considerations
- Chip Floor planning consideration
- Utilization factor and aspect ratio
- Concept of pre-placed cells
- De-coupling capacitors
- Power planning
- Pin placement and logical cell placement blockage
- Steps to run floorplan using OpenLANE
- Review floorplan files and steps to view floorplan/a>
- Review floorplan layout in Magic
- Library building and Placement
- Netlist binding and initial place design
- Optimize placement using estimated wire-length and capacitance
- Final placement optimization
- Need for libraries and characterization
- Congestion aware placement using RePlAce
- Cell design and characterization flows
- Inputs for cell design flow
- Circuit design steps
- Layout design step
- Typical characterization flow
- General timing characterization parameters
- Timing threshold definitions
- Propagation delay and transition time
# Day 3 - Design library cell using Magic Layout and ngspice characterization
- Labs for CMOS inverter ngspice simulations
- IO placer revision
- SPICE deck creation for CMOS inverter
- SPICE simulation lab for CMOS inverter
- Switching Threshold Vm
- Static and dynamic simulation of CMOS inverter
- Lab steps to git clone vsdstdcelldesign
- Inception of layout ̂A CMOS faabrication process
- Create Active regions
- Formation of N-well and P-well
- Formation of gate terminal
- Lightly doped drain (LDD) formation
- Source Ã�Â� drain formation
- Local interconnect formation
- Higher level metal formation
- Lab introduction to Sky130 basic layers layout and LEF using inverter
- Lab steps to create std cell layout and extract spice netlist
- Sky130 Tech File Labs
- Lab steps to create final SPICE deck using Sky130 tech
- Lab steps to characterize inverter using sky130 model files
- Lab introduction to Magic tool options and DRC rules
- Lab introduction to Sky130 pdk's and steps to download labs
- Lab introduction to Magic and steps to load Sky130 tech-rules
- Lab exercise to fix poly.9 error in Sky130 tech-file
- Lab exercise to implement poly resistor spacing to diff and tap
- Lab challenge exercise to describe DRC error as geometrical construct
- Lab challenge to find missing or incorrect rules and fix them
# Day 4 - Pre-layout timing analysis and importance of good clock tree
- Timing modeling using delay tables
- Lab steps to convert grid info to track info
- Lab steps to convert magic layout to std cell LEF
- Introduction to timing libs and steps to include new cell in synthesis
- Introduction to delay tables
- Delay table usage Part 1
- Delay table usage Part 2
- Lab steps to configure synthesis settings to fix slack and include vsdinv
- Timing analysis with ideal clocks using openSTA
- Setup timing analysis and introduction to flip-flop setup time
- Introduction to clock jitter and uncertainty
- Lab steps to configure OpenSTA for post-synth timing analysis
- Lab steps to optimize synthesis to reduce setup violations
- Lab steps to do basic timing ECO
- Clock tree synthesis TritonCTS and signal integrity
- Clock tree routing and buffering using H-Tree algorithm
- Crosstalk and clock net shielding
- Lab steps to run CTS using TritonCTS
- Lab steps to verify CTS runs
- Timing analysis with real clock using openSTA
- Setup timing analysis using real clocks
- Hold timing analysis using real clocks
- Lab steps to analyze timing with real clocks using OpenSTA
- Lab steps to execute OpenSTA with right timing libraries and CTS assignment
- Lab steps to observe impact of bigger CTS buffers on setup and hold timing
# Day 5 -Final step for RTL2GDS using tritinRoute and openSTA
- Routing and design rule check (DRC)
- Introduction to Maze Routing Ã�Â� LeeÃ�Â�s algorithm
- LeeÃ�Â�s Algorithm conclusion
- Design Rule Check
- Power Distribution Network and routing
- Lab steps to build power distribution network
- Lab steps from power straps to std cell power
- Basics of global and detail routing and configure TritonRoute
- TritonRoute Features
- TritonRoute feature 1 - Honors pre-processed route guides
- TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing
- TritonRoute method to handle connectivity
- Routing topology algorithm and final files list post-route

# Introduction to Openlane flow
-OpenLANE is a completely automated RTL to GDSII flow which embeds in it different opensource tools, namely, OpenROAD, Yosys, ABC, Magic etc., apart from many custom methodology scripts for design exploration and optimization. Openlane is built around Skywater 130nm process node and is capable of performing full ASIC implementation steps from RTL all the way down to GDSII. The flow-chart below gives a better picture of openlane flow as a whole (Image Courtesy: efabless/openlane)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/3bd62a5f-a480-401a-b15a-66ffee4394ee)

# Overview of Physical Design flow
Place and Route (PnR) is the core of any ASIC implementation and Openlane flow integrates into it several key open source tools which perform each of the respective stages of PnR. Below are the stages and the respective tools (in ( )) that are called by openlane for the functionalities as described:

- Synthesis
  - Generating gate-level netlist (yosys).
  - Performing cell mapping (abc).
  - Performing pre-layout STA (OpenSTA).
- Floorplanning
  - Defining the core area for the macro as well as the cell sites and the tracks (init_fp).
  - Placing the macro input and output ports (ioplacer).
  - Generating the power distribution network (pdn).
- Placement
  - Performing global placement (RePLace).
  - Perfroming detailed placement to legalize the globally placed components (OpenDP).
- Clock Tree Synthesis (CTS)
  - Synthesizing the clock tree (TritonCTS).
- Routing
  - Performing global routing to generate a guide file for the detailed router (FastRoute).
  - Performing detailed routing (TritonRoute)
- GDSII Generation
  - Streaming out the final GDSII layout file from the routed def (Magic).

# Lab reports from Day 1
- Design preparation and initiate Openlane
![Screenshot from 2024-05-27 11-22-45](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/2a09579c-da4a-454e-ba36-687e6205442d)
![Screenshot from 2024-05-27 11-36-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7791eab0-3070-40b1-80ec-0db1f6b58c3b)

- Design Specifications of picorv32a
![Screenshot from 2024-05-27 11-36-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/0f80d2a1-a80c-4da5-acc3-2f3ed194675f)

- Run synthesis
![Screenshot from 2024-05-27 11-49-54](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/08d5d42a-02c9-4cd9-a59e-eb339d7b5183)
![Screenshot from 2024-05-27 11-33-36](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4244c9f4-b5f7-41de-998c-1e42c92ffa92)

- STA report
![Screenshot from 2024-05-27 12-07-34](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/29f78cc5-e4b1-42df-904a-f74f4394cb04)
![Screenshot from 2024-05-27 12-07-23](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ed05b8ab-e73c-4d19-a53f-ca832e285dfb)


- Characterise synthesis results
![Screenshot from 2024-05-27 11-56-56](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/0254fda9-1161-483b-b871-a1cb52046215)
![Screenshot from 2024-05-27 12-00-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d026cd35-784e-4ff1-b87d-cdc85df364bf)
![Screenshot from 2024-05-27 11-56-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ccba3fff-cb04-420a-aeac-45d718eb45ef)

- We know, Flop ratio = Number of counter D-FF / Number of total cells
- Flop ratio = 1613 / 14876 = 0.1084
- Flop ratio % = 10.84
  
# Lab reports from Day 2
- Review floorplan files
![Screenshot from 2024-05-27 23-46-56](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c59fdb93-0cbf-44ae-b896-826f561cd3b9)
![Screenshot from 2024-05-28 13-08-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a95f2778-7c55-47e3-ae64-cdcf1180dbe0)
![Screenshot from 2024-05-28 13-04-43](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4e482775-64fe-428e-9ada-8f0679f00c54)
![Screenshot from 2024-05-27 23-17-42](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/66901b96-a237-4945-ab9e-e30147dd83cc)
![Screenshot from 2024-05-28 13-09-01](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/36676065-7ffb-4279-9401-9ffcb3c7fa6a)
- From the picorv32a.def file, it is seen that width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer. 

- Floorplan layout in Magic
![Screenshot from 2024-05-27 23-25-50](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/478e02bd-eb6b-481e-bf59-8aae5e312942)
![Screenshot from 2024-05-27 23-49-19](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/0abb122a-b883-4b4c-8740-54ddbb8c0b89)
![Screenshot from 2024-05-27 23-48-03](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b0fa5dd1-6ed3-44b4-aea4-0510cf11bcc4)

- Congestion aware placement using RePlAce
![Screenshot from 2024-05-28 12-56-13](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/623ebb9c-5e23-4e63-967a-989ce691f96a)
![Screenshot from 2024-05-28 12-56-56](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7c0f8e9f-fe9b-49dc-b81b-25086fe7a8f0)
![Screenshot from 2024-05-28 12-57-09](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/72a4c600-d204-4e1d-a126-edca3311a777)
  

