


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
> For more information and working of MAGIC, go to "http://opencircuitdesign.com/magic/index.html"


### NGSPICE

  1. After the file is saved, invoke the .spice file in ngspice `ngspice sky130_inv.spice`. If ngspice not available, use `sudo apt install ngspice`.
     ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ae7b999a-aa26-422c-bf94-22ab8a098e9d)
  2. Plot the graph using `plot y vs time a`.
  3. Calculate the cell rise and fall delays for PVT characteristics.
     ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/10187b06-394c-4361-a434-f01b2929d053)



## DAY 4: LAB SESSIONS

1. Go to the tracks.info file to check where the routing will happen in the metal layer.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dab60563-7fc9-418e-b80f-be779e7f0786)

2. Update the grid in the MAGIC tool using the tckon terminal as per the tracks.info data.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2acfb577-fd87-4d33-9d4a-6b6954a853e1)

3. Now to update the width of the standard cell. Should be odd multiple of x pitch.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/41eef897-e280-498b-ab5c-18e2fbb6839b)

4. Ports can be defined by selecting the port and then Edit >> Text..
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9a745d78-7f3f-47e6-be71-8aa83c8f8fe8)

5. Before extracting LEF, save the cell as `save sky130_vsdinv.mag`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ca93edd8-53e4-4dc3-acc1-817f575cb470)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f44b6453-a882-47e7-b431-971a438280f0)

6. Open the saved file and create the LEF using `lef write` in the tckon terminal.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/a2fcfda2-c56f-47d3-a593-2ca178a6b95c)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3c13c73a-164a-4f82-8e1c-a5e6f33454ee)

7. As the port A was enabled, it creates it as pin.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/50f10d6c-572d-41c4-b992-2ce64de7577d)

8. Now this lef file will be moved in the src folder for the picorv32a to use.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/778b2c18-9c91-4105-b8b3-7321edfa01b9)


### OPENLANE

1. To use new cell in synthesis, will check the lib files. The libs are different as per process corners. 
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9b1b7726-13f3-441a-af2b-8201a87117d8)

2. Copy the libs to the src location.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4721df9e-6520-4ef4-ac4b-6ab553153d46)

3. Modify config.tcl as following.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e9c2360e-3b25-4a7a-bfef-c1f4bfd4bb44)

