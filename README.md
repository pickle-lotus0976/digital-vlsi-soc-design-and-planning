# Open-Source ASIC Implementation: RISC-V (picorv32a) to GDSII

## Project Overview
This repository documents the **RTL-to-GDSII physical design** of the `picorv32a` RISC-V core. Utilizing the **Sky130 PDK** and the **OpenLANE** flow, this project goes beyond automated script execution to explore the intricacies of ASIC design. The focus is on understanding, debugging, and optimizing every stage of the flow—from logic synthesis to final layout generation—including the custom design and integration of a standard cell.

---

## Technology Stack & EDA Tools

The project leverages a fully open-source toolchain on Ubuntu Linux:

| Category | Tool / Technology |
| :--- | :--- |
| **PDK** | SkyWater 130nm (Sky130A) |
| **RTL Design** | `picorv32a` RISC-V Core |
| **Flow Management** | OpenLANE |
| **Synthesis** | Yosys + ABC |
| **Static Timing Analysis** | OpenSTA |
| **Physical Design (CTS)** | TritonCTS |
| **Routing** | TritonRoute |
| **Layout & GDSII** | Magic |
| **Extraction** | SPEF Extractor |
| **Simulation** | Ngspice |

---

## Execution Roadmap

The implementation is structured into a 5-day workflow, mirroring a real-world physical design cycle.

### Day 1: Synthesis & Flow Setup
**Objective:** Transforming RTL into a gate-level netlist.
* **Environment Setup:** Initialized the OpenLANE flow and verified the design hierarchy.
* **Logic Synthesis:** Used **Yosys** to translate Verilog RTL into a generic netlist.
* **Technology Mapping:** Mapped the design to Sky130 standard cells using **ABC**.
* **Analysis:** Reviewed synthesis reports to establish a baseline for cell utilization, die area, and initial timing slack.

### Day 2: Floorplanning & Placement
**Objective:** Defining the physical constraints and cell arrangement.
* **Floorplanning:** Established the die area, core utilization, and aspect ratio.
* **IO & Power Planning:** Aligned I/O pins and generated standard cell rows.
* **Placement:** Executed global and detailed placement of standard cells.
* **Verification:** Checked for legal placement, ensuring correct row orientation and sufficient spacing to prevent congestion.

### Day 3: Custom Standard Cell Design
**Objective:** Bridging circuit design with physical implementation.
* **Circuit Design:** Designed a CMOS inverter schematic (`sky130_vsdinv`) and verified it via **Ngspice** simulations.
* **Layout:** Created a DRC-aware layout in **Magic**, extracting the LEF file for abstraction.
* **Library Characterization:** Analyzed timing libraries (`.lib`) to understand delay, slew, and capacitance models.
* **Integration:** Plugged the custom cell into the OpenLANE flow, enabling the tool to use it during synthesis and timing analysis.

### Day 4: Timing Closure & CTS (Incomplete)
**Objective:** Ensuring signal integrity and robust clock distribution.
* **Status:** This stage is currently a work in progress. I was unable to complete the labs for this section.
* **Intended Work:**
    * Performing pre-layout STA using OpenSTA to identify setup and hold violations.
    * Tuning synthesis parameters and performing manual ECOs to reduce negative slack.
    * Executing Clock Tree Synthesis (CTS) using TritonCTS.
    * Analyzing the impact of CTS buffers on slew, skew, area, and power.

### Day 5: Routing & Sign-off (Incomplete)
**Objective:** Final interconnects and GDSII generation.
* **Status:** The work for this day has not yet been started as it is dependent on the completion of Day 4.
* **Intended Work:**
    * Generating the Power Distribution Network (PDN), including rings, straps, and rails.
    * Executing global and detailed routing using TritonRoute.
    * Performing SPEF extraction to model wire parasitics.
    * Conducting final sign-off STA and generating the GDSII file.

---

## Project Status

**Current Status:** Work in Progress.

The project has been successfully carried out through Day 3 (Custom Cell Integration). The final stages of the flow—specifically Timing Closure (Day 4) and Routing/GDSII Generation (Day 5)—are currently incomplete. Future updates will focus on resolving timing violations and completing the physical implementation flow.

---

## Conclusion

This repository serves as a proof-of-concept for industry-aligned physical design using open-source tools. It demonstrates the progress made in setting up the flow, synthesizing the design, and integrating custom cells. The final closure and tape-out stages are currently pending further development.
