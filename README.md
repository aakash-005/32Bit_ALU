# 32Bit_ALU Simulation

# Aim: 

Write a verilog code for 32 bit ALU supporting four logical and four arithmetic operations,use case statement and if statement for ALU behavioral modeling.

To Verify the Functionality using Test Bench.

# Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

## Design Information and Bock Diagram:

The ALU will take in two 32-bit values, and control line. An Arithmetic unit does the following task like addition subtraction, multiplication and logical operations. As the input is given in 32 bit we get 32 bit output. The arithmetic will show only one output at a time so a selector is necessary to select one of the operator.

![image](https://github.com/user-attachments/assets/e574788c-253f-46da-8468-298fe2844f7a)

### Fig 1 : Block Diagram of 32 Bit ALU 

## Creating a Work space :

Create a folder in your name (Note: Give folder name without any space) and Create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

## Creating Source Codes 

In the Terminal, type gedit <filename>.v (ex: gedit alu_32bit.v). 

A Blank Document opens up into which the following source code can be typed down. 

(Note : File name should be with HDL Extension)

## a)To Verify the Functionality using Test Bench

## Source Code – Using Case Statement :

module alu_32bit_case(y,a,b,f);

input [31:0]a;

input [31:0]b;

input [2:0]f;

output reg [31:0]y;

always@(*)

begin

case(f)

3'b000:y=a&b; //AND Operation

3'b001:y=a|b; //OR Operation

3'b010:y=~(a&b); //NAND Operation

3'b011:y=~(a|b); //NOR Operation

3'b100:y=a^b; //XOR Operation

3'b101:y=~(a^b); //XNOR Operation

3'b110:y=~a; //NOT of a

3'b111:y=~b; //NOT of b

endcase

end

endmodule

Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Creating Test bench:

Similarly, create your test bench using gedit <filename_tb>.v or <filename_tb>.vhdl to open a new blank document (alu_32bit_tb_case).

## Test Bench :

module alu_32bit_tb_case;

reg [31:0]a;

reg [31:0]b;

reg [2:0]f;

wire [31:0]y;

alu_32bit_case test2(.y(y),.a(a),.b(b),.f(f));

initial

begin

a=32'h00000000;

b=32'h10101010;

#10 f=3'b000;

#10 f=3'b001;

#10 f=3'b010;

#10 f=3'b011;

#10 f=3'b100;

#10 f=3'b101;

#10 f=3'b110;

#10 f=3'b111;

#50 $finish;

end

endmodule

Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Functional Simulation: 

Invoke the cadence environment by type the below commands 

tcsh (Invokes C-Shell) 

source /cadence/install/cshrc (mention the path of the tools) 

(The path of cshrc could vary depending on the installation destination)
      
After this you can see the window like below 

![Screenshot 2025-04-28 144600](https://github.com/user-attachments/assets/a2d59cce-cb66-44e4-8455-db2c56a4c974)

### Fig 2: Invoke the Cadence Environment

To Launch Simulation tool 

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design 

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG 


It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .

![Screenshot 2025-04-29 130545](https://github.com/user-attachments/assets/1bfb002b-5a98-4af1-bba3-87b914f0ffe7)

### Fig 3: Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in below figure 

Click the cds.lib file and save the file by clicking on Save option 

![Screenshot 2025-04-29 130618](https://github.com/user-attachments/assets/7efbb14d-9061-47cb-ad60-92d9c02e84a4)

### Fig 4:cds.lib file Creation

Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. 

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .

We are simulating verilog design without using any libraries 

A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure 

![Screenshot 2025-04-29 130635](https://github.com/user-attachments/assets/1ad10be3-ac7b-4465-b1d7-d46670686906)

### Fig 5: Selection of Don’t include any libraries

A ‘NCLaunch window’ appears as shown in figure below

Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .

To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. 

![Screenshot 2025-04-29 130651](https://github.com/user-attachments/assets/b6ca6fb9-8864-4de6-95d3-0857be52abca)

### Fig 6: Nclaunch Window

## Step 1: Compilation:

– Process to check the correct Verilog language syntax and usage 

Inputs: Supplied are Verilog design and test bench codes 

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file 

## 	Steps for compilation: 

1. Create work/library directory (most of the latest simulation tools creates automatically)
   
2. Map the work to library created (most of the latest simulation tools creates automatically)
   
3. Run the compile command with compile options
   
i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v 

Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation 

![Screenshot 2025-04-29 130700](https://github.com/user-attachments/assets/7adbc1ad-93d2-4866-823b-dc53d6c476fe)

### Fig 7: Compiled database in worklib

After compilation it will come under worklib you can see in right side window

Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. 

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical

directory paths. For this Design, you will define a library called “worklib”

#3 Step 2: Elaboration:– 

To check the port connections in hierarchical design

Inputs: Top level design / test bench Verilog codes 

Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file 

## 	Steps for elaboration 

– Run the elaboration command with elaborate options 

1.It builds the module hierarchy

2.Binds modules to module instances 

3.Computes parameter values

4.Checks for hierarchical names conflicts

5.It also establishes net connectivity and prepares all of this for simulation

After elaboration the file will come under snapshot. Select the test bench and simulate it.

![Screenshot 2025-04-29 130752](https://github.com/user-attachments/assets/fcfc6b9b-3fa4-41ce-b083-8450b02dd57c)

## Fig 8: Elaboration Launch Option

## Step 3: Simulation: 

– Simulate with the given test vectors over a period of time to observe the output behaviour. 

Inputs: Compiled and Elaborated top level module name 

Outputs: Simulation log file, waveforms for debugging 

Simulation allow to dump design and test bench signals into a waveform 

Steps for simulation – Run the simulation command with simulator options

![Screenshot 2025-04-29 130814](https://github.com/user-attachments/assets/4c393bd8-d2b7-4c29-a0e6-e402493773a7)

## Fig 9: Design Browser window for simulation

![Screenshot 2025-04-29 130838](https://github.com/user-attachments/assets/b067c9ca-b505-4917-a772-9df13c5d8193)

## Fig 10:Simulation Waveform Window

![Screenshot 2025-04-29 130901](https://github.com/user-attachments/assets/859a89da-57f5-4be5-afd5-387fab8c72e2)

## Fig 11:Simulation Waveform Window

### Result

The functionality of a 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool.














      







