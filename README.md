# OpenLANE Workshop

VSD Workshop performing the full RTL to GDSII flow using the open-source tool OpenLANE and the open-source PDK provided by Skywater.

<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Best-README-Template</h3>

  <p align="center">
    An awesome README template to jumpstart your projects!
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template">View Demo</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Report Bug</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

This project gives an interactive tutorial experied during the VSD Advanced Physical Design workshop using OpenLANE.

OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips.


<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.
* npm
  ```sh
  npm install npm@latest -g
  ```

### Installation

1. Get a free API Key at [https://example.com](https://example.com)
2. Clone the repo
   ```sh
   git clone https://github.com/your_username_/Project-Name.git
   ```
3. Install NPM packages
   ```sh
   npm install
   ```
4. Enter your API in `config.js`
   ```JS
   const API_KEY = 'ENTER YOUR API';
   ```

### RTS-to-GDSII Introduction

From conception to product, the ASIC design flow is an iterative process that is not static for every design. The details of the flow may change depending on ECO’s, IP requirements, DFT insertion, and SDC constraints, however the base concepts still remain. The flow can be broken down into 11 steps:
    1. Architectural Design – A system engineer will provide the VLSI engineer with specifications for the system that are determined through physical constraints. The VLSI engineer will be required to design a circuit that meets these constraints at a microarchitecture modeling level.
    2. RTL Design/Behavioral Modeling – RTL design and behavioral modeling are performed with a hardware description language (HDL). EDA tools will use the HDL to perform mapping of higher-level components to the transistor level needed for physical implementation. HDL modeling is normally performed using either Verilog or VHDL. One of two design methods may be employed while creating the HDL of a microarchitecture:
        a. 	RTL Design – Stands for Register Transfer Level. It provides an abstraction of the digital circuit using:
            i. 	Combinational logic
            ii. 	Registers
            iii. 	Modules (IP’s or Soft Macros)
        b. 	Behavioral Modeling – Allows the microarchitecture modeling to be performed with behavior-based modeling in HDL. This method bridges the gap between C and HDL allowing HDL design to be performed
    3. RTL Verification
    4. DFT Insertion    
    5. Logic Synthesis – Logic synthesis uses the RTL netlist to perform HDL technology mapping. The synthesis process is normally performed in two major steps:
        a. 	GTECH Mapping – Consists of mapping the HDL netlist to generic gates what are used to perform logical optimization based on AIGERs and other topologies created from the generic mapped netlist.
        b. 	Technology Mapping – Consists of mapping the post-optimized GTECH netlist to standard cells described in the PDK
Standard Cells – Standard cells are fixed height and a multiple of unit size width. This width is an integer multiple of the SITE size or the PR boundary. Each standard cell comes with SPICE, HDL, liberty, layout (detailed and abstract) files used by different tools at different stages in the RTL2GDS flow.
    6. Post-Synthesis STA Analysis: Performs setup analysis on different path groups.
    7. Floorplanning – Goal is to plan the silicon area and create a robust power distribution network (PDN) to power each of the individual components of the synthesized netlist. In addition, macro placement and blockages must be defined before placement occurs to ensure a legalized GDS file. In power planning we create the ring which is connected to the pads which brings power around the edges of the chip. We also include power straps to bring power to the middle of the chip using higher metal layers which reduces IR drop and electro-migration problem.
    8. Placement – Place the standard cells on the floorplane rows, aligned with sites defined in the technology lef file. Placement is done in two steps: Global and Detailed. In Global placement tries to find optimal position for all cells but they may be overlapping and not aligned to rows, detailed placement takes the global placement and legalizes all of the placements trying to adhere to what the global placement wants.
    9. CTS – Clock tree synteshsis is used to create the clock distribution network that is used to deliver the clock to all sequential elements. The main goal is to create a network with minimal skew across the chip. H-trees are a common network topology that is used to achieve this goal.
    10.  Routing – Implements the interconnect system between standard cells using the remaining available metal layers after CTS and PDN generation. The routing is performed on routing grids to ensure minimal DRC errors.
The Skywater 130nm PDK uses 6 metal layers to perform CTS, PDN generation, and interconnect routing.
Shown below is an example of a base RTL to GDS flow in ASIC design:

## Workshop Introduction
The inputs to the ASIC design flow are:

    - Process Design Rules: DRC, LVS, PEX
    - Device Models (SPICE)
    - Digital Standard Cell Libraries
    - I/O Libraries

Process Design Kit (PDK) is the interface between the CAD designers and the foundry. The PDK is a collection of files used to model a fabrication process for the EDA tools used in designing an IC. PDK’s are traditionally closed-source and hence are the limiting factor to open-source Digital ASIC Design. Google and Skywater have broken this stigma and published the world’s first open-source PDK on June 30th, 2020. This breakthrough has been a catalyst for open-source EDA tools. This workshop focuses on using the open-source RTL2GDS EDA tool, OpenLANE, in conjunction with the Skywater 130nm PDK to perform the full RTL2GDS flow as shown below:

OpenLANE flow consists of several stages. By default, all flow steps are run in sequence. Each stage may consist of multiple sub-stages. OpenLANE can also be run interactively as shown here.

    1. Synthesis
        - Yosys - Performs RTL synthesis using GTech mapping
        - abc - Performs technology mappin to standard cells described in the PDK. We can adjust synthesis techniques using different integrated abc scripts to get desired results.
        - OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports
        - Fault – Scan-chain insertion used for testing post fabrication. Supports ATPG and test patterns compaction.
    2. Floorplan and PDN
        - init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
        - ioplacer - Places the macro input and output ports
        - pdn - Generates the power distribution network
        - tapcell - Inserts welltap and decap cells in the floorplan
        - Placement – Placement is done in two steps, one with global placement in which we place the designs across the chip, but they will not be legal placement with some standard cells overlapping each other, to fix this we perform a detailed placement which legalizes the design and ensures they fit in the standard cell rows
        - RePLace - Performs global placement
        - Resizer - Performs optional optimizations on the design
        - OpenPhySyn - Performs timing optimizations on the design
        - OpenDP - Perfroms detailed placement to legalize the globally placed components
    3. CTS
        - TritonCTS - Synthesizes the clock distribution network (the clock tree)
    4. Routing
        - FastRoute - Performs global routing to generate a guide file for the detailed router
        - TritonRoute - Performs detailed routing
        - SPEF-Extractor - Performs SPEF extraction
    5. GDSII Generation
        - Magic - Streams out the final GDSII layout file from the routed def
    6. Checks
        - Magic - Performs DRC Checks & Antenna Checks
        - Netgen - Performs LVS Checks

## Day 1

Skywater PDK Files
 The Skywater PDK files we are working with are described under $PDK_ROOT. There are three subdirectories needed for the workshop:

![](/images/1.png)

  1. Skywater-pdk – Contains all the foundry provided PDK related files
  2. Open_pdks – Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility
  3. Sky130A – The open-source compatible PDK files

### Invoking OpenLane

![](/images/2.png)

  - ./flow.tcl is the script which runs the OpenLANE flow
  - OpenLANE can be run interactively or in autonomous mode 
  - To run interactively, use the -interactive option with the ./flow.tcl script 

### Package Importing
Different software dependencies are needed to run OpenLANE. To import these into the OpenLANE tool we need to run:

![](/images/3.png)

### User-defined and Example Designs
All designs run within OpenLANE are extracted from the openlane/designs folder:

![](/images/4.png)

### Design Folder Hierarchy

![](/images/5.png)

Each design hierarchy comes with two distinct components:
  1. Src folder - Contains verilog files and sdc constraint files
  2. Config.tcl files - Design specific configuration switches used by OpenLANE

An example of a configuration file is given:

  ![](/images/6.png)

### Prepare Design
Prep is used to make file structure for our design. To set this up do:

  ![](/images/7.png)

After running this look in the openlane/design/picro32a folder and you will see there is a new directory structure created in this folder under the runs folder so to enable OpenLANE flow:

  ![](/images/8.png)

The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.

In addition, preparing the design in OpenLANE merges the technology LEF and cell LEF information. Technology LEF information contains layer definitions and a set of restricted design rules needed for PnR flow. The cell LEF contains obstruction information of each standard cell needed to minimize DRC errors during PnR flow:

  ![](/images/9.png)

### Synthesis

To run synthesis:

  ![](/images/10.png)

Note: Ensure the WNS is an acceptable number, if not please adjust the clock period to fix STA errors.

##  Day 2 - Chip Floorplanning

In Floorplanning we typically set the:
  1. 	Die Area
  2. 	Core Area
  3. 	Core Utilization
  4. 	Aspect Ratio
  5. 	Place Macros
  6. 	Power distribution network (Normally done here but done later in OpenLANE)
  7. 	Place input and output pins

### Aspect Ratio and Utilization Factor

Two key descriptions of a floorplan are utilization and aspect ratio. The amount of area of the die core the standard cells are taking up is called utilization. Normally we go for 50-70% utilization to, or utilization factor of 0.5-0.7. Keeping within this range allows for optimization of placement and realizable routing of a system. Aspect ratio can specify the shape of your chip by the height of the core area divided by the width of the core area. An aspect ratio of 1 discribes the chip as a square.

### Preplaced Cells

Preplaced cells, or MACRO’s, are important to enable hierarchical PnR flow. Preplaced cells enable VLSI engineers to granularize a larger design. In floorplanning we define locations and blockages for preplaced cells. Blockages are needed to ensure no standard cells are mapped where the placeplaced cells are located.

### Decoupling Capacitors

Decoupling capacitors are placed local to preplaced cells during Floorplanning. Voltage drops associated with interconnect wires can heavily affect our noise margin or put it into an indeterminate state. Decoupling capacitor is a big capacitor located next to the macros to fix this problem. The capacitor will charge up to the power supply voltage over time and it will work as a charge reservoir when a transition is needed by the circuit instead of the charge coming from the power supply. Therefore it “decouples” the circuit from the main supply. The capacitor acts like the power supply.

### Power Planning

Power planning during the Floorplanning phase is essential to lower noise in digital circuits attributed to voltage droop and ground bounce. Coupling capacitance is formed between interconnect wires and the substrate which needs to be charged or discharged to represent either logic 1 or logic 0. When a transition occurs on a net, charge associated with coupling capacitors may be dumped to ground. If there are not enough ground taps charge will accumulate at the tap and the ground line will act like a large resistor, raising the ground voltage and lowering our noise margin. To bypass this problem a robust PDN with many power strap taps are needed to lower the resistance associated with the PDN.

### Pin Placement

Pin placement is an essential part of floorplanning to minimize buffering and improve power consumption and timing delays. The goal of pin placement is to use the connectivity information of the HDL netlist to determine where along the I/O ring a specific pin should be placed. In many cases, optimal pin placement will be accompanied with less buffering and therefore less power consumption. After pin placement is formed we need to place logical cell blockages along the I/O ring to discriminate between the core area and I/O area:

### Floorplanning with OpenLANE

To run floorplan in OpenLANE:

  ![](/images/11.png)

As with all other stages, the floorplanning will be run according to configuration settings in the design specific config.tcl file. The output the the floorplanning phase is a DEF file which describes core area and placement of standard cell SITES:

  ![](/images/12.png)

### Viewing Floorplan in Magic
To view our floorplan in Magic we need to provide three files as input:

  1. Magic technology file (sky130A.tech)
  2. Def file of floorplan
  3. Merged LEF file

  ![](/images/13.png)
    
  ![](/images/14.png)


### Placement
The next step in the Digital ASIC design flow after floorplanning is placement. The synthesized netlist has been mapped to standard cells and floorplanning phase has determined the standard cells rows, enabling placement. OpenLANE does placement in two stages:
  1. Global Placement - Optimized but not legal placement. Optimization works to reduce wirelength by reducing half parameter wirelength
  2. Detailed Placement - Legalizes placement of cells into standard cell rows while adhering to global placement

To do placement in OpenLANE:
  ![](/images/15.png)

For placement to converge the overflow value needs to be converging to 0. At the end of placement cell legalization will be reported:
  ![](/images/16.png)

### Viewing Placement in Magic
To view placement in Magic the command mirrors viewing floorplanning:
  ![](/images/17.png)

### Standard Cell Design Flow
Cell design is done in 3 parts:
  1. Inputs - PDKs (Process design kits), DRC & LVS rules, SPICE models, library & user-defined specs.
  2. Design Steps - Design steps of cell design involves Circuit Design, Layout Design, Characterization. The software GUNA used for characterization. The characterization can be classified as Timing characterization, Power characterization and Noise characterization.
  3. Outputs - Outputs of the Design are CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir), timing, noise, power.libs, function.

