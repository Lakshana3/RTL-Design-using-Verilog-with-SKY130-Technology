# RTL-Design-using-Verilog-with-SKY130-Technology

## **Index**

1. Introduction to Verilog RTL Design and Synthesis
	1. Introduction to open-source simulator Iverilog
		1. Introduction to Iverilog design test bench
	2. Labs using Iverilog and Gtkwave
		1. Lab1 Introduction to lab
		2. Lab2 Introduction iverilog gtkwave part1
		3. Lab2 Introduction iverilog gtkwave part2
	3. Introduction to Yosys and Logic synthesis
		1. Introduction to yosys
		2. Introduction to logic synthesis part1
		3. Introduction to logic synthesis part2
	4. Labs using Yosys and Sky130 PDKs
		1. Lab3 Yosys 1 good mux Part1
		2. Lab3 Yosys 1 good mux Part2
		3. Lab3 Yosys 1 good mux Part3
2. Timing libs, Hierarchical vs flat synthesis and Efficient flop coding styles
	1. Introduction to timing .libs
		1. Lab4 Introduction to dot Lib part1
		2. Lab4 Introduction to dot Lib part2
		3. Lab4 Introduction to dot Lib part3
	2. Hierarchical vs Flat Synthesis
		1. Lab5 Hier Synthesis Flat Synthesis Part1
		2. Lab5 Hier Synthesis Flat Synthesis Part2
	3. Various Flop Coding Styles and Optimization
		1. Why Flops and Flop coding styles part1
		2. Why Flops and Flop coding styles part2
		3. Lab flop synthesis simulations part1
		4. Lab flop synthesis simulations part2
		5. Interesting optimisations part1
		6. Interesting optimisations part2
3. Combinational and Sequential Optimizations
	1. Introduction to Optimizations
		1. Introduction to Optimisations part1
		2. Introduction to Optimisations part2
		3. Introduction to Optimisations part3
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
4. GLS, Blocking vs Non-Blocking and Synthesis-Simulation Mismatch
	1. GLS, Synthesis-Simulation mismatch and Blocking Non-blocking statements
		1. GLS Concepts And Flow Using Iverilog
		2. Synthesis Simulation Mismatch
		3. Blocking And Non-Blocking Statements In Verilog
		4. Caveats With Blocking Statements
	2. Labs on GLS and Synthesis-Simulation Mismatch
		1. Lab GLS Synth Sim Mismatch part1
		2. Lab GLS Synth Sim Mismatch part2
	3. Labs on Synth-Sim mismatch for Blocking statement
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

### 1. Introduction to open-source simulator Iverilog

#### 1. Introduction to Iverilog design test bench

Simulator is a tool used to check if the RTL design is adhering to the given spec by simulating it.
The Open Source tool used here is Iverilog.

RTL design is a set of verilog codes which has the functionality to meet the given design specs.

Testbench is a code which is used to check the functionality of the design by giving stimulus test vectors.

How does the simulator work?
- Looks for changes on input signals
- When input changes, the output is evaluated
- No change in input means no change in output

![d1sk1l1_1](/images/d1sk1l1_1.png)

Design can have one/more primary inputs and one/more primary outputs. 
For primary inputs we need to generate stimulus and we need to observe the stimulus from the outputs. 
The design is instantiated in a testbench(Tb). Tb does not have primary inputs or outputs. 

Iverilog based simulation flow:
![d1sk1l1_2](/images/d1sk1l1_2.png)

Design and Tb are applied to iverilog. Output of it is .vcd(value change dump) file. To view the waveform and verify the design we use the gtkwave tool.

### 2. Labs using Iverilog and Gtkwave

#### 1. Lab1 Introduction to lab

This section is about tool flow setup and files setup for running labs. 

Create VLSI folder and clone the following github repos:
kunalg123/vsdflow
kunalg123/sky130RTLDesignAndSynthesisWorkshop

