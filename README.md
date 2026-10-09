تفضل كود ملف **`README.md`** كاملاً ومصلحاً بنسبة 100% مع ضبط التنسيق وإغلاق بلوك المجلدات، انسخه دفعة واحدة وضعه في محرر GitHub:

```markdown
# 16-Tap FIR Low-Pass Filter: From MATLAB to MicroBlaze SoC HW/SW Co-Design

A complete, production-grade **16-Tap FIR Low-Pass Filter** design pipeline targeted for AMD/Xilinx FPGA platforms using Vivado. The project transitions from MATLAB architectural fixed-point modeling to pure Verilog RTL logic, packaged as a reusable **AXI-mapped IP Core** for Hardware-Software Co-design on a **MicroBlaze Soft-Core Processor**.

---

## 🏗️ Architectural Roadmap

- [x] **Phase 1: MATLAB Verification Environment** (Fixed-point Q1.15 modeling, visualizations & Hex datasets)
- [ ] **Phase 2: Verilog RTL Core Development** (Symmetric MAC pipeline, 16-bit Q1.15 architecture)
- [ ] **Phase 3: Automated Testbench Verification** (Self-checking RTL simulation against MATLAB Golden Models)
- [ ] **Phase 4: Vivado IP Packaging** (AXI4-Lite for Control/Status + AXI4-Stream for Audio Data)
- [ ] **Phase 5: MicroBlaze SoC Hardware-Software Co-Design** (Block Design integration, AXI DMA, Vitis C Drivers)

---

## 📐 Filter Specifications

| Parameter | Value | Details |
| :--- | :--- | :--- |
| **Filter Order / Taps** | 15 / 16 Taps | Linear Phase Symmetric Type-I FIR |
| **Sampling Frequency ($F_s$)** | 48 kHz | Audio processing rate |
| **Passband Cutoff ($F_{pass}$)** | 4 kHz | Passband ripple protection |
| **Stopband Cutoff ($F_{stop}$)** | 10 kHz | High-frequency noise rejection |
| **Data Format** | Q1.15 Signed | 16-bit 2's Complement |
| **Target Architecture** | MicroBlaze SoC | AXI4-Stream / AXI4-Lite Compatible |

---

## 📁 Repository Structure

```text
microblaze-axi-fir-filter-soc/
├── Matlab/                      # MATLAB Workspace & Verification Environment
│   ├── filter_Designer/         # Exported magnitude, phase & pole-zero plots
│   ├── filter_visualization/    # Fixed-point quantized frequency response plots
│   ├── Goldens/                 # Hex outputs from Golden Model (golden_caseX.hex)
│   ├── matlab_filter/           # Quantized coefficient file (fir_coeffs.hex) & FDA session
│   ├── src/                     # Core MATLAB scripts (Quantization, Stimulus & Golden)
│   └── TestVectors/             # Generated input test stimuli (stimulus_caseX.hex)
├── hdl/                         # Verilog RTL source code (fir_core.v & AXI wrapper)
├── tb/                          # Self-checking testbench environments (tb_fir_core.v)
├── vivado_ip/                   # Packaged Custom IP repository for Vivado IP Catalog
└── sw/                          # Vitis embedded C drivers & MicroBlaze firmware

```

---

## 🧪 Verification Test Cases

1. **Case 1:** 1 kHz + 18 kHz — Stopband rejection test.
2. **Case 2:** 1 kHz + 7 kHz — Transition band behavior test.
3. **Case 3:** 1 kHz + 3 kHz — Multi-tone passband fidelity test.

---

## 👥 Handover Notes & Task Distribution

### For RTL & Hardware Verification Engineer (Phase 2 & 3):

1. **RTL Module (`hdl/fir_core.v`):**
* Implement a 16-tap FIR filter using Q1.15 fixed-point arithmetic (16-bit signed inputs/outputs).
* Load coefficients directly from `Matlab/matlab_filter/fir_coeffs.hex`.


2. **Testbench (`tb/tb_fir_core.v`):**
* Load stimulus vectors from `Matlab/TestVectors/stimulus_caseX.hex` using `$readmemh`.
* Compare simulation results against `Matlab/Goldens/golden_caseX.hex`.



### For MicroBlaze Systems Engineer (Phase 4 & 5):

1. Wrap `fir_core.v` into a Custom IP using Vivado IP Packager (AXI4-Lite / AXI4-Stream).
2. Build MicroBlaze SoC Block Design in Vivado IP Integrator.
3. Develop C drivers in Vitis (`sw/`) to process audio streams via DMA/Interrupts.

```

```
