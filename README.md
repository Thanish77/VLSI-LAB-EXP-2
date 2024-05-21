# SIMULATION AND IMPLEMENTATION OF COMBINATIONAL LOGIC CIRCUITS

**AIM:** 

To simulate ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.2.

**APPARATUS REQUIRED:** 

VIVADO 2023.2

**PROCEDURE:**

1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

**ENCODER**


**LOGIC DIAGRAM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/2e8f1810-ca75-4699-9c0b-51048fa99931)

 
**VERILOG CODE**
```
module encoder(a,y);
input [7:0]a;
output[2:0]y;
or(y[2],a[6],a[5],a[4],a[3]);
or(y[1],a[6],a[5],a[2],a[1]);
or(y[0],a[6],a[4],a[2],a[0]);
endmodule
```
**OUTPUT WAVEFORM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/848b6dee-a959-4f43-bfd8-e2e33eb0cb4c)


**DECODER**

**LOGIC DIAGRAM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/eeaa2ee1-69ed-475d-ba0b-35793e3f6e9c)


**VERILOG CODE**
```
module decoder1(a,y);
input [2:0]a;
output[7:0]y;
and(y[0],~a[2],~a[1],~a[0]);
and(y[1],~a[2],~a[1],a[0]);
and(y[2],~a[2],a[1],~a[0]);
and(y[3],~a[2],a[1],a[0]);
and(y[4],a[2],~a[1],~a[0]);
and(y[5],a[2],~a[1],a[0]);
and(y[6],a[2],a[1],~a[0]);
and(y[7],a[2],a[1],a[0]);
endmodule
```
**OUTPUT WAVEFORM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/02b6f72e-c9c4-4098-b2ff-7ef56c9ca106)


**MULTIPLEXER**

**LOGIC DIAGRAM** 
 
![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/4b929430-dd40-49dd-b429-018c8305a317)


**VERILOG CODE**
```
module mux(s,c,a);
input [2:0]s;
input [7:0]a;
wire [7:0]w;
output c;
and(w[0],a[0],~s[2],~s[1],~s[0]);
and(w[1],a[1],~s[2],~s[1],s[0]);
and(w[2],a[2],~s[2],s[1],~s[0]);
and(w[3],a[3],~s[2],s[1],s[0]);
and(w[4],a[4],s[2],~s[1],~s[0]);
and(w[5],a[5],s[2],~s[1],s[0]);
and(w[6],a[6],s[2],s[1],~s[0]);
and(w[7],a[7],s[2],s[1],s[0]);
or (c,w[0],w[1],w[2],w[3],w[4],w[5],w[6],w[7]);
endmodule
```
**OUTPUT WAVEFORM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/2f86ed68-bd2d-47c6-9cfc-a89456b7ef75)

 
**DEMULTIPLEXER**

LOGIC DIAGRAM 

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/bcde5ecd-f84b-4b7c-8637-265dc53f43c1)

 
**VERILOG CODE**
```
module demux_8(s,a,y);
input [2:0]s;
input a;
output [7:0]y;
and(y[0],a,~s[2],~s[1],~s[0]);
and(y[1],a,~s[2],~s[1],s[0]);
and(y[2],a,~s[2],s[1],~s[0]);
and(y[3],a,~s[2],s[1],s[0]);
and(y[4],a,s[2],~s[1],~s[0]);
and(y[5],a,s[2],~s[1],s[0]);
and(y[6],a,s[2],s[1],~s[0]);
and(y[7],a,s[2],s[1],s[0]);
endmodule
```
**OUTPUT WAVEFORM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/1601743a-a87d-40b6-bc8a-5ddde297d927)

MAGNITUDE COMPARATOR

**LOGIC DIAGRAM** 

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/f9e418b2-b601-42ca-9c2c-a3d5273c0c7b)

**VERILOG CODE**
```
module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
 if (a==b)
 begin
  eq = 1'b1;
  lt = 1'b0;
  gt = 1'b0;
 end
 else if (a>b)
 begin
  eq = 1'b0;
  lt = 1'b0;
  gt = 1'b1;
 end
 else
 begin
  eq = 1'b0;
  lt = 1'b1;
  gt = 1'b0;
 end
end 
endmodule
```
**OUTPUT WAVEFORM**

![image](https://github.com/REkha18s/VLSI-LAB-EXP-2/assets/161815097/a2c7d3bb-72b2-40f3-aebd-c9611d3b407d)


**RESULT:**

   Thus the simulation and implementation of combinational logic circuit is done and outputs are verified successfully.



