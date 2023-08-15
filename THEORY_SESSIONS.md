# THEORY SESSIONS
## DAY 1: Inception of open source EDA, OpenLANE and Sky130PDK

### How computers talk

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


### RISC-V introduction

RISC-V Instruction Set Architecture (ISA): C propgram is written and compiled to assembly language programs (RISC-V) and then converted to computer language (Binary) for the computer layout (q flow).
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e39b454b-92c4-4b24-862f-9dfb82974abf)


### How application software interacts with Hardware

1. RISC-V ISA is introduced to the system software to interpret and transform the set of instructions to be read by the harware
2. Inside the system software, RTL code is then given to the synthesis tool and the RTL synthesis is created.
3. Physical design implementation of picrov32 takes place.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ce0ad461-547a-44b1-8fe7-ba29d03c4042)
