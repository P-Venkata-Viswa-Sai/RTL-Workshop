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

```
cd VSDBabySoc
make pre_synth_sim
```
This command lines generates vcd file of pre_synth_sim from the  makefile present in the directory VSDBabySoC

```
gtkwave output/pre_synth_sim/pre_synth_sim.vcd

GTKwave Analyzer v3.3.116 (w)1999-2000 BSI

[0] start time
[84999000] end time
```
![GTKWave Simulation](https://github.com/P-Venkata-Viswa-Sai/RTL-Workshop/blob/main/Week2/BabySoC%20Fundamentals%20%26%20Functional%20Modelling/Screenshot%202025-10-04%20154335.png)


This is the gtkwave simulation of the RTL behavior of vsdbabysoc.


In the image:

**CLK**: Input clock signal to the RVMYTH core, originally sourced from the PLL.

**reset**: Input reset signal to the RVMYTH core, originally from an external source.

**OUT (digital)**: Output signal from the VSDBabySoC module, originating from the DAC. Due to simulation limits, this behaves as a digital signal but represents an analog output.

**RV_TO_DAC[9:0]**: 10-bit output port [9:0] from the RVMYTH core, connected to register #17.

**OUT (analog)**: Real datatype wire simulating analog values, the output wire from the DAC module.

**Explanation:**
The clock is generated with a PLL (Phase locked loop) and drives the RVMYTH CPU core to simulate results based on the ISA of the core(RISC-V here).In this simulation, the RVMYTH core is continuously sending 10-bit digital values (RV_TO_DAC[9:0]) to the DAC. The first OUT signal is the digital representation of the DAC.Since the DAC converts these digital steps into a real value, the output (red waveform) does not appear as a flat digital line but instead forms smooth wave of analog values.

# Post synthesis simulation of vsdbabysoc

After synthesis with Yosys, the design is converted from RTL code into a gate-level netlist. The post-synthesis simulation runs this gate-level version, so the waveforms may look a bit more detailed or slightly delayed compared to pre-synthesis (because now actual gates, flip-flops, and propagation delays are modeled). Functionally, the behavior remains the same as the RTL simulation, which helps confirm that the synthesis process did not break the design.

```
gtkwave output/post_synth_sim/post_synth_sim.vcd

GTKwave Analyzer v3.3.116 (w)1999-2000 BSI

[0] start time
[84999000] end time
```
![GTKWave Simulation](https://github.com/P-Venkata-Viswa-Sai/RTL-Workshop/blob/main/Week2/BabySoC%20Fundamentals%20%26%20Functional%20Modelling/Screenshot%202025-10-04%20192300.png
 )

**Explanation:**

In the post-synthesis simulation, the clock from the PLL drives the RVMYTH core, while reset makes sure the design starts in a known state. Once running, the core pushes out 10-bit data from register #17 on its OUT[9:0] bus. This data goes into the DAC, which then produces two forms of output in the simulation: a digital OUT (just for representation) and a real OUT that shows the actual analog behavior. This flow confirms that, even after synthesis, the signals move correctly from the core to the DAC and finally into an analog waveform.



 