### Standard Cell Characterization
Standard Cell Libraries consist of cells with different functionality/drive strengths. These cells need to be characterized by liberty files to be used by synthesis tools to determine optimal circuit arrangement. The open-source software GUNA is used for characterization.

Characterization is a well-defined flow consisting of the following steps:

  1. Link Model File of CMOS containing property definitions
  2. Specify process corner(s) for the cell to be characterized
  3. Specify cell delay and slew thresholds percentages
  4. Specify timing and power tables
  5. Read the parasitic extracted netlist
  6. Apply input or stimulus
  7. Provide necessary simulation commands 

## Day 3 
OpenLANE has the benefit of allowing changes to internal switches of the ASIC design flow on the fly. This allows users to experiment with floorplanning and placement without having to reinvoke the tool.

### Spice Simulations
To simulate standard cells spice deck wrappers will need to be created around our model files. 
  - SPICE deck will comprise of:
  - Model include statements
  - Component connectivity, including substrate taps
  - Output load capacitance
  - Component values
  - Node names
  - Simulation commands

To plot the output waveform of the spice deck we will use ngspice. The steps to run the simulation on ngpice are as follows:
  1. Source the .cir spice deck file
  2. Run the spice file by: run
  3. Run: setplot → allows you to view any plots possible from the simulations specified in the spice deck
  4. Select the simulation desired by entering the simulation name in the terminal
  5. Run: display to see nodes available for plotting
  6. Run: plot <node> vs <node> to obtain output waveform