4. Now using following commands start the OPENLANE tool.
```
docker
./flow.tcl -interactive
package require openlane 0.9
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6af3cf5b-48b7-427b-9f6e-d250d1405583)

5. Now using `prep -design picorv32a -tag 09-08_16-0 overwrite` the updated config will be used. Then provide the following commands.
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f3dc80cb-8532-4ecf-85c9-c6b34e0cb7e1)

  > If error is show as below for the FASTEST and SLOWEST, update the LIB_MIN and LIB_MAX to LIB_FASTEST and LIB_SLOWEST simultaneously.
  > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e10677f5-c484-4565-8376-3d22110c76d9)

6.  Run systhesis using `run_synthesis`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ea21fb90-e5ea-4d13-a718-b0746a444eb9)

7.  Make modification in the flow.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/7c6d5fcc-f7aa-46a5-8654-caff17f57745)

8. Run floorplan. Use `run_floorplan`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/072845b4-b03b-4f0c-9df4-be0f1bca42c6)

  > If errors found for run_floorplan, follow the commands one by one:
  > ```
  > init_floorplan
  > place_io
  > global_placement_or
  > tap_decap_or
  > run_placement
  > run_cts
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cd8580d4-a201-409d-a463-f0a0b788902a)
  > gen_pdn
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6f835a1f-16a1-4bc0-b512-ed2b2ab94a8d)
  > run_routing
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/10f2d841-610d-4a99-ac63-8e89dc710dd5)
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3fa662d3-d2f5-4438-98d3-e0b7c02c5f75)
  > ```     
  
9. Now go to the placement location of the run and then read the lef and def in MAGIC. Zoom into the cells and find the 'vsdinv' cell and `expand` after using 's' on the cell.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/bdcdd921-2e04-44fa-9273-700d3cde4fbe)


### OpenSTA (Engine integrated with Openlane)

1. Create a new sdc 'mybase.sdc' using gvim and update the following in it.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/102088cf-8d26-44fb-9645-ecabc42831bc)

2. Now create a pre_sta.conf file using gvim and update the following in it.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/691bdfa3-4143-4c42-8842-8b453d9f4f74)

3. Invoke the OpenSTA using the pre_sta.conf file in the openlane directory. Command: `sta pre_sta.conf`
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c7cd4814-6c4b-4024-a9d1-5cd9528ce520)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6ff174f9-d581-4d8d-be36-6b3bc4b8294e)


4. Set `set ::env(SYNTH_FANOUT) 4` in the openlane tab for the above STA run to reduce the slack.
  We can check the connections of the net.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/15239466-10bf-4c4b-b1c4-e22aaaf38994)

5. Replace cell as per requirement to increase the size with the command `replace_cell _13160_ sky130_fd_sc_hd__o2111a_4` . To check reports use `report_checks -fields {net cap slew input_pins} -digits 4`. Resize any cells as per requirement to reduce the slack in the reports.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3ec914f6-e505-4774-8fce-39002583882a)

6. If require to check the timing report through a net from startpoint to endpoint, use `report_checks -from _27860_ -to _27762_ -through _13165_` . This will help to check the report for the specific path.

7. Replace the synthesis path in the run directory with the updated timing run data using `write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/synthesis/picorv32a.synthesis.v`. This replaces the existing verilog with the updated timing verilog.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e278a75c-612f-4b38-806d-d265e7f02f05)

8. Verify the replaced cell in the netlist for verification. Ex: use the cell instance _13160_ and check if the resize happened. It should increase from 2 to 4 size.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/89e32cd5-7533-4604-be26-3d153408d9ec)

9. Run the floorplan `run_floorplan` and placement `run_placement` without the synthesis now or it will update the netlist again. 


### TritonCTS

1. Once placement is completed move on to CTS stage, check the README file in configuration directory for the variables. Run CTS `run_cts`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/73260b0f-f4e2-43f4-9558-834abe596481)

2. In TCL, TCL proc - defination are made in flow and called during runs.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/d3a4d5fa-f197-445e-9c1c-30c38b1250b5)

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/b07cad66-663e-45c2-b914-5022cb6ffab2)
  
  > As per flow, synthesis in not part of the openroad scripts whereas others all are present.
  > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6e08172d-6fcc-4c93-be6d-6edcccc91562)

3.  Inside the or_cts.tcl, we can check the variables using `echo`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6c303434-8565-4193-bda3-da20845dc456)


4. Inside the same or_cts.tcl file, clock_tree_synthesis where the **TritonCTS** engine is used and the control is passed to it.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/747733ea-067f-4cd0-94d3-bae1e239cf59)

5. Check the clock buffers used.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c02f28d0-a36e-43e5-a3a0-e263db1af7e6)

  > Current drawback for TritonCTS - it cannot create optimized CTS for multiple corners.
6. Compare the CTS_MAX_CAP from the tcl script and the typical lib.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/66668371-0075-4e2c-90f1-075c476aafd7)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3794131a-cb67-4eaf-a0e5-fddec107ec40)


### OPENROAD

1. Invoke the openroad `openroad`. As we are inside the openlane, we can use the variables.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/328d9199-696a-44f7-9b8b-e681f111a863)

2. Timing analysis is done after creating db using the lef and def files and only once is required to be created. Post cts def to be used.
```
read_lef /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results/cts/picorv32a.cts.def
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/1f7e79be-0436-4c23-9958-6f4af6405a1e)

    > NOTE: as we have invoked the openroad in its directory, no need to provide the full path or else will face error.
    
3. Create the db file.
```
write_db pico_cts.db
read_db pico_cts.db
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6c05ff3b-3612-4988-af94-841801b84a9a)

4. Follow the same statements as in the .conf file.
```
read_verilog /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results//synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -min $::env(LIB_FASTEST)
read_sdc /openLANE_flow/designs/picorv32a/src/mybase.sdc
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cb4cc9da-2939-4399-9752-14bd86a3cfa1)

5. As clocks have been built, the propagated clocks will calculate the actual cell delay in the clock path and check the reports.
```
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/549d68d6-562a-467e-8c5f-51446e948cb8)

6. As per the above commands, we are using 'min_max' by using the 'typical' lib only. So exit and load openroad again.

7. Now to do analysis for the 'typical' library.
```
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results//synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/mybase.sdc
set_propagated_clock [all_clocks]
```

8. Now check the report again. Use `report_checks -path_delay min_max -fields {slew trans net cap input_pin} -format full_clock_expanded -digits 4`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4ec6f47d-add1-4da7-9e93-df5cee290db9)

   > **Example: Updating the clock buffer list to remove the 'clkbuf_1' and add it again.**
   > In TCL, lreplace does not overwrite the list. So need to write into the list `set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]`. Run cts after this `run_cts` to check the modifications.
   > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/95f0167b-7a8b-4022-b9fb-620fb6ed0f24)
   >
   > TritonCTS will hang, check the process using `top`. Kill process `kill -9 <PID>` for openroad.
   > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6bae4397-3740-467d-a61a-a44973e8207c)
   > 
   > Check the CURRENT_DEF variable which is set to the post cts def. Use `echo $::env(CURRENT_DEF)`
   > 
   > Use the def after placement `set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results/placement/picorv32a.placement.def`
   > 
   > Check `echo $::env(CTS_CLK_BUFFER_LIST)` and run_cts. Then follow the commands in Step 7. Check the slack using `report_clock_skew -hold` and `report_clock_skew -setup`.
   > 
   > To add the clock buffer again into the list, `set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]`


## DAY 5

### Power Distribution Network (PDN)

1. Invoke openlane and check the CURRENT_DEF `echo $::env(CURRENT_DEF)`. Use gen_pdn
