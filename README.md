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
- Source and drain formation
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
- Introduction to Maze Routing and Lee's algorithm
- Lee's Algorithm conclusion
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


# Theory from day 1 : Inception of open-source EDA, OpenLANE and sky130 PDK

## Introduction to Openlane flow
-OpenLANE is a completely automated RTL to GDSII flow which embeds in it different opensource tools, namely, OpenROAD, Yosys, ABC, Magic etc., apart from many custom methodology scripts for design exploration and optimization. Openlane is built around Skywater 130nm process node and is capable of performing full ASIC implementation steps from RTL all the way down to GDSII. The flow-chart below gives a better picture of openlane flow as a whole (Image Courtesy: efabless/openlane)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/3bd62a5f-a480-401a-b15a-66ffee4394ee)

## Overview of Physical Design flow
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
    

## Get familiar to open-source EDA tools
  
Basic Linux Commands:

cd : opens the particular folder

ls : lists the content of the folder

pwd : shows the present working directory

mkdir : to make a new directory

command --help : shows the complete use that command

clear : clears the terminal screen

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a709df4f-230e-4ea0-8b96-87aeb42a3c43)

  
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

# Theory from Day 2 : Good floor planning considerations

## Utilization factor and aspect ratio

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5a859f99-e1b6-489b-824d-39fcc8938756)

-  Utilization Factor = Area occupied by netlist / Total area of the core
   
 - Let's put the dimensions we have, we get
 
 Utilization factor = 4*1sq.unit / 2unit *2unit = 1

- So, utilization factor = 1 (It means core has utilized all the area and no spane left)

- Aspect Ratio = Height / width = 2 unit / 2unit = 1

- Whenever Aspect Ratio is 1 it signifies that chip is square shaped. When it is not 1 it means the chip is in rectangular shape.

## De-coupling capacitors

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a08e7796-5ab4-4d5f-9025-686cf1e8d578)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e7e344a1-9394-4848-9114-42848649ca03)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/39c482f7-4797-40fa-b87b-fbf9d7fceba7)

## Power planning

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9c79bea2-3346-4600-9ae5-2cd5a24c1831)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ccf815f2-c72e-46d7-baff-d3115ccaa389)

## Pin placement and logical cell placement blockage

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b4546543-5def-4070-a2bc-d754f653cf39)

## Cell design flow and layout design

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d61d0089-4716-473c-90be-ac3f6b9fea34)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/81368482-4fc6-4aba-b2a8-80063674e6d9)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5b41482e-4553-4e81-9703-7dfb92a267de)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/53367975-5864-43bf-8056-8a12ddc6ac50)

## Characterization flow

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c940cd8d-444c-4eda-8c75-8f247345ffd3)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/dc9207c6-b04a-48c2-ae26-d398005e573b)

## Timing definitions

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/55ae5d3c-caa6-4bfa-a3b2-7f5d983e347a)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5fc8dfce-3c92-440c-a2f7-5bc234fd7c2d)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/229ece98-724d-42f1-af7c-b6e131057562)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/badfaadf-0bd7-48f9-892f-c42e9d13170b)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5c81d7d0-809c-4b2e-a509-7c6e1161b92b)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a8555b06-1f80-4ef3-ab1a-12e585752ed8)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f292bb26-6ee6-490d-abda-7fea68289630)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9e6b0f2a-ffb9-4ef6-9baa-fbc5908f7a9c)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7f8d0527-879b-43b8-8cdf-a163d45af6e4)

    
## Lab reports from Day 2

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


# Theory from Day 3 : Design library cell using Magic Layout and ngspice characterization

## SPICE deck creation for CMOS inverter

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4f6b953f-ff7b-4874-9cdc-5ccfa27294e2)

- Values for the PMOS and NMOS. We have taken the same size of both PMOS and NMOS.

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/71cb51cd-7960-4ed2-8283-6f91cb685298)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f9045f20-2785-4633-ae11-3a1d0a6929a6)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/22565bed-feca-4e5d-bfb4-1e7dcf32c28c)