### Switching Threshold of a CMOS Inverter 

CMOS cells have three modes of operation:
  - Cutoff - No inversion
  - Triode - Inversion but no pinchoff in channel
  - Saturation - Inversion and pinchoff in channel

The voltages at which the switch between the modes of operation happens is dependent on the threshold voltage of the device(s). Threshold voltage is a function of the W/L ratio of a device, therefore varying the W/L ratio will vary the output waveform of CMOS devices. 

To enable efficient description of the varying waveforms a single parameter called switching threshold is used. Switching threshold is defined at the intersection of Vin = Vout. A perfectly symmetrical device will have a switching threshold such that Vin = Vout = VDD/2. 

### 16-Mask CMOS Process Steps

  - Substrate Selection : Selection of base layer on which other regions will be formed.
  - Create an active region for transistors : SiO2 and Si3N2 deposited. Pockets created using photoresist and lithography.
  - Nwell & Pwell formation : Pwell uses boron and nwell uses phosphorus. Drive in diffusion by placing it in a high temperature furnace.
  - Creating Gate terminal : For desired threshold value NA (doping Concentration) and Cox to be set.
  - Lightly Doped Drain (LDD) formation : LDD done to avoid hot electron effect and short channel effect.
  - Source and Drain formation : Forming the source and drain.
  - Contacts & local interconnect Creation : SiO2 removed using HF etch. Titanium deposited using sputtering.
  - Higher Level metal layer formation : Upper layers of metals deposited.

