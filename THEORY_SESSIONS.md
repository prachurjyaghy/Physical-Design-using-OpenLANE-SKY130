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
   b. PDKs are interface between fab and designers. Process Design Kit is collection of files to model a fabrication. (Includes Process Design Rules: DRC, LVS, PEX..., 
      device models, Digital Standard Cell libraries, IO libraries)
3. Google and Skywater releases OS PDK for ASIC implementation. Using Apache 2.0 license. Uses FOSS 130nm Production PDK.
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
         > Failure mechanism to be considered in VLSI physical design. Atoms in traces can experience diffusion (real interconnects). Eventually leaves an open                   circuit (driven bycurrent density and temperature of conductor of the interconnect).
         
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

#### 2.4 OpenLANE details ASIC design flow

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
   3. STA: Extraction of SPEFs and OpenSTA (integrated in Openroad) after which the reports are generated with timing violations.
   4. Physical Verification:
      a. Magic helps for DRCs and SPICE extraction from layout.
      b. Magic and netgen used for LVS (extracted SPICE by Magic vs Verilog netlist).
      

## DAY 2: Good floorplan vs bad floorplan and introduction to library cells

### 1. Chip floor planning considerations

#### 1.1 Utilization factor and aspect ratio
1.  Define height and width of core and die.
![WhatsApp Image 2023-08-15 at 15 17 27(8)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/79976536-0e08-40a5-921c-c862376ab5ba)
![WhatsApp Image 2023-08-15 at 15 17 27(7)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/36c1d09b-dd78-47eb-a376-9eb11b03fca9)

2.  Utilization factor = (Area occupied by netlist) / (Area of core)
![WhatsApp Image 2023-08-15 at 15 17 27(6)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/fe0e95d6-e99d-446b-9bac-915b95a972b2)
![WhatsApp Image 2023-08-15 at 15 17 27(4)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/57c10aa9-d8c0-4fd8-9fb6-541475e5d419)

3.  Aspect ratio = Height / Width
![WhatsApp Image 2023-08-15 at 15 17 27(5)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4b8de65e-e972-489b-b345-376bb4a6f2e8)


#### 1.2 Pre-placed cells
1.  Combinational logic output has multiple gates.
![WhatsApp Image 2023-08-15 at 15 17 27(3)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/600eb15b-9a0b-4485-a151-155371eb83ed)

   a. Divided as cut1 & cut2 which is separated as 2 blocks. IO pins are extended for connection.
   ![WhatsApp Image 2023-08-15 at 15 17 27(2)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/84f8e583-0cc7-4f41-ad88-810a7a84ad07)

   b. Blackboxes as two different IP's / modules. Users can implement separately for reuse.
2. IPs example: memory, clock gating cell, comparator, MUX. Plcaement is fixed before routing and automates PnR tools


#### 1.3 De-coupling capacitors
1. Discharge of capacitor should be handled by source voltage. This is due to wire resistance, the Vdd -> Vdd' and will not be detected as logic '1'.
![WhatsApp Image 2023-08-15 at 15 17 27(1)](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/fd6db1ce-bb31-4a71-b098-340730a55b83)

2. This region is noise margin. For detections, logic '0' -> '1' should be in NML and logic '1' -> '0' should be in NMH regions.
3. During switching, decoupling capacitors will send current to the circuit needed. When no switching happens, it gets charge from the source.
4. In the design, surronding block will have DECAPs placed and supply required current to the needed blocks.
![WhatsApp Image 2023-08-15 at 15 17 27](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/31f07d66-9ff4-4427-8eec-10e825807b6d)


#### 1.4 Powerplanning
1. Example of 16-bit bus where logic '1' is charged to Vdd and logic '0' is charged to Vss.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/22e1f884-854a-40b6-85b5-68aa39c4bbbe)

