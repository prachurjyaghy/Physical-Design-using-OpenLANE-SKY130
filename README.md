# Physical-Design-using-OpenLANE-SKY130
Advanced Physical Design Workshop using OpenLANE/SKY130

DAY 3: LAB SESSION
GIT CLONE of "vlsistdcelldesign"
  1. First go to the directory of vlsistdcelldesign on github.
  2. Clone the github repo "https://github.com/nickson-jose/vsdstdcelldesign.git" by the following command "git clone https://github.com/nickson-jose/vsdstdcelldesign.git"
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2591669a-ab7b-47b0-a9a7-c12d938a9062)

  3. After the cloning is completed, copy the tech file using the following: "cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/"
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ef076efc-74cc-4bd1-8958-7110816d13e3)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dbdad075-807a-4f08-bf76-a835f774d9f4)
MAGIC TOOL
  1. Open MAGIC tool to see the standard cell design in the cloned directory location. Command "magic -T sky130A.tech sky130_inv.mag &"
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/14614ce0-1c41-4506-a074-8c4ae7902230)

  3. In the tool, use 's' and 'v' simultaneously to center the cell design.
  4. To select any part of the design, hover the mouse pointer to it and click 's' to select it.
  5. On the right hand side, all the layers are described.
  6. Using 's' 3x will select the whole connection layer where the mouse is pointed in the design.
  7. Now in the terminal of MAGIC tool, after selecting any part of the design using 's', type 'what'. PMOS and NMOS has been decribed the terminal.
