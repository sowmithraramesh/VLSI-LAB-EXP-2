# SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

## AIM: 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

## APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

## PROCEDURE:
#### STEP:1  Start  the Xilinx navigator, Select and Name the New project.
#### STEP:2  Select the device family, device, package and speed.       
#### STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
#### STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
#### STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
#### STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
#### STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
#### STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
#### STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
#### STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
#### STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.



## ENCODER
### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)

## VERILOG CODE
```
module EC(e0,e1,e2,e3,e4,e5,e6,e7,d0,d1,d2);
input e0,e1,e2,e3,e4,e5,e6,e7;
output d0,d1,d2;
or g1(d0,e1,e3,e5,e7);
or g2(d1,e2,e3,e6,e7);
or g3(d2,e4,e5,e6,e7);
endmodule
```
### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-2/assets/166893766/403cbdf7-33c1-4835-9f83-ec6e1af0b506)

## DECODER
### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)
### VERILOG CODE
```
module dec3to8(d0,d1,d2,y0, y1,y2,y3,y4,y5,y6,y7);
input d0,d1,d2;
output y0,y1,y2,y3,y4,y5,y6,y7;
wire w1,w2,w3;
not g1(w1,d0);
not g2(w2,d1);
not g3(w3,d2);
and g4(y0,w1,w2,w3);
and g5(y1,w1,w2,d2);
and g6(y2,w1,d1,w3);
and g7(y3,w1,d1,d2);
and g8(y4,d0,w2,w3);
and g9(y5,d0,w2,d2);
and g10(y6,d0,d1,w3);
and g11(y7,d0,d1,d2);
endmodule

```
### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-2/assets/166893766/e60f5616-8741-4a63-a2d9-a53b4fd9ad24)

## MULTIPLEXER

### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)

### VERILOG CODE
```
module mux(a,s,y);
input [7:0]a;
input[2:0]s;
output y;
reg y;
always@({s,a})
  begin
      case(s)
        3’b000: y=a[0];
        3’b001: y=a[1];
        3’b010: y=a[2];
        3’b011: y=a[3];
        3’b100: y=a[4];
        3’b101: y=a[5];
        3’b110: y=a[6];
        3’b111: y=a[7];
endcase
end
endmodule
```
### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-2/assets/166893766/b460796d-facc-4276-a799-c4990f2367c3)

## DEMULTIPLEXER

### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)

### VERILOG CODE
```
module demux_1_to_4(
    input d,
    input s0,
    input s1,
    output y0,
    output y1,
    output y2,
    output y3
    );	
assign s1n = ~ s1;
assign s0n = ~ s0;
assign y0 = d& s0n & s1n;
assign y1 = d & s0 & s1n;
assign y2 = d & s0n & s1;
assign y3 = d & s0 & s1;
endmodule
```
### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-2/assets/166893766/1a8130e2-7fb9-4e8e-9516-cac4a3a0addb)

## MAGNITUDE COMPARATOR

### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)

### VERILOG CODE
```
module magcomp(a, b, eq, lt, gt);
  input [3:0] a,b;
  output reg eq, lt, gt;

  always @(a,b)
  begin
    if (a == b)
    begin
      eq = 1;
      lt=1'b0;
      gt=1'b0;
      end

    if (a < b)
    begin
      lt = 1;
      eq=1'b0;
      gt=1'b0;
      end
      
      
    if (a > b)
    begin
      gt = 1;
      eq=1'b0;
      lt = 0;
  end
  end
  endmodule
```
### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-2/assets/166893766/2a8d4714-79e6-499b-84cc-f759fc17964c)

## RESULT:
          Thus,The Encoder, Decoder, Multiplexer, Demultiplexer,Magnitude Comparator are implemented and simulated successfully using Xilinx ISE.


