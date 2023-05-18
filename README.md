
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)

[My Design](#my-design)

[Day 7-9](#day-7-9)

## Day 0

<details>
 <summary> Summary </summary>
	
I installed the needed tools.

</details>	
	
 <details>
 <summary> Yosys </summary>


 I installed Yosys using the following commands:
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys-master 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install
```
Below is the screenshot showing sucessful installation:

<img width="642" alt="yosys-installation" src="https://user-images.githubusercontent.com/49097440/236971441-0680e294-0229-41a8-84b8-9a81c173f667.png">


Below is the screenshot showing sucessful launch:

<img width="568" alt="yosys" src="https://user-images.githubusercontent.com/49097440/236971495-4115ae24-e7e0-460a-81ce-86b5adcb4a15.png">

</details>
 <details>
 <summary> OpenSTA </summary>


 I installed and built OpenSTA (including the needed packages) using the following commands:
 ```bash
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
Below is the screenshot showing sucessful installation:

<img width="644" alt="OpenSTA-installation" src="https://user-images.githubusercontent.com/49097440/236971562-dfd752d0-d04d-47c2-abb9-753fecebe0de.png">


Below is the screenshot showing sucessful launch:

<img width="570" alt="OpenُSTA" src="https://user-images.githubusercontent.com/49097440/236971590-b2fac0d1-bfd1-43fb-a3d4-9fc2febeb414.png">

</details>
 <details>
 <summary> ngspice </summary>


 I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:
 ```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
Below is the screenshot showing sucessful installation:

<img width="641" alt="ngspice-installation" src="https://user-images.githubusercontent.com/49097440/236971614-fe6ebc3a-8ea2-4526-92b5-4b22747a0853.png">


Below is the screenshot showing sucessful launch:

<img width="573" alt="ngspice" src="https://user-images.githubusercontent.com/49097440/236971646-05bd8b13-6166-4fec-ae35-cd5ded8d4741.png">

</details>
 <details>
 <summary> iverilog </summary>


 I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="iverilog-installation" src="https://user-images.githubusercontent.com/49097440/236971696-39580165-f629-4404-bef8-45ebfbedcdcd.png">


 Below is the screenshot showing sucessful launch:
 
 <img width="560" alt="iverilog" src="https://user-images.githubusercontent.com/49097440/236971782-a5ae1815-7ca0-4514-8b9c-6464b012b5c7.png">

</details>
 <details>
 <summary> gtkwave </summary>


 I installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="gtkwave-installation" src="https://user-images.githubusercontent.com/49097440/236971803-bae61afb-35d0-4548-84f8-a687f552500c.png">


Below is the screenshot showing sucessful launch:

<img width="572" alt="gtkwave" src="https://user-images.githubusercontent.com/49097440/236971818-0c6906c4-2839-4913-8d1e-fc173c5d9251.png">

</details>
 <details>
 <summary> magic </summary>


 I installed magic using the following commands:
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```
 Below is the screenshot showing sucessful installation:
 
 <img width="570" alt="magic-installation" src="https://user-images.githubusercontent.com/49097440/236971835-1479cd26-709f-4f1d-9fd2-a389727ad995.png">


Below is the screenshot showing sucessful launch:

<img width="635" alt="magic" src="https://user-images.githubusercontent.com/49097440/236971851-c1ac2fc1-8aa0-4f26-aa4a-ef053c7b47cb.png">
</details>

## Day 1

<details>
 <summary> Summary </summary>

This section shows how I simulated and synthesized a 2x1 mux using iverilog and yosys respectively. iverilog generates from the RTL design and its testbench a value changing dump file (vcd). gtkwave is the tool used to plot the simulation results of the design. Yosys is a tool which synthesizes RTL designs into a netlist. It is also used to test the synthesized netlist when we provide it with a testbench.

</details>	
	
<details>
 <summary> Verilog codes </summary>
The verilog codes of the 2x1 mux (good_mux.v) and its testbench (tb_good_mux.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>

 <details>
 <summary> Simulation: iverilog and gtkwave </summary>
 
 I used the following commands to simulate and view the plots of the RTL design:
	
 ```bash
 iverilog <name verilog: good_mux.v> <name testbench: tb_good_mux.v>
 ./a.out
 gtkwave tb_good_mux.vcd
 ```
	
 Below is the screenshot of the gtkwave plots:
	
 <img width="639" alt="Screen Shot 2023-05-09 at 9 21 02 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2c757bfc-b8ca-41f0-b18d-e976dd02552c">

 </details>

<details>
 <summary> Synthesis: Yosys </summary>
	
 In the directory of the verilog files, I used the following commands to synthesize and view the synthesized deisgn:
	
 ```bash
yosys> read_liberty -lib <path to lib file>
yosys> read_verilog <path to verilog file>
yosys> synth -top <top_module_name>
yosys> abc -liberty <path to lib file>
yosys> show
 ```
 Below is the screenshot of the synthesized design:
	
	
 <img width="504" alt="Screen Shot 2023-05-09 at 9 56 15 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f67d773d-6cc0-435d-bb95-ce62be7e8525">

	
 I used the following commands to generate the netlist:
 ```bash
 yosys> write_verilog <file_name_netlist.v>
 yosys> write_verilog -noattr <file_name_netlist.v>
 ```
 
 Below is the screenshot of the generated netlist:
 
 <img width="636" alt="Screen Shot 2023-05-09 at 10 04 07 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/57513c10-1c2f-4ae8-9a34-535d5f9d3e18">
 
 </details>
	
## Day 2

<details>
 <summary> Summary </summary>

I first synthesized a multiple module (made of two submodules) at the multiple module level (both in hierarchical and flattened forms) then at the submodule level. Synthesis at the submodule level is important for two reasons: 1-) when we have multiple instances of same module (we synthesize once and replicate this netlist multiple times and stitch together the replicas to get the multiple module netlist, and 2-) when we want to divide and conquer (in massive designs) so that the tool can generate a portion by portion of the overall netlist and then we can stitch together the netlist portions to get the multiple module netlist.
After that, I sumulated the different flop designs using iverilog and gtkwave, then synthesized the designs.
Finally, I synthesized 2 designs that were special; their synthesis used optimizations.

</details>	
	
<details>
 <summary> Verilog codes </summary>
The verilog codes of the multiple module (multiple_modules.v), the D-flipflop with asynchronous reset (dff_asyncres.v), the D-flipflop with asynchronous set (dff_async_set.v), the D-flipflop with synchronous reset (dff_syncres.v), their respective testbenches (tb_*), mult_2.v and mult_8.v are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>
	
<details>
 <summary> Synthesis: multiple_modules level </summary>
		
I used the following commands to synthesize and view the design of the hierarchical multiple module:
		
```bash		
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_modules.v>
yosys> synth -top <name: multiple_modules>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: multiple_modules>
yosys> write_verilog -noattr <name: multiple_modules_hier.v>
```
Below is the screenshot of the generated hierarchical design:
		
<img width="530" alt="hier" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4844a043-c175-4de0-b1b7-e3e06a99017a">
	
Below is the screenshot of the generated hierarchical netlist:
		
<img width="645" alt="hiernetlist" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/bfc43804-7293-48e3-b588-cfadf39bda76">

I used the following additional commands to synthesize and view the design of the flattened multiple module:
		
```bash
yosys> flatten
yosys> write_verilog -noattr <name: multiple_modules_flat.v>
```	
Below is the screenshot of the generated flattened design:
		
<img width="574" alt="flatten" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b5b4d527-fa39-46a3-9ae5-8c3b70ebae83">

Below is the screenshot of the generated flattened netlist:
		
<img width="645" alt="flattennetlist" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/461ed9dc-6c37-4c41-888a-f7c5e84b1442">

</details>
<details>
 <summary> Synthesis: sub_module1 level </summary>
		
I used the following commands to view the synthesized design of the submodule:
		
```bash		
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_modules.v>
yosys> synth -top <name: sub_module1>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: sub_module1>
```
	
Below is the screenshot of the generated design:
		
<img width="418" alt="synth_submodule1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2be34dc4-2bab-496e-8683-8d2bb1f90ed2">
		
</details>
<details>
<summary> Simulation: dff with asynchronous reset </summary>

I used the following commands to simulate the RTL design of the dff with asynchronous reset:
	
```bash	
iverilog <name verilog: dff_asyncres.v> <name testbench: tb_dff_asyncres.v>
./a.out
gtkwave <name vcd file: tb_dff_asyncres.vcd>
```	
	
Below is the screenshot of the simulation:
	
<img width="466" alt="asyncres" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9ac7b0c9-a88f-459e-8b86-7613d645ef6a">
	
</details>
<details>
<summary> Simulation: dff with asynchronous set </summary>
I used the following commands to simulate the RTL design of the dff with asynchronous set:
	
```bash	
iverilog <name verilog: dff_async_set.v> <name testbench: tb_dff_async_set.v>
./a.out
gtkwave <name vcd file: tb_dff_async_set.vcd>
```
	
Below is the screenshot of the simulation:
	
<img width="489" alt="asyncset" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ebfebce2-d568-48dc-ac00-5d66fe78ff5e">

</details>
<details>
<summary> Simulation: dff with synchronous reset </summary>
	
I used the following commands to simulate the RTL design of the dff with synchronous reset:
	
```bash	
iverilog <name verilog: dff_syncres.v> <name testbench: tb_dff_syncres.v>
./a.out
gtkwave <name vcd file: tb_dff_syncres.vcd>
```	
	
Below is the screenshot of the simulation:
	
<img width="476" alt="syncres" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6d20f785-a07f-4eae-801d-f7dac19159b6">

</details>
<details>
 <summary> Synthesis: dff with asynchronous reset </summary>

I used the following commands to synthesize the design:
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_asyncres.v>
yosys> synth -top <name: dff_asyncres>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_asyncres>
```
Below is the screenshot of the synthesized design:
	
<img width="415" alt="asyncressynth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/420f2db1-3c7c-44d8-98ed-be6e9ef6bc7e">
	
</details>
<details>
 <summary> Synthesis: dff with asynchronous set </summary>

I used the following commands to synthesize the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_async_set.v>
yosys> synth -top <name: dff_async_set>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_async_set>
```
Below is the screenshot of the synthesized design:
	
<img width="415" alt="asyncsetsynth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/bdb9efd8-3f3b-4048-81e0-7996107f5a31">
	
</details>
<details>
 <summary> Synthesis: dff with synchronous reset </summary>
	
I used the following commands to synthesize the design:
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_syncres.v>
yosys> synth -top <name: dff_syncres>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_syncres>
```
Below is the screenshot of the synthesized design:
	
<img width="418" alt="syncressynth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/805a803c-c7d5-4049-9107-28852c15a4e7">

</details>
<details>
 <summary> Synthesis: mult_2.v </summary>
	
I used the following commands to synthesize and view the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mult_2.v>
yosys> synth -top <name: mul2>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: mul2>
yosys> write_verilog -noattr <name: mul2_net.v>
```
	
Below is the screenshot of the synthesized design, note that no hardware was used (no cells are synthesised) as multiplying a 3-bit input by a power of two is equivalent to shifting for output:
	
<img width="453" alt="mul2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/63af05e1-945d-4a24-862c-f97fbcd45922">
	
Below is the screenshot of the netlist:
	
<img width="636" alt="mul2_net" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/cd6ffe25-388b-48d4-a133-20758c730e58">
	

</details>
<details>
 <summary> Synthesis: mult_8.v </summary>
	
I used the following commands to synthesize and view the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mult_8.v>
yosys> synth -top <name: mult8>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: mult8>
yosys> write_verilog -noattr <name: mult8_net.v>
```
	
Below is the screenshot of the synthesized design, note that no hardware was used (no cells are synthesised) as multiplying a 3-bit input (special case) by a nine is equivalent to replicating the input twice for output:
	
<img width="414" alt="mult8" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ea3937da-6fe9-45b6-a90d-1af514d175ec">
	
Below is the screenshot of the netlist:
	
<img width="645" alt="mult8_net" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9aec2099-3427-4b6f-9d6a-694f846d69bf">


</details>
	
## Day 3
	
<details>
 <summary> Summary </summary>

I have synthesized designs with optimizations. Combinational logic optimizations include 1-) constant propagation (when the combination is just propagating a constant) and 2-) boolean logic optimization (when boolean rules are used to simplify the expression). Sequential logic optimizations include 1-) sequential constant propagation (when constant is propagated with clock involved), 2-) state optimization (when unused states are optimized), 3-) retiming (when logic is split to decrease timing of the different logic portions and increase frequency), and 4-) sequential logic cloning (when physical aware synthesis is done to optimize the floop plan)

</details>	
	
<details>
 <summary> Verilog codes </summary>
	The verilog codes used (opt_*, dff_const*, tb_dff_const*, and counter_opt*) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
	</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check.v </summary>
I used the below commands to view the synthesized design of opt_check.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check.v>
yosys> synth -top <name: opt_check>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 2-input and gate is realized as was expected when optimizations are applied:
	
<img width="676" alt="opt_check" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/24e58532-806f-4ddb-bd6f-67496c516633">

</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check2.v </summary>
	I used the below commands to view the synthesized design of opt_check2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check2.v>
yosys> synth -top <name: opt_check2>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
Below is the screenshot of the obtained optimized design, as we can see a 2-input or gate is realized as was expected when optimizations are applied:
	
<img width="676" alt="opt_check1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6b1f4bf7-3ade-4ce2-a3fd-f2698147c2ad">


</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check3.v </summary>
	
I used the below commands to view the synthesized design of opt_check3.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check3.v>
yosys> synth -top <name: opt_check3>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 3-input and gate is realized as was expected when optimizations are applied:
	
<img width="444" alt="opt_check3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ce988dc4-46a3-4506-a72a-244bc7c0b3a1">


</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check4.v </summary>
	
I used the below commands to view the synthesized design of opt_check4.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check4.v>
yosys> synth -top <name: opt_check4>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 2-input xnor gate is realized as was expected when optimizations are applied:
	
<img width="474" alt="opt_check4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9eef8e44-b195-4f3a-9e15-b016c4743074">


</details>
		
<details>
 <summary> Combinational logic optimizations: multiple_module_opt.v </summary>
	
I used the below commands to view the synthesized design of multiple_module_opt.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_module_opt.v>
yosys> synth -top <name: multiple_module_opt>
yosys> flatten 
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see 2 and gates and 1 or gate are realized as was expected when optimizations are applied:
	
<img width="419" alt="multiple_module_opt" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5f730390-73fa-49a7-96a6-0d80a20d2547">



</details>
	
<details>
 <summary> Combinational logic optimizations: multiple_module_opt2.v </summary>
	
I used the below commands to view the synthesized design of multiple_module_opt2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_module_opt2.v>
yosys> synth -top <name: multiple_module_opt2>
yosys> flatten 
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see no standard cells are realized as was expected when optimizations are applied:
	
<img width="421" alt="multiple_module_opt2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/91e7701e-0982-4a89-bf6d-0a90c81c6fc0">



</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const1.v </summary>
	
I used the below commands to simulate the design of dff_const1.v:
	
```bash
iverilog <name verilog: dff_const1.v> <name testbench: tb_dff_const1.v>
./a.out
gtkwave tb_dff_const1.vdc
```	

Below is the screenshot of the obtained simulation, a we can see even when reset is zero, Q waits for next rising edge of clock:
	
<img width="578" alt="dff_const1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/8833cf95-1957-4cc6-8352-80f40e99364f">

	
I used the below commands to view the synthesized design of dff_const1.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const1.v>
yosys> synth -top <name: dff_const1>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design:
	
<img width="506" alt="dff_const1_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/1809d6c2-f10e-404c-bd4a-6d8de7157bfb">



</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const2.v </summary>
	
I used the below commands to simulate the design of dff_const2.v:
	
```bash
iverilog <name verilog: dff_const2.v> <name testbench: tb_dff_const2.v>
./a.out
gtkwave tb_dff_const2.vdc
```	

Below is the screenshot of the obtained simulation, as we can see Q is one regardless of the value of reset and clock:
	
<img width="629" alt="dff_const2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ba0220c8-f045-425a-b8e6-9ea8031d45f6">

I used the below commands to view the synthesized design of dff_const2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const2.v>
yosys> synth -top <name: dff_const2>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design:
	
<img width="438" alt="dff_const2_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/37d60203-d433-4e23-92fd-92b9d2d20334">


</details>

	
<details>
 <summary> Sequential logic optimizations: dff_const3.v </summary>
	
I used the below commands to simulate the design of dff_const3.v:
	
```bash
iverilog <name verilog: dff_const3.v> <name testbench: tb_dff_const3.v>
./a.out
gtkwave tb_dff_const3.vdc
```	

Below is the screenshot of the obtained simulation, as we can see Q does not follow Q1 immediately:
	
<img width="574" alt="dff_const3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/95620b55-a454-428a-b0c7-b021f90c1b96">

I used the below commands to view the synthesized design of dff_const3.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const3.v>
yosys> synth -top <name: dff_const3>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, the 2 flipflops are retained and optimization could not remove any of them:

<img width="651" alt="dff_const3synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0e5f3ab6-d7e7-410d-a007-e0da72123889">


</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const4.v </summary>
	
I used the below commands to simulate the design of dff_const4.v:
	
```bash
iverilog <name verilog: dff_const4.v> <name testbench: tb_dff_const4.v>
./a.out
gtkwave tb_dff_const4.vdc
```	

Below is the screenshot of the obtained simulation, as we can see Q and Q1 are one regardless of clk and reset:

<img width="614" alt="dff_const4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e10cc842-c807-48c6-b491-b9022abace3d">
	
I used the below commands to view the synthesized design of dff_const4.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const4.v>
yosys> synth -top <name: dff_const4>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and no hardware was used as expected:
	
<img width="424" alt="dff_const4_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b229eeee-ea9e-4058-ba1b-2688f440aadb">

</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const5.v </summary>
	
I used the below commands to simulate the design of dff_const5.v:
	
```bash
iverilog <name verilog: dff_const5.v> <name testbench: tb_dff_const5.v>
./a.out
gtkwave tb_dff_const5.vdc
```	

Below is the screenshot of the obtained simulation, as we can see when reset is zero, Q1 becomes one on the next rising edge of clk, and Q follows Q1 on the next rising edge of clk:

<img width="604" alt="dff_const5" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/1e0d481a-ea0a-45dd-82fe-4d31ece6ea97">

	
I used the below commands to view the synthesized design of dff_const5.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const5.v>
yosys> synth -top <name: dff_const5>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and the 2 flipflops are retained:
	
<img width="629" alt="dff_const5_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b4a8e84a-f1ad-4e2f-9120-199bd7424114">

</details>
	
<details>
 <summary> Sequential logic optimizations for unused outputs: counter_opt.v </summary>
	
I used the below commands to view the synthesized design of counter_opt.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: counter_opt.v>
yosys> synth -top <name: counter_opt>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and the only used output (count[0]) is present and 1 flipflop is used:
	
<img width="684" alt="counter_opt" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/10549f0f-c8d0-4bc8-8069-e14d80770a53">
	
</details>
	
<details>
 <summary> Sequential logic optimizations for 3 used outputs: counter_opt2.v </summary>
	
I used the below commands to view the synthesized design of counter_opt2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: counter_opt2.v>
yosys> synth -top <name: counter_opt2>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and 3 flipflops are used in addition to the counting logic of all bits:
	
<img width="681" alt="counter_opt2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0d8a2613-cae2-4ab6-a8c1-a9bece64dce1">
	
</details>

## Day 4

<details>
 <summary> Summary </summary>

I have performed Gate Level Simulation (GLS). GLS is when the testbench is run with the netlist as design under test to ensure there are no synthesis and simulation mismatches, and it is important as it 1-) verifies the logical correctness of the post-synthesis design and 2-) ensures the timing of design is met. Synthesis and simulation mismatches can happen due to a lot of reasons including missing sensitivity list (some signal changes are not captured by the circuit because they are missing from the sensitivity list), blocking vs non-blocking assignments (inside an always block, "=" statements inside it are blocking meaning they are executed in order they are written, assignments (<=) on the other hand are non-blocking so they are executed in parallel => non-blocking should be used with sequential circuits. Note that the synthesis will yield same circuit with blocking and non-blockin; it will yield what would be obtained as if the statements where written in non-blocking format, so in case they weren't written as such a mismatch will occur with the simulation), and non-standard verilog coding.
	
</details>
	
<details>
 <summary> Verilog codes </summary>
The verilog codes (*_mux.v and blocking_caveat.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>
	
<details>
 <summary> Simulation, synthesis, and GLS: ternary_operator_mux.v </summary>

I used the below commands to simulate the design of ternary_operator_mux.v:
	
```bash
iverilog <name verilog: ternary_operator_mux.v> <name testbench: tb_ternary_operator_mux.v>
./a.out
gtkwave tb_ternary_operator_mux.vdc
```	

Below is the screenshot of the obtained simulation, we can see that when sel is high y follows i1, and when sel is low y follows i0:

<img width="453" alt="ternary_operator_mux" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/625dda82-ef2d-413d-87cf-b04e384ad813">

I used the below commands to synthesize the design into a netlist and view the synthesized design of ternary_operator_mux.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: ternary_operator_mux.v>
yosys> synth -top <name: ternary_operator_mux>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr <name of netlist: ternary_operator_mux_net.v>
yosys> show
```
	
Below is the screenshot of the obtained design:

<img width="442" alt="ternary_operator_mux_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0972ae92-3793-40e3-ab39-8265f06788c0">

Below is the screenshot of the obtained netlist:
	
<img width="670" alt="mux_net" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/92d8ae38-6702-429e-a0ca-92a949f0c6b6">

I used the below commands to carry out GLS of ternary_operator_mux.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to sky130_fd_sc_hd__tt_025C_1v80.lib: ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib> <name netlist: ternary_operator_mux_net.v> <name testbench: tb_ternary_operator_mux.v>
./a.out
gtkwave tb_ternary_operator_mux.vdc
```	
	
Below is the screenshot of the obtained simulation, and this matches with pre-synthesis simulation:
	
<img width="546" alt="gls_ternary" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/86ea7d0a-2cce-4fa0-adea-e4b0620ff37b">

	
</details>

<details>
 <summary> Simulation, synthesis, and GLS: bad_mux.v </summary>

I used the below commands to simulate the design of bad_mux.v:
	
```bash
iverilog <name verilog: bad_mux.v> <name testbench: tb_bad_mux.v>
./a.out
gtkwave tb_bad_mux.vdc
```	

Below is the screenshot of the obtained simulation, we can see that when inputs change, y is not evaluated which is wrong behavior:

<img width="577" alt="bad_mux" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/7175bd2a-5561-49e8-ac44-727a30f6f0d4">


I used the below commands to synthesize the design into a netlist and view the synthesized design of bad_mux.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: bad_mux.v>
yosys> synth -top <name: bad_mux>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr <name of netlist: bad_mux_net.v>
yosys> show
```
	
Below is the screenshot of the obtained design:

<img width="444" alt="bad_mux_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b0bdcc26-59a5-4fce-8bb2-98ed16dbfc9f">

	
Below is the screenshot of the obtained netlist:

<img width="681" alt="bad_mux_net" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f38873d6-ec31-4f24-8b50-881c079fe5c7">
	
I used the below commands to carry out GLS of bad_mux.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to sky130_fd_sc_hd__tt_025C_1v80.lib: ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib> <name netlist: bad_mux_net.v> <name testbench: tb_bad_mux.v>
./a.out
gtkwave tb_bad_mux.vdc
```	
	
Below is the screenshot of the obtained simulation, and this mismatches with pre-synthesis simulation:
	
<img width="572" alt="gls" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2079af8e-a38a-4e68-bc8c-53b43886aeac">
	
</details>

<details>
 <summary> Simulation, synthesis, and GLS: blocking_caveat.v </summary>

I used the below commands to simulate the design of blocking_caveat.v:
	
```bash
iverilog <name verilog: blocking_caveat.v> <name testbench: tb_blocking_caveat.v>
./a.out
gtkwave tb_blocking_caveat.vdc
```	

Below is the screenshot of the obtained simulation, and as we can see d is seeing the precious values, and hence it is acting as if there was a flop in the circuit which is not the case (incorrect behavior):

<img width="599" alt="blocking_caveat" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e0a96a0b-8dbd-40e9-af33-cce8eeb060b9">

I used the below commands to synthesize the design into a netlist and view the synthesized design of blocking_caveat.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: blocking_caveat.v>
yosys> synth -top <name: blocking_caveat>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr <name of netlist: blocking_caveat_net.v>
yosys> show
```
	
Below is the screenshot of the obtained design:

<img width="435" alt="blocking_caveat_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/016610f4-1824-4bc8-858e-e8c4d5f1c053">
	
Below is the screenshot of the obtained netlist:

<img width="674" alt="blocking_caveat_net" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/29232088-b13e-42f3-a21a-08c843f1e92b">

I used the below commands to carry out GLS of blocking_caveat.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: blocking_caveat_net.v> <name testbench: tb_blocking_caveat.v>
./a.out
gtkwave tb_blocking_caveat.vdc
```	
	
Below is the screenshot of the obtained simulation, and this mismatches with pre-synthesis simulation due to blocking statement:
	
<img width="469" alt="blocking_conveat_gls" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0094a4df-ef93-4a5a-8d78-38f27735b6c4">
	
</details>

## Day 5
	
<details>
 <summary> Summary </summary>

I have first learned about "if" and "case" statements which are used inside always blocks. "if" statements are used to convey priority logic (ony one portion can be executed), and the hardware will look like a series of muxes in hardware, but in "case" statements there is no inferred priotity (sequential execution can mean multiple portions can be executed) but also the hardware would be a series of muxes. Inferred latches can occur if there is an incomplete "if" statement (no else), in this case the hardware will have a latch storing a previous output value. This is bad coding example unless the latch is intended (like in case of a counter). Incomplete "case" can lead to inferred latches too, and to avoid that code the "case" with a default. Another caveat of "case" statements is partial assignments which also creates inferred latches, and to avoid that we should assign all the outputs in all the segments of the case. In "case" statements, one must be careful that portions should not be overlapping otherwise they could be executed due to the sequential non-prioritized execution of those statement.
Then I have learned about looping constructs: for loop (inside always block) and generate for loop (cannot be used inside always block). The for loop is used to evaluate expressions in blocking format (provides code efficiency as complexity of circuits increases) while the generate for loop is used to instantiate hardware (provides code efficiency when hardware instantiation increases in complexity). 
	
</details>

<details>
 <summary> Verilog codes </summary>	

The verilog codes (incomp*.v, *_case.v, *_generate.v, demux_case.v, and RCA.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
	
</details>
	
<details>
 <summary> Simulation and synthesis: incomp_if.v </summary>

I used the below commands to simulate the design of incomp_if.v:
	
```bash
iverilog <name verilog: incomp_if.v> <name testbench: tb_incomp_if.v>
./a.out
gtkwave tb_incomp_if.vdc
```	

Below is the screenshot of the obtained simulation, we can see that there is an inferred latch as output is latching to a constant value when select is not high:

<img width="524" alt="incomp_if" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c64ba438-2358-431b-ad91-d187cb733fa7">


I used the below commands to view the synthesized design of incomp_if.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: incomp_if.v>
yosys> synth -top <name: incomp_if>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, and a latch is seen as was expected:

<img width="401" alt="incomp_if_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/71763ef1-3ec8-437a-a369-967b6d1bfa4f">

</details>
	
<details>
 <summary> Simulation and synthesis: incomp_if2.v </summary>

I used the below commands to simulate the design of incomp_if2.v:
	
```bash
iverilog <name verilog: incomp_if2.v> <name testbench: tb_incomp_if2.v>
./a.out
gtkwave tb_incomp_if2.vdc
```	

Below is the screenshot of the obtained simulation, we can see that the output latches a constant value when i0 and i2 are zero:

<img width="500" alt="incomp_if2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/144a4706-ff21-4363-b25f-6662b1339242">


I used the below commands to view the synthesized design of incomp_if2.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: incomp_if2.v>
yosys> synth -top <name: incomp_if2>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, and we can see a latch as was expected:

<img width="402" alt="incomp_if2_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6a881ff9-3d8b-462a-832b-642f123a1855">

</details>

<details>
 <summary> Simulation and synthesis: incomp_case.v </summary>

I used the below commands to simulate the design of incomp_case.v:
	
```bash
iverilog <name verilog: incomp_case.v> <name testbench: tb_incomp_case.v>
./a.out
gtkwave tb_incomp_case.vdc
```	

Below is the screenshot of the obtained simulation, we can see that the output latches a constant value when select has a vlaue of 2 or 3 (when sel[1] is 1):

<img width="453" alt="incomp_case" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5d106ee8-07ac-4eab-9803-721d0ba0a0ae">


I used the below commands to view the synthesized design of incomp_case.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: incomp_case.v>
yosys> synth -top <name: incomp_case>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, and we can see a latch as was expected:
	
<img width="623" alt="incomp_case_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5279b522-f996-4ce6-8d73-a1a6354b9a3e">

</details>

<details>
 <summary> Simulation and synthesis: comp_case.v </summary>

I used the below commands to simulate the design of comp_case.v:
	
```bash
iverilog <name verilog: comp_case.v> <name testbench: tb_comp_case.v>
./a.out
gtkwave tb_comp_case.vdc
```	

Below is the screenshot of the obtained simulation, we can see that the output follows i2 when select has a value of 2 or 3 (when sel[1] is 1):

<img width="639" alt="comp_case" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2d3f3a7e-9795-4a85-b6ab-9d849b2e720b">

I used the below commands to view the synthesized design of comp_case.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: comp_case.v>
yosys> synth -top <name: comp_case>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, and we do not see a latch as was expected:
	
<img width="593" alt="comp_case_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/fc321697-44b0-48ed-8988-326f7dcfdbc7">

</details>
	
<details>
 <summary> Synthesis: partial_case_assign.v </summary>

I used the below commands to view the synthesized design of partial_case_assign.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: partial_case_assign.v>
yosys> synth -top <name: partial_case_assign>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, and we see one latch for x output as was expected, and the boolean expressions of x and y that were expected are also inferred by the design obtained:
	
<img width="569" alt="partial_case_assign" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6be0228a-1611-4144-98aa-0e09724639fa">

</details>

<details>
 <summary> Simulation, synthesis, and GLS: bad_case.v </summary>

I used the below commands to simulate the design of bad_case.v:
	
```bash
iverilog <name verilog: bad_case.v> <name testbench: tb_bad_case.v>
./a.out
gtkwave tb_bad_case.vdc
```	

Below is the screenshot of the obtained simulation, we can see that when sel is "11", the simulator is getting confused and output y is taking a constant "1" value:
	
<img width="635" alt="bad_case" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4af4ae42-39ea-4412-9cad-ad63d5c69920">

I used the below commands to synthesize and view the synthesized design of bad_case.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: bad_case.v>
yosys> synth -top <name: bad_case>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr bad_case_net.v
yosys> show
```
	
Below is the screenshot of the obtained design, and there is no inferred latch:
	
<img width="417" alt="bad_case_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ce2801e6-6848-420a-a647-741e362343ea">
	
I used the below commands to carry out GLS of bad_case.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: bad_case_net.v> <name testbench: tb_bad_case.v>
./a.out
gtkwave tb_bad_case.vdc
```	
	
Below is the screenshot of the obtained simulation, and this mismatches with pre-synthesis simulation. When sel is "11", y takes value of i3 and no latching happens here:
	
<img width="635" alt="gls_bad_case" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/33125774-e5bb-4649-8614-1d04bc6926d2">

</details>

<details>
 <summary> Simulation, synthesis, and GLS: mux_generate.v </summary>

I used the below commands to simulate the design of mux_generate.v:
	
```bash
iverilog <name verilog: mux_generate.v> <name testbench: tb_mux_generate.v>
./a.out
gtkwave tb_mux_generate.vdc
```	

Below is the screenshot of the obtained simulation, we can see it's a 4:1 mux functionality:
	
<img width="637" alt="mux_generate" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/68db59a3-f58b-42cd-a6e7-55775213a6ac">

I used the below commands to synthesize and view the synthesized design of mux_generate.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mux_generate.v>
yosys> synth -top <name: mux_generate>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr mux_generate_net.v
yosys> show
```
	
Below is the screenshot of the obtained design, and it is a 4:1 mux:
	

<img width="477" alt="mux_generate" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/7088fd71-6d8c-4ca1-b7dd-de5aff78fa12">

I used the below commands to carry out GLS of mux_generate.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: mux_generate_net.v> <name testbench: tb_mux_generate.v>
./a.out
gtkwave tb_mux_generate.vdc
```	
	
Below is the screenshot of the obtained simulation, and this matches with pre-synthesis simulation:

<img width="635" alt="mux_generate_gls" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c18f62ac-7ddd-4c93-874a-fc02755a236c">

</details>
	
<details>
 <summary> Simulation: demux_case.v </summary>

I used the below commands to simulate the design of demux_case.v:
	
```bash
iverilog <name verilog: demux_case.v> <name testbench: tb_demux_case.v>
./a.out
gtkwave tb_demux_case.vdc
```	

Below is the screenshot of the obtained simulation, we can see it's a 1:8 demux functionality:
	
<img width="640" alt="demux_case" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5270c179-191c-4691-ae64-f9dc75c1921e">


</details>
	
<details>
 <summary> Simulation, synthesis, and GLS: demux_generate.v </summary>

I used the below commands to simulate the design of demux_generate.v:
	
```bash
iverilog <name verilog: demux_generate.v> <name testbench: tb_demux_generate.v>
./a.out
gtkwave tb_demux_generate.vdc
```	

Below is the screenshot of the obtained simulation, we can see it's a 1:8 demux functionality (same as demux_case.v):
	
<img width="612" alt="demux_generate" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f85b43b6-c2fd-431f-a020-c666dba1d948">


I used the below commands to synthesize and view the synthesized design of demux_generate.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: demux_generate.v>
yosys> synth -top <name: demux_generate>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr demux_generate_net.v
yosys> show
```
	
Below is the screenshot of the obtained design, and it is a 1:8 demux:
	
<img width="530" alt="demux_gnerate_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c4cf0c7e-ea2d-4274-b92c-a29501922479">


I used the below commands to carry out GLS of demux_generate.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: demux_generate_net.v> <name testbench: tb_demux_generate.v>
./a.out
gtkwave tb_demux_generate.vdc
```	
	
Below is the screenshot of the obtained simulation, and this matches with pre-synthesis simulation:

<img width="489" alt="Screen Shot 2023-05-15 at 8 09 26 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5529ad20-c7d1-43b5-b6ca-a85e2f41ec33">


</details>
	
<details>
 <summary> Simulation, synthesis, and GLS: rca.v </summary>

I used the below commands to simulate the design of rca.v:
	
```bash
iverilog <name verilog: rca.v> <name verilog: fa.v> <name testbench: tb_rca.v>
./a.out
gtkwave tb_rca.vdc
```	

Below is the screenshot of the obtained simulation, we can see it's an 8-bit RCA functionality:
	
<img width="491" alt="rca" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/24818b94-0b13-4af9-a863-143ee0f0057e">

I used the below commands to synthesize and view the synthesized design of rca.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: rca.v>
yosys> read_verilog <name of verilog file: fa.v>
yosys> synth -top <name: rca>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr rca_net.v
yosys> show
```
	
Below is the screenshot of the obtained design, and it is an 8-bit RCA:

<img width="543" alt="rca_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/106a4de4-23a4-49c1-b60f-d7275028d9c8">

I used the below commands to carry out GLS of rca.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: rca_net.v> <name testbench: tb_rca.v>
./a.out
gtkwave tb_rca.vdc
```	
	
Below is the screenshot of the obtained simulation, and this matches with pre-synthesis simulation:

<img width="554" alt="rca_gls" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/7236dd1d-81d5-4248-9863-f147ee0b46c8">

</details>
	
## My Design
	
<details>
 <summary> Summary </summary>
	
I chose a 4-bit updown counter in order to practice the flow I learned in the first training module (days 1-5). The updown counter counts either up or down.

</details>	
	
<details>
 <summary> Verilog codes </summary>	

The original verilog code and its associated testbench of the updown counter can be found on https://www.fpga4student.com/2017/03/verilog-code-for-counter-with-testbench.html
	
I have modified the testbench (named tb_mariam_updown_counter) in order to dump the vcd file and I changed when some signals change values too. Note that I have also renamed the verilog module as mariam_updown_counter. The modified testbench can be found below:
	
```bash
// FPGA projects using Verilog/ VHDL
// fpga4student.com: FPGA projects, Verilog projects, VHDL projects
// Verilog code for up-down counter with testbench
// Testbench Verilog code for up-down counter
// modified by Mariam Rakka
`timescale 1ns / 1ps
module tb_mariam_updown_counter;
	reg clk, reset,up_down;
	wire [3:0] counter;
	mariam_updown_counter uut(.clk(clk), .reset(reset), .up_down(up_down), .counter(counter));

	initial begin 
	$dumpfile("tb_mariam_updown_counter.vcd");
	$dumpvars(0,tb_mariam_updown_counter);
	clk=0;
	reset=1;
	up_down=0; #20;
	reset=0; #200;
	up_down=1; #220;
	#300 $finish;
	end

always #5 clk=~clk;
endmodule 
```
	
</details>

<details>
 <summary> Simulation, synthesis, and GLS: mariam_updown_counter.v </summary>

I used the below commands to simulate the design of mariam_updown_counter.v:
	
```bash
iverilog <name verilog: mariam_updown_counter.v> <name testbench: tb_mariam_updown_counter.v>
./a.out
gtkwave tb_mariam_updown_counter.vdc
```	

Below is the screenshot of the obtained simulation, we can see that when reset is high, counter is 0. Otherwise when reset is low, if updown is low, counter counts up by a value of 1 (until 15 in decimal is reached as 15 is 1111 in binary and this is the highest value of our 4-bit counter, after which, counter counts up again starting from 0) on positive edges of the clock, but if updown is high, counter counts down by a value of 1 (until 0 in decimal is reached as 0 is 0000 in binary and this is the lowest value of our 4-bit counter, after which, counter counts down again starting from 15) on positive edges of the clock:
	
<img width="634" alt="mydesign" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/7e97c3ef-2e07-41e2-bc7d-b8d6ed2bdd24">

	
I used the below commands to synthesize and view the synthesized design of mariam_updown_counter.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mariam_updown_counter.v>
yosys> synth -top <name: mariam_updown_counter>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> write_verilog -noattr mariam_updown_counter_net.v
yosys> show
```
	
Below is the screenshot of the obtained design:
	
<img width="1461" alt="mydesign_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/3485bcef-e87c-41de-ae5c-77b4b0e713bd">
	
I used the below commands to carry out GLS of mariam_updown_counter.v:
	
```bash
iverilog <path to verilog model: ../mylib/verilog_model/primitives.v> <path to verilog model: ../mylib/verilog_model/sky130_fd_sc_hd.v> <name netlist: mariam_updown_counter_net.v> <name testbench: tb_mariam_updown_counter.v>
./a.out
gtkwave tb_mariam_updown_counter.vdc
```	
	
Below is the screenshot of the obtained simulation, and this matches with pre-synthesis simulation:
	
<img width="575" alt="mydesign_gls" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f42b6269-b810-4b34-8111-7e1d38475fdf">

Below is the code of the generated netlist:

```bash
/* Generated by Yosys 0.27+22 (git sha1 0f5e7c244, x86_64-conda-linux-gnu-cc 11.2.0 -fvisibility-inlines-hidden -fmessage-length=0 -march=nocona -mtune=haswell -ftree-vectorize -fPIC -fstack-protector-strong -fno-plt -O2 -ffunction-sections -fdebug-prefix-map=/root/conda-eda/conda-eda/workdir/conda-env/conda-bld/yosys_1680770278298/work=/usr/local/src/conda/yosys-0.27_29_g0f5e7c244 -fdebug-prefix-map=/usr/bin/miniconda3=/usr/local/src/conda-prefix -fPIC -Os -fno-merge-constants) */
	
module mariam_updown_counter(clk, reset, up_down, counter);
  wire _00_;
  wire _01_;
  wire _02_;
  wire _03_;
  wire _04_;
  wire _05_;
  wire _06_;
  wire _07_;
  wire _08_;
  wire _09_;
  wire _10_;
  wire _11_;
  wire _12_;
  wire _13_;
  wire _14_;
  wire _15_;
  wire _16_;
  wire _17_;
  wire _18_;
  wire _19_;
  wire _20_;
  wire _21_;
  wire _22_;
  wire _23_;
  wire [3:0] _24_;
  input clk;
  wire clk;
  output [3:0] counter;
  wire [3:0] counter;
  reg [3:0] counter_up_down;
  input reset;
  wire reset;
  input up_down;
  wire up_down;
  sky130_fd_sc_hd__clkinv_1 _25_ (
    .A(_13_),
    .Y(_09_)
  );
  sky130_fd_sc_hd__clkinv_1 _26_ (
    .A(_23_),
    .Y(_17_)
  );
  sky130_fd_sc_hd__xor2_1 _27_ (
    .A(_23_),
    .B(_14_),
    .X(_18_)
  );
  sky130_fd_sc_hd__xnor2_1 _28_ (
    .A(_09_),
    .B(_18_),
    .Y(_10_)
  );
  sky130_fd_sc_hd__maj3_1 _29_ (
    .A(_13_),
    .B(_23_),
    .C(_14_),
    .X(_19_)
  );
  sky130_fd_sc_hd__xnor2_1 _30_ (
    .A(_23_),
    .B(_15_),
    .Y(_20_)
  );
  sky130_fd_sc_hd__xnor2_1 _31_ (
    .A(_19_),
    .B(_20_),
    .Y(_11_)
  );
  sky130_fd_sc_hd__nand4b_1 _32_ (
    .A_N(_23_),
    .B(_14_),
    .C(_15_),
    .D(_13_),
    .Y(_21_)
  );
  sky130_fd_sc_hd__o31a_1 _33_ (
    .A1(_17_),
    .A2(_15_),
    .A3(_19_),
    .B1(_21_),
    .X(_22_)
  );
  sky130_fd_sc_hd__xnor2_1 _34_ (
    .A(_16_),
    .B(_22_),
    .Y(_12_)
  );
  always @(posedge clk, posedge reset)
    if (reset) counter_up_down[0] <= 1'h0;
    else counter_up_down[0] <= _24_[0];
  always @(posedge clk, posedge reset)
    if (reset) counter_up_down[1] <= 1'h0;
    else counter_up_down[1] <= _24_[1];
  always @(posedge clk, posedge reset)
    if (reset) counter_up_down[2] <= 1'h0;
    else counter_up_down[2] <= _24_[2];
  always @(posedge clk, posedge reset)
    if (reset) counter_up_down[3] <= 1'h0;
    else counter_up_down[3] <= _24_[3];
  assign counter = counter_up_down;
  assign _13_ = counter_up_down[0];
  assign _24_[0] = _09_;
  assign _23_ = up_down;
  assign _14_ = counter_up_down[1];
  assign _24_[1] = _10_;
  assign _15_ = counter_up_down[2];
  assign _24_[2] = _11_;
  assign _16_ = counter_up_down[3];
  assign _24_[3] = _12_;
endmodule
```
	
</details>
	
## Day 7-9
	
<details>
 <summary> Summary </summary>
I have learned about Static Timing Analysis (STA). First, it is important to note that min delay (Thold<=Tcq_inflop+Tcomb) and max delay (Tclk>= Tcq_inflop+Tcomb+Tsetup_captureflop) are two sides of the same coin: if there was no min delay we could have met any max delay requirement by pushing the clock. But when we push the clock we interfere with the time of the "capture" flop. Delay is a function of inflow of current (i.e. input transition): if there is fast current sourcing, we will get less delay (fast-rise). Delay is also a function of load capacitance. The timing arcs in combinational cells consist the delay information from every input pin to every outp-ut pin it can control. The timing arcs in a sequantial cell consist of delay from clock to Q for D flipflop or of delay from clock to Q and that from D to Q in case of a D latch. In both cases, timing arcs in a sequential cell also consist of setup/hold delays from clock to D. Note that setup/hold are around the sampling. Below is a picture noting the timing arcs in the sequential case.
	
<img width="653" alt="sta_note" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/a6992e61-eab3-472b-a94d-8571e87cabac">

Timing paths have start points (input ports or/and clock pins of registers) and end points (output ports or/and D pin of DFF/DLAT). Tming paths always start at one start point and end at one end point: clock to D timing paths are the register-register timing paths, clock to output and input to D timing paths are IO timing paths, input to output timing paths are indesirable to have in designs. A critical path is that which decides or limits the clock frequency because it has the most delay incurred. If I reduce the delay in the critical path, I can increase the freq (fclk=1/Tclk, where Tclk>= Tcq+Tcomb+Tsetup). It is Tclk that decides Tcomb and not vice versa. That is why we need the constraints, 1-) I set the clock period and my synthesis tool will work to optimize the register-register time paths (by choosing what cells to connect in combinational logic part) to meet that constraint (Tcq and Tsetup are picked up from .lib) => register-register timing paths are constraints by clock. 2-) I need to contstraint the input delay in order to have synchronous paths (from external registers to internal registers) working on the same clock => input-register timing paths are constrained by the input external delay and clock. 3-) I have to constraint the output delay as to have synchronous paths (from internal registers to external registers) working on the same clock => register-output timing paths are constrained by the output external delay and clock. Note that register-output and input-register timing paths are collectively the IO timing paths (delay associated to them is called IO delay modeling). IO pathes also need to be constrained for max delay (setup) and min delay (hold).
	

From input side perspective: Tclk=Tinp-ext+Tint where Tint=Tinputlogic+Tsetup, here external delay is accounted for, but the input signals are not ideal, the transitions (non-zero rise time) will lead Tinputlogic to increase hence violating the setup time => need to model those input transitions by adding constraints => Input-register time paths are constrained by input external delay, clock, and input transitions.
	
From output side perspective: Tclk=Tint+Topext where Tint=Tcq+Toplogic and Topext includes Tsetup, here external delay accounted for, but output load is not and this might lead to setup violations => need to model output load (from specs) by adding constraints. Register-input time paths are constrained by output external delay, clock, and output load.
	
Rule of thumb: The Tclk is 70% for external delay and 30% internal delay. The synthesis tools infer the cell delay numbers from the .lib file.
	
Some .lib file terminologies: 
	
1-) max capacitance limit: determines the maximum loading capacitance, beyond which the tool should break out the circuit and add buffers.
	
2-) delay model lookup table: delay = f(input transition+output load), so for every cell there is a table that has the delay values corresponding to a pair of input transition value (index_2) and output load value (index_1). Numbers not in table are interpolated.
	
3-) _and2_2 is wider, faster and has more area than _and2_0
		
4-) unateness: positive unateness is when the input rises (one pin), the output either does not change or it also rises (true for AND, OR). Negative unateness is when the input rises (one pin), the output either does not change or it falls (true for NOT, NAND, NOR). XOR is non-unate as input rise in one pin can cause either rise or fall in output. In D fliflop, with respect to clock, Q has no unateness, but with respect to  => This information is used by the tool to propagate the signal. 
	
5-) timing_type: combinational or falling_edge/rising_edge conveys combinatioal or sequential logic respectively. setup_falling and setup_rising indicate that the setup time is measured at the falling and rising edge respectively. 
	
</details>
	
<details>
 <summary> Useful dc shell commands </summary>	
	
In order to show the library name, the file name, and the path, use the following command:
	
```bash
list_lib
```	
	
In order to list the library cells of name containing "and" (this includes nand) one by one, use the following commands:
	
```bash
foreach_in_collection <looping variable: my_lib_cell> [get_lib_cells */*and] {
set <another variable: my_lib_cell_name [get_object_name $my_lib_cell];
echo $my_lib_cell_name; 
}
```

In order to view pins of a library, display direction (this is the attribute we are querying, when =2 it means pin is output) of all pins we use the following commands:
	
```bash
get_lib_pins <path/librarycellnamefromprevcommand/*> 
foreach_in_collection <variable name: my_pins> [get_lib_pins <path/librarycellnamefromprevcommand/*>] {
set <another variable: my_pin_name [get_object_name $my_pins];
set <another variable: pin_dir> [get_lib_attribute $my_pin_name <attribute name:direction>];
echo $my_pin_name $pin_dir;
}
```
	
In order to select a pin (output) and view its functionality and area, then view the capacitance of a certain pin, check whether it is a clock pin or not, use the following commands:

```bash
get_lib_attribute <nameoflibpinfromprevcommands> function
get_lib_attribute <nameofcellfromprevcommands> area
get_lib_attribute <nameoflibpinfromprevcommands> capacitance
get_lib_attribute <nameoflibpinfromprevcommands> clock
```

In order to find output pin and its functionality for each cell in a list, write a script (my_script.tcl, shown below), then source it:
	
```bash
set <variable name: my_list> [list <path/librarycellnamefromprevcommand \
path/librarycellnamefromprevcommand\
path/librarycellnamefromprevcommand ]
foreach <variable name: my_cell> $my_list {
	foreach_in_collection <variable name: my_lib_pin> [get_lib_pins $(my_cell)/*] {
		set <variable name: my_lib_pin_name> [get_object_name $my_lib_pin];
		set <variable name: a> [get_lib_attribute $my_lib_pin_name direction];
		if { $a > 1 } {
			set <variable name: fn> [get_lib_attribute $my_lib_pin_name function];
			echo $my_lib_pin_name $a $fn;
		}
	}
```

In order to find out all cells in library that are sequential, use the following command:

```bash
get_lib_cells */* -filter "is_sequential == true"
```

In order to write all available attributes that can be used to do queries to a file, use the following command:
	
```bash
list_attributes -app > <name: a>
```
	
</details>
	