The `/home/lakshanaramalingam1997/VLSI/vsdflow` directory will install all the necessary tools for the lab.

Inside this directory `/home/lakshanaramalingam1997/VLSI/sky130RTLDesignAndSynthesisWorkshop`,
- my_lib contains all the library files
- my_lib/lib contains sky130 standard cell library which is used for synthesis
- my_lib/verilog_models contains standard cell verilog models of standard cells present in .lib file
- verilog_files contains all .v source files and tb files needed for labs

![d1sk2l1_1](/images/d1sk2l1_1.png)
![d1sk2l1_2](/images/d1sk2l1_2.png)
![d1sk2l1_3](/images/d1sk2l1_3.png)

#### 2. Lab2 Introduction iverilog gtkwave part1

How to use Iverilog and Gtkwave?

Go to design folder verilog_files and load design in iverilog using cmd `iverilog design_file.v tb_design_file.v`.
An executable file called a.out will be created.
When it's executed, it dumps the .vcd file. 
Load the vcd file in gtkwave to view the waveform.
The testbench is seen, within which the uut(unit under test) is seen. 
The waveform shows the functionality of a MUX.

![d1sk2l2_1](/images/d1sk2l2_1.png)
![d1sk2l2_2](/images/d1sk2l2_2.png)
![d1sk2l2_3](/images/d1sk2l2_3.png)

#### 3. Lab2 Introduction iverilog gtkwave part2

To view and edit files we use the gvim editor. 
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

### 3. Introduction to Yosys and Logic Synthesis

#### 3a. Introduction to yosys

Synthesizer is a tool used for converting RTL design to netlist(representation of design in the form of .lib files(std cells) - netlist is a true representation of the design).
The Open Source tool used for synthesis is Yosys.
Apply RTL design and .lib file to Yosys and get the netlist file.
- read_verilog is used to read design
- read_liberty is used to read .lib file -> need not be given if yosys is already invoked
- write_verilog is used to write out the netlist output

![d1sk3l1_1](/images/d1sk3l1_1.png)

How to verify the synthesized output?
Use the synthesized netlist file, the testbench we used before(because primary i/p and o/p are the same) and give it as input to iverilog to generate the vcd file and simulate it using gtkwave and verify. 
The stimulus should be the same as output observed during RTL simulation. 

![d1sk3l1_2](/images/d1sk3l1_2.png)

#### 3b. Introduction to logic synthesis part1

RTL design is a behavioral representation of the design spec written using verilog HDL.
Synthesis 
- maps the RTL code to digital logic ckt
- RTL to gate level translation
- Design is converted into gates and connections are made in between the gates
- this is written out as netlist file

![d1sk3l2_1](/images/d1sk3l2_1.png)

.lib
- collection of all logical modules like and, or, not, inv, etc. - rich enough implement any boolean logic functionality
- has diff flavors of same gate (2i/p, 3i/p, slow, medium and fast versions of gates)
	- Why? **Addpic**
	  Combinational delay in logic path determines the max speed of operation of digital logic ckt.
	  
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

A Synthesizer will first do a syntactical check and then start to map the design.
- Module maps to top level ports of the design.
- assign is realized as mux
- always block is realized as a flop
- clk and reset and internal connections are made.

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

***add screenshots***

#### 4b. Lab3 Yosys 1 good mux Part2

***addpic***

The realization of 2x1 MUX.

#### 4c. Lab3 Yosys 1 good mux Part3

write_verilog - cmd to write netlist
-noattr -> to remove extra info to snip and give out only the necessary info

- created instantiations
- created internal nets to make connections
- netlist representation of MUX
- top module of netlist is what we used before
***Addsc***

![d1sk4l3_1](/images/d1sk4l3_1.png)
![d1sk4l3_2](/images/d1sk4l3_2.png)
![d1sk4l3_3](/images/d1sk4l3_3.png)
![d1sk4l3_4](/images/d1sk4l3_4.png)