## Inception of layout of CMOS faabrication process
![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c4cac354-2275-46f2-ba33-4f822235b05f)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7da34b24-0657-49e5-bd79-b01f79a26633)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/535fac0a-1a40-4225-ae21-65d85d9808d6)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/564f24e6-b8cf-43b3-aa0b-64374e4864ac)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d8bd1c70-d811-4e12-be3b-544a35e119b8)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/729e32e4-1169-4797-bcb7-7a1ff7cd285a)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/af2d0373-629a-4a50-ac63-da4c4658f5b8)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/690ecfbd-0deb-480f-b846-16c05866dc68)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/18e68777-6366-45d1-a5df-5442ba8a4dd1)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5daa9cc6-3513-4689-ab0c-1c8978634042)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c1526d6d-8bfb-4a1f-b1d5-e59c98913f49)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e2037431-454d-4bcd-b375-b764a9eebb49)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c3e6b754-0632-4a4c-bed6-2dfaf39bfba2)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/75cc080e-7731-4e64-8174-cd78451f9ae1)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/cd469f4c-4cb0-4859-aa5a-c4d380bf7e70)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/bd8f3bb3-fc3c-4709-bc15-739529444daf)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/22733ddd-9f4d-456e-bf14-0004bfbf37ad)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4640af3b-4174-48ce-871e-420ab5aeb2e1)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/05fed4f1-bc4a-4857-8ebf-d3e9617851fb)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e6a6da27-5c59-443a-afe1-97b0266ff7e2)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/962afe72-b48b-43c9-a48b-9e24cbb0cbce)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/637dd77c-be40-4cb7-bfb6-18a7dabc4841)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/548b4b1a-e1ad-4a0a-99ef-05880fb45eb0)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b4cc1339-0b10-44ae-ba55-ea26cfb7eac5)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f57fa59b-deb5-4e28-9062-4b06e61b1fb4)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/36a894c0-9a7b-4b20-95f4-5ebed1ad3e12)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a37e358e-2a28-4c34-9506-534cc902be78)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/bd2d92d4-af43-49a9-9e6e-e09c2ee30bab)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/77c68dbb-e5f0-4cfa-9efc-ead0fef296a9)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ab67ad90-21e1-4fde-b4e5-2fde58f32b65)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/133239b9-2ee1-4afd-a944-adde91910584)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/06a6c9f5-1e59-4509-adf7-2afb501f494b)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5a61b2bd-4553-4d91-8340-f8b8f78af913)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a17b012d-f7b5-4ecd-9371-62eaed058423)

  
# Lab reports from Day 3
- IO placer revision

![Screenshot from 2024-05-29 12-51-00](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c7375c51-2ddf-4e12-ae99-0885459a583d)

- Clone custom inverter standard cell design from github repository and load the custom inverter layout in magic

![Screenshot from 2024-05-30 20-49-17](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/04f3c746-b4b1-4875-83f2-9d87724e956e)

![Screenshot from 2024-05-30 21-03-12](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/0ce66388-c892-4ae1-888a-59bd250aa6a1)

- pshort.lib

![Screenshot from 2024-05-30 21-31-14](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7a738cad-6ddf-428b-81db-bf406ffb7bcf)
 
- Spice extraction of inverter in magic

![Screenshot from 2024-05-30 21-49-26](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/aaf736fe-d2f6-4919-9a52-87e34a50969d)

- ngspice simulation

![Screenshot from 2024-05-30 22-36-57](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c289787e-09f0-4541-91ef-7b95b5f81f9e)

![Screenshot from 2024-05-30 22-37-32](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/cba97ec5-8d7b-4b11-a5ae-395d65da6706)

- Characterize inverter using sky130 model files

![Screenshot from 2024-05-30 23-17-07 (1)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/cabd2728-892e-4a86-8b84-b9bda9fe9d30)

- Rise time
  (2.246 - 2.182)e-09 = 64psec
- Fall time
  (4.095 - 4.051)e-09 = 44psec
- Propagation delay
  (2.210 - 2.150)e-09 = 60psec
- Cell fall delay
  (4.077 - 4.050)e-09 = 27psec

- Content of .magicrc file 

