# Open-Source ASIC Implementation: RISC-V (picorv32a) to GDSII

## Project Overview
This repository documents the work-in-progress **RTL-to-GDSII physical design** of the `picorv32a` RISC-V core. Utilizing the **Sky130 PDK** and the **OpenLANE** flow, this project aims to explore the intricacies of ASIC design. The focus is on understanding, debugging, and optimizing the flow—from logic synthesis to layout—including the custom design of standard cells.

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

### Day 3: Custom Standard Cell Design (Partially Completed)
**Objective:** Bridging circuit design with physical implementation.
* **Circuit Design:** Designed a CMOS inverter schematic (`sky130_vsdinv`) and verified it via **Ngspice** simulations.
* **Layout:** Created a DRC-aware layout in **Magic**, extracting the LEF file for abstraction.
* **Library Characterization:** Successfully analyzed timing libraries (`.lib`) to understand delay, slew, and capacitance models.
* **Integration Issue:** I am currently stuck at the integration step. While the cell is designed and characterized, I am facing configuration issues integrating the custom LEF/LIB files into the OpenLANE flow within the GitHub Codespaces environment.

### Day 4: Timing Closure & CTS (Pending)
**Objective:** Ensuring signal integrity and robust clock distribution.
* **Status:** Pending completion of Day 3 integration.
* **Intended Work:**
    * Performing pre-layout STA using OpenSTA to identify setup and hold violations.
    * Tuning synthesis parameters and performing manual ECOs to reduce negative slack.
    * Executing Clock Tree Synthesis (CTS) using TritonCTS.

### Day 5: Routing & Sign-off (Pending)
**Objective:** Final interconnects and GDSII generation.
* **Status:** Pending completion of prior stages.
* **Intended Work:**
    * Generating the Power Distribution Network (PDN).
    * Executing global and detailed routing using TritonRoute.
    * Performing SPEF extraction and post-route STA.
    * Generating the final GDSII file.

---

## Project Status

**Current Status:** Work in Progress (Blocked).

The project is complete through the custom cell design and characterization on Day 3. I am currently troubleshooting the integration of the custom `sky130_vsdinv` cell into the OpenLANE flow on GitHub Codespaces. The remaining steps (Timing Closure and Routing) will be addressed once this integration issue is resolved.

---

## Conclusion

This repository demonstrates my progress in the physical design flow using open-source tools. While I have successfully completed the RTL synthesis, floorplanning, placement, and custom cell characterization, the final integration and sign-off stages are currently pending resolution of toolchain configuration issues.
