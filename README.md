# Traffic_Signal_Controller
Verilog implementation of a Traffic Signal Controller for making real life decisions between highway and country roads to control the flow of cars on different roads.

This project implements a traffic signal controller for a highway (hwy) and country road (cntry) using a finite state machine (FSM). The controller detects vehicles on the country road (x) and adjusts signals accordingly. In this project, the hwy signal is always green and the cntry signal is always red until a car (x=1) is detected on the country road in which case the hwy signal turns red and the cntry signal turns green. Once all the cars have passed and there is no car (x=0) on the country road, the hwy and cntry go back to their original state. All these transitions of the hwy and cntry signals take place along with the approprirate real life time delays which can be seen in the output waveforms.

# Module Details (sig_control.v) - Inputs & Outputs
|Signal|Direction|Description|
| ------------- | ------------- | ------------- | 
|clk	  | Input	 | Clock signal (Simulation: 10ns cycle).|
|clr	  | Input	 | Active HIGH reset.|
|x	    | Input	 | Car detection on country road (1 if car is present).|
|hwy	  | Output | 2-bit traffic signal for highway.|
|cntry |	Output | 2-bit traffic signal for country road.|

# Traffic Light Encoding
|Light|Binary Code|
| ------------- | ------------- |
|RED	   | 00|
|YELLOW  | 01|
|GREEN	 | 10|

# Finite State Machine (FSM)
|State	| Highway Light | Country Road Light  | Transition Condition|
| ------------- | ------------- | ------------- | ------------- |
|S0    |    GREEN	      |     RED	            | Car detected (x=1) → S1|
|S1	   |   YELLOW	      |      RED	          | Delay (Y2RDELAY) → S2|
|S2	   |    RED	        |      RED	          | Delay (R2GDELAY) → S3|
|S3	   |    RED	        |     GREEN	          | No car (x=0) → S4|
|S4	   |    RED	        |    YELLOW	          | Delay (Y2RDELAY) → S0|

The module sig_control.v is made using these above FSM conditions and parameters and then it is tested using the testbench module stimulus.v in which the proper working of the module can be checked using these above conditions.