## 2. Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

### 1. Introduction to timing .libs

#### 1a. Lab4 Introduction to dot Lib part1

This section talks about .lib file. 
Open sky130 lib.
:syn off - syntax off
1st line - name of lib -> `sky130_fd_sc_hd__tt_025C_1v80`
130nm - library
tt - typical process -> process variations due to fabrication (PVT is mentioned in lib)
025C - temp at which the silicon works 
1v80 - voltage at which the silicon works
Libraries are characterized to model the variations in PVT.
***addsc***

![d2sk1l1_1](/images/d2sk1l1_1.png)
![d2sk1l1_2](/images/d2sk1l1_2.png)
![d2sk1l1_3](/images/d2sk1l1_3.png)

#### 1b. Lab4 Introduction to dot Lib part2

The .lib file contains:
- technology cmos
- delay model 
- operating units
- operating condns -> PVT

cell -> keyword cell marks beginning of cell definition
:g// -> different flavors of same cells

cell a2111o - different features of the cell
To understand functionality check equivalent verilog model (open another file)
.lib also has
- area information
- pp(powerport) information
- describe each i/p pin - i/p C, power, transition, delay associated with pin, timing info

***Addsc and gifs***

![d2sk1l2_1](/images/d2sk1l2_1.png)
![d2sk1l2_2](/images/d2sk1l2_2.png)
![d2sk1l2_3](/images/d2sk1l2_3.png)
![d2sk1l2_4](/images/d2sk1l2_4.png)
![d2sk1l2_5](/images/d2sk1l2_5.png)
![d2sk1l2_6](/images/d2sk1l2_6.png)
![d2sk1l2_7](/images/d2sk1l2_7.png)
![d2sk1l2_8](/images/d2sk1l2_8.png)
![d2sk1l2_9](/images/d2sk1l2_9.png)
![d2sk1l2_10](/images/d2sk1l2_10.png)
![d2sk1l2_11](/images/d2sk1l2_11.png)
![d2sk1l2_12](/images/d2sk1l2_12.png)
![d2sk1l2_13](/images/d2sk1l2_13.png)
![d2sk1l2_14](/images/d2sk1l2_14.png)
![d2sk1l2_15](/images/d2sk1l2_15.png)
![d2sk1l2_16](/images/d2sk1l2_16.png)
![d2sk1l2_17](/images/d2sk1l2_17.png)
![d2sk1l2_18](/images/d2sk1l2_18.png)
![d2sk1l2_19](/images/d2sk1l2_19.png)
![d2sk1l2_20](/images/d2sk1l2_20.gif)

#### 1c. Lab4 Introduction to dot Lib part3

Lets pick a smaller cell to check its different flavors.
Picking and gate and2_0.
Opening its verilog model.

and2_0 - and2_2 - and2_4
area < < 
employs wider cells < <
power < <
delay > >

![d2sk1l3_1](/images/d2sk1l3_1.png)
![d2sk1l3_2](/images/d2sk1l3_2.png)
![d2sk1l3_3](/images/d2sk1l3_3.png)
![d2sk1l3_4](/images/d2sk1l3_4.png)
![d2sk1l3_5](/images/d2sk1l3_5.png)
![d2sk1l3_6](/images/d2sk1l3_6.png)
![d2sk1l3_7](/images/d2sk1l3_7.png)
![d2sk1l3_8](/images/d2sk1l3_8.png)

***addsc***

### 2. Hierarchical vs Flat Synthesis

#### 2a. Lab05 Hier synthesis Flat synthesis part1

During synthesis the number of modules and their heirarchy mentioned in the design is normally preserved. Its called Heir synthesis. 
Lets load multiple_modules.v
It has:
- sub_1 and
- sub_2 or
- m_m -> instantiates and & or gate
Launch yosys, read lib, read_v, synth -top mul_m (when you have multiple modules, mention the module that you want to synthesize)
show report
abc -lib
show multiple_modules -> hierarchical design because hierarchies are preserved not showing underlying design. 
write_v check netlist

