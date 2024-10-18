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
![Day_3_3rd](https://github.com/user-attachments/assets/d7807495-7218-4cda-970f-7d7ac2e132c1)

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

![Day_3_4th](https://github.com/user-attachments/assets/413d2e57-6f0d-4f91-8886-7e9e6be231e2)

NMOS and PMOS identified

![Day_3_5th](https://github.com/user-attachments/assets/9c5c3704-287c-48dd-b467-ebcc0bd54e47)

![Day_3_6th](https://github.com/user-attachments/assets/79372808-24ac-48a0-879c-30015f4dde7e)

Output Y connectivity to PMOS and NMOS drain verified

![Day_3_7th](https://github.com/user-attachments/assets/aeb46ccb-2ed4-41df-b926-f6f9efc9c14a)

PMOS source connectivity to VDD (here VPWR) verified

![Day_3_8th](https://github.com/user-attachments/assets/8a84338a-34db-4b5c-b789-759a6d7fdbc7)

NMOS source connectivity to VSS (here VGND) verified

![Day_3_9th](https://github.com/user-attachments/assets/48df8798-6ef7-4509-85b3-594d7c8058c2)

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

![Day_3_10th](https://github.com/user-attachments/assets/e955eede-332a-421c-a183-bd02cf4be25e)

Screenshot of created spice file

![Day_3_sp_initial](https://github.com/user-attachments/assets/4cdaa7fc-1f54-43ad-9d62-18737db7ecb6)

#### 4. Editing the spice model file for analysis through simulation.

Final edited spice file ready for ngspice simulation

![Day_3_sp_final](https://github.com/user-attachments/assets/c662846c-10bf-4c5a-8766-6f1a05bc715e)

#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

![Day_3_ngspice_1](https://github.com/user-attachments/assets/d5b440a7-bbd5-4257-a109-07514cb6b535)

Screenshot of generated plot

![Day_3_ngspice_plot](https://github.com/user-attachments/assets/a3991fc9-56b8-4d1a-bbd7-a7cd371e417e)

'''
Rise transition time = (Time taken for output to rise to 80%) - (Time taken for output to rise to 20%)

Fall transition time = (Time taken for output to fall to 20%) - (Time taken for output to fall to 80%)

20% of output = 20% of 3.3V = 660 mV

80% of output = 80% of 3.3V = 2.64 V
'''

![Day_3_20_per](https://github.com/user-attachments/assets/ca305e95-bfcd-4397-8f6c-7ba24a3a3a95)

![Day_3_80_per](https://github.com/user-attachments/assets/32683d09-e57d-4465-bdc9-9d5f27356879)

![Day_3_50_per](https://github.com/user-attachments/assets/41fe92a2-3037-4daf-aebb-67ead61809bb)

'''
DRC checks & corrected tech file
'''

![Day_3_met3](https://github.com/user-attachments/assets/b45bf466-b504-449a-906d-d144908eb24a)
![Day_3_drc](https://github.com/user-attachments/assets/ef3b1227-50ff-4c0d-be11-bc1a0e4f2721)


</details>

##
<details>
  <summary>Day 4: Pre-layout timing analysis and importance of good clock tree</summary>

  ## Lab Work
  **Section 4 tasks:-**
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```
Commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```


#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save sky130_vsdinv.mag
```
![Day4_save_mag](https://github.com/user-attachments/assets/3dddbaa0-8085-4e96-99f0-eae812dfb3fe)


Command to open the newly saved layout

```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```

Screenshot of newly saved layout

![Day4_new_layout](https://github.com/user-attachments/assets/eb2a4ee0-5893-4b95-ae70-02ddb946567e)

#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

![Lef_write](https://github.com/user-attachments/assets/19c8960c-b5c5-4ef7-a923-4c0114214e74)

![Lef_view](https://github.com/user-attachments/assets/2c70745b-3ed6-4aa3-be26-4e1e932bef4c)

#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

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

Screenshot of commands run

![copy_lib_&_lef](https://github.com/user-attachments/assets/1a24da60-f2d7-4d7e-998c-333d52074097)


#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

![edit_config_file](https://github.com/user-attachments/assets/962a0432-e8e2-436e-8f16-967ddd68a83a)


#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of commands run

![start_openlane](https://github.com/user-attachments/assets/1c78c132-628d-4e01-b550-6c100c53cd3b)

![lef_&_synth](https://github.com/user-attachments/assets/b47f13d6-556e-454d-b00e-0e98d0acb360)

![synth_complete](https://github.com/user-attachments/assets/0d1333db-254d-49ae-9afb-91ba965c6b48)


#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

![chip_area](https://github.com/user-attachments/assets/6bd6970a-ee71-4bd2-b2bb-9f4cba5fb0c2)


![tns_&_wns](https://github.com/user-attachments/assets/66b85c75-a4c4-4f19-bb93-3ae1ee113de4)

Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

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
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro
</details>

##
<details>
  <summary>Day 5: Final steps for RTL2GDS using tritonRoute and openSTA</summary>

  ## Lab Work
  **Section 5 tasks:-**
1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
2. Perfrom detailed routing using TritonRoute.
3. Post-Route parasitic extraction using SPEF extractor.
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.




</details>
