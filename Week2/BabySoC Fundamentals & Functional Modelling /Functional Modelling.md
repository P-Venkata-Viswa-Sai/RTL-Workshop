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
- **Why not off-chip clocks?**
  - Delays, jitter, frequency mismatches, crystal drift.  

### 3. DAC (Digital-to-Analog Converter)  
- Converts binary → analog signals.  
- **Types:**
  - Weighted Resistor DAC  
  - R-2R Ladder DAC  
- **In BabySoC:**  
  - A **10-bit DAC** is used.  
  - Enables multimedia outputs (sound, video).  

---
 
