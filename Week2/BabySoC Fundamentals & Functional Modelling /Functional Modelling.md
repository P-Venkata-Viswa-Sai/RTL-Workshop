# VSDBabySoC Modelling

##  What is VSDBabySoC?
VSDBabySoC is a compact **System-on-Chip (SoC)** based on the **RISC-V architecture**.  
It was designed to:
- Test three open-source IPs (CPU, PLL, DAC) together.  
- Calibrate analog components in a small-scale SoC.  

**Main Components:**
- RVMYTH (RISC-V CPU)  
- 8× Phase-Locked Loop (PLL)  
- 10-bit Digital-to-Analog Converter (DAC)  

---

##  How VSDBabySoC Works
1. **Initialization & Clock Generation**  
   - The PLL generates a stable, synchronized clock.  
   - Keeps CPU and DAC aligned to avoid timing mismatches.  

2. **Data Processing in RVMYTH**  
   - The CPU updates **r17 register** with values.  
   - These values are cycled continuously for DAC conversion.  

3. **Analog Output via DAC**  
   - DAC converts digital values into analog signals.  
   - Output is saved in file **OUT**.  
   - Can drive analog devices like speakers, TVs, and mobile displays.  

---

##  BabySoC Components

### 1. RVMYTH (RISC-V CPU)  
- Open-source, customizable CPU.  
- Executes instructions and communicates with peripherals.  

### 2. PLL (Phase-Locked Loop)  
- Generates a stable clock signal.  
- Ensures synchronization across BabySoC.  
- **Structure:**
  - Phase Detector  
  - Loop Filter  
  - Voltage-Controlled Oscillator (VCO)  

### 3. DAC (Digital-to-Analog Converter)  
- Converts binary → analog signals.  
- **Types:**
  - Weighted Resistor DAC  
  - R-2R Ladder DAC  
- **In BabySoC:**  
  - A **10-bit DAC** is used.  
  - Enables multimedia outputs (sound, video).  

---
# BabySoC Project
So, in this project here it contains different modules such as
- vsdbabysoc.v(Top-Level SoC Module)
- rvmyth.v (RISC-V Core)
- avsdpll.v (PLL Module)
- avsddac.v (DAC Module)

This project demonstrates integration of these IP cores and aims to simulate and verify the design behavior using pre-synthesis and post-synthesis simulations.
This work discusses the different aspects of designing a small SoC based on RVMYTH (a RISCV-based processor). This SoC will leverage a PLL as its clock generator and controller and a 10-bit DAC as a way to talk to the outside world. Other electrical devices with proper analog input like televisions, and mobile phones could manipulate DAC output and provide users with music sound or video frames. 

---
## About synthesis
Before going into that, let us know  What “Synthesis” Means
In digital design, synthesis is the process of converting RTL code (behavioral Verilog) into a gate-level netlist built from real logic cells — like NANDs, NORs, flip-flops — from a standard cell library (like Sky130).
It includes two parts Pre synthesis and post synthesis.
### Pre Synthesis
Here we are directly checking the logic of the written code without involving any real actual gates.
We are doing it so that we can check the logical and functional correctness of it before actual implementation on hardware so that they will be fast respnse of correct or wring and gives us no damage in hardware if somthing is really wrong.
### Post synthesis

It is the actual implementation of our code onto the thousands of real gates.
This we do because we can check whether the logic doesnt change we are implementing on actual circuits and ensure that we are getting no time delays in it or any race conditions.

---
## vsdbabysoc.v (Top-Level SoC Module)
This is the top level module which integrates the other three modules.
Before going into that let us know  What “Synthesis” Means
In digital design, synthesis is the process of converting RTL code (behavioral Verilog) into a gate-level netlist built from real logic cells — like NANDs, NORs, flip-flops — from a standard cell library (like Sky130).

### Presynthesis Modelling
It includes verifying the RTL code behaviour before synthesizing it into software. It checks the functional correctness of logic using test benches rather than directly implementing onto gates.


 
