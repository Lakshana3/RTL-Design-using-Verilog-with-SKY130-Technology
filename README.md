# RTL-Design-using-Verilog-with-SKY130-Technology

## **Index**

1. Introduction to Verilog RTL design and Synthesis
	1. Introduction to open-source simulator iverilog
		1. Introduction to iverilog design test bench
	2. Labs using iverilog and gtkwave
		1. Lab1 introduction to lab
		2. Lab2 Introduction iverilog gtkwave part1
		3. Lab2 Introduction iverilog gtkwave part2
	3. Introduction to Yosys and Logic synthesis
		1. Introduction to yosys
		2. introduction to logic synthesis part1
		3. introduction to logic synthesis part2
	4. Labs using Yosys and Sky130 PDKs
		1. Lab3 Yosys 1 good mux Part1
		2. Lab3 Yosys 1 good mux Part2
		3. Lab3 Yosys 1 good mux Part3
2. Timing libs, hierarchical vs flat synthesis and efficient flop coding styles
	1. Introduction to timing .libs
		1. Lab4 Introduction to dot Lib part1
		2. Lab4 Introduction to dot Lib part2
		3. Lab4 Introduction to dot Lib part3
	2. Hierarchical vs Flat Synthesis
		1. Lab5 Hier Synthesis Flat Synthesis Part1
		2. Lab5 Hier Synthesis Flat Synthesis Part2
	3. Various Flop Coding Styles and optimization
		1. Why Flops and Flop coding styles part1
		2. Why Flops and Flop coding styles part2
		3. Lab flop synthesis simulations part1
		4. Lab flop synthesis simulations part2
		5. Interesting optimisations part1
		6. Interesting optimisations part2
3. Combinational and sequential optimizations
	1. Introduction to optimizations
		1. Introduction to optimisations part1
		2. Introduction to optimisations part2
		3. Introduction to optimisations part3
	2. Combinational logic optimizations
		1. Lab06 Combinational Logic Optimisations part1
		2. Lab06 Combinational Logic Optimisations part2
	3. Sequential logic optimizations
		1. Lab07 Sequential Logic Optimisations part1
		2. Lab07 Sequential Logic Optimisations part2
		3. Lab07 Sequential Logic Optimisations part3
	4. Sequential optimizations for unused outputs
		1. Seq optimisation unused outputs part1
		2. Seq optimisation unused outputs part2
4. GLS, blocking vs non-blocking and Synthesis-Simulation mismatch
	1. GLS, Synthesis-Simulation mismatch and BlockingNon-blocking statements
		1. GLSConceptsAndFlowUsingIverilog
		2. SynthesisSimulationMismatch
		3. BlockingAndNonBlockingStatementsInVerilog
		4. CaveatsWithBlockingStatements
	2. Labs on GLS and Synthesis-Simulation Mismatch
		1. Lab GLS Synth Sim Mismatch part1
		2. Lab GLS Synth Sim Mismatch part2
	3. Labs on synth-sim mismatch for blocking statement
		1. Lab Synth sim mismatch blocking statement part1
		2. Lab Synth sim mismatch blocking statement part2
5. If, case, for loop and for generate
	1. If Case constructs
		1. IF CASE Constructs part1
		2. IF CASE Constructs part2
		3. IF CASE Constructs part3
	2. Labs on Incomplete If Case
		1. Lab Incomplete IF part1
		2. Lab Incomplete IF part2
	3. Labs on Incomplete overlapping Case
		1. Lab incomplete overlapping Case part1
		2. Lab incomplete overlapping Case part2
		3. Lab incomplete overlapping Case part3
		4. Lab incomplete overlapping Case part4
	4. for loop and for generate
		1. For Loop and For Generate part1
		2. For Loop and For Generate pa2t2
		3. For Loop and For Generate pa3t3
	5. Labs on for loop and for generate
		1. Lab For and For Generate part1
		2. Lab For and For Generate part2
		3. Lab For and For Generate part3
		4. Lab For and For Generate part4


## **1. Introduction to Verilog RTL design and Synthesis**

### 1. Introduction to open-source simulator iverilog

#### 1. Introduction to iverilog design test bench

Simulator - tool used to check if the RTL design is adhering to the given spec by simulating it.
The Open Source tool used here is Iverilog.

RTL design - set of verilog codes which has the functionality to meet the given design specs.

Testbench - Code used to check the functionality of the design by giving stimulus test vectors.

How does the simulator work?
- Looks for changes on input signals
- When input changes, the output is evaluated
- No change in input, no change in output

![d1sk1l1_1](/images/d1sk1l1_1.png)

Design can have 1/more primary inputs and 1/more primary outputs. 
For primary inputs we need to generate stimulus and for the outputs we need to observe the stimulus. 
Design is instantiated in testbench. Tb does not have primary inputs or outputs. 

Iverilog based simulation flow:
![d1sk1l1_2](/images/d1sk1l1_2.png)

Design and Tb are applied to iverilog. Output of it is .vcd(value change dump) file. To view the waveform and verify the design we use the gtkwave tool.

### 2. Labs using iverilog and gtkwave

#### 1. Lab1 introduction to lab

This section is about tool flow setup and files setup for running labs. 

Create VLSI folder and clone the following github repos:
kunalg123/vsdflow
kunalg123/sky130RTLDesignAndSynthesisWorkshop

/home/lakshanaramalingam1997/VLSI/vsdflow - will install all the necessary tools for the lab

Inside this directory 
`/home/lakshanaramalingam1997/VLSI/sky130RTLDesignAndSynthesisWorkshop`
my_lib contains all library files
my_lib/lib - has sky130 std cell library using for synthesis
my_lib/verilog_models - has std cell verilog models of std cells present in .lib
verilog_files - contains all .v source files and tb files needed for labs

