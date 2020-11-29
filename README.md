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

### Workshop Introduction
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



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



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