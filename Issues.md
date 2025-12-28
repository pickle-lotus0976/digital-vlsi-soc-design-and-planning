Engineering Issues and Solutions LogProject: RISC-V (picorv32a) Physical DesignDate: December 28, 2025This document records technical challenges encountered during the OpenLANE flow, debugging steps taken, and final resolutions.Issue 1: Placement Resizer Segmentation FaultFieldDetailStatusResolvedSeverityCritical (Flow Blocking)StagePlacement (Step 12)Error DescriptionThe OpenROAD flow crashed during the resizer optimization step.[ERROR]: during executing openroad script /openlane/scripts/openroad/resizer.tcl
[ERROR]: Log: picorv32a/runs/RUN_2025.12.28_14.22.50/logs/placement/12-resizer.log
child killed: segmentation violation

Root CauseThe OpenROAD resizer module crashed during the design optimization phase. The resizer attempted parasitic RC calculations that triggered a memory access violation within the containerized environment.Solution AppliedDisabled design and timing optimizations for the resizer module to bypass the unstable routine.# config.tcl modifications
set ::env(PL_RESIZER_DESIGN_OPTIMIZATIONS) 0
set ::env(PL_RESIZER_TIMING_OPTIMIZATIONS) 0
set ::env(GLB_RESIZER_TIMING_OPTIMIZATIONS) 0

Result: Placement completed successfully.Issue 2: Clock Tree Synthesis (CTS) Segmentation FaultFieldDetailStatusUnresolved (Workaround Applied)SeverityCritical (Flow Blocking)StageCTS (Step 14)Error DescriptionRunning run_cts resulted in an immediate segmentation fault during the sta::ReduceToPi operation.[INFO]: Running Clock Tree Synthesis
[ERROR]: during executing openroad script /openlane/scripts/openroad/cts.tcl
Signal 11 received
Stack trace:
0# 0x00000000000D429A7 in openroad
1# 0x00007367D15E400 in /lib64/libc.so.6
...
child killed: segmentation violation

Root Cause AnalysisPrimary Cause: OpenROAD CTS module instability in OpenLane 1.0.2.Contributing Factors:Parasitic capacitance/resistance calculation errors.Potential incompatibility with the custom inverter timing model.Memory corruption during operations in the containerized environment.Solutions Attempted (Failed)Modified CTS Buffer Config: Explicitly defined buffer list and root buffers.Relaxed Timing Constraints: Increased CLOCK_PERIOD to 20ns and CTS_TARGET_SKEW to 200ps.Reduced Design Complexity: Lowered PL_TARGET_DENSITY to 0.5.Interactive Debugging: Attempted step-by-step execution to isolate the failure.Workaround ImplementedSkipped the CTS step to allow the flow to proceed to PDN generation and routing.# config.tcl modifications
set ::env(RUN_CTS) 0

Advantages: Allows flow to continue to PDN/Routing for physical verification.Limitations: Clock network is ideal. Timing analysis will not reflect real clock tree delays.Note: This workaround allows for checking cell integration geometry but is invalid for final sign-off.
