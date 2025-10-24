# Exp-6a.-Finite-State-Machine-for-Sequence-Detector-1011
# Aim 
To design and simulate a Finite-State-Machine-for-Sequence-Detector-1011 using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required 

Vivado 2023.1 

# Procedure

Launch Vivado 2023.1 Open Vivado and create a new project.
Design the Verilog Code Write the Verilog code for the RAM,ROM,FIFO
Create the Testbench Write a testbench to simulate the memory behavior. The testbench should apply various and monitor the corresponding output.
Create the Verilog Files Create both the design module and the testbench in the Vivado project.
Run Simulation Run the behavioral simulation to verify the output.
Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.
# Code
# Mealy 1011
// Verilog code
```
module mealy_fsm_1011(
            input clk,rst,xin,
            output reg zout
        );
        parameter [2:0] s1 = 3'b000,
                        s2 = 3'b001,
                        s3 = 3'b010,
                        s4 = 3'b011;
       reg [2:0] ps,ns;
 always@(posedge clk)
   begin
      if(rst)
          ps <= s1;
      else
          ps <= ns;
   end      
 always@(xin or ps)
     begin 
         case(ps)
           s1 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end 
           s2 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end             
           s3 : if(xin) begin
                     ns = s4;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end              
           s4 : if(xin) begin
                     ns = s1;
                     zout = 1;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end              
       endcase
    end
endmodule
```

# Test bench
```
module mealy_fsm_1011_tb;
        reg clk_t,rst_t,xin_t;
        wire zout_t;
        
        mealy_fsm_1011 dut(.clk(clk_t),.rst(rst_t),.xin(xin_t),.zout(zout_t));
           
     initial
        begin
            clk_t = 1'b1;
            rst_t = 1'b1;
          #100
            rst_t = 1'b0;
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1; 
          #100
           xin_t = 1'b1;              
      end
       always #50  clk_t = ~clk_t;                 
endmodule
```
# output Waveform
<img width="1919" height="1079" alt="Screenshot 2025-10-24 104743" src="https://github.com/user-attachments/assets/e40d28ed-4ebd-40c2-8713-acd3b461b9d1" />


# Moore 1011

// write verilog code for ROM using $random
```
module moore_1011 (
    input   clk,rst,xin,
    output reg  zout
);
parameter [2:0]
s0= 3'b000,
s1= 3'b001,
s2= 3'b010,
s3= 3'b011,
s4= 3'b100;
reg [2:0] ps,ns;
always @( posedge clk) 
begin
if (rst)
ps<=s0;
else
ps<=ns;
end

always @ (xin or ps)
begin 
case (ps)
s0 :
if (xin)
begin
ns=s1;
zout=0;
end
else
begin  
ns=s0;
zout=0;
end

s1 :
if (xin)
begin
ns=s1;
zout=0;
end
else
begin  
ns=s2;
zout=0;
end

s2 :
if (xin)
begin
ns=s3;
zout=0;
end
else
begin  
ns=s0;
zout=0;
end

s3 :
if (xin)
begin
ns=s4;
zout=0;
end
else
begin  
ns=s2;
zout=0;
end

s4 :
if (xin)
begin
ns=s1;
zout=1;
end
else
begin  
ns=s0;
zout=1;
end
endcase
end
endmodule 
```

# Test bench
```
module moore_1011_tb;
        reg clk_t,rst_t,xin_t;
        wire zout_t;
        
        moore_1011 dut(.clk(clk_t),.rst(rst_t),.xin(xin_t),.zout(zout_t));
           
     initial
        begin
            clk_t = 1'b1;
            rst_t = 1'b1;
          #100
            rst_t = 1'b0;
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1; 
          #100
           xin_t = 1'b1;              
      end
       always #50  clk_t = ~clk_t;                 
endmodule
```
# output Waveform

<img width="1919" height="1079" alt="Screenshot 2025-10-24 105100" src="https://github.com/user-attachments/assets/0fe48e62-2c0c-49a4-b88a-f8a30b65ac17" />


# Conclusion

The Mealy and Moore state machine for sequence 1011 was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the sequence operations and observing the output waveforms.