![Screenshot from 2024-05-31 21-14-58 (1)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/46003628-2c24-42df-9846-e101c3d0f06c)

![Screenshot from 2024-05-31 21-15-58](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/166a53d6-4f22-4983-a124-baaa233c9b23)

- Lab introduction to Magic tool options and DRC rules

![Screenshot from 2024-05-31 21-18-52](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5522ac97-6959-47d9-bd76-2450af2bc100)

![Screenshot from 2024-05-31 21-20-05](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e01fae5f-672c-4567-9541-9d0d97a99a12)

![Screenshot from 2024-05-31 21-52-42](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/97fb507b-9269-47df-b7be-c72e99f75d91)

![Screenshot from 2024-05-31 21-50-41](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/1ef5bb28-5b41-4b23-8c34-7a9cfb5c9fef)

- Lab exercise to fix poly.9 error in Sky130 tech-file

![Screenshot from 2024-05-31 21-58-47](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/6e658e83-1f2f-4250-8fc3-70a6def6c516)

![Screenshot from 2024-05-31 22-26-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/73f81d1c-758f-48e0-84eb-f6140ec369df)

![Screenshot from 2024-05-31 22-27-39](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/fd8750e7-9a39-4b7f-8643-064f6b92d2be)

- Lab challenge exercise to describe DRC error as geometrical construct

![Screenshot from 2024-05-31 22-50-03](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/33b67270-2e52-43f4-954b-3e23f8408b6d)

![Screenshot from 2024-05-31 22-52-06](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ba095386-42e4-4c21-a3ce-d9f77fc37311)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7a65e767-b5bd-437f-96cf-5a0df4bd2267)

- Lab challenge to find missing or incorrect rules and fix them

![Screenshot from 2024-05-31 23-01-20](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9f47206e-ca91-4ad2-937d-853fed427a5c)


# Theory from Day 4 : Pre-layout timing analysis and importance of good clock tree

## Delay tables

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4bd479ba-f21b-46e0-8aff-056c556375ba)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/5acd9f78-e16d-4386-ac14-b5195de1a473)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c1bfbcbb-09c9-43b2-b066-6fcb767e72de)

- Assume c1=c2=c3=c4=25fF and Cbuf1=Cbuf2=30fF

Total Cap at node 'A'=> 60fF

Total Cap at node 'B'=> 50fF

Total Cap at node 'C'=> 50fF

- Example:

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/3391b8d0-999f-4b3c-9070-8b3cd4e6a771)

## Timing analysis using openSTA

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9d67dc66-3560-4bfc-801d-75ebc0c323aa)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/92d1cfaf-d2fe-4adc-8a5b-62cca0f6a22d)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/47da6ba6-3ba7-4b77-afe0-5605cb877593)

## Clock tree routing

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e6ac2afb-5390-4f5e-a89d-f1caf14b8fde)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/89b79dd5-23f8-4843-a6a7-2665304b25a9)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/101156a5-3e30-423a-aec0-9db15eaebda3)

## Crosstalk and Clock net shielding

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/153741ff-d438-4153-8fdb-a2c41e7806f8)

## Setup and Hold timing analysis

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/99745eb5-7fb9-432f-9a20-dac42f65daef)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/db39e623-dde6-43cc-9dcd-798e4db6ebc2)

- Slack= Data arrival time - data required time.
- Slack should either be positive or 0. If slack goes to negative it is referred to as violation.

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ae9a25f4-a9c1-48a8-a3d1-d59a20ea54f9)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/922b71c6-4330-449c-9138-afcf88bd8ff4)

   
# Lab reports from Day 4

- Lab steps to convert grid info to track info

![Screenshot from 2024-06-01 12-02-57](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/50e30f5c-76ff-42c6-a1fd-18e824eb48ac)

![Screenshot from 2024-06-01 12-10-27](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ee6c97ec-419c-4a02-a14d-70e702418562)

![Screenshot from 2024-06-01 12-14-53](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9823df8d-4ff8-4afd-92e9-ec8a1817c282)

- Lab steps to convert magic layout to standard cell LEF