2. All capactors which were charged to 'V' volts, will have to discharge to '0' volts through single 'Ground' tap point. This will cause bump in 'Ground' tap point.
3. Initial bump due to multiple switching to '0'.
4. Moreover, all capacitors which were at '0' volts will have to charge to 'V' volts through single Vdd tap point. This lowering of voltage at 'Vdd' tap point is voltage droop. This happens due to a single power source.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9ea698de-c328-4760-8450-3a229ab97c92)

#### 1.5 Placement blockages
1. After the preplaced cells are fixed in the design, this will will create a blockage and make sure no other cell placed there.
2. Pins will be placed as well for the logic connections.


### 2. Library binding and placement

#### 2.1 Netlist binding and initial place design
1. Views of gates and given physical form from the netlist.
2. All components are done the same and in real time, the gates are in square / rectangle form only. They are placed in a shelf known as library.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8d8d65a0-8346-4875-b3a7-0e42135fa8bd)

#### 2.2 Optimize placement with wire length and capacitance
1. Cells are now palced as per the pins and logic and tracks.
2. Since preplaced cells are placed, the cells are placed far from the input pins.
3. Estimate the capacitance. Due to huge length, there could be loss of data, so repeater is added.

#### 2.3 Final placement optimization
1. Certain logics are abutted due to zero timing delay and high speed requirements
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/31f4d241-ccc3-47b7-802c-7736f478860e)

2. Setup timing analysis will be done to check placement.

#### 2.4 Library and characterization
1. Logic synthesis (.v/sdc) -> Floorplanning (data from .v as per connection) -> placement (depends on logic pin connections -> CTS (take care of clock to reach each logic) -> routing (stage where actual connection happens based on the logic connections).
2. Common in all the stages: Gates and cells which are collections of gate libraries represented to tool by .lef and .libs.


### 3.  Cell design and characterization flows

#### 3.1 Inputs for cell design flows
1. Library contains macros/ IPs, standard cells, ICG.
2. Different functionality and sizes with HVT, SVT, LVT.

#### 3.2 Cell design flow:
Example: Inverter design flow
1. Inputs:
   a. PDKs
   b. DRC and LVS rules: Foundry defines the rules for real time implementation
   c. SPICE: model parameters from foundry
   d. libs and user defined specs: Physical parameters like drive strength, height, metal layer, pin location

2. Design steps:
   a. Circuit design
3. 


## DAY 5: Final steps for RTL2GDS using tritonRoute and openSTA

### 1. Routing and design rule check

#### 1.1 Maze routing / Lee's algorithm
1. By using any two point to connect logics, routing should be done with less possible bends.
2. Algorithm creates routing grid for the two points. One is source and other is target.
3. It tries to label all the adjacent grids to its source with numbers in ascending order. 1 being the adjacent and number increases as the grid increases. Only horizontal and vertical grids allowed. No diagonal labelling.
4. Labelling will continuing under the placement blockages as well. Under die labelling will not occur.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c555f34c-080e-4be9-97ad-487a32019c25)
5. Now route the two points with the least possible bend.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5cc7f120-3aae-415d-acde-ae5595b1022c)
6. Limitation: when having millions of route, this algorithm will take lot of memory and time.


#### 1.2 Design rule check
1. 3 basic rules as per lithography requirement in fabrication:
   a. Minimum wire width
   b. Minimum wire pitch
   c. Minimum wire spacing
2. There are multiple rules given from foundry when checking the design.
3. DRC violation: Signal short.
   a. To solve this, the signal has to be re routed to other metal layers.
   b. Via width and spacing has to be checked.
4. Parasitic extraction:
   a. Each wire has certain resistance and capacitance value, which needs to be extracted after routing for timing analysis by STA tools.


### 2. Routing using TritonRoute

1. Global route:
   a. Routing grid is divided into rectangle blocks and is done by FastRoute.
   b. Routing guide for each net is created.
   c. Initial route guide -> Splitting -> Bridging -> Merging -> Preprocessed route guides.
3. Detail route:
   a. Output of FastRoute is actually routeguide for the detail route and is done by TritonRoute.
   b. Use of algorithm to find the best wire connectivity.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ab649e47-463c-4130-a615-51cc96476bf7)
