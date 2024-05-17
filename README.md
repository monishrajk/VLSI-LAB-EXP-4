
### SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

### AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.2.

### APPARATUS REQUIRED:

VIVADO 2023.2

### PROCEDURE:
STEP:1 Start the Vivado, Select and Name the New project.<br>
STEP:2 Select the device family, device, package and speed. <br>
STEP:3 Select new source in the New Project and select Verilog Module as the Source type.<br>
STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.<br>
STEP:5 Select the Behavioural Simulation in the Source Window and click the check syntax.<br>
STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.<br>


### SR FLIPFLOP
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/1b2177a8-188e-4f48-b15a-d7c9b8593b3b)
### VERILOG CODE:
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/fde5adbc-d127-43c7-9c3a-c97e33c69621)

### JK FLIPFLOP
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/fe2a5529-43ac-4082-8cac-c76d3b0e7b7c)
### VERILOG CODE:
```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/b12acba8-0471-448a-8dc6-4bc19cde4bc3)

### T FLIPFLOP
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/697518d6-da49-48c9-85b5-91688460a237)

### VERILOG CODE:
```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/1d84bc96-d7b9-44bf-9f1b-b1793188a121)

### D FLIPFLOP
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/d09dddf0-3f9f-4e6d-9f69-3787c39000d2)

### VERILOG CODE:
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
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/0daf167d-d841-4311-8c4a-278de39d27c4)

### COUNTER
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/15be6215-2b4d-48e6-8f2e-d6932e27e3b0)
### UPDOWN COUNTER:
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/19856d87-24ca-4363-84aa-12799c6fecc6)

### VERILOG CODE:
```
module udc(clk,rst,updown,out);
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
### Output:
  ![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/fd74457f-1f35-4e94-a628-5efff9ba956f)

### Mod-10 Counter:
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/637add02-e848-4f74-a8b8-9e183a68df4b)
### Verilog Code:
```
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/20fb126a-6ff9-48a3-876f-64c9b710f28c)

### RIPPLE CARRY COUNTER:
### LOGIC DIAGRAM:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/c8966ae1-c506-4bfc-a6e3-028ea15d87a2)

### VERILOG CODE:
```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module rcc(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf2(q[1],q[0],rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```
### OUTPUT:
![image](https://github.com/Nandhak23/VLSI-LAB-EXP-4-/assets/160568515/9738870c-f3e1-40a5-87be-5a6cb680ca91)

### RESULT:
Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGN are simulated and synthesised using Vivado 2023.2.


