# ***_Sign-off-Timing-Analysis_***

***

# **_Table of Contents_**

## [Introduction]()

Static Timing Analysis (STA) is a technique used in digital circuit design to evaluate the timing characteristics of a circuit. The objective of STA is to ensure that a design meets its timing requirements, which are typically expressed as constraints on the minimum and maximum delays of critical paths in the circuit. STA is a critical step in the design process, as it helps ensure that a circuit will operate reliably and meet its performance requirements. It does not depend on test vector or a test bench, rather uses mathematical techniques. It only works with synchronous systems and does not do logical simulations.

OpenSTA is an open-source software tool used for Static Timing Analysis (STA) in digital circuit design. The inputs to STA are Netlist, constraints and logic library. STA breaks the path as Ports and Sequential Elements. 

## [OpenSTA]()

Let us take an example of the verilog file attached below. These contain inputs, outputs and wires. NAND, NOR, INV cells have been used, which are defined by the standard cells which is in the same directory. 
![verilogfiled1](https://user-images.githubusercontent.com/54993262/220512324-9c6418ed-2d64-40d0-9cd8-9673d4894e9f.png)

This is the snapshot of the liberty cell:
![lib_nand](https://user-images.githubusercontent.com/54993262/220512884-fcaa687b-30b4-4217-b14e-c36da3617802.png)
It also contains the name of library, name of technology, the units and PVT values. The liberty file contains information regarding the cell area, capacitance, leakage power etc.  

Now we have to run the TCL script. Here we have to mention the SDC file, which contains the design constraints & timing constraints
![Day1-tcl-script](https://user-images.githubusercontent.com/54993262/220513073-747647dc-2841-4788-a35f-1024a9a9c90c.png)

The output is as follows:
![correctop1](https://user-images.githubusercontent.com/54993262/220513513-8ec86863-cb19-4066-8b26-4a7ea748e8d2.png)
![correctop2](https://user-images.githubusercontent.com/54993262/220513525-8daeb71f-1da4-408a-8c6c-2e55de4e3b84.png)
![correctop3](https://user-images.githubusercontent.com/54993262/220513519-54adeafa-22a3-4e51-94c6-587659ea7b5e.png)

It shows if the slack is met or violated. 

## Components of Timing Path:
* Start Point
* End Point
* Combinational Logic

## Slack Calculation
Slack = Required Time - Arrival Time

Positive slack indicates that the data arrives earlier than the required time. 

## Timing Constraints
These are specified in the Synopsis Design Constraints Format

![image](https://user-images.githubusercontent.com/54993262/220515387-a6b6e513-01c7-40d6-9925-bfc4c10f6895.png)
The first line of code generates a clock of period 10, and gives the info regarding the rise and fall times.

## To find the number of cells 
One option is to write a python script:
![python_script](https://user-images.githubusercontent.com/54993262/220517728-12031387-c00b-4f1c-82e9-f57697567677.png)

Other is to use the following command
![image](https://user-images.githubusercontent.com/54993262/220518732-61bca606-9305-4032-8b8a-087760c4e659.png)
![image](https://user-images.githubusercontent.com/54993262/220519431-de054c7f-e05a-4372-bf2f-41b09e0d1a6e.png)

Pins of Nand2
![image](https://user-images.githubusercontent.com/54993262/220526363-31a9e9b1-f1f3-4516-9411-6dfadd2b0dd1.png)
![image](https://user-images.githubusercontent.com/54993262/220526586-758b073e-c7bf-4dec-855e-ee2524d8a736.png)

The capacitance of a Nand2 and Nand3 would be different

STA 
* Setup and hold check, clock gating check, Async pin check, data to data checks.
* Apart from timing, even Design Rule Check also done by STA. 
  Slew is calculated from 30% VDD to 70% VDD. 
* Load Analysis - Maximum and minimum capacitance on Ports and Nets. Fanout Load capacitanceon Ports and Output pins
* Clock Skew Analysis - Skew is difference in delay between clocks at different point. Positive skew indicates more delay in capture than launch. 
* Pulse Width Check - The clock gets shrinked when the clock travles through the path. It becomes narrower then there is a pulse width violation. 

## SPEF File
Standard Parasitic Exchange Format(SPEF) file describe parasitic information w.r.t design. It is automatically generated by the tool. read_spef can be used to read it. 