OR will be inferred as NAND implementation with 2 INVs i/ps
NAND will have stacked NMOS
NOR will have stacked PMOS which is always bad 
PMOS has poor mobility and to improve we have to make it a light cell to get something called good logical effort.

![d2sk2l1_1](/images/d2sk2l1_1.png)
![d2sk2l1_2](/images/d2sk2l1_2.png)
![d2sk2l1_3](/images/d2sk2l1_3.png)
![d2sk2l1_4](/images/d2sk2l1_4.png)
![d2sk2l1_5](/images/d2sk2l1_5.png)
![d2sk2l1_6](/images/d2sk2l1_6.png)
![d2sk2l1_7](/images/d2sk2l1_7.png)
![d2sk2l1_8](/images/d2sk2l1_8.png)
![d2sk2l1_9](/images/d2sk2l1_9.png)
![d2sk2l1_10](/images/d2sk2l1_10.png)
![d2sk2l1_11](/images/d2sk2l1_11.png)

***addsc
addpic***

#### 2b. Lab05 Hier synthesis Flat synthesis part2

Hierarchies are preserved in _hier.v 

Do flatten - used to write up a flat netlist
flatten -> shows no hierarchies hier are flattened out, directly see instantiation of gates
write_v -noattr
!gvim
show both files
show -> output is shown with the underlying components because we flattened the hierarchies

To synthesize in submodule 1 level
synth -> inferring only 1 module
abc
show
seeing only the and gate
Why submodule level synthesis?
If there are multiple instantiations of a same component in the top module, we can synthesize the module 1 time and then replicate it multiple times in the top module.
- When we have multiple instance of same module
- When we want to divide and conquer approach ina massive design - doing synth portion by portion and then stitch all the netlists at the top level

***Addsc***

![d2sk2l2_1](/images/d2sk2l2_1.png)
![d2sk2l2_2](/images/d2sk2l2_2.png)
![d2sk2l2_3](/images/d2sk2l2_3.png)
![d2sk2l2_4](/images/d2sk2l2_4.png)
![d2sk2l2_5](/images/d2sk2l2_5.png)
![d2sk2l2_6](/images/d2sk2l2_6.png)
![d2sk2l2_7](/images/d2sk2l2_7.png)
![d2sk2l2_8](/images/d2sk2l2_8.png)
![d2sk2l2_9](/images/d2sk2l2_9.png)
![d2sk2l2_10](/images/d2sk2l2_10.png)
![d2sk2l2_11](/images/d2sk2l2_11.png)
![d2sk2l2_12](/images/d2sk2l2_12.png)
![d2sk2l2_13](/images/d2sk2l2_13.png)
![d2sk2l2_14](/images/d2sk2l2_14.png)
![d2sk2l2_15](/images/d2sk2l2_15.png)
![d2sk2l2_16](/images/d2sk2l2_16.png)
![d2sk2l2_17](/images/d2sk2l2_17.png)

----------------------------------------------------------------------------------------------------------------------------------------
### 3. Various Flop Coding Styles and optimization

#### 3a. Why Flops and Flop coding styles part1

Basics of flop: why it's needed?
Any combinational ckt has propagation delay because of which the o/p glitches. 
More combinational ckts -> more glitches
To avoid, we need an element to store the value -> flip flops
Even if the i/p of the flop glitches, the flop will change the o/p only at the clk edge thereby shielding glitches. 
We need to initialize the flops using reset/set and they can be async or sync to the clock.

***addpic
addsc***

#### 3b. Why Flops and Flop coding styles part2

Flop with async res
async set

Sync set -> Sync will come in D pin of flop
Sync res waits for clk -> always block only evaluates on posedge of clk

Both reset and set are there then they may cause race conditions.

Both sync and async res, 
***addpic addsc***

#### 3c. Lab flop synthesis simulations part1

