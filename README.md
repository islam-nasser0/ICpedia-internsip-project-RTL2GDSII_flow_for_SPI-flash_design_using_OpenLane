# RTL2GDSII_flow_for_SPI-flash_design_using_OpenLane
## Introduction 
We have the “wbqspiflash” design, and we want to perform RTL2GDSII flow  (logic synthesis and proceed through physical synthesis steps)
## Target
Close timing and DRC with the minimum die area and maximum frequency possible, we want to sell the chip, so we don’t trap with high frequency and the chip doesn’t 
operate because of timing violations 
## PDKS
Sky-Water 130nm

## BEFORE STARTING
I had big problem with STA after synthesis it run in the 
typical corner only not all corners and that make me relaxed with timing in all 
phases and shocked me in signoff.
### Solution:
• Start from flow.tcl (search for run_synthesis proc) I didn’t find it.
• Grep it the found it in scripts/tcl_commands/synthesis.tcl
• With some tracing run_sta proc founded and has a switch of (-pre_sta)
• Grep for run_sta to find in scripts/tcl_commands/sta.tcl and has two flage 
(-pre_sta , -multi_corner)
• I back to run_sta proc and change the switch to -multi_corner and it works 
Alhamdulillah.


![image](https://github.com/islam-nasser0/RTL2GDSII_flow_for_SPI-flash_design_using_OpenLane/assets/111699435/99a30b06-39c9-41b1-be43-b67e9b36ca38)

### Conclusion → We can run multi-corner static timing analysis after synthesis.


## Workflow:
- Change configurations of phases (synthesis, floorplan, Power plan, …) to specify your design constrains
- Configurations are being called by commands in separate files and commands are being called by scripts of tools to run the flow    
- The flow is iterative you change in configurations to reach the optimal tradeoff you accept 
- I run 10 iterations to reach the acceptable numbers I satisfied with, you can find all details in GitHub 
- Finally stream GDSII using Magic and view it using Klayout
  
## Project iterations

![image](https://github.com/islam-nasser0/RTL2GDSII_flow_for_SPI-flash_design_using_OpenLane/assets/111699435/3137a31b-4d8a-478a-af6d-39c3cf4e4cb0)


## iteration 1

![image](https://github.com/islam-nasser0/RTL2GDSII_flow_for_SPI-flash_design_using_OpenLane/assets/111699435/01c1c574-007e-452d-ad96-a49a2ec86b22)

## iteration 2


## iteration 3
## iteration 4
## iteration 5
## iteration 6
## iteration 7
## iteration 8
## iteration 9
## iteration 10
## iteration 11


## Results
clock period = 12ns with slack 0.11ns and core area = 41367um2


