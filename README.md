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

![Day_1_1st](https://github.com/user-attachments/assets/86ea864f-a067-4728-8fb6-e29a1b167942)

![Day_1_2nd](https://github.com/user-attachments/assets/54066379-1cea-4513-8bef-4ada25778b7e)

![Day_1_3rd](https://github.com/user-attachments/assets/9856dcaf-bf96-40c2-a36b-17140be30ece)

![Day_1_4th](https://github.com/user-attachments/assets/adeb3ee3-2749-4f68-9a29-aeeda652fe42)

![Day_1_5th](https://github.com/user-attachments/assets/21afc9e1-00ca-44ea-a8fd-d3e71fada072)

</details>


<details>
  <summary>Day 2: Good floorplan vs bad floorplan and introduction to library cells</summary>


![Day_2_1st](https://github.com/user-attachments/assets/128ee5bf-9e44-4633-bcba-e5f4ee592727)

![Day_2_2nd](https://github.com/user-attachments/assets/60be9a64-fb77-45ed-9ebc-4df210783c9c)

![Day_2_3rd](https://github.com/user-attachments/assets/d5b90993-53ac-4de7-9b00-0b07daa692b0)

![Day_2_4th](https://github.com/user-attachments/assets/e4275ee7-d59b-4ad2-8ea2-e7fa419a0f8c)

![Day_2_5th](https://github.com/user-attachments/assets/f3737117-30f9-4216-9832-9dca6bc74d95)

![Day_2_6th](https://github.com/user-attachments/assets/16059256-a109-4649-a6cb-cf25664fe5a5)

![Day_2_7th](https://github.com/user-attachments/assets/da7dc87c-a7b7-4372-ab6e-bf60e30f2648)

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