asyncres
RTL simul
reset when low before clk
q is sync to clk
when reset is 1, immediately q goes low.

asynset
rtl simul
upon edge of clk, changes in d are seen on q
but when the set is true, irrespective of clk, q goes 1 till the set is true.

syncres
rtl simul
When reset is 1, q waits for posedge clk and goes 0.

addsc

#### 3d. Lab flop synthesis simulations part2

Synthesize asyn_res
yosys
dfflibmap - usually there will be a separate flop lib under std cell library so need to tell the tool explicitly where to pick the flops from. Here it is all in the same file. 
show
flop has active low reset so inv is used

aynsc set

syncres -> 

addpic addsc

#### 3e. Interesting optimisations part1

mult2
yosys
show

addpic
addsc

#### 3f. Interesting optimisations part2

a 3bit y 6bit
write_v mult2
gvim

read_v mult8
write_v 

addpic addsc

## 3. Combinational and sequential optimizations

### 1. Introduction to optimizations
#### 1a. Introduction to optimisations part1

Combinational logic optimization: why?
- to squeeze logic to get most optimized design in terms of area and power
Techniques:
- Constant propagation - direct optimization
- Boolean logic optimization - using K-map or Quine McKluskey algorithms

Constant propagation:

Boolean logic optimization:

Synth tool does these kind of optimization to get the most optimized logic
Sc-draw pics

#### 1b. Introduction to optimisations part2

Sequential logic optimizations techniques:
1. Basic
	- Sequential constant propagation
2. Advanced
	- State optimization
	- Retiming
	- Sequential Logic Cloning (Floor plan aware synthesis)

Sequential constant propagation:
Q is always 0 so y is always 1 irrespective of clk, reset.
sc-pic

Set flop:
When set=1, Q=1 else 0 so q takes both values so this can't be optimized so the logic will be retained as such (coz q does not take constant value)
Q is not= !set
sc-pic

#### 1c. Introduction to optimisations part3

State optimization
- optimization of unused state
- can realize most condensed state machine

Cloning
- of logic is done when u r doing physical aware synth
- to avoid large routing delays
- if large +ve slack available at flop A, include 2 copies of A driving the B and C - no timing issues will come

Retiming:
- some portion of  the logic is splitted between flops to have approx equal delay to improve performance
- partitioning logic and useful slack to increase freq of op of ckt

sc-pic

### 2. Combinational logic optimizations

#### 2a. Lab06 Combinational Logic Optimisations part1

opt files
optcheck 
optcheck2 redundancy

yosys
opt_clean -purge -> cmd to do optimization - all optimizations are done
show

show - nand realization of or

addsc addpic

#### 2b. Lab06 Combinational Logic Optimisations part2

optcheck3
yosys

addpic

optcheck4

mmopt5
flatten
opt_clean

drawpicfor4and5 addsc

### 3. Sequential logic optimizations

#### 3a. Lab07 Sequential Logic Optimisations part1

dff_const
1.v
Q becomes 1 at posedge of clk
Rst may get deasserted anywhere here but Q will wait for posedge of clk

2.v
Q will always be 1

RTL simul
synth

dfflibmap - for seq ckts have separate libs usually but here it is the same lib so mention it to tell the synth where to choose the libs from

till show for dff_const1

drawpicfromsc
addsc

#### 3b. Lab07 Sequential Logic Optimisations part2

from read_v for dffconst2
when synth of dffconst1 it has inferred a dff
now it has not inferred any flop or cells

more examples
const3 gvim

drawpicfromsc addsc

#### 3c. Lab07 Sequential Logic Optimisations part3

rtl simul for const3
Q1 is not primary output, its and internal signal so get it from uut

Synth
dfflibmap mela highlight

addsc

dffconst4and5
Drawpicfor4and5 addsc

### 4. Sequential optimizations for unused outputs

#### 4a. Seq optimisation unused outputs part1

