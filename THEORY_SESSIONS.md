# THEORY SESSIONS


## DAY 1: Inception of open source EDA, OpenLANE and Sky130PDK

### 1. How computers talk

1. Chips come in packages as per requirement of fabrication.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/231cb865-45ba-4d6c-9428-7358e3ee9e15)

2. Ex: QFN-48 with 7x7nm.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4e3b395e-c2f8-4812-a565-ec4d68003989)

3. Chip is placed in the centre and connected by wire bonds (technique of fabrication) to the boundaries of chip.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ccf75817-b8e2-4b4d-b5d6-7c97b55decff)

   a. Chip connection is made by PADs
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/b3c0f887-ef50-45f5-9dcd-c755ec03a691)

   b. Core contains all digital logic (Foundry IPs like SOC, SRAM DAC, ADC, PLL ... & Macros like SPI, RISCV SOC).
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5ac2ab3b-ab06-426c-a5eb-dd98bc5792fa)

   c. Die is where the chip is fabricated
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e002a27a-7acf-47f7-917e-c1c3a12239c2)


#### 1.1 RISC-V introduction

RISC-V Instruction Set Architecture (ISA): C propgram is written and compiled to assembly language programs (RISC-V) and then converted to computer language (Binary) for the computer layout (q flow).
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e39b454b-92c4-4b24-862f-9dfb82974abf)


#### 1.2 How application software interacts with Hardware

1. RISC-V ISA is introduced to the system software to interpret and transform the set of instructions to be read by the harware
2. Inside the system software, RTL code is then given to the synthesis tool and the RTL synthesis is created.
3. Physical design implementation of picrov32 takes place.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ce0ad461-547a-44b1-8fe7-ba29d03c4042)



### 2. SoC Design and OpenLANE

#### 2.1 Components of open source digital ASIC design
1. Lynn Conway and Carver Mead pioneered "structured" design methodology based on lambda based rules.
   a. Fabless design companies emerged due to this.
   b. PDKs are interface between fab and designers. Process Design Kit is collection of files to model a fabrication. (Includes Process Design Rules: DRC, LVS, PEX... ,            device models, Digital Standard Cell libraries, IO libraries)
2. Google and Skywater releases OS PDK for ASIC implementation. Using Apache 2.0 license. Uses FOSS 130nm Production PDK.
   a. 130 nm has good performance which do not need advanced nodes.
   b. Fabrication is cheaper.
   c. Ex: Intel: P4EE @ 3.46GHz (Q4'04). OSU team reproted 327 MHz post layout clock frequency for single RV32i CPU.

#### 2.2 Simplified RTL2GDSII flow
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/79bea548-a023-43a6-8b3b-e02dfdf7a166)

   **SYNTHESIS**
   1. Converts RTL to circuit out of components from standard cell library.
   2. Standard cells have regular layout.
   3. Each cell has different views/ models (Electrical, HDL, SPICE and Layout(Abstract and Details))

   **FLOOR AND POWER PLANNING**
   1. Chip floor planning requires partition of the chip die between different system building blocks and place the IO pads.
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/819e87ab-c98f-4951-a6ff-b7ba03739890)

   2. Macro planning requires dimensions, pin locations rows design.
   3. Powerplanning requires horizontal & vertical stripes and connecting to each other.
      a. Reduces resistance
      b. Addresses electromigration
         > Electromigration:
         > Failure mechanism to be considered in VLSI physical design. Atoms in traces can experience diffusion (real interconnects). Eventually leaves an open circuit                  (driven bycurrent density and temperature of conductor of the interconnect).
         
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/833befac-7db2-4ba4-8f5b-6a1e676eb21d)

   **PLACEMENT**
   1. Place cells on floorplan rows, aligned with sites.
   2. Two steps:
      a. GLobal: Optimal position of all cells(may not be legal).
      b. Detail: Global cells positioned are altered to be made legal.
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/efdc27a3-1c8c-4aef-981d-694d83e0a215)

   
   **CLOCK TREE SYNTHESIS**
   1. Creates a clock distribution network.
      a. deliver clock to all cells
      b. with min skew (0 is hard to achieve)
      c. in good shape
      d. usually a tree

   **SIGNAL ROUTING**
   1. Implement the interconnects using available metal layers.
   2. Lowest layer is for local interconnect layer and is made of titanium alloy.
   3. All above layers are of aluminium layers.
   4. Grid routing format:
      a. Global: generates routing guides.
      b. Detail: uses routing guides to implement the actual wiring.

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/925eb1e6-89f1-4d5c-ace5-a88c88cf0a47)

   **SIGN OFF**
   1. Physical Verification: DRC , Layout vs schematic (final layout mathces the Gate level netlist)
   2. Timing Verification: STA


#### 2.3 OpenLANE and Strive chipsets

   **OpenLANE**
   1. Apache 2.0 license [OSS]
   2. Started as OD flow for OS Tape-out experiments
   3. StriVe is a family of open everything SoCs. (Open PDK, Open EDA, Open RTL)
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c141ff81-2866-4249-8512-3c26f42a2e7b)

   4. Goal to produce clean GDSII with no human intervention
   5. Tuned for Skywater 130nm Open PDK
   6. Containerized for functional out of the box and instructions to build and run natively will follow
   7. Modes of operations:
      a. Autonomous: get final GDS with reports after sometime
      b. Interactive: run commands step by step to check intermediate results and do experimentation

#### OpenLANE details ASIC design flow

   **Design exploration utility**
   1. Sweep the design configurations to generate reports which shows design matrices and violations generated and find configurations for optimal use in OpenLANE.
   2. Regression testing.
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/53cbc2ab-7ea5-4bd0-a12c-088e4e402fed)

   3. Run OpenLANE on ~70 designs and compare the results to the best known results. Difference will be reported.
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f0007914-9054-47be-94b3-37dcc306ccdb)

   
   **Design for Test (DFT)**
   1. Scan insertion
   2. Automatic test patterm generation (ATPG)
   3. Test patterns compaction
   4. Fault coverage
   5. Fault simulation
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6f549859-7b07-4df6-9339-0769def877e3)


   **Physical Implementation (OpenRoad)**
   1. PnR:
      a. Floor/power planning
      b. End decoupling capacitors and tap cells insertion
      c. Placement: GLobal and detailed
      d. Post placement optimization
      e. CTS
      f. Routing: Global and detailed
   2. Fake antenna swapping script:
      a. metal wire segment fabricated when long enough can be an antenna.
      b. collects charges and damage transistors. Length is constrained. Job of routers.
      c. Add fake antenna diode next to every cell I/P after placement.
      d. Run Magic (antenna checker) on routed layout violation reported on cell I/P pin.
      
