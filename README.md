# Router-1-3
Fusion Compiler provides a unified RTL-to-GDSII flow — meaning synthesis, placement, CTS, routing, and signoff all happen in a single environment, enabling better PPA (Power, Performance, Area) and faster convergence, which is very effective for 28 nm technology.

**RTL-to-GDSII flow using Synopsys Fusion Compiler in 28nm (Router 1:3 is presumably one of the projects or design blocks):**

🔹 1. **Input Stage****

Inputs:

RTL (Verilog/VHDL)

Standard cell library (28 nm PDK) — .lib, .lef, tech file

Constraints — timing (.sdc), floorplan (.def), power intent (.upf)

Design rules and parasitics info (.tlu+)

Goal: Prepare the design environment and import all required files into Fusion Compiler.

🔹2. **Synthesis**

Fusion Compiler performs logical synthesis (DC Ultra-level) directly in the same environment used for physical implementation.

Tasks:

Read RTL and constraints

Optimize for timing, area, power

Generate initial netlist

Key commands:
create_lib<tech_and_ref_libs_path>
read_verilog <rtl_files>
read_sdc <constraints.sdc>
load_up<name.upf>
synthesize -to_mapped
write_db synth.db

🔹 3. Floorplanning

Define chip/block outline, core area, IO placement, and power grid.

Fusion Compiler supports in-design planning — interactively updates timing and congestion.

Tasks:

Place macros and pins

Create power/ground rings and straps

Define voltage domains

🔹 4. Placement

Standard cell placement with physical and timing optimization.

Fusion Compiler performs timing-driven and congestion-aware placement.

Incremental optimization (post-placement synthesis) ensures timing closure.

🔹 5. Clock Tree Synthesis (CTS)

Build balanced and low-skew clock trees.

Optimize for insertion delay, skew, and power.

Verify with report_clock_tree and timing analysis (report_timing).

🔹 6. Routing

Fusion Compiler integrates IC Compiler II-quality routing.

Global and detailed routing with DRC fixing and timing optimization.

Parasitic extraction (RC extraction using StarRC or integrated tools).

🔹 7. Signoff Checks

Run physical verification (DRC/LVS) and timing signoff (PrimeTime integration).

Power integrity: IR drop and EM analysis.

Generate reports for WNS/TNS, area, and power.

🔹 8. GDSII Generation

Export final layout database:

write_gds final.gds


Also generate DEF, SPEF, and other deliverables for tapeout.

🔹 Output Files
Type	Example
Layout	router1_3_final.gds
Netlist	router1_3_final.v
Timing	router1_3.sdf, router1_3_timing.rpt
Power	router1_3_power.rpt
Parasitics	router1_3.spef