counter_opt - 3 bit up counter
count[0] toggles on every clk cycle and other outputs are unused
yosys
show

Any logic which is not having any relation with the outputs will be optimized by the synthesizer. 

sc-pic addsc

#### 4b. Seq optimisation unused outputs part2

Modify rtl -> counteropt2
Using all the 3 bits so 3 flops will be present.
yosys

logic feeding those intermediary o/ps will also be optimized away

sc-pic addsc

## 4. GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

### 1. GLS, Synthesis-Simulation mismatch and BlockingNon-blocking statements

#### 1a. GLS Concepts And Flow Using Iverilog

GLS - gate level simulation
Validated RTL code by simulating it with testbench
Now use netlist as dut and run testbench which is same because netlist is logically same as RTL code

Why GLS?
- verify logical correctness of design after synthesis
- ensuring timing of design is met (for this, run GLS with delay annotation)

GLS using Iverilog:
Design(netlist), gate level verilog models(needed because meaning of std cells need to be defined to the tool), testbench
Gate level verilog model can be functional or timing aware(if they are then check timing validation)

sc-pic

#### 1b. Synthesis Simulation Mismatch

Why is functional validation of netlist needed? - synth sim mismatch can happen
Because of:
- Missing sensitivity list
- Blocking vs Non-Blocking assignments
- Non standard verilog coding

Missing sensitivity list:
how does the simulator work? - o/p changes only when there is change in i/p - simulator looks for activity

Synthesizer doesn't look at the sensitivity list. It'll only look at the functionality which is mux. 

sc-pic

#### 1c. Blocking And NonBlocking Statements In Verilog

B and NB statement -> comes into pic only while using always block
B:
- B statement uses = to write assignments
- executes statements in order it is written

NB:
-  <= 
- executes parallelly
- when always is entered, all the RHS will be executed and evaluates and assigned to LHS
- parallel evaluation

Caveats with B:
Shift reg

2 flops:- q=q0 and q0=d
q0=d and q=q0 - q0 already has recent value of d - only 1 flop

sc-pic

#### 1d. Caveats With Blocking Statements

But if we use NB, order doesn't matter
So ** always use NB for writing sequential circuits**.

Caveats with B:
aim: create a ckt y=(a|b)&c
mimic a flop in a combi ckt but when we synth there'll be no flop

Bcoz of these, we need to run GLS on netlist and match that with expected o/pp and see there are no synth-sim mismatches.

sc-pic

### 2. Labs on GLS and Synthesis-Simulation Mismatch

#### 2a. Lab GLS Synth Sim Mismatch part1

To run GLS, we need netlist, 
mux files
rtl simul - 2x1 MUX
synth -yosys
show -> drawpic
GLS
2 files needed to read std cell models
GLS output

addsc sc-pic

#### 2b. Lab GLS Synth Sim Mismatch part2

bad_mux
rtl simul -> flop kind of behavior
synth 
simul-synth mismatch due to missing sensitivity list

addsc sc-pic

### 3. Labs on synth-sim mismatch for blocking statement

#### 3a. Lab Synth sim mismatch blocking statement part1

blocking_caveaat.v
iverilog

addsc sc-pic

#### 3b. Lab Synth sim mismatch blocking statement part2

synth
show -> no latch
GLS -> looks at instantaneous value whereas in simul it looked at the past value
Synth-sim mismatch due to blocking statements (avoid B statements as much as possible)

addsc

## 5. If, case, for loop and for generate

### 1. If Case constructs

#### 1a. IF CASE Constructs part1

If statements -> used to create priority logic
Danger/Caution with if -> Inferred latches due to bad coding style(incomplete if statements)
So a combi ckt will add a latch(to retain the value of y).
Note: Combi ckt cannot have inferred latches.
**For a negative D latch to go into latch state, EN should be low.
For a D latch,  if EN is 1, ip passes to op. if en is 0, latch holds its op.
sc-pic

