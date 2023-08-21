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
2. Different functionality and sizes with HVT, SVT, LVT
   
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/93e734e5-a918-41a1-9413-9a7e54855466)


#### 3.2 Cell design flow:
Example: Inverter design flow
1. Inputs:
   a. PDKs
   b. DRC and LVS rules: Foundry defines the rules for real time implementation
   c. SPICE: model parameters from foundry
   d. libs and user defined specs: Physical parameters like drive strength, height, metal layer, pin location
   
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c9fb5a51-254d-41be-881f-8f6c6989fedd)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ae46084c-6759-464e-83bc-9a644fc680c9)


3. Design steps:
   a. Circuit design: as per value required parameters are udpated
   b. Layout: implement the values in design
   c. Characterization: helps to get the timing, noise adn power
   
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/0b12c6ef-b154-4e95-9b19-ebd746be69ab)



#### 3.3 Characterization flow:
1. Inputs:
   a. layout of buffers
   b. description og gate of buffer
   c. SPICE netlist
2. Read the model files
3. Extracted SPICE netlist
4. Recognise behaviour of buffer
5. Read the sub circuit of inverter
6. Attach the necessary power sources
7. Apply stimulus as pulse, etc
8. Provide necessary output capacitances
9. Necessary simulation commands (.tran, .dc)
10. Feed all the inputs to characterization software **GUNA** (Timing, Noise and Power characterization models will be created)

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/feb7d722-6b6e-4e2f-b12d-c0308cae4106)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/bb90b5aa-f06a-4ad4-bfcf-d18ccf8108b3)



### 4. General timing characterization parameters

#### 4.1 TIming threshold definitions
1. Slew threshold is calculated using the 20% of high / low values
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/04d71764-5103-430e-9e64-a8c4122e255a)

2. Rise and fall is calculated using the 50% of the high and low values
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/26a97e78-5fff-44a6-9268-d6a71c188f2f)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cd17cf41-815a-499e-b615-772fa6460adc)



#### 4.2 Propagation delay (using example output waveform)
1.  Delay = time(out_*_thr) - time(in_*_thr)
2.  Incase threshold values increase, then there could be negative delay
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/1bb21dbc-b0a3-4fad-8cbd-d3315b79aa97)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f64b3c93-6e85-46d5-8ed5-09bf6b437ae2)

3.  Slew rise/fall = time(slew_high) - time(slew_low)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/110ae12e-2a18-463d-80e2-d7751c053806)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/31a6c426-c1cd-4913-a58d-91a963d7074f)



## DAY 3: Design lib cell using Magic layout and ngspice characterization

### 1. SPICE deck creation for CMOS inverter

#### 1.1 SPICE deck creation
1. Component connectivity

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3a767605-2e5c-4693-b7c7-d65c3048eedd)

2. Component values

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c084b14c-6f50-44bf-8e58-64ecc8e86dd2)

3. Identify nodes

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6e7866ea-9e6d-4aec-abc5-8ed694a7c8f0)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5aea682f-a9b1-4594-b7a1-99e375d6e477)

4. Name nodes

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ba993fc8-d67a-4e7e-94d9-000ebfbd43bb)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/fa991e94-0b83-41fb-b38a-a71ec00618f3)

5. Model file "tsmc_025um_model.mod" contains all the tech files and has data of CMOS



#### 1.2 Switching threshold Vm
1. CMOS Inverter Robustness can be determined by the switching of the the threshold voltage, Vm
   a. Switching Threshold, Vm
   b. Vm is Vin = Vout in graph after a tangent is drawn

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f22edc48-0f8a-4011-9f36-91fcdd192a8c)

   c. Since current is flowing in same but differnt direction, therefore Vgs - Vds => Idsp = -Idsn
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2c22d5a9-5a69-4d9b-9a1c-f182cb3369ff)



#### 1.3 Static and dynamic simultation of CMOS inverter
1. For Dynamic simulation, we can replace the input by pulse waveform generator
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f1d482c8-c4e6-4de2-9772-748134555115)



### 2. Inception of layout of CMOS fabrication process (16-mask CMOS process)

#### 2.1 Create Active regions
1. Selecting a substrate
   a. Substrate doping should be less than 'well' doping
   b. Ex: p-type, high resistivity (5~50 ohms), doping level (10<sup>15</sup> cm<sup>-3</sup>)