### Magic Layout Viewer of Inverter Standard Cell

Refer to: https://github.com/nickson-jose/vsdstdcelldesign for cell files.

For easier access to critical files within the lab I suggest doing the following:
  1. Sudo pluma /etc/environment (can open with preferred document viewer)
  2. Add the following variables to the file:
    ![](/images/18.png)

Replace the file locations as specified in your user hierarchy

To invoke Magic:
  ![](/images/19.png)
  ![](/images/20.png)

### Magic Key Features:

  1. Color Palette - Defines layers and associated colors
Continuous DRC
  2. Device Inference - Automatic recognition of NMOS and PMOS devices

### Device Inference

Select the specific layer/device by hovering over the object and pressing, s, iteratively, until you traverse the hierarchy to the specified object:
![](/images/21.png)

Run the what command in the tkcon window:
![](/images/22.png)

### DRC Erros

DRC errors in magic will be highlighted with white dotted lines. DRC checks are continuous in Magic, therefore the designer may ensure the design is DRC free during creation instead of performing the iterative DRC checks when the cell layout is completed.
![](/images/23.png)

To fix DRC errors select DRC find next error:
![](/images/24.png)

The associated DRC error will be displayed in the tkcon window:
![](/images/25.png)

For more information on DRC errors plase refer to: https://skywater-pdk--136.org.readthedocs.build/en/136/
For more information on how to fix these DRC errors using Magic please refer to: http://opencircuitdesign.com/magic/

