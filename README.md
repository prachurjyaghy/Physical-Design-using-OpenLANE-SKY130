


# Physical-Design-using-OpenLANE-SKY130
**Advanced Physical Design Workshop using OpenLANE/SKY130**

## DAY 3: LAB SESSIONS

### GIT CLONE of "vlsistdcelldesign"
  1. First go to the directory of vlsistdcelldesign on github.
  2. Clone the github repo "https://github.com/nickson-jose/vsdstdcelldesign.git".

  Command: `git clone https://github.com/nickson-jose/vsdstdcelldesign.git`
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2591669a-ab7b-47b0-a9a7-c12d938a9062)

  4. After the cloning is completed, copy the tech file.
  
  Command: `cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/`
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ef076efc-74cc-4bd1-8958-7110816d13e3)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dbdad075-807a-4f08-bf76-a835f774d9f4)

### MAGIC TOOL
  1. Open MAGIC tool to see the standard cell design in the cloned directory location. Also the tkcon terminal for MAGIC will open.

  Command:
  `magic -T sky130A.tech sky130_inv.mag &`
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/14614ce0-1c41-4506-a074-8c4ae7902230)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3b1c391e-f467-48de-a439-3fa26ebebf46)

  2. In the tool, use 's' and 'v' simultaneously to center the cell design.
  3. To select any part of the design, hover the mouse pointer to it and click 's' to select it.
  4. On the right hand side, all the layers are described.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9b617de5-b883-476a-9aaf-c2b659d6da9f)

  5. Using 's' 3x will select the whole connection layer where the mouse is pointed in the design.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/d1dc4152-199f-4271-94f6-53497b3decf2)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/76368cf5-b155-4800-a2dc-d76c42eee9ce)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8e131995-dd88-4026-a160-0f2e152e9b90)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3fb5087b-a2c0-4659-8a1e-38e2796e193a)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/09b547c1-251a-4a6f-bb40-fab04d1a41c5)

  6. Now in the tkcon terminal, after selecting any part of the design using 's', type `what`. PMOS and NMOS has been decribed the terminal.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c96cc201-e20d-4723-90a5-ef728a66ec31)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/079e8873-9579-443f-919d-664035806852)

  7. Go through the vlsistdcelldesign for more details on the cell design of the cloned github.
  8. MAGIC tool is also a DRC check tool and the design always has to be DRC clean. It can highlight the same and errors will be shown in the terminal.
  9. To know the logic, it has to be extracted to SPICE in ngspice:

     a. In the vlsistdcelldesign directory, use `extract all`.
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ea0a5ebd-ca49-47c7-9264-e939f0ac2b80)
     
     b. Extracted file is created with .ext.
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/206acbb3-32eb-456d-961a-90fdd484b4d6)
     
     c. To use in the **ngspice** tool: `ext2spice cthresh 0 rthresh 0`. Does parasitic extraction as well.

     d. To create .spice file : ext2spice
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/51f06562-4ca8-486e-bfad-c01c49664d65)
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e1251cd7-141a-4f70-83ca-da223dad0062)
        > In the .spice file:
        > Contains the details of the PMOS and NMOS and its connection. Update the .spice file as below which includes the pshort and nshort libs, scale, pulse input and transient analysis commands.
        > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/643d6892-ac72-451f-ba65-7930ef5180fc)
        > If file not updated as above, then the below error could be shown for sub ckt
        > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/20fbaa5f-38a9-4b76-804a-379125349f67)

     e. After the file is saved, invoke the .spice file in ngspice `ngspice sky130_inv.spice`. If ngspice not available, use `sudo apt install ngspice`.
     ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ae7b999a-aa26-422c-bf94-22ab8a098e9d)

     f. 
     g. 
