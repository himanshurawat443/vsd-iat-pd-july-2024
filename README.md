[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
# Digital VLSI SoC design & Planning
> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM

##
<details>
  <summary>Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK</summary>

## Lab work
- **Core** is an area in the chip where the fundamental logic of the design is placed. It encapsulates all the combinational circuit, soft and hard IPs, and nets.

- **Die** is an area of chip that encapsulates the core and IO pads. Die is imprinted multiple times along the silicon area or wafer to increase the throughput.

- **IO Pads** are the pins that act as the source of communication between core and the outside world. Pad cells surround the rectangular metal patches where external bonds are made. input,output and power pad.
  
- **IPs**  are manually designed or need some human interference (or intelligence) essentially to define and create them like SRAM, ADC, DAC, PLLs.

- **PDKs** are interface between foundary and design engineers. PDKs contains set of files to model fabrication process for the design tools used to design IC like device models, DRC, LVS, Physical extraction, layers, LEF, standard cell libraries, timing libraries etc. SkyWater 130nm is the PDK used in this workshop specifically sky130_fd_sc_hd and openLANE is built around this PDK.

Section 1 tasks:- 
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.


```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```
```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

```
Screenshots of commands run

![Day_1_1st](https://github.com/user-attachments/assets/86ea864f-a067-4728-8fb6-e29a1b167942)

![Day_1_2nd](https://github.com/user-attachments/assets/54066379-1cea-4513-8bef-4ada25778b7e)

![Day_1_3rd](https://github.com/user-attachments/assets/9856dcaf-bf96-40c2-a36b-17140be30ece)

![Day_1_4th](https://github.com/user-attachments/assets/adeb3ee3-2749-4f68-9a29-aeeda652fe42)

Calculation of Flop Ratio and DFF % from synthesis statistics report file

![Day_1_5th](https://github.com/user-attachments/assets/21afc9e1-00ca-44ea-a8fd-d3e71fada072)

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

</details>

##
<details>
  <summary>Day 2: Good floorplan vs bad floorplan and introduction to library cells</summary>

  ## Lab Work
Section 2 tasks:- 
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```
Area of die in microns = Die width in microns * Die height in microns
```
#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan
```
Screenshot of floorplan run

![Day_2_1st](https://github.com/user-attachments/assets/128ee5bf-9e44-4633-bcba-e5f4ee592727)

![Day_2_2nd](https://github.com/user-attachments/assets/60be9a64-fb77-45ed-9ebc-4df210783c9c)

![Day_2_3rd](https://github.com/user-attachments/assets/d5b90993-53ac-4de7-9b00-0b07daa692b0)

![Day_2_4th](https://github.com/user-attachments/assets/e4275ee7-d59b-4ad2-8ea2-e7fa419a0f8c)

![Day_2_5th](https://github.com/user-attachments/assets/64e0353a-4f8f-4fe6-aee7-7129e927172b)

#### 2. Calculate the die area in microns from the values in floorplan def.
According to floorplan def
```
1000 Unit Distance = 1 Micron

Die width in unit distance = 660685 - 0 = 660685

Die height in unit distance = 671405 - 0 = 671405

Distance in microns = Value in Unit Distance / 1000

Die width in microns = 660685 / 1000} = 660.685 Microns

Die height in microns = 671405 / 1000 = 671.405 Microns

Area of die in microns = 660.685 * 671.405 = 443587.212425 Square Microns
```
#### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Screenshots of floorplan def in magic (Equidistant placement of ports)
![Day_2_6th](https://github.com/user-attachments/assets/f3737117-30f9-4216-9832-9dca6bc74d95)

Port layer as set through config.tcl
![Day_2_7th](https://github.com/user-attachments/assets/16059256-a109-4649-a6cb-cf25664fe5a5)

![Day_2_8th](https://github.com/user-attachments/assets/da7dc87c-a7b7-4372-ab6e-bf60e30f2648)

</details>

##
<details>
  <summary>Day 3: Design library cell using Magic Layout and ngspice characterization</summary>

  ## Lab Work
**Section 3 tasks**:-
1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

#### 1. Clone custom inverter standard cell design from github repository

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

Screenshot of commands run
<img width="615" alt="Day_3_3rd" src="https://github.com/user-attachments/assets/d7807495-7218-4cda-970f-7d7ac2e132c1">

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

<img width="533" alt="Day_3_4th" src="https://github.com/user-attachments/assets/413d2e57-6f0d-4f91-8886-7e9e6be231e2">

NMOS and PMOS identified

<img width="454" alt="Day_3_5th" src="https://github.com/user-attachments/assets/9c5c3704-287c-48dd-b467-ebcc0bd54e47">
<img width="395" alt="Day_3_6th" src="https://github.com/user-attachments/assets/79372808-24ac-48a0-879c-30015f4dde7e">

Output Y connectivity to PMOS and NMOS drain verified

<img width="242" alt="Day_3_7th" src="https://github.com/user-attachments/assets/aeb46ccb-2ed4-41df-b926-f6f9efc9c14a">

PMOS source connectivity to VDD (here VPWR) verified

<img width="217" alt="Day_3_8th" src="https://github.com/user-attachments/assets/8a84338a-34db-4b5c-b789-759a6d7fdbc7">

NMOS source connectivity to VSS (here VGND) verified

<img width="269" alt="Day_3_9th" src="https://github.com/user-attachments/assets/48df8798-6ef7-4509-85b3-594d7c8058c2">

#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

Screenshot of tkcon window after running above commands

<img width="443" alt="Day_3_10th" src="https://github.com/user-attachments/assets/e955eede-332a-421c-a183-bd02cf4be25e">

Screenshot of created spice file

<img width="367" alt="Day_3_sp_initial" src="https://github.com/user-attachments/assets/4cdaa7fc-1f54-43ad-9d62-18737db7ecb6">

#### 4. Editing the spice model file for analysis through simulation.

Final edited spice file ready for ngspice simulation

<img width="374" alt="Day_3_sp_final" src="https://github.com/user-attachments/assets/c662846c-10bf-4c5a-8766-6f1a05bc715e">

#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

<img width="564" alt="Day_3_ngspice_1" src="https://github.com/user-attachments/assets/d5b440a7-bbd5-4257-a109-07514cb6b535">

Screenshot of generated plot

<img width="559" alt="Day_3_ngspice_plot" src="https://github.com/user-attachments/assets/a3991fc9-56b8-4d1a-bbd7-a7cd371e417e">

<img width="439" alt="Day_3_20_per" src="https://github.com/user-attachments/assets/ca305e95-bfcd-4397-8f6c-7ba24a3a3a95">
<img width="499" alt="Day_3_80_per" src="https://github.com/user-attachments/assets/32683d09-e57d-4465-bdc9-9d5f27356879">
<img width="506" alt="Day_3_50_per" src="https://github.com/user-attachments/assets/41fe92a2-3037-4daf-aebb-67ead61809bb">




<img width="559" alt="Day_3_met3" src="https://github.com/user-attachments/assets/b45bf466-b504-449a-906d-d144908eb24a">
<img width="560" alt="Day_3_drc" src="https://github.com/user-attachments/assets/ef3b1227-50ff-4c0d-be11-bc1a0e4f2721">


</details>

##
<details>
  <summary>Day 4: Pre-layout timing analysis and importance of good clock tree</summary>
</details>

##
<details>
  <summary>Day 5: Final steps for RTL2GDS using tritonRoute and openSTA</summary>
</details>
