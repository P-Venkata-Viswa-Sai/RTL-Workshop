# Baby Soc fundamentals and functional modelling
This is the second week of RTL workshop where we are going to discuss about SoC fundamentals
##  What is a System-on-Chip (SoC)?
System of chip in short is a chip that contains almost main parts of a motherboard of a laptop or deskatop in a small area compared to the laptop. With this we can easily fit the modules easily in a small area for smart phones so that they are easily portable. 
### Advantages of it are :-
- Reduces power consuption and area because they are spaced together.
- Improves performance and Lowers cost.
- Easily portable and makes life easy.
- There will be efficient memory transfor between components.
---
## Key components of SoC 
### 1. CPU (Central Processing Unit)
   - It is the main part of SoC.
   - It handles all instructions, mathematical calculations, like a bridge of all other components.
### 2. GPU (Graphics Processing Unit)
   - It rapidly accelerates the computer graphics. It gives good resolution for video games and increase the experience of it.
### 3. DSP (Digital Signal Processing)
   - It involves in processing of Audio, Video and display related functions.
### 4. Memory
   - It involves two components RAM and ROM.
   - RAM is related to for temparary storage of data while processing.
   - ROM involves the storage of date wherever power is given to him.
### 5. Power Managemnet
   - It gives the power to all the components of the SoC so that it performs efficiently.
### 6. Other components
   - These includes modules like wifi, bluetooth, Camera, Location,.. etc.
---

## Why BabySoC?  
BabySoc is like a model for SoC where we can easily experiment and understand how the operations are happening.
- **Simplified model** for beginners.  
- Contains only **essential blocks** (CPU + small memory + I/O).  
- Avoids industrial-level complexity.  
- Acts as a **stepping stone** before RTL & physical design.  

---

##  Why BabySoC is a Simplified Model for Learning SoC Concepts

The **BabySoC** is designed as a **minimal and educational version of a full System-on-Chip (SoC)**.  
It includes only the *core functional elements* needed to demonstrate how an SoC works, without the complexity of commercial chips.

- **Essential Components Only:**  
  Contains just three main IP blocks — the **RVMYTH RISC-V CPU**, **Phase-Locked Loop (PLL)**, and **Digital-to-Analog Converter (DAC)**.  
  This makes it lightweight and easy to simulate.

- **Focus on Conceptual Learning:**  
  Allows learners to understand how the **CPU, clock system, and peripherals** communicate and synchronize.

- **Simplified Interconnect:**  
  No complex bus architectures or multi-core communication — just direct, understandable connections.

- **Fast Simulation & Debugging:**  
  Smaller design = quicker simulations in **Icarus Verilog** and easier waveform visualization in **GTKWave**.

- **Open-Source & Accessible:**  
  Built using open-source IPs (RVMYTH, PLL, DAC) → anyone can experiment, modify, and learn.

 **In short**  
BabySoC removes unnecessary industrial complexity while preserving the key principles of SoC design — making it an ideal learning model for students and beginners in VLSI and embedded systems.

---

##  The Role of Functional Modelling Before RTL and Physical Design

**Functional modelling** is the first step in the SoC design flow.  
It defines **how the system should behave logically**, before worrying about transistor-level or gate-level implementation.

###  Purpose of Functional Modelling
- To **verify the SoC architecture** and ensure all components (CPU, memory, peripherals) communicate correctly.
- To **test functionality early**, before time-consuming RTL and physical design stages.
- To **identify design flaws quickly** and correct them with minimal cost.

###  How It Fits in the Design Flow
1. **Functional Modelling (Behavioral Level)**  
   - Implemented in high-level Verilog (behavioral constructs).  
   - Checks *logical correctness* and *data flow*.

2. **RTL Design (Register-Transfer Level)**  
   - Defines actual registers, signals, and hardware structure.  
   - Focuses on clock cycles and hardware timing.

3. **Physical Design (Layout Level)**  
   - Converts RTL into transistor placement, routing, and fabrication-ready layout.

###  Key Benefits
- Faster simulation compared to RTL.  
- Easier debugging and architectural experimentation.  
- Reduces risk of functional errors before synthesis and layout.
---