2. Create active region for transistors
   a. Create isolation between every pockets
   b. 40nm of SiO<sub>2</sub>
   c. 80nm of SiN<sub>4</sub>
   d. 1um photoresist (-ve/ +ve film). Defines regions. **Mask 1** is the protection region for exposure avoidance using photo-lithography
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6adb9905-968c-4791-8340-1c6b8f1f990c)
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/bf224db3-dc31-4fd1-8561-f724eb4d73bc)
   
   
3. After UV light
   a. The photoresist layer will be etched off
   b. With chemical solution, the Si<sub>3</sub>N<sub>4</sub> layer photoresist layer is removed
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ba9b7d02-7bef-408d-adca-a4ffb742060f)

   c. In oxidation furnace, the SiO<sub>2</sub> will grow (known as isolation area). The process is called **LOCUS**
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3dc7a15b-f5fb-401c-b9f9-b06c16808989)



#### 2.2  Formation of P & N well
1.  N & P well formation. **Mask 2** will be used now.
2.  After photoresist, using mask and UV light, the photoresist is cleared.
3.  Then **Boron** (p-type impurity) ion-implementation creates P-well. This implemntation passes through SiO<sub>2</sub> layer
4.  Similar for n-well, using **Mask 3**, **Phosphorus** (n-type impurity) ion-implementation creates N-well
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/b72d7cba-8336-4c4a-8273-e753020a6899)

5.  Then push the whole into driving furnace to create wells into the substrate
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8ee1a343-71b4-4cab-9acf-6d1e7aadcba4)



#### 2.3 Gate formation
1. Doping concentation and oxide capacitance
2. Using **Mask 4** and **Boron** ion-implementation (low energy) to create doping concentration P-well
3. Using **Mask 5** and **Arsenic** to creating N-well
4. Fix the oxide by etching original using **HF**(Hydrogen Flouride) solution. This regrows quality oxide layer thickness as per threshold voltage requirement.
5. Polysilicon **Mask 6** creates gate

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5ef6f09e-2e9c-4b68-86bf-56da0e49a58d)


#### 2.4 LDD formation (Lightly Doped Drain formation)
1. Attain doping profile for PMOS (P+, P-, N) and NMOS (N+, N-, P). The P- and N- regions are created for Hot electron effect and short channel effect
2. **Mask 7** and **Mask 8** is created for the doping profile
3. Plasma anisotropic etching is carried out

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ad51c2da-ee2a-46e8-8981-ae224cd11841)


#### 2.5 Source and Drain formation
1. Thin screen of SiO<sub>2</sub> to avaoid channeling dueing implants
2. **Mask 9** and **Mask 10** is used to create **P+** and **N+** implants
3. Put in furnace which is called *high temperature anealing*

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4c1f3b17-889b-411b-a89a-c3eaac1968f1)


#### 2.6 Formation of contacts and interconnects
1. Remove the SiO<sub>2</sub> screen with **HF** solution
2. Deposit titanium using sputtering on wafer surface. Heat in N<sub>2</sub>
   a. TiSi<sub>2</sub> layer is created for metal contacts
   b. TiN is created for local contacts

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8edb37f8-fdcf-4c63-a8f1-ccb3f7bf45cb)


#### 2.7 Higher level metal formation
1. **Mask 11** is used to form metal contacts. It consists of 1um of SiO<sub>2</sub> with phosphorus and boron deposited
2. **Mask 12** is used to form sapce for interconnects

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c0558f86-475c-463f-afaf-2c0ed25c8361)

3. **Mask 13** is where **aluminium** metal is used for interconnects
4. **Mask 14** defines the contact holes
5. **Mask 15** is used to define patern for third level of interconnects. This is dilectric SiN<sub>4</sub> to protect chip
6. **Mask 16** is used to open contact holes

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4eb79061-8de2-4420-bb09-ef9e1f7d066e)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4ae0d86d-1698-45eb-982d-bf78f6d115aa)




## DAY 4: Pre-timing layout analysis and importance of good clock tree

### 1. Introduction to Delay tables