![Screenshot from 2024-06-01 12-20-18](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/7835700b-c117-459a-b085-03e138654911)

![Screenshot from 2024-06-01 12-24-20](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/8f4aa1ee-6567-4bbd-80da-c92d14373c26)

- Introduction to timing libs and steps to include new cell in synthesis

![Screenshot from 2024-06-01 12-29-43](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d762f8e0-7f50-431d-aa31-d6e5f4265774)

![Screenshot from 2024-06-01 12-29-46](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/eaf334ba-e193-4a0b-83b3-dadb1d2ae92a)

- sky130_vsdinv.lef

![Screenshot from 2024-06-01 12-24-54](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ae14fb32-d37c-4aee-800a-5f0f4caca752)

- Different library files

![Screenshot from 2024-06-01 12-32-45](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c7b0a99a-c3e2-41ea-a9d6-b0b1b0cebe75)

![Screenshot from 2024-06-01 12-35-03](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/64368cfd-b05f-4be7-8a1a-c3ef4fcd279a)

![Screenshot from 2024-06-01 12-35-16](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/05490d6d-83b1-4336-b35b-f55e1dbe697b)

- config.tcl file 

![Screenshot 2024-06-04 200637](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/070442ae-b6fe-484a-b17a-25c17641cef6)


- OPENLANE execution
- Commands:

  ./flow.tcl -interactive

  package require openlane 0.9

  prep -design picorv32a

  set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      

  add_lefs -src $lefs

  run_synthesis

![Screenshot from 2024-06-01 12-47-47](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a4d373bc-f107-43de-90a1-39d79f1fe432)

![Screenshot from 2024-06-01 12-49-15](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b849cd23-b5bd-476f-8179-fe3a5066531a)

- README.md file

![Screenshot from 2024-06-01 13-22-17](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9ff9fa35-28a1-48db-8cb7-b5effc6a568e)

- Re-synthesis for reduced slack

![Screenshot from 2024-06-01 13-31-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/000204d8-c04b-47f8-97c8-3146b0afe303)

![Screenshot from 2024-06-01 13-54-49](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/94bcdc4f-b3a5-453e-8b4a-8905af118495)

- Floorplan and Placement
- Commands:

   init_floorplan

   place_io
  
   tap_decap_or

![Screenshot from 2024-06-02 22-20-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/3ff976cc-3907-4323-8746-748b75a63d04)

![Screenshot from 2024-06-02 22-20-47](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/cf94cb0a-b7c3-4ab8-bdfd-a99a885e36ea)

![Screenshot from 2024-06-02 22-20-54](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/21518fa3-7be0-4d05-bf73-535746f3cae0)

![Screenshot from 2024-06-02 22-22-04](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/fd6fea61-ac9f-4582-9899-2086acd47d63)


- Placement succesfully generated

![Screenshot from 2024-06-01 19-42-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/3acb9c97-0993-4d35-99e7-733d3e65e936)

- Running expand window in tckon

![Screenshot from 2024-06-02 22-26-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/476c95a3-c322-4d88-979a-b55f485fc845)

![Screenshot from 2024-06-02 22-28-27](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/82f7f77e-a53c-493b-9dd9-51d3b56e4888)

![Screenshot from 2024-06-02 22-28-41](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/877a1a13-806a-4066-8b6a-fb0444c905f4)

- Post-Synthesis timing analysis with OpenSTA tool

- Commands:

  #Change directory to openlane

  cd Desktop/work/tools/openlane_working_dir/openlane

  #Command to invoke OpenSTA tool with script

  sta pre_sta.conf

![Screenshot from 2024-06-03 12-42-04](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/12f4e2e1-0403-4ad4-846a-69a8b702baa4)

- pre_sta.conf file

![Screenshot from 2024-06-02 14-14-14](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/03415ebe-a0b6-4c29-bccc-8da786de0ace)

- my_base.sdc file

![Screenshot from 2024-06-02 14-12-21 (1)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/4a6d82b2-4bd7-4143-a06e-055cdd6760b5)

-  Make timing ECO fixes to remove all violations

