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








