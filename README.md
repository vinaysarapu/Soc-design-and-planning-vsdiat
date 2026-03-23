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
<img width="1920" height="947" alt="ol 1" src="https://github.com/user-attachments/assets/b0c5b808-aceb-43c7-a9a6-f9a92022fdbb" />