#### 1b. IF CASE Constructs part2

Incomplete if statements are allowed when we intend to have it like in the case of a counter. 
Always think of what hardware will translate to when we write code.

Case statement: (if and case are used inside always block and var used for if and case should be reg var)

Caveats with Case:
1. Incomplete case statement - leads to inferred latches - to avoid incomplete cases, code case with default

sc-pic

#### 1c. IF CASE Constructs part3

2. Partial assignments in case
2 o/ps in case -> so 2 muxes inferred
NOte: Assign all the o/ps in all the segments of case

3. Comparision b/w if and case
If has priority -> only one portion can execute here
Case doesn't have priority -> it checks every case - whole case will be evaluated
If there is a bad case statement like 2'b1? -> this can cause unpredictable outputs 
Like 2'b1? can be called when sel=10 or 11.
Note: should not have overlapping case statements

sc-pic

### 2. Labs on Incomplete If Case

#### 2a. Lab Incomplete IF part1

incomp files gvim
incompif
If always translates into a MUX. 
Pos D latch
rtl 
synth show
tool infers a latch instead of a mux because of incomp if

addsc sc-pic

#### 2b. Lab Incomplete IF part2

incompif2
rtl
synth
if both i0 and i2 are 0 then it latches (pos latch)

addsc sc-pic

### 3. Labs on Incomplete overlapping Case

#### 3a. Lab incomplete overlapping Case part1

incompcase gvim
when sel[1] is 0, ip is seen at op. when sel[1] is 1, the value is latched. 
en = !sel[1] 
so in transparent mode, en=1. in latch mode, en=0.

rtl
synth

addsc sc-pic

#### 3b. Lab incomplete overlapping Case part2

compcase
No latch
rtl
synth - no latches inferred - 4x1MUX

partialcase gvim

addsc sc-pic

#### 3c. Lab incomplete overlapping Case part3

synth - only 1 latch for x

badcase
tool gets confused
diff simulators behave differently because this is not expected
synthesizer will choose the most optimum solution
rtl

addsc sc-pic

#### 3d. Lab incomplete overlapping Case part4

synth - no inferred latches - prob with overlapping case - all cases should be mutually exclusive
GLS

addsc sc-pic

### 4. for loop and for generate

#### 4a. For Loop and For Generate part1

Looping constructs in verilog:
- for loop - always used inside always block; used for evaluating expressions; multiple evaluations; for creating a simplified code
- generate for loop - used outside always (cant be used inside always); used for instantiating hw multiple times; hw replication

2x1MUX 4x1MUX 32X1MUX
If we need to instantiate multiple muxes in an efficient way, use generate for loop outside always block with blocking statements(executes line by line).

sc-pic

#### 4b. For Loop and For Generate pa2t2

Demux - same case

1x8 DEMUX 

To generate multiple instances of a gate, use for generate(for replicating hardware).

sc-pic

#### 4c. For Loop and For Generate pa3t3

RCA

sc-pic

### 5. Labs on for loop and for generate

#### 5a. Lab For and For Generate part1

muxgen gvim
rtl
clk and reset are tb signals
synth
GLS

sc-pic addsc

#### 5b. Lab For and For Generate part2

demuxcasse and gen
y_int initialized to 0 - avoid inferred latches
rtl

synth

sc-pic addsc

#### 5c. Lab For and For Generate part3

RCA - each addition can be performed by a FA. 4 additions - 4 FAs
Fa = 3ip(i0, i1, c), 2op(s, co)

1st way - instantiate 4 FAs
2nd way - use for generate to replicate FA 4 times by using for loop

gvim
Rule for addition: N bit + N bit = N+ 1 bits
N bit + M bit = Max(N,M) + 1 bit

Making 0th instance of FA 
genvar - var used in for generate loop

sc-pic addsc

#### 5d. Lab For and For Generate part4

rtl
change num1,2 and sum to decimal values

synth
gls


sc-pic addsc
