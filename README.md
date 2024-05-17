
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM:
```
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.
```
# APPARATUS REQUIRED:
```
Vivado™ ML 2023.2
```
# PROCEDURE:
```
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.
```
# LOGIC DIAGRAM:
# SR FLIPFLOP:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/a2c83e72-1d4e-4f9f-ad74-59e21f03f9d2)
# CODE:
```
  module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# OUTPUT:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/2b9dc1e9-45dd-4023-ac9f-29d3521b0cb7)
# JK FLIPFLOP:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/4c21b463-86fd-42e5-bfe0-10beacd72de1)
# CODE:
```
  module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# OUTPUT:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/f4961dd1-2293-406f-a925-ae239c689930)
# TFLIPFLOP:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/2bd5cc22-b9e8-43c5-bdfe-5e152c5e70e1)
# CODE:
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# OUTPUT:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/db7727a0-86ca-42fe-b408-0b12467ee926)
# D FLIPFLOP:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/277830a5-23e3-4147-8af7-3cb5ea8eb55c)
# CODE:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
# OUTPUT
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/a56341ae-5e6c-4a92-bed2-fa365e5758b1)
# COUNTER:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/924f9f35-ac19-44b4-ad55-48d46fceff13)
# CODE MOD 10 COUNTER:
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
# OUTPUT:
![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/9dfcfb65-0e77-49dc-a64d-15f75f3854e2)
# CODE RIPPLE COUNTER:
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# OUTPUT:

![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/c6f1f4e2-f1a1-483f-98eb-45281576b355)
# CODE UP DOWN COUNTER :
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
# OUTPUT:

![image](https://github.com/Devikavijaya/VLSI-LAB-EXP-4/assets/164987794/cc21bfe3-1e7a-47fe-b47d-0c35c4c078b2)

# RESULT:
```
Simulate And Synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN is Successfully Verified using Vivado Software.
```










