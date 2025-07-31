
# 5-Stage RV32I Pipelined RISC-V CPU Core | Verilog, Hazard Handling, Simulation

A modular, synthesizable CPU core implementing the RV32I instruction set architecture (ISA), designed in Verilog with a classic 5-stage pipeline. This processor supports basic forwarding and stalling for hazard handling and is validated via simulation with waveform output.

---

## Features

- Implements 5-stage pipeline: **IF, ID, EX, MEM, WB**
- Supports key RV32I instructions: `ADD`, `SUB`, `ADDI`, `LW`, `SW`, `BEQ`, `JAL`, `AND`, `OR`
- **Hazard Handling**: Basic data forwarding and stalling logic
- Modular design with reusable components
- Fully testable with Verilog testbench and `.hex` program loader
- Simulation-ready with `Icarus Verilog` + `GTKWave`

---

## 📐 Architecture Diagram

<p align="center">
  <img src="docs/block_diagram.png" width="700"/>
</p>

> Visualizing datapath modules including PC, Register File, ALU, Control Unit, Pipeline Registers, and Instruction/Data Memory.

---

## Pipeline Stages

| Stage | Function |
|-------|----------|
| IF    | Fetch instruction from memory using PC |
| ID    | Decode instruction, read registers |
| EX    | Perform ALU operations or compute memory addresses |
| MEM   | Access memory for load/store |
| WB    | Write result back to register file |

---

## Instruction Support

| Type | Instructions |
|------|--------------|
| R-type | `ADD`, `SUB`, `AND`, `OR` |
| I-type | `ADDI`, `LW` |
| S-type | `SW` |
| B-type | `BEQ` |
| J-type | `JAL` |

---

## Hazard Handling

- **Data Forwarding** for EX/MEM and MEM/WB hazards
- **Stalling Logic** for load-use hazard
- **No Branch Prediction** — PC updated upon BEQ/JAL decision

---

## Simulation

Tested using a hand-written `.hex` file (assembly encoded) and Verilog testbench.

### Run Simulation (Icarus Verilog)

```bash
iverilog -o cpu_test sim/testbench.v src/*.v
vvp cpu_test
gtkwave dump.vcd