- Commands:

  #Reports all the connections to a net

  report_net -connections _12771_

  #Checking command syntax

  help replace_cell

  #Replacing cell

  replace_cell _15446_ sky130_fd_sc_hd__o21bai_4

  #Generating custom timing report

  report_checks -fields {net cap slew input_pins} -digits 4

![Screenshot from 2024-06-03 12-43-48](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/754dfbb1-5fa3-4433-8016-b46082e54241)

![Screenshot from 2024-06-03 12-44-58](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/64bb5e8d-a8bf-49a4-9f45-573b4dbdbc94)

![Screenshot from 2024-06-03 12-43-09](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9f3dd500-c0f9-4257-8aae-896e19784054)

![Screenshot from 2024-06-03 12-45-36](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/6cc7f5a7-0f71-4615-83e0-2ed8c4c75f65)

- Slack is reduced from -5.59 to -5.5031

-  Cell getting replaced

![Screenshot from 2024-06-03 12-45-57](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f77c402d-9495-4d04-9507-f4a45d613d57)

- Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts

![Screenshot from 2024-06-03 12-55-59](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/6b471a90-54ba-407d-ab3b-d47ac391a9aa)

- Write verilog file

![Screenshot from 2024-06-03 12-55-42](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f03e18ef-39de-4a75-b3a6-4b9cd022bf12)

- Verified that the netlist is overwritten

![Screenshot from 2024-06-03 12-59-28](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b080051b-1f55-4b07-a700-935c249905e8)

- Load the design and run necessary stages

![Screenshot from 2024-06-03 13-02-41](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/83d3f957-6fa4-43f0-a976-fae0269cdbd2)

![Screenshot from 2024-06-03 13-03-39](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/53f5fd24-a5ca-495c-92e2-9c175f141501)

![Screenshot from 2024-06-03 13-05-52](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/484fc7a3-33eb-4bd0-93af-a27bddf5857d)

- cts.tcl

![Screenshot from 2024-06-03 13-08-34](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9dd6dd49-f091-46c8-b102-bd7c8d56dade)

![Screenshot from 2024-06-03 13-08-46](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b9dd3575-85f4-428b-a013-79f1e58a8984)

- or_cts.tcl

![Screenshot from 2024-06-03 13-11-10](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e37b99d2-0f47-4f94-9342-a859e87f99bf)

![Screenshot from 2024-06-03 13-11-21](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e65da2c2-6d75-45c4-a18b-afc1097997d9)

- Post-CTS OpenROAD timing analysis

![Screenshot from 2024-06-03 17-33-08 (1)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c1d94c30-5049-4b4e-b58a-1fa51ac93565)

![Screenshot from 2024-06-03 17-36-51 (1)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/8142a276-b6c6-4e25-91e0-f1e50ae534da)

![Screenshot from 2024-06-03 17-37-13 (2)](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/60c1d463-29ce-4bd3-8d33-ea8abb3d7e1a)

![Screenshot from 2024-06-03 17-37-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9f58836c-5ed5-41d7-a24c-f87ec22b9d0c)

![Screenshot from 2024-06-03 17-37-33](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ed2646c8-2692-4476-9aee-3d70f5a63ec9)

![Screenshot from 2024-06-03 17-37-56](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/af8b2b4d-d4b6-45f7-bac3-277d32a21c79)

- Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'

![Screenshot from 2024-06-03 17-40-06](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ec13eac7-fd90-434b-b294-ff4e74ba4573)

![Screenshot from 2024-06-03 17-41-08](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/8262dd92-4d32-45f9-80c5-dce6266d6537)

![Screenshot from 2024-06-03 17-44-13](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a401fe2e-f51e-411f-8c7e-7f9718d0539d)

![Screenshot from 2024-06-03 17-44-39](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/27f97015-bad3-47bc-bcfd-edcad0d439c8)

![Screenshot from 2024-06-03 17-44-44](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/f83b0fc4-3fee-4a7f-b490-6a35e8432f6d)

![Screenshot from 2024-06-03 17-45-09](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e9d56740-36b7-4f12-92c5-3207622e7b76)

![Screenshot from 2024-06-03 17-45-58](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/a5ed38e2-471e-4c61-8f02-671b95a235d6)


