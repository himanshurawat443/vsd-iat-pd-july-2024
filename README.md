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

"Desktop/work/tools/openlane_working_dir/openlane" --> directory you should be in everytime

Run >> docker  #in openlane directory
	• Bash shell will be opened
Shell >> pwd --> to check directory (/openLANE_flow)
         >> ls -ltr # to check contents
         >> ./flow.tcl -interactive

	• OpenLANE flow will start running interactively

%package require openlane 0.9  (0.9 should be displayed)
% cd designs/picorv32a
%prep -design picorv32a --> Merges lib.lef & tech.lef together

	• New directory with Run Date & time would be created in "picorv32a/runs/<run_with_date_&_time>"
	• cd runs/<new_run>/tmp && less merged.lef
	• Files to check config.tcl & sky130a_sky____config.tcl in picorv32a dir

%run_synthesis --> make sure to be in openlane directory
Task 1 --> to find Flop ratio (no. of DFFs required by design) dfxtp2
Flop count = dfxtps present / Total no. of cells
>> cd reports/synthesis/yosys.rpt contains Report of synthesis done

<img width="587"  alt="Day_1_1st" align="center" src="https://github.com/user-attachments/assets/86ea864f-a067-4728-8fb6-e29a1b167942">

![Day_1_1st](https://github.com/user-attachments/assets/86ea864f-a067-4728-8fb6-e29a1b167942)
</details>

<details>
  <summary>Day 2: Good floorplan vs bad floorplan and introduction to library cells</summary>
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