### PEX Extraction with Magic
To extract the parasitic spice file for the associated layout one needs to create an extraction file:
![](/images/26.png)

After generating the extracted file we need to output the .ext file to a spice file:
![](/images/27.png)
![](/images/28.png)

### Spice Wrapper for Simulation
![](/images/29.png)

To run the simulation with ngspice, invoke the ngspice tool with the spice file as input:
![](/images/30.png)

The plot can be viewed by plotting the output vs time while sweeping the input:
![](/images/31.png)

##  Day 4
Place and routing (PnR) is performed using an abstract view of the GDS files generated by Magic. The abstract information will include metal and pin information. The PnR tool will use the abstract view information, formally defined as LEF information, to perform interconnect routing in conjunction to routing guides generated from the PnR flow.

### An Introduction to LEF Files
  - Technology LEF - Contains layer information, via information, and restricted DRC rules
  - Cell LEF - Abstract information of standard cells
![](/images/32.png)

Tracks are used during the routing stage, routes can go over the tracks, or metal traces can go over the tracks. What the file is saying is that for the li1 layer the x or horizontal track is at an offset of 0.23 and a pitch of 0.46. The offset is the distance from the origin to the routing track in either the x or y direction. It is half the pitch so that means the tracks are centered around the origin. 

### Standard Cell Pin Placement
On-track standard cell pin placement is essential for DRC free PnR flow. Pins must align with the li1 and met1 preferred routing directions. During standard cell creation this concept must be accounted for. To ensure a cell is aligned with routing grids in Magic we can display a grid on top of the gds file.

To display the grid in magic:
![](/images/33.png)

Viewing the grid we can ensure our pin placement is optimized for PnR flow:
![](/images/34.png)

### LEF Generation from Magic
Magic allows users to generate cell LEF information directly from the Magic terminal. To generate the cell LEF file from Magic perform:
![](/images/35.png)

Generated cell LEF file:
![](/images/36.png)

### How to Include New Cell in OpenLANE
In order to include the new cells in OpenLANE we need to do some initial configuration:
  1. Fully characterize new cell with GUNA for specified corners
  2. Include cell level liberty file in top level liberty file
  3. Reconfigure synthesis switches in the config.tcl file:
  ![](/images/37.png)

Note: This step will also include any extra LEF files generated for the custom standard cell(s)
Overwrite previous run to include new configuration switches:

  4. Overwrite previous run to include new configuration switches:
  ![](/images/38.png)

  5. Add additional statements to include extra cell LEFs:
  ![](/images/39.png)

  5. Check synthesis logs to ensure cell has been integrated correctly

### Fixing Slack Violations
VLSI engineers will obtain system specifications in the architecture design phase. These specifications will determine a required frequency of operation. To analyze a circuit's timing performance designers will use static timing analysis tools (STA). When referring to pre clock tree synthesis STA analysis we are mainly concerned with setup timing in regards to a launch clock. STA will report problems such as worst negative slack (WNS) and total negative slack (TNS). These refer to the worst path delay and total path delay in regards to our setup timing restraint. Fixing slack violations can be debugged through performing STA analysis with OpenSTA, which is integrated in the OpenLANE tool. To describe these constraints to tools such as In order to ensure correct operation of these tools two steps must be taken:

  1. Design configuration files (.conf) - Tool configuration files for the specified design
  2. Design Synopsys design constraint (.sdc) files - Industry standard constraints file 