# Theory from Day 5: Final step for RTL2GDS using tritinRoute and openSTA

## Maze Routing

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c4598afb-048a-4484-8a8b-46442b518cf3)

## Design rule check (DRC)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/573af34f-baf6-41e2-8a80-70fb6cbf0861)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/30ce54a2-5c5e-4e49-8750-d414d382f30b)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/6cf9a27f-c6e6-4490-a14c-2f2caae5e0c5)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9a4611e2-3972-4877-9144-4b8cd853d9d4)

## Power straps to Standard Cell

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/c35d6824-5653-49a1-b4ef-2eed28e15ff6)

## Routing

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ee090ea0-8cba-4170-8341-2607c669012b)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/2b89ab17-f931-42b1-a002-0d19c6dade9c)

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/caac272e-45c8-4cc5-bd20-5ce583f436e1)

## Handling connectivity

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/0f7c8714-1f36-47a7-aced-51717418355d)

- Rouitng algorithm

![image](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/9e021ab9-58d8-4675-ac1f-665c669877b2)

  
# Lab reports from Day 5

- Perform generation of Power Distribution Network (PDN)

![Screenshot from 2024-06-03 21-19-05](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/cb897a62-c727-488d-b4d8-7e552dd4e45e)

- Load PDN def in magic in another terminal

- Commands:

  #Change directory to path containing generated PDN def

  cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-06_15-41/tmp/floorplan/

  #Command to load the PDN def in magic tool

  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &

![Screenshot from 2024-06-03 21-21-12](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d50a5dc7-a23e-463b-90a3-39b81205b363)

![Screenshot from 2024-06-03 21-22-05](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/b06fdd80-badd-4463-b62f-df62fe9f89ba)

![Screenshot from 2024-06-03 21-22-10](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e6834d4d-6ce0-47a9-8295-91368f45c71b)

![Screenshot from 2024-06-03 22-02-29](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/ad819144-09d4-47f6-90d6-2a24ff64e764)

- Perform detailed routing using TritonRoute and explore the routed layout

![Screenshot from 2024-06-03 21-23-45](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/539d3fc5-0af9-42d4-9768-0b703f2cd63d)

![Screenshot from 2024-06-03 21-40-34](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/6677bd01-b23c-4718-a6ca-45b93fb67a7b)

- Load routed def in magic

- Commands:

  #Change directory to path containing routed def

  cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-06_15-41/results/routing/

  #Command to load the routed def in magic tool

  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

![Screenshot from 2024-06-03 22-12-24](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e8115836-1a93-48a5-a51d-366586fe0d1d)

![Screenshot from 2024-06-03 22-06-48](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/75572598-922e-4cc9-a663-ef3138e1bafb)

![Screenshot from 2024-06-03 22-08-34](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/e9f32f8c-cb8d-448b-98a0-53b8c1795c7b)

![Screenshot from 2024-06-03 22-02-35](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/661ebc00-c21f-4b35-9af1-f9ad34d69eaf)

![Screenshot from 2024-06-03 22-03-06](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/917855c5-f3a8-44dc-a387-0c98f3fd62c3)

- Parasitics command is already run and spef is extracted
 
- fastroute.guide file

![Screenshot from 2024-06-03 22-05-23](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/2367c823-dd63-4de6-b6b5-6f2dc18f569a)

![Screenshot from 2024-06-03 22-05-27](https://github.com/amanh-iitj/SOC-Design-and-Planning/assets/155350256/d314b083-4124-48a7-bd38-1eb86027721a)

## SPEF extraction

- Post-Route parasitic extraction using SPEF extractor
- In runs folder, where routing outputs are dumped and we'll find the SPEF there. 

- Commands:

  #Command extract spef

  python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-06_15-41/tmp/merged.lef 
  /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-06_15-41/results/routing/picorv32a.def

  
# Acknowledgements
- Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.
- Nickson P Jose, Physical Design Engineer, Intel Corporation.
- R. Timothy Edwards, Senior Vice President of Analog and Design, efabless Corporation.






















  


















  






  
#
