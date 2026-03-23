# Soc-design-and-planning-vsdiat
## overview
# VSDIAT Physical Design Workshop

This repository documents my hands-on learning and implementation of the VSDIAT Physical Design workshop using OpenLane.

## 📌 Objective
To understand the complete RTL-to-GDSII flow including:
- Floorplanning
- Placement
- Clock Tree Synthesis (CTS)
- Routing
- Timing Analysis

## 🛠️ Tools Used
- OpenLane
- Sky130 PDK
- Docker

## Section 1 
####  Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit
```
screenshots of command run
<img width="1920" height="947" alt="ol2" src="https://github.com/user-attachments/assets/97193d76-cd68-4112-aceb-81c89dc8a8c8" />
<img width="1920" height="947" alt="ol3" src="https://github.com/user-attachments/assets/ad36ff6c-5369-4465-bd04-157e5c19732e" />
####  Calculate the flop ratio.
Screenshots of synthesis  with required values highlighted
<img width="1920" height="947" alt="ol4" src="https://github.com/user-attachments/assets/6c30bf97-741d-4c55-b360-2fd96ec09dc8" />
<img width="1920" height="947" alt="ol5" src="https://github.com/user-attachments/assets/5fa40d6e-aea9-4aa8-a8ca-36c6b6caf556" />

Calculation of Flop Ratio and DFF % from synthesis statistics report file

Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429
```
```math
Percentage\ of\ DFF's = 0.094325 * 100 = 10.8429\ \%
```
## Section 2 
 Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane
```
```tcl
#since synthesis is already completed 
# Now we can run floorplan
run_floorplan
```
Screenshot of floorplan run
<img width="1920" height="947" alt="ol6" src="https://github.com/user-attachments/assets/4436f214-c07e-4a99-b5ee-0d755b3e966a" />
<img width="1920" height="947" alt="ol7" src="https://github.com/user-attachments/assets/83fdeace-a38c-494c-9c47-15e6430ad104" />

####  Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def
<img width="1920" height="947" alt="ol9" src="https://github.com/user-attachments/assets/a022269c-27bb-4ab1-912c-0fd046c1088c" />

According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

####  Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
Screenshots of floorplan def in magic

<img width="1920" height="947" alt="floorplan" src="https://github.com/user-attachments/assets/a0b7c211-de79-4bbb-bcec-379ab61c2614" />

<img width="1920" height="947" alt="fp cells" src="https://github.com/user-attachments/assets/a20dcf74-e9bb-495f-bd67-dd910649859a" />

<img width="1920" height="947" alt="ports" src="https://github.com/user-attachments/assets/66066fa5-f1df-4ecb-9ea3-abbac696246d" />


name of the selected cell in tikikon 
<img width="1920" height="947" alt="name of cell" src="https://github.com/user-attachments/assets/7361a56f-68ea-4a6d-943f-9c6b828ece5f" />

####  Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run

<img width="1920" height="947" alt="ol11 plc done" src="https://github.com/user-attachments/assets/0089063c-52f2-4b50-96f1-be1ca357b17b" />


####  Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic 

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of placement def in magic


<img width="1920" height="947" alt="ol 13 plc magic" src="https://github.com/user-attachments/assets/ce4d2a49-fd8e-4c41-b175-4754b178fdd6" />


<img width="1920" height="947" alt="ol13 std clls in mgc" src="https://github.com/user-attachments/assets/11826fc2-d4c6-4fd0-95a1-2c7e12b5a564" />


<img width="1920" height="947" alt="ol14 std cells info" src="https://github.com/user-attachments/assets/35904a2a-95af-4a46-aad2-5771bd26b917" />






