For the design to be complete, the worst negative slack needs to be above or equal to 0. If the slack is outside of this range we can do one of multiple things:

  1. Review our synthesis strategy in OpenLANE
  2. Enable cell buffering
  3. Perform manual cell replacement on our WNS path with the OpenSTA tool
  4. Optimize the fanout value with OpenLANE tool

To invoke OpenSTA with the configuration file:
![](/images/40.png)

### Cell Fanout Example:
![](/images/41.png)

The delay of this cell is large due to a high load capacitance due to high fanout. To fix this problem we can re-run synthesis within OpenLANE after reconfiguring the maximum fanout load value.

###Cell Replacement Example:

![](/images/42.png)

To determine what loads our net is driving in OpenSTA we can report net connecitons:
![](/images/43.png)

To increase the drive strength of our buffer:
![](/images/44.png)

After performing this optimization we can use the write_verilog command of OpenSTA to output the improved netlist for use in the OpenLANE flow:
![](/images/45.png)

### Clock Tree Synthesis

After running floorplan and standard cell placement in OpenLANE we are ready to insert our clock tree for sequential elements in our design. Two of the main concerns with generation of the clock tree are:
  1. Clock skew - Difference in arrival times of the clock for sequential elements across the design
  2. Delta delay - Skew introduced through capacitive coupling of the clock tree nets

To run clock tree synthesis (CTS) in OpenLANE:
![](/images/46.png)

Note: To ensure timing constraints CTS will add buffers throughout the clock tree which will modify our netlist

### Viewing Post-CTS Netlist

OpenLANE will generate a new .def file containing information of our design after CTS is performed. To view this netlist we need to invoke the .def file with the Magic tool:

![](/images/47.png)

### Post-CTS STA Analysis

OpenLANE has the OpenROAD application integrated into its flow. The OpenROAD application has OpenSTA integrated into its flow. Therefore, we can perform STA analysis from within OpenLANE by invoking OpenROAD.

To invoke OpenROAD from OpenLANE:
![](/images/48.png)

In OpenROAD the timing analysis is done by creating a .db database file. This database file is created from the post-cts LEF and DEF files. To generate the .db files within OpenROAD:
![](/images/49.png)

Note: Whenever the DEF file changes we need to recreate this .db file

After .db generation users can perform tool configuration followed by reporting the propagated clock timing analysis:
![](/images/50.png)

##  Day 5

After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network in OpenLANE:
![](/images/51.png)

### Power Distribution Network Generation

To generate the PDN in OpenLANE:
![](/images/52.png)

The PDN feature within OpenLANE will create:
  1. Power ring global to the entire core
  2. Power halo local to any preplaced cells
  3. Power straps to bring power into the center of the chip
  4. Power rails for the standard cells
  ![](/images/53.png)

Note: The pitch of the metal 1 power rails defines the height of the standard cells

### Global and Detailed Routing

OpenLANE uses TritonRoute as the routing engine for physical implementations of designs. Routing consists of two stages:

  1. Global Routing - Routing guides are generated for interconnects on our netlist defining what layers, and where on the chip each of the nets will be reputed
  2. Detailed Routing - Metal traces are iteratively laid across the routing guides to physically implement the routing guides

### To run routing in OpenLANE:
![](/images/54.png)





<!-- CONTACT -->
## Contact

Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Img Shields](https://shields.io)
* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Pages](https://pages.github.com)
* [Animate.css](https://daneden.github.io/animate.css)
* [Loaders.css](https://connoratherton.com/loaders)
* [Slick Carousel](https://kenwheeler.github.io/slick)
* [Smooth Scroll](https://github.com/cferdinandi/smooth-scroll)
* [Sticky Kit](http://leafo.net/sticky-kit)
* [JVectorMap](http://jvectormap.com)
* [Font Awesome](https://fontawesome.com)





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
