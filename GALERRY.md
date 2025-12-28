# Project Gallery & Execution Log

## 1. SKYWater130 DAY 1-2
*Understanding the Open-Source ASIC Flow and Standard Cell Design.*

| Image | Description |
| :--- | :--- |
| ![Foundry IPs](Pictures/Screenshot_2025-12-25_21-56-39.png) | **Chip Architecture:** Overview of RISC-V SoC, Macros, and Foundry IPs. |
| ![Cell Design Flow](Pictures/Screenshot_2025-12-27_19-41-41.png) | **Standard Cell Design Flow:** Inputs (PDKs, Rules) and Outputs (CDL, GDSII, LEF). |
| ![Euler Path](Pictures/Screenshot_2025-12-27_19-55-42.png) | **Layout Theory:** Using Euler's path for consistent transistor gating. |
| ![Stick Diagram](Pictures/Screenshot_2025-12-27_19-55-56.png) | **Stick Diagram:** Conceptual layout of the CMOS inverter. |

---

## 2. SKYWater130 DAY 3
*Designing the `sky130_vsdinv` cell, analyzing robustness, and extracting parameters.*

| Image | Description |
| :--- | :--- |
| ![Spice Deck](Pictures/Screenshot_2025-12-27_22-28-43.png) | **SPICE Deck:** Writing the SPICE netlist for the CMOS inverter. |
| ![VTC Curve](Pictures/Screenshot_2025-12-27_23-45-17.png) | **Static Analysis:** Plotting the Voltage Transfer Characteristic (VTC). |
| ![Switching Threshold](Pictures/Screenshot_2025-12-27_23-43-39.png) | **Robustness:** Analyzing the switching threshold (Vm) and noise margins. |
| ![Transient Sim](Pictures/Screenshot_2025-12-28_10-54-42.png) | **Transient Response:** Final Ngspice simulation showing Input (Blue) vs Output (Red). |

---

## 3. Physical Layout (Magic)
*Drawing the layout in Magic VLSI, adhering to Sky130 DRC rules.*

| Image | Description |
| :--- | :--- |
| ![Magic Layout](Pictures/Screenshot_2025-12-28_00-44-13.png) | **Final Layout:** The completed `sky130_vsdinv` layout in Magic. |
| ![Grid Setup](Pictures/Screenshot_2025-12-28_11-06-22.png) | **Grid Alignment:** Configuring the grid to match the track pitch. |
| ![DRC Checks](Pictures/Screenshot_2025-12-28_05-13-12.png) | **DRC Verification:** Checking Metal3 area and spacing rules. (Course Challange) |
| ![DRC Terminal](Pictures/Screenshot_2025-12-28_05-35-29.png) | **DRC Logs:** Analyzing terminal output and fixing issues for poly and diffusion spacing violations. (Course Challange) |

---

## 4. Integration & Debugging Log (Work in Progress)
*Attempting to plug the custom cell into the OpenLANE flow.*

| Image | Description |
| :--- | :--- |
| ![File List](Pictures/Screenshot_2025-12-28_12-39-06.png) | **File Check:** Verifying `.lef` and `.lib` files are present in the source directory. |
| ![Config](Pictures/Screenshot_2025-12-28_12-38-33.png) | **Configuration:** Editing `config.tcl` to include `EXTRA_LEFS` and `LIB_SYNTH`. |
| ![Error Log](Pictures/Screenshot_2025-12-28_13-12-12.png) | **Current Blocker:** OpenLANE encountering a segmentation fault during the Placement Resizer step. |
| ![Debug](Pictures/Screenshot_2025-12-28_17-53-35.png) | **Debugging:** Attempting to manually load the placement DEF to investigate the failure. |
