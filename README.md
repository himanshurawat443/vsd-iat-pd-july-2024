# vsd-iat-pd-oct-2024
# Day1 Labs
libs.ref: Houses the design libraries, including standard cells, IO cells, and other related files.
    lef: Library Exchange Format files describing the cell layouts.
    lib: Liberty files for timing and power analysis.
    gds: GDSII files containing the graphical layout of the cells.
    verilog: Verilog models of the cells.
libs.tech: Contains technology files tailored for specific EDA tools.
    magic: Magic technology files.
    klayout: KLayout technology files and layer properties.
    ngspice: SPICE models for circuit simulation.
    openroad: Files for OpenROAD flow.
    drc: Design Rule Check files.
    lvs: Layout Versus Schematic check files.
    pex: Parasitic Extraction files.
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