![d1sk2l1_1](/images/d1sk2l1_1.png)
![d1sk2l1_2](/images/d1sk2l1_2.png)
![d1sk2l1_3](/images/d1sk2l1_3.png)

#### 2. Lab2 Introduction iverilog gtkwave part1

How to work with iverilog and gtkwave?

Go to design folder verilog_files and load design in iverilog using cmd 
`iverilog design_file.v tb_design_file.v`
An executable file called a.out will be created.
When it's executed, it dumps the vcd file. 
Load the vcd file in gtkwave. 
The testbench is seen within which the uut(unit under test) is seen. 
The waveform shows the functionality of a MUX.

![d1sk2l2_1](/images/d1sk2l2_1.png)
![d1sk2l2_2](/images/d1sk2l2_2.png)
![d1sk2l2_3](/images/d1sk2l2_3.png)

#### 3. Lab2 Introduction iverilog gtkwave part2

To view and edit files we use gvim editor. 
Here we are seeing the design file and testbench file of 2x1 MUX(Output selects the input signal based on the sel input). 

Tb instantiates the design(uut). 
Starts dumping the vcd file.
These are stimulus generators.

Apply stimulus to inputs - sel, i0, i1.
No stimulus observer in this tb.

![d1sk2l3_1](/images/d1sk2l3_1.png)
![d1sk2l3_2](/images/d1sk2l3_2.png)
![d1sk2l3_3](/images/d1sk2l3_3.png)
![d1sk2l3_4](/images/d1sk2l3_4.png)

### 3. Introduction to Yosys and Logic synthesis

#### 3a. Introduction to yosys

Synthesizer is a tool used for converting RTL design to netlist(representation of design in the form of .lib files(std cells) - netlist is a true representation of the design)
The Open Source tool used is Yosys.
Appy RTL design and .lib file to Yosys and get the netlist file.
read_verilog to read design
read_liberty to read .lib file -> need not be given if yosys is already invoked
write_verilog to write out the netlist output

![d1sk3l1_1](/images/d1sk3l1_1.png)

How to verify the synthesized output?
Use the synthesized netlist file, the testbench we used before(because primary i/p and o/p are the same) and give it as input to iverilog to generate the vcd file and simulate it using gtkwave and verify. 
The stimulus should be the same as output observed during rtl simulation. 

![d1sk3l1_2](/images/d1sk3l1_2.png)

#### 3b. introduction to logic synthesis part1

RTL design - behavioral representation of the design spec written using verilog HDL
Synthesis maps the RTL code to digital logic ckt. 
- RTL to gate level translation
- Design is converted into gates and connections are made in between the gates
- this is written out as netlist file

![d1sk3l2_1](/images/d1sk3l2_1.png)

.lib
- collection of all logical modules like and, or, not, inv,- rich enough implement any boolean logic functionality
- has diff flavors of same gate (2i/p, 3i/p, slow, medium and fast versions of gates)
	- Why? **Addpic**
	  Combinational delay in logic path determines the max speed of op of digi logic ckt.
	  
![d1sk3l2_2](/images/d1sk3l2_2.png)

#### 3c. Introduction to logic synthesis part2

So why do we have slow cells in the library?
**Addpic**
Faster cells vs Slower cells:
Load in a digital logic ckt is capacitance; so faster the charging/discharging of C, lesser is the cell delay.
Propagation delay - time for i/p to cause change in the o/p.
So how fast the i/p changes depends on how fast the cell can drive the i/p. 
So larger C means slower drive strength.
To charge/discharge the C fast, we need transistors capable of sourcing more current meaning wider transistors. 
Wider transistors -> low delay(faster cells) -> more area and power
Narrow transistors -> more delay(slower cells) -> less area and power
So need to guide the synthesizer to select optimum flavor of cells for implementation of the logic ckt by giving constraints.
More use of fast cells -> may have hold time violations and consume more area and power
More use of slow cells -> may result in sluggish ckt, may not meet performance 

Synthesizer - 1st will do syntactical check and start to map the design.
Module maps to top level ports of the design.
assign -> mux
always -> flop
clk and reset and internal connections are made.

![d1sk3l3_1](/images/d1sk3l3_1.png)

### 4. Labs using Yosys and Sky130 PDKs

#### 4a. Lab3 Yosys 1 good mux Part1

Invoke yosys.
Read  the library and give the relative path.
Read the verilog design file.
synth -top -> mention what's the module we are going to synthesize

Open verilog file using gvim - mux - combinational logic - no flop present

abc -lib path -> to gen netlist -> converts rtl file to gates 
show - cmd to see logic it has realized

![d1sk4l1_1](/images/d1sk4l1_1.png)
![d1sk4l1_2](/images/d1sk4l1_2.png)
![d1sk4l1_3](/images/d1sk4l1_3.png)
![d1sk4l1_4](/images/d1sk4l1_4.png)
![d1sk4l1_5](/images/d1sk4l1_5.png)
![d1sk4l1_6](/images/d1sk4l1_6.png)

**add screenshots**

#### 4b. Lab3 Yosys 1 good mux Part2

**addpic**

The realization of 2x1 MUX.

#### 4c. Lab3 Yosys 1 good mux Part3

write_verilog - cmd to write netlist
-noattr -> to remove extra info to snip and give out only the necessary info

- created instantiations
- created internal nets to make connections
- netlist representation of MUX
- top module of netlist is what we used before
**Addsc**

![d1sk4l3_1](/images/d1sk4l3_1.png)
![d1sk4l3_2](/images/d1sk4l3_2.png)
![d1sk4l3_3](/images/d1sk4l3_3.png)
![d1sk4l3_4](/images/d1sk4l3_4.png)


