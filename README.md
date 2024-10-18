[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
# Digital VLSI SoC design & Planning
> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM


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

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```
Screenshots of commands runned 

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


<details>
  <summary>Day 2: Good floorplan vs bad floorplan and introduction to library cells</summary>

Section 2 tasks:- 
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
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

<details>
  <summary>Day 3: Design library cell using Magic Layout and ngspice characterization</summary>


</details>

<details>
  <summary>Day 4: Pre-layout timing analysis and importance of good clock tree</summary>
</details>

<details>
  <summary>Day 5: Final steps for RTL2GDS using tritonRoute and openSTA</summary>
</details>
