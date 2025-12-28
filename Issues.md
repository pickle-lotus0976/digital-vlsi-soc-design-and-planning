# Engineering Issues and Solutions Log

**Project:** RISC-V (picorv32a) Physical Design
**Date:** December 28, 2025

This document records technical challenges encountered during the OpenLANE flow, debugging steps taken, and final resolutions.

---

## Issue 1: Placement Resizer Segmentation Fault

| Field | Detail |
| :--- | :--- |
| **Status** | Resolved |
| **Severity** | Critical (Flow Blocking) |
| **Stage** | Placement (Step 12) |

### Error Description
The OpenROAD flow crashed during the resizer optimization step.

```text
[ERROR]: during executing openroad script /openlane/scripts/openroad/resizer.tcl
[ERROR]: Log: picorv32a/runs/RUN_2025.12.28_14.22.50/logs/placement/12-resizer.log
child killed: segmentation violation