#### 1.1 Delay tables with examples
1. Delay tables helps to create the propagation delays from one logic cell to another
2. Assume capacitance at nodes:
   a. Buffers in same level to be of same size
   b. Ouput capacitance is not contant and varies at each buffers and also varies the input transition at buffer inputs
   c. To capture the above, delay tables were created for each type of cells
3. Size: W x L ratio for Buffer '1' and '2' sizes. These are internal PMOS and NMOS
4. For respective delay as per the input , take example for 40ps from the below snap. Equation is used
5. For high Fanout, delay propagation happens and can increase the skew.
6. Under specific condition, the clock propagation can be stopped

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5f33b452-1ce2-4430-9661-a254a8b6c8da)
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/46db8bcd-dc84-494c-b0ed-c7601d22c5ec)
   

### 2. Setup timing analysis and FR setup time 

#### 2.1 Setup analysis using Single clock
1. When ideal clock is used, the clock tree is not built yet
2. On Zeroth clock, 1 clock edge that reaches the Launch Clock
3. On Tth clock, 1 clock edge that reaches the Capture Clock
4. Check this out with an example:
   a. Assume Combinational Logic delay as 'theta'
   b. For circuit to work, 'theta' < T
   c. When clk = 0, data reaches to Q<sub>m</sub> from D in the MUX
   d. When clk = 1, MUX1 output is given as feedback to input and then Q<sub>m</sub> goes to MUX2
   e. Time required by the Capture Clock for the Combinational Logic data before the next clock edge is checked

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3c00e3e2-aaea-4fe8-9974-053dd3945822)
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5f497650-f75f-4f0a-a186-8ebdc6bb75d8)


#### 2.2 Setup analysis adding Uncertainity/ Jitter
1. Jitter is when the clock source (PLL) might have variation, which can give clock edge between 0 and T ns to arrive early or late. It could be temperature variation of clock period
2. Uncertainity is considered as the combination of the variations in the clock signal
3. So we can now have to add the uncertainity to the previous Setup analysis

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cf6b177e-e1fe-47a5-a46a-f9dc699bd32e)

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5fabe468-0bf7-47b4-b385-9a7e9918be04)


### 3. Clock tree routing 

#### 3.1 Buffering using H-tree
1. Differnce between Capcute Clock and Launch CLock path is 'SKEW'
2. Repeater for clocks ahve equal rise and fall times
3. With addition of Buffer, the clock from port reaches the Flip-Flops so that the clock data is reproduced at Flip-Flop

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/41217386-94b5-4e4e-b526-9f7a44103dc9)


#### 3.2 Crosstalk and clock net shielding
1. Shielding is the protection for the clock net to reduce the crosstalk or coupling. They are either connected to VDD or VSS. Only the critical clock nets are shielded or else it could increase area
2. Crosstalk is the coupling between 2 long wires, which adds delay due to switching
3. Glitch is caused when VDD droop to the coupling wire i.e victim. Logic might change the result that it was expected to produce

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/0e944d43-181d-43dd-bd24-6eb0374853a1)



### 4. Timing analysis with real clocks using openSTA

#### 4.1 Setup analysis with real clocks
1. Check the example and calculate the Combinaltional Delay delay 'theta'

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3534f33b-4f4d-472e-a090-c4a812ff6b97)

2. Combinaltional delay will now add the clock network delay as well where the buffer from the source clock is also considered

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/917e9665-204a-410e-8975-5382a43f01eb)

3. The initial clock period will add the 'delta' 1 and 2 in it to accomodate the buffer delays

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c6687b47-fc95-449f-94cf-2969c81e0054)

4. Actual delay diagram for the clock path

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/1b9d7e70-8951-44ee-b818-400061e4859d)



#### 4.2 Hold analysis with real clocks
1. Check the example to calculate the data

   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2e63744e-d446-4768-8f36-0c40e86110b3)

2. Since data is in the Flip-Flop, time required to send Q<sub>m</sub> to Q is the MUX2 delay. It holds the data before the next clock arrives
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/399296bc-a6db-46ec-ab4a-caafe5dea6f5)

3. Check the SKEW
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dcf13302-da65-4576-84f4-ef763ae98cc0)

4. Actual delay diagram for the clock path in hold
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e4b1902c-c470-4b8f-a1ed-408098474b64)

   > For common clock paths, CPPR (derates) for the OCV factors are considered and added to the clock path. This factors in the real time fabrication factors.




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
