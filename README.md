
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)

[My Design Part 1](#day-6)

[Day 7](#day-7)

[Day 8](#day-8)

[My Design Part 2](#day-9)

[Day 10](#day-10)

[Day 11](#day-11)

[Day 12](#day-12)

[Day 13](#day-13)

[Day 14](#day-14)

[Day 15](#day-15)

[My Design Part 3](#day-16)

[Day 17](#day-17)

[Day 18](#day-18)

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
	
## Day 6
	
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
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
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

(* top =  1  *)
(* src = "mariam_updown_counter.v:4.1-18.10" *)
module mariam_updown_counter(clk, reset, up_down, counter);
  wire 00;
  wire 01;
  wire 02;
  wire 03;
  wire 04;
  wire 05;
  wire 06;
  wire 07;
  wire 08;
  (* src = "mariam_updown_counter.v:15.23-15.45|/usr/bin/miniconda3/bin/../share/yosys/techmap.v:270.26-270.27" *)
  wire 09;
  (* src = "mariam_updown_counter.v:15.23-15.45|/usr/bin/miniconda3/bin/../share/yosys/techmap.v:270.26-270.27" *)
  wire 10;
  (* src = "mariam_updown_counter.v:15.23-15.45|/usr/bin/miniconda3/bin/../share/yosys/techmap.v:270.26-270.27" *)
  wire 11;
  (* src = "mariam_updown_counter.v:15.23-15.45|/usr/bin/miniconda3/bin/../share/yosys/techmap.v:270.26-270.27" *)
  wire 12;
  wire 13;
  wire 14;
  wire 15;
  wire 16;
  (* src = "mariam_updown_counter.v:5.11-5.26" *)
  wire 17;
  (* src = "mariam_updown_counter.v:5.11-5.26" *)
  wire 18;
  (* src = "mariam_updown_counter.v:5.11-5.26" *)
  wire 19;
  (* src = "mariam_updown_counter.v:5.11-5.26" *)
  wire 20;
  wire 21;
  wire 22;
  wire 23;
  wire 24;
  wire 25;
  wire 26;
  (* src = "mariam_updown_counter.v:4.41-4.46" *)
  wire 27;
  (* src = "mariam_updown_counter.v:4.47-4.54" *)
  wire 28;
  (* force_downto = 32'd1 *)
  (* src = "mariam_updown_counter.v:15.23-15.45|/usr/bin/miniconda3/bin/../share/yosys/techmap.v:270.26-270.27" *)
  wire [3:0] 29;
  wire 30;
  wire 31;
  wire 32;
  wire 33;
  (* src = "mariam_updown_counter.v:4.36-4.39" *)
  input clk;
  wire clk;
  (* src = "mariam_updown_counter.v:4.69-4.76" *)
  output [3:0] counter;
  wire [3:0] counter;
  (* src = "mariam_updown_counter.v:5.11-5.26" *)
  wire [3:0] counter_up_down;
  (* src = "mariam_updown_counter.v:4.41-4.46" *)
  input reset;
  wire reset;
  (* src = "mariam_updown_counter.v:4.47-4.54" *)
  input up_down;
  wire up_down;
  sky130_fd_sc_hd_clkinv_1 _34 (
    .A(17),
    .Y(09)
  );
  sky130_fd_sc_hd_clkinv_1 _35 (
    .A(28),
    .Y(21)
  );
  sky130_fd_sc_hd_clkinv_1 _36 (
    .A(27),
    .Y(13)
  );
  sky130_fd_sc_hd_xor2_1 _37 (
    .A(28),
    .B(18),
    .X(22)
  );
  sky130_fd_sc_hd_xnor2_1 _38 (
    .A(09),
    .B(22),
    .Y(10)
  );
  sky130_fd_sc_hd_maj3_1 _39 (
    .A(17),
    .B(28),
    .C(18),
    .X(23)
  );
  sky130_fd_sc_hd_xnor2_1 _40 (
    .A(28),
    .B(19),
    .Y(24)
  );
  sky130_fd_sc_hd_xnor2_1 _41 (
    .A(23),
    .B(24),
    .Y(11)
  );
  sky130_fd_sc_hd_nand4b_1 _42 (
    .A_N(28),
    .B(18),
    .C(19),
    .D(17),
    .Y(25)
  );
  sky130_fd_sc_hd_o31a_1 _43 (
    .A1(21),
    .A2(19),
    .A3(23),
    .B1(25),
    .X(26)
  );
  sky130_fd_sc_hd_xnor2_1 _44 (
    .A(20),
    .B(26),
    .Y(12)
  );
  sky130_fd_sc_hd_clkinv_1 _45 (
    .A(27),
    .Y(14)
  );
  sky130_fd_sc_hd_clkinv_1 _46 (
    .A(27),
    .Y(15)
  );
  sky130_fd_sc_hd_clkinv_1 _47 (
    .A(27),
    .Y(16)
  );
  (* src = "mariam_updown_counter.v:8.1-16.4" *)
  sky130_fd_sc_hd_dfrtp_1 _48 (
    .CLK(clk),
    .D(29[0]),
    .Q(counter_up_down[0]),
    .RESET_B(30)
  );
  (* src = "mariam_updown_counter.v:8.1-16.4" *)
  sky130_fd_sc_hd_dfrtp_1 _49 (
    .CLK(clk),
    .D(29[1]),
    .Q(counter_up_down[1]),
    .RESET_B(31)
  );
  (* src = "mariam_updown_counter.v:8.1-16.4" *)
  sky130_fd_sc_hd_dfrtp_1 _50 (
    .CLK(clk),
    .D(29[2]),
    .Q(counter_up_down[2]),
    .RESET_B(32)
  );
  (* src = "mariam_updown_counter.v:8.1-16.4" *)
  sky130_fd_sc_hd_dfrtp_1 _51 (
    .CLK(clk),
    .D(29[3]),
    .Q(counter_up_down[3]),
    .RESET_B(33)
  );
  assign counter = counter_up_down;
  assign 17 = counter_up_down[0];
  assign 29[0] = 09;
  assign 28 = up_down;
  assign 18 = counter_up_down[1];
  assign 29[1] = 10;
  assign 19 = counter_up_down[2];
  assign 29[2] = 11;
  assign 20 = counter_up_down[3];
  assign 29[3] = 12;
  assign 27 = reset;
  assign 30 = 13;
  assign 31 = 14;
  assign 32 = 15;
  assign 33 = 16;
endmodule
```
	
</details>
	
## Day 7
	
<details>
 <summary> Summary </summary>
I have learned about Static Timing Analysis (STA). First, note that setup time is the time the input data signals must be stable (either high or low) before the active clock edge occurs while hold time is the time the input data signals must be stable (either high or low) after the active clock edge occurs. It is important to note that min delay (Thold<=Tcq_inflop+Tcomb) and max delay (Tclk>= Tcq_inflop+Tcomb+Tsetup_captureflop) are two sides of the same coin: if there was no min delay we could have met any max delay requirement by pushing the clock. But when we push the clock we interfere with the time of the "capture" flop. Delay is a function of inflow of current (i.e. input transition): if there is fast current sourcing, we will get less delay (fast-rise). Delay is also a function of load capacitance. The timing arcs in combinational cells consist the delay information from every input pin to every outp-ut pin it can control. The timing arcs in a sequantial cell consist of delay from clock to Q for D flipflop or of delay from clock to Q and that from D to Q in case of a D latch. In both cases, timing arcs in a sequential cell also consist of setup/hold delays from clock to D. Note that setup/hold are around the sampling. Below is a picture noting the timing arcs in the sequential case.
	
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
	

## Day 8
	
<details>
 <summary> Summary </summary>
	
I learned about advanced constraints. There is a delay in routing the clock which is not seen by the synthesis too due to the below ASIC flow, where clock routing is done post synthesis in the Clock Tree Synthesis (CTS) step shown below:
	
<img width="717" alt="sta_note" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0203b6cd-8363-49a6-a6bc-8fc100bb6f7b">
	
The clock generation happens through aan osillator, PLL, or external clock source. All these sources have inherent varitions in the clock period due to stochastic effects, so a practical clock has a non-zero rise time and there is also gitter (capture edge of clock doesn't come exactly where it is expected and hence capture window is reduced). In a practical clock network, all flops may not see the clock edge at the same instance, this is known as clock skew => These delays should be considered by the sythesis through constraints.
	
Clock modeling should take into consideration the latency of source (time taken by source to generate the clock), period, clock network latency (time taken by the clock distribution network), clock skew (clock path delay mismatches which causes difference in the arrival of the clock), and jitter. After CTS however, the skew and clock network constraints must be removed. These sources are shown below:
	
<img width="556" alt="sta_note5" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/326edcbf-f523-4fba-823e-e482ae84dadb">

I also learned how to convey all the constraits we learned about using the Synopsys Design Constraints format understood by the DC.
	
Important terminology associted with constraints:
	
1-) ports: primary IOs of the design 
	
2-) nets: interconnections between pins (associated with gates) or between pin and port. A net can have only one driver (multidriven nets are corrupted, but within one standard cell this is fine as the sizing decides what drives what etc like in a latch), but it can drive multiple pins.
	
</details>
	
<details>
 <summary> Verilog codes </summary>	
	
The verilog codes used (lab8_circuit.v and lab14_circuit.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
	
</details>
	
<details>
 <summary> Useful dc shell commands </summary>	
	
To query the pins, check whether a pin is a clock, check all clocks reaching a pin (here clocks created by commands further down will be shown), and query ports in dc shell, use the following commands (note that port, pin, clock, etc are all names which are case sensitive):
	
```bash
get_pins *;
get_attribute [get_pins <pin_name>] clock;
get_attribute [get_pins <pin_name>] clocks;
get_ports clk;
get_ports *clk*;
get_ports *;
get_ports * -filter "direction == in";
get_ports * -filter "direction == out";	
```

To query the clocks in dc shell (if is_generated is false this means the clock is a master clock), use the following commands:
	
```bash
get_clocks *;
get_clocks *clk*;
get_clocks * -filter "period > 10";
get_attribute [get_clocks my_clk] is_generated;	
report_clocks my_clk;
```
	
To query the physical and/or hierarchical cells (and check whether they are hierarchical or physical) in dc shell, use the following commands:
	
```bash
get_cells * -hier;
get_attribute [get_cells u_combo_logic] is_hierarchical; 	
get_attribute [get_cells u_combo_logic/U1] is_hierarchical;
```
	
To create a clock in dc (note: clocks must be created on the clock generators like PLL or oscillators or primary IO pins for external clocks. Clocks must not be created on hierarchical pins because they are not clock generators) (note2: creating a clock by default assumes a 50% duty cycle and starting phase is high, to change the phase/duty cycle use -wave {1st_rise_edge_time 2nd_rise_edge_time} with the first command), set the network latency and uncertainty constraints (remember to reduce the uncertatinty delay post CTS to reflect only jitter, and by default the comand below sets the setup uncertainty value), use the following commands:

```bash
create_clock -name <clock name> -per <period> [get_ports <clock definition point i.e. pin to define clock at>];
set_clock_latency <latency> [get_clocks <name of clock>];
set_clock_uncertainty <value of jitter and skew delay> [get_clocks <name of clock>];
```
	
To set the IO path constraints (the values are with respect to the clock edge, i.e. after it), use the following commands: 

```bash
set_input_delay -max <value> -clock [get_clocks <name clock>][get_ports <name of all input ports, use *>];
set_input_delay -min <value> -clock [get_clocks <name clock>][get_ports <name of all input ports, use *>];
set_input_transition -max <value> [get_ports <name of all input ports, use *>];
set_input_transition -min <value> [get_ports <name of all input ports, use *>];
set_output_delay -max <value> -clock [get_clocks <name clock>][get_ports <name of all output ports, use *>];
set_output_delay -min <value> -clock [get_clocks <name clock>][get_ports <name of all output ports, use *>];
set_output_load -max <value> [get_ports <name of all output ports, use *>];
set_output_load -min <value> [get_ports <name of all output ports, use *>];
```
	
</details>
	
<details>
 <summary> Inserting constraints: lab8_circuit.v </summary>	
	
To create a clock, use the following command:
	
```bash
create_clock -name <clock name: MYCLK> -per <period: 10> [get_ports <name: clk>];
```
	
The design of the circuit after creating the master clock (which will propagate to all clock pins because it is created at clk pin which is connected to all clock pins in the circuit) is shown below:
	
<img width="1159" alt="sta_design" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/06456eeb-8b39-4717-a084-5b550e8e7879">
	
To remove the already created clock then create another clock with a modified waveform, then view it, use the following command:
	
```bash
remove_clock <name: MYCLK>
create_clock -name <clock name: MYCLK> -per <period: 10> [get_ports <pin name: clk>] -wave {<1st rising edge:5> <second rising edge: 10>};
report_clocks *;
```
	
To add constraints to the clock created above (model source clock latency and clock network attributes) and print the timing report for setup and hold, use the following commands:
	
```bash
set_clock_latency -source <latency: 1> [get_clocks <name of clock: MYCLK>];
set_clock_latency <latency: 1> [get_clocks <name of clock: MYCLK>];
set_clock_uncertainty -setup <value of jitter and skew delay: 0.5> [get_clocks <name of clock: MYCLK>];
set_clock_uncertainty -hold <min value of jitter and skew delay: 0.1> [get_clocks <name of clock: MYCLK>];
report_timing -to <destination pin name: REGC_reg/D> -delay max;
report_timing -to <destination pin name: REGC_reg/D> -delay min;
```

The resulting timing reports are shown below. In first report, we can see that arrival time (Tcq+Tcomb) is less than or equal required time (Tclk-Tuncertainty-Tsetup), their subtracted value is the slack, which when met means we are good. In second report, we can also see that (Thold+Tuncertainty) is less than or equal (Tcq+Tcomb)min. The tool subtracts the uncertainty for setup purposes and adds the uncertainty for hod purposes:

<img width="529" alt="timing_report" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/034b4b58-a994-4db8-b64d-6a1994ea0ff2">
	
<img width="526" alt="timing_report_hold" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/41edf239-4ebb-43e9-88bd-2c6f3ee97115">
	
In order to report information about all ports (for now we will not see transition delays on input ports and no delays due to loads on output ports), use the command below:
	
```bash
report_port -verbose;
```

To add IO constraints (for external input delay, input transitions, external output delay, and output loads) and print the timing report, use the commands below:
	
```bash
set_input_delay -max <value: 5> -clock [get_clocks <name: MYCLK>] [get_ports <name: IN_A>];
set_input_delay -max <value: 5> -clock [get_clocks <name: MYCLK>] [get_ports <name: IN_B>];
set_input_delay -min <value: 1> -clock [get_clocks <name: MYCLK>] [get_ports <name: IN_A>];
set_input_delay -min <value: 1> -clock [get_clocks <name: MYCLK>] [get_ports <name: IN_B>];
set_input_transition -max <value: 0.3> [get_ports <name: IN_A>];
set_input_transition -max <value: 0.3> [get_ports <name: IN_B>];
set_input_transition -min <value: 0.1> [get_ports <name: IN_A>];
set_input_transition -min <value: 0.1> [get_ports <name: IN_B>];
report_timing -from <source pin name: IN_A> -trans -cap -nosplit > <name output file: a_trans>;
set_output_delay -max <value: 5> -clock [get_clocks <name: MYCLK>] [get_ports <name: OUT_Y>];
set_output_delay -min <value: 1> -clock [get_clocks <name: MYCLK>] [get_ports <name: OUT_Y>];
set_load -max <value: 0.4> [get_ports <name: OUT_Y>];
report_timing -to <destination pin name: OUT_Y> -trans -cap -nosplit > <name output file: out_load>;
report_port -verbose;
```
	
Below is the timing report reported from IN_A (slack is 4.08 now):
	
<img width="537" alt="timing_report_ina" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b8e67ecb-e2fa-45ad-a7db-66ef90caeae3">

Below is the timing report reported from OUT_Y (slack is 1.88 now):

<img width="538" alt="timing_report_out" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/70d7f19d-2ae8-4961-b240-09c4ce4862b4">
	
A generated clock is used to later on model the propagation delay (flight delay) of the clock seen at the output port. To create a generated clock and constraint the above design taking into consideration the generated clock (modeling the propagation delay), use the following commands:
	
```bash
create_generated_clock -name <name: MYGEN_CLK> -master [get_clocks <name master clock: MYCLK>] -div <division value usefor for clock division: 1> [get_ports OUT_CLK];
set_clock_latency -max <value: 1> [get_clocks MYGEN_CLK];
set_output_delay -max <value: 5> -clock [get_clocks <name: MYGEN_CLK>] [get_ports <name: OUT_Y>];
set_output_delay -min <value: 1> -clock [get_clocks <name: MYGEN_CLK>] [get_ports <name: OUT_Y>];
report_timing -to <destination pin name: OUT_Y>;
```
	
Below is a screenshot of the reported timing:
	
<img width="536" alt="timing_report_generated" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/905f5449-7f15-4268-8d4b-cff59c14def1">
	
The below screenshot summarizes important notes about input delay:
	
![input_delay_notes](https://github.com/mariamrakka/vsd-hdp/assets/49097440/c74f0f4d-5891-4583-8006-797a4094c910)

The below screenshot summarizes important notes about output delay:	
	
<img width="1341" alt="output_delay_notes" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/89814e5c-3345-43b6-9bd9-02a84cd0ac0c">

If we have two outputs, we can either use the commands in the below first screenshot or those in the below second screenshot to constraint the lower path:
	
<img width="1376" alt="io_constraingts_revisited" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4a362c0c-0886-4c1f-8a9f-9ee00e1d5f86">

<img width="1512" alt="io_constraints_revisited__part2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9c139bbc-83be-4245-b717-cbfb2fb39702">
	
Below are two interesting cases where we need to add constraints from blocks (with negative edge clock) outside our module, and the corresponding commands to add those constraints are shown:
	
<img width="1484" alt="io_constraints_part3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/cebc4257-c163-4574-8650-3f6943d9ff8a">

<img width="1401" alt="io_constraints_part4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e49de88f-3fd7-44f9-a07e-370567a80c99">

Below is a case where we need to use a set_driving_cell constraint, which is useful and accurate to model transition of pins between modules:
	
<img width="1503" alt="set_driving_cell" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/01430c96-44dd-4f27-af67-1bce7c4089d4">

	
</details>
	
<details>
 <summary> Inserting constraints: lab14_circuit.v </summary>
	
The design of this circuit is similar to that of lab18_circuit.v, but has additional inputs, gate and output in the module as shown below:
	
<img width="1221" alt="design_lab14" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0f016ae1-b3b1-45be-869a-e817045422eb">

	
We constraint the model above by using all constraints we discussed in lab8_circuit.v and in addition we add either the constraints in the first set of commands below then recompile to get an optimization as our constraint added will lead to a violation (because previous compilation did not take into account this newly added path) that will be fixed post compilation, or we add the constraints that follow in second set of commands which use a virtual clock (either ways work, but note that virtual clock does not need a source name and we need to be careful to have the latency in between equivalent to 0.1ns, and we have that as out of 10ns from virtual clock, 5ns is to input delay and 4.9ns is to output delay hence what is left is 0.1ns for the logic so this is correct):
	
```bash
set_max_latency <value:0.1> -from [all_inputs] -to [get_port OUT_Z];
compile_ultra;
report_timing -to <name: OUT_Z>;
```

```bash
create_clock -name MYVCLK -per <value: 10>;
set_input_delay -max <value: 5> [get_ports <name: IN_C>] -clock [get_clocks MYVCLK];
set_input_delay -max <value: 5> [get_ports <name: IN_D>] -clock [get_clocks MYVCLK];
set_output_delay -max <value: 4.9> [get_ports <name: OUT_Z>] -clock [get_clocks MYVCLK];
compile_ultra;
report_timing -to <name: OUT_Z>;
```
	
Below is the reported timing from the both approaches (one screenshot because both apply same constraints and optimizations and hence we get same timing report):
	
<img width="423" alt="constraints_lab14" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/a99c6fe5-900d-4a3b-baeb-ea07b68c3181">

	
</details>
	
## Day 9
	
<details>
 <summary> Summary </summary>
	
I added constraints to my design (the updown counter), and I used OpenSTA to perform analysis with constraints and produce the timing reports. I defined the constraints in "mariam_updown_counter.sdc" file and I defined the OpenSTA commands in "my_script.tcl" file.
	
</details>
	
<details>
 <summary> Adding constraits: mariam_updown_counter.sdc </summary>
	
I defined the consraints in the .sdc file as below:
	
```bash
create_clock -name MYCLK -per 10 [get_ports clk];
set_clock_latency -source 2 [get_clocks MYCLK];
set_clock_latency 1 [get_clocks MYCLK];
set_clock_uncertainty -setup 0.5 [get_clocks MYCLK];
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK];
set_input_delay -max 4 -clock [get_clocks MYCLK] [get_ports up_down];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports up_down];
set_input_transition -max 0.5 [get_ports up_down];
set_input_transition -min 0.1 [get_ports up_down];
set_load -max 0.13 [get_ports counter];
set_load -min 0.1 [get_ports counter];
```
	
</details>
	
<details>
 <summary> Using OpenSTA: my_script.tcl </summary>
	
The .tcl file is defined as below:
	
```bash
read_liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mariam_updown_counter_net.v
link_design mariam_updown_counter
read_sdc mariam_updown_counter.sdc
report_checks -fields {nets cap slew input_pins} -digits {4} > mariam_report.rpt
```
	
To run this script in OpenSTA, I used the following command:
	
```bash
sta my_script.tcl
```
	
Screenshots of the .rpt report can be found below, as we can see the tool optimized the logic and the slack is met (4.4234):

<img width="624" alt="Screen Shot 2023-05-20 at 9 45 42 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/44b4571b-c0e1-426a-bfa5-eed18e5ad4b4">
	
<img width="631" alt="Screen Shot 2023-05-20 at 9 46 37 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/647968f6-2821-4267-96fa-5b0167523d07">


</details>
	
## Day 10
	
<details>
 <summary> Summary </summary>
	
I learnt about circuit design and spice simulations. In circuit design we see how connecting transistors and other components in a certain way would result in a certain functionality. Spice simulations are used to verify that a circuit is functioning as expected, to generate delays of a cell (source of delay tables).
	
First, I learnt about the NMOS transistors and their characteristics. NMOS is an n-channel (on p-substrate), has 4 terminals, has 2 isolation regions, has 2 n+ diffusion regions, has a gate oxide, has a poly-Si (metal gate) which is placed on top of gate oxide, and has 4 terminals (bulk, source, drain, gate). PMOS is just an inverted NMOS (p+ on n-substrate) but all other characteristics are common. The threshold voltage accurate describes the transistor. For an NMOS, if Vgs=0, and we drain drain, source and bulk, we get 2 back to back p-n junction diodes. Now if we apply a potential Vgs, a negatively charged region (depletion region) forms between n+ regions. Now if we keep increasing Vgs until Vgs=threshold voltage=Vto (Vsb=0 here, and Vto is a function of process manufacturing), we get strong surface inversion. If we keep increasing Vgs now, a continuous channel is created between n+ (gate attracts negative n+ as no p+ are left to repel, they are all depleted) -> cutoff region. If Vsb is positive (with D grounded and Vgs small voltage to form depletion region), the depletion layer width increases near S), now as Vgs increases in this case, depletion layer width increases, but in this case (unlock above case where Vsb=0) the negative charges formed due to depletion are attracted towards the S terminal which is connected to positive node of voltage source, this needs additional potential to achieve strong surface inversion whereby it happens for Vgs=Vto+V1 (V1=lembda*sqrt(abs(-2Phi+Vsb))-sqrt(abs(-2Phi)) and lambda=sqrt(2*q*N*A*Epsilon_Si)/Cox).
	

If Vgs increased beyond strong inversion (beyond Vt) and apply drain voltage then the voltage across channel is not constant anymore, and V(x) is the voltage at point x along the channel, and Vgs-V(x) is the gate-to-channel voltage at that point. The charges induced in the channel is proportional to Vgs-V(x)-Vt, in particular, Q(x)= -Cox ((Vgs-V(x))-Vt) where Cox=Epsilon_ox/tox where tox is oxide thickness. From device point of view there are drift (due to potential difference) and diffusion currents (due to difference in carrier concentration). Here focus is on the drift current, Id, (velocity of charge) that is flowing over the channel width. Id= -Vn(x)*Q(x)*Width where velocity Vn(x)=mobility*electric=Mu_N*dV/dx, so sunstituting and integrating dx over channel length will give the V-I relationship of NMOS => Id= Mu_N*Cox *W/L *[(Vgs-Vt)*Vds-Vds^2/2], we call Mu_N*Cox=Kn' or process conductance and kn'*(W/L)=Kn is the gain factor. -> Linear region (for Vds <= Vgs - Vt), Id=Kn(Vgs-Vt)Vds.

If Vds = Vgs-Vt, pinch-off phenomena starts, and the channel begins to disappear (voltage across channel remains ~ constant at Vgs-Vt). When Vds>Vgs-Vt, the channel pinches off, and current saturates. -> Saturation region (for Vds > Vgs-vt), Id=kn/2(Vgs-vt)^2. The change in channel can be modeled accurately by including lambda (channel length modulation) in the equation: Id=kn/2(Vgs-vt)^2*(1+lambda*Vds). 
	
A correct spice setup includes the model files (technology model files representing the MOSFETs through parameters and equations) and spice netlist (describes the circuit we are trying to simulate in a specific syntax)
	
</details>
	
<details>

 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git	
	
</details>
	
<details>

 <summary> Important spice syntax </summary>
	
Before writing a netlist, we need to define names for the nodes in the circuit.
	
To include a technology file then define a resistor, transistor, voltage source, and a capacitor use the syntax below:
	
```bash
.LIB "<name: xxx>.mod" CMOS_MODELS
R<name> <1st node> <second node> <value>
M<name> <drain> <gate> <source> <bulk> <name in tech file> w=<value> L=<value>
V<name> <1st node> <second node> <value>
C<name> <1st node> <second node> <value>
```
	
Technology file (xxx.mod) of NMOS and PMOS should have the following syntax:
	
```bash
.lib cmos_models
.Model <name that should match in netlist> NMOS (TOX = .. VTH0 = .. U0 = .. GAMMA1 = ..)
.Model <name that should match in netlist> PMOS (TOX = .. VTH0 = .. U0 = .. GAMMA1 = ..)
.endl
```
	
To simulate a spice netlist with sweeping (left side will be sweeped for each value on the right side), use the following syntax in the netlist:
	
```bash
.<mode: dc> <voltage node to sweep: Vin> <start value: 0> <end value: 2.5> <steps: 0.1> <voltage node to sweep: Vdd> <start value: 0> <end value: 2.5> <steps: 2.5> 
```

To use ngspice for plotting, use the following commands:
	
```bash
ngspice <spice file name>
plot -<name node>
```
	
</details>

<details>

 <summary> Ngspice simulation: day1_nfet_idvds_L2_W5.spice  </summary>
	
To use ngspice for plotting, use the following commands:
	
```bash
ngspice <name: day1_nfet_idvds_L2_W5.spice>
plot -<name: vdd#branch>
```
	
Below is the screenshot of the obtained result of Id vs Vds for different Vgs. We can see that as Vds increases, Id goes from cutoff to linear region to saturation region:
	
<img width="562" alt="ngspice1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/1162c8b0-fda5-49ee-a3a0-84faa15adf74">

</details>

## Day 11
	
<details>

 <summary> Summary </summary>
	
I learned about velocity saturation and the basics of CMOS inverter Voltage Transfer Characteristics (VTC). If we inspect the I-V charachteristic of an NMOS, when Vgs>=Vt, then we see two regions, one with linear increase of current when Vds<=Vgs-vt and one with saturated current when Vds>Vgs-Vt. When W/L is constant but W and L (from long channel to short channel device) have decreased in value, we stop seeing quadratic dependance of Ids on Vgs after a certain Vgs value, and we see linear dependance, and also peak current decreases from long channel case due to velocity saturation effect. At higher electric fields, velocity becomes constant (after it was linear for lower fields) due to scattering effects. Velocity Vn(x)= Mu_n*epsilon/(1 + epsilon/epsilon_c) for epsilon <= epsilon_c and Vn(x)=Vsat for epsilon >= epsilon_c. We note that long channel (L>250nm) has 3 modes of operation: cutoff, resistive, and saturation, while short channel (L<250nm) has 4 modes of operation: cutoff, resistive, velocity saturation, and saturation. For short channel case: Id=0 for Vgs<Vt (cutoff) and otherwise, Id=Kn*[((Vgs-Vt)*Vmin)-Vmin^2/2]*[1+lambda*Vds] where Vmin=min(Vgs-Vt, Vds, Vdsat) according to region of operation (Vdsat is the voltage at which device velocity saturates and is independent of Vgs or Vds, and it is a technology operation). 
	
A CMOS acts like a switch, open when |Vgs|<|Vt| and closed (with finite ON resistance) when |Vgs|>|Vt|. When Vin=Vdd, the pmos is off, nmos is on, and Vout is 0 (open switch). When Vin is 0, PMOS is on and NMOS is off and Vout is Vdd (closed switch). In either case, there is a resistance with the switch which represents the equivalent resistance of the nmos (Rn) and pmos (Rp) respectively as shown in the picture below.
	
<img width="1427" alt="cmos" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e57ebfb0-3e6e-4f2a-82f3-56cdc993e8c9">
	
The VTC of a CMOS (Vout vs Vin) is derived by first converting IdN vs VdsN and IdP (IdP=-IdN) vs VdsP to IdN vs Vout for different Vin (load curve for PMOS) as shown in first picture, then getting similarly IdN vs Vout for different Vin (load curve for NMOS) as shown in second picture. Finally, for we superimpose load of NMOS on PMOS, and for intersection points between common Vin values gives us the common Vout value in the VTC. VTC has 5 regions: 1-) PMOS linear, NMOS off, 2-) PMOS linear, NMOS saturation, 3-) PMOS and NMOS in saturation, 4-) PMOS saturation, NMOS linear, and 5-) PMOS off, NMOS linear as shown in third picture (1, 3, and 5 regions are of importance).  	
	
<img width="1504" alt="vtc1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b6fa5dc3-a564-45b5-a559-d37411dcfdb9">
	
<img width="1015" alt="VTC_2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/a7fd3a23-3a8c-4171-b9a4-c550958a3cf1">
	
<img width="504" alt="VTC_3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/1210d506-816c-4726-83dd-e331c3b02ded">

	
</details>
	
<details>	
	
 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git	
	
</details>

<details>

 <summary> Ngspice simulation: day2_nfet_idvds_L015_W039.spice  </summary>
	
To use ngspice for plotting, use the following commands:
	
```bash
ngspice <name: day2_nfet_idvds_L015_W039.spice>
plot -<name: vdd#branch>
```
	
Below is the screenshot of the obtained result of Id vs Vds for different Vgs. We can see that for low value of Vgs, Id shows quadratic behavior and for high Vgs, Id shows linear behavior due to velocity saturation effect (we have short channel here):
	
<img width="496" alt="ngspice_2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/55fb03a7-fe27-4074-8898-f3af01e94f27">


</details>
	
<details>

 <summary> Ngspice simulation: day2_nfet_idvgs_L015_W039.spice  </summary>
	
To use ngspice for plotting, use the following commands:
	
```bash
ngspice <name: day2_nfet_idvgs_L015_W039.spice>
plot -<name: vdd#branch>
```
	
Below is the screenshot of the obtained result of Id vs Vgs for constant Vds. We can see that for low value of Vgs, Id shows quadratic behavior and for high Vgs, Id shows linear behavior due to velocity saturation effect (we have short channel here):
	
<img width="468" alt="Screen Shot 2023-05-23 at 5 44 41 PM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/1ccf77e7-7902-4cc0-910b-48929344d446">
	
To calculate the thrshold voltage in ngspice, use the plot above and extend a line tangent to the linear line (the slope), until it meets the x-axis and that would be the value of the threshold voltage. 

</details>
	
## Day 12
	
<details>

 <summary> Summary </summary>
	
I learned how to simulate a CMOS circuit using spice in order to obtain the VTC and evaluate the static behavior. Spice deck needed to write a netlist: component connectivity, component values, identify nodes and name them. The switching voltage Vm is that where Vin=Vout (nmos and pmos in saturation), and it defines the robustness of the CMOS. It is derived by setting IdsP=-IdsN to get Vm=R*Vdd/(1+R) where R=(Kp*VdsatP)/(Kn*VdsatN) and where Kp=Wp/Lp*Kp' and Kn=Wn/Ln*Kn'. Given target Vm, we can derive from the previous equation the needed W/L ratios. 
	
</details>
	
<details>	
	
 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
	
</details>

<details>

 <summary> Important spice syntax </summary>
	
To define a pulse, use the syntax as defined in the picture below:
	
<img width="1175" alt="pulse" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2afa04c5-e02b-47e9-8480-56855e688f6a">

	
</details>	
	
<details>

 <summary> Ngspice simulation: day3_inv_vtc_Wp084_Wn036.spice  </summary>
	
To use ngspice for plotting, use the following commands:

```bash
ngspice <name: day3_inv_vtc_Wp084_Wn036.spice>
plot <name: out> vs <name: in>
```
	
Below is the screenshot of the obtained result of the VTC, where switching threshold is around 0.876v:
	
<img width="515" alt="ngspice4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/bd6f663d-7f0c-4618-aa55-801e621761d7">

	
</details>
	
	
## Day 13
	
<details>

 <summary> Summary </summary>
	
I learned the effect of increasing the pmos width. When the pmos width is wider than that of nmos, the switching voltage of the VTC shifts to the right slightly (advantage). As width of pmos increases as an integer multiple of that of nmos (for same L), the rise delay and fall delay decreases rapidly (time to charge decreases as width is wider) and increases  respectively. For one some sizing (factor of 2), we observe an equal rise and fall times (symmetric property which is a typical characteristic of a clock inverter/buffer where resistance of pmos is approximately equal to resistance of nmos in that case due to the W/L ratios). Other sizing for inverters is used to get regular inverter/buffer that would be preferred in the data path. 
	
</details>
	
<details>
	
 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
	
</details>
	
<details>
	
<summary> Ngspice simulation: day3_inv_tran_Wp084_Wn036.spice  </summary>
	
To use ngspice for plotting, use the following commands:

```bash
ngspice <name: day3_inv_tran_Wp084_Wn036.spice>
plot <name: out> vs <name: time> <name: in>
```
	
Below is the screenshot of the obtained result of the transient analysis, where rise delay and fall delay are around 0.322ns and 0.285ns at 0.9v (50%) respectively:
	
<img width="516" alt="spice5" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b2b477df-8cf9-4428-8c6f-929a6459aba9">


</details>
	
## Day 14
	
<details>

 <summary> Summary </summary>
	
I learned about noise margin, which is another characteristic that defines static behavior of the inverter (robustness). When Vin<=VIL (logic 0), Vout is expected to ber VOH, and when Vin>=VIH (logic 1), vout is expected to be VOL (note that the slope at VIL and VIH is -1). The noise margin is defined as VIH-VIL (undefined region: voltage ranges at which the logic does not differentiate between 0 and 1). Noise margin high (interpereted as logic 1) = VOH-VIH and noise margin low (interpreted as logic 0) = VIL-VOL. Ideally, we want a CMOS inverter to have a noise margin of 0. When the width of the pmos increases with respect to nmos width, noise margin high increases while noise margin low stays the same then drops as the pmos is responsible for the high value output. Digital design relies on the areas of noise margin high and noise margin low. 
	
</details>
	
<details>
	
 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
	
</details>
	
<details>
	
<summary> Ngspice simulation: day4_inv_noisemargin_wp1_wn036.spice  </summary>
	
To use ngspice for plotting, use the following commands:

```bash
ngspice <name: day4_inv_noisemargin_wp1_wn036.spice>
plot <name: out> vs <name: in>
```
	
Below is the screenshot of the obtained result of the VTC, and VIL is around 0.7v and VOH is around 1.7v. VOL is around 0.08v and VIH is around 1v (noise margin low is around 0.62v and noise margin high=0.7):

<img width="636" alt="ngspice6" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/8a7f3f5e-10cf-49b9-a558-ac912c6f6d1c">

</details>


## Day 15
	
<details>

 <summary> Summary </summary>
	
I learned about power supply scaling and device variation, where the effect of those on the CMOS is another characteristic that defines static behavior of the inverter (robustness). 
	
CMOS inverter can operate at supply voltage of even 0.5v and advantages are: at 0.5v, the gain (rate of change of output as input changes, change in output voltage dibided by change in input voltage at slopes of -1) is huge (close to 50% compared to 2.5v) and energy consumed is 1/2*CV^2 so less energy is consumed (close to 90% improvement compared to 2.5v). Disadvantage of using 0.5 power supply: very slow operation as fall time and rise time are huge -> huge impact on performance. 
	
Etching is the process of creating patterns on substrates, in which materials will be removed selectively from a thin film on a substrate. Variation in L and W takes place because of non-ideal mask, which in turn impacts the drain current. Variation in oxide thickness is due to non-idealities in the fabriaction process that leads to non-ideal oxidation process, which in process affacts the drain current. In a chain of inverters, sources of variation affect the inverters on sides more severely. To mimic device variations, Wn and Wp were varied from a strong pmos-weak nmos to a weak pmos-strong nmos, and from the VTCs we could see that there is a small shift in Vm, the switching voltgae, and small variations in the noise margins (high and low) -> the CMOS inverter is highly robust to device variation. 
	
</details>
	
<details>
	
 <summary> Codes </summary>
	
The used models of MOSFEts and netlists for simualtions are taken from https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
	
</details>
	
<details>
	
<summary> Important spice syntax </summary>
	
To define a loop in order to scale the power supply, use the syntax as defined in the picture below:
	

<img width="766" alt="loop" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2b0bc598-e128-41f4-a0af-89c6637f65bd">

	
</details>	
	
<details>
	
<summary> Ngspice simulation: day5_inv_supplyvariation_Wp1_Wn036.spice  </summary>
	
To use ngspice for plotting, use the following commands:

```bash
ngspice <name: day5_inv_supplyvariation_Wp1_Wn036.spice>
```
	
Below is the screenshot of the obtained result of the VTC curves for different supply voltages, gain in curve corresponding to 1.8v is (1.706-0.076)/(1.008-0.772)=6.907. Gain in curve corresponding to 0.8v is (0.770-0.021)/(0.511-0.428)=9.024 (increases as supply voltage decreases, but then decreases again because supply would not be enough for the device to operate):

<img width="689" alt="voltagesupply1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/655d6e68-1198-4522-9aff-506ffa0f155f">

<img width="448" alt="gains" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2a57ef4a-6d37-4857-8ae7-3eee708d785a">

</details>
	
<details>
	
<summary> Ngspice simulation: day5_inv_devicevariation_wp7_wn042.spice  </summary>
	
To use ngspice for plotting, use the following commands:

```bash
ngspice <name: day5_inv_devicevariation_wp7_wn042.spice>
plot <name: out> vs <name: in>
```
	
Below is the screenshot of the obtained result of the VTC curve, and since Wp is larger than Wn we can see that the output logic 1 is held for longer than output logic 0 (because of strong pfet and weak nfet), and subsequently the switching voltage shifts to the right (compared to Vdd/2, in an ideal CMOS) to a value of 0.987v which is very close to Vdd/2=0.9, so even with huge device variation, the CMOS device is pretty robust:

<img width="645" alt="devicevariation" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/dcca50be-9b5d-4cba-8bdd-3c10428eb7b4">


</details>
	
## Day 16 
	
<details>
	
<summary> Summary </summary>
	
I performed post-synthesys STA on my design using different ss (slow slow),ff (fast fast),tt (typical typical) PVT corners, then I reported the WNS (Worst Negative Slack), TNS (Total Negative Slack = sum of the negative slack paths), and WHS (Worst Hold Slack) values. Note that the skywater tt, ss and ff corners are found in https://github.com/Geetima2021/vsdpcvrd.git
	
I used the previously defined constraints in "mariam_updown_counter.sdc" file and I defined the OpenSTA commands for different corners (tt, ff, ss) in "my_script_tt.tcl", "my_script_ff.tcl", "my_script_ss.tcl" file. As there is one tt corner, 5 ff corners, and 7 ss corners, I would only change the name of corresponding .lib file in the three main scripts
	
</details>
	
<details>
 <summary> Adding constraits: mariam_updown_counter.sdc </summary>
	
Recall that I already defined the consraints in the .sdc file as below:
	
```bash
create_clock -name MYCLK -per 10 [get_ports clk];
set_clock_latency -source 2 [get_clocks MYCLK];
set_clock_latency 1 [get_clocks MYCLK];
set_clock_uncertainty -setup 0.5 [get_clocks MYCLK];
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK];
set_input_delay -max 4 -clock [get_clocks MYCLK] [get_ports up_down];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports up_down];
set_input_transition -max 0.5 [get_ports up_down];
set_input_transition -min 0.1 [get_ports up_down];
set_load -max 0.13 [get_ports counter];
set_load -min 0.1 [get_ports counter];
```
	
</details>
	
<details>
 <summary> Using OpenSTA: my_script_*.tcl </summary>
	
The my_script_tt.tcl for tt corner is defined as below (note that -delay_path min_max produces the wht and wst respectively):
	
```bash
read_liberty ../../vsdpcvrd/resources/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mariam_updown_counter_net.v
link_design mariam_updown_counter
read_sdc mariam_updown_counter.sdc
report_checks -fields {nets cap slew input_pins} -digits {4} -path_delay min_max > mariam_report_tt_025C_1v80.rpt
report_tns >> mariam_report_tt_025C_1v80.rpt
```
	
The my_script_ff.tcl for ff corner is defined as below (note that -delay_path min_max produces the wht and wst respectively):
	
```bash
read_liberty ../../vsdpcvrd/resources/timing_libs/sky130_fd_sc_hd__ff_*
read_verilog mariam_updown_counter_net.v
link_design mariam_updown_counter
read_sdc mariam_updown_counter.sdc
report_checks -fields {nets cap slew input_pins} -digits {4} -path_delay min_max > mariam_report_ff_*.rpt
report_tns >> mariam_report_ff_*.rpt
```
	
The my_script_ss.tcl for ss corner is defined as below (note that -delay_path min_max produces the wht and wst respectively):
	
```bash
read_liberty ../../vsdpcvrd/resources/timing_libs/sky130_fd_sc_hd__ss_*
read_verilog mariam_updown_counter_net.v
link_design mariam_updown_counter
read_sdc mariam_updown_counter.sdc
report_checks -fields {nets cap slew input_pins} -digits {4} -path_delay min_max > mariam_report_ss_*.rpt
report_tns >> mariam_report_ss_*.rpt
```
	
To run this script in OpenSTA, I used the following command as much as needed (i.e. once for tt, 5 times for ff, and 7 times for ss):
	
```bash
sta my_script_tt.tcl
sta my_script_ff.tcl
sta my_script_ss.tcl
```

Note that all reports generated for pvt corners are included in this repository under the directory sta_out_corners.
	
Below you can find the values obtained in the report and a corresponding plot:
	
	
<img width="494" alt="mypvt0" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/7981c89a-5e51-45d2-bb52-e0c24f9335ad">
	
![mypvt](https://github.com/mariamrakka/vsd-hdp/assets/49097440/6736e86e-8ba0-4e57-9940-b84d27d875b6)

</details>
	
## Day 17

<details>
 <summary> Summary </summary>
	
I learnt about RISC-V ISA, physical implementation, and SoC design using OpenLane. Chip is at the center of a package, and a chip has PADs which allow signals to pass in and out of the chip (from core where the digital logic sits to outside or vice versa). Note that the die defines the size of the chip. A typical core consists of a CPU SoC, ADCs/DACs, SPI, PLL, and SRAM. PLL, SRAM, and DAC/ADC are called as foundary IPs. Foundary is a big factory that has machines where chips get manufactured. IP is intellectual property (needs intelligence to be built). SPI and CPU SoC are macros. Macros are pure digital logic. We need an interface (some files) to communicate with the foundary. 
	
The application software or apps are handled by the system software (OS, compiler, assembler) in order to run on the hardware. The OS handles IO operations, allocates memory, and handles low level system functions. The compiler transforms the high level language into low level instructions according to the unerlying hardware. The assembler then converts the instructions (abstract ISA, or 'architecture' of computer) to respective binary that is eventually fed to the hardware. The RTL implements the instructions (the ISA), then RTL is synthesized into netlist which is physically implemented in hardware. 
	
Digital ASIC design requires RTL of the IPs, EDA tools, and PDKs. Open source deigital ASIC design is facilitated by open-source RTL designs (in github for example), open-source EDA tools (OpenRoad, OpenLane, Qflow), and open-source PDKs. A PDK=Process Design Kit is the iterface between the fabrication and design (which were separated in the past). PDK includes device models, design rules, standard cell libraries, I/O libraries, etc.. Regular PDKs are distributed under NDAs, but open PDKs (130nm, released by Google) do not require NDAs. ASIC design Flow: Synthesis (takes RTL as input, output is gate-level netlist. Standard cells have regular layouts), FP+PP (floor planning. Planning chip and macro. Includes power planning), Place (placing cells on the floor plan. Global and detailed placement), CTS (creating clock distribution network to route the clock), Route (implementing the interconnect using metal layers. Global and detailed routing takes place in divide and conquer approach), Sign off (output is GDSII. Physical verifications (DRC, LVS), and timing verifications (STA)). The PDK is used in all these steps. Developing an open ASIC design flow is tough as there are worries in tool qualification, tool calibration, and missing tools. 
	
OpenLane is an open ASIC design flow (relies on multiple open-source tools). The main goal is produce a clean GDSII (no LVS, DRC, STA violations) without human intervention. OpenLane is tuned for skywater 130 open PDK. OpenLane can be used to produce GDSII for either macros or chips. It has two modes: autonomous (one click of button) or manual (step by step). It provides a mean to sweep configurations allowing design space exploration, and has a large number of design examples available publicly. Below is the detailed ASIC design flow in OpenLane. 

<img width="945" alt="openlane2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c6dbf878-b529-48b0-861c-5149db478804">
	
Note that DFT (design for testing) step is optional and facilitated by Fault tool. Note that we need to deal with antenna rules violations: when a metal wire segment is fabricated, it can act as an antenna which leads to damage some transistor gates during fabrication => two solutions: bridging and inserting antenna diodes. The two solutions are shown side-to-side below: 
	
<img width="893" alt="openlane3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/81caa1b3-c418-4d2b-bf11-d87213313435">

OpenLane deals with those antenna violations and gives the user option to user either OpenLane or OpenRoad solution. The pdk directory inside the OpenLane directory has skywater-pdk which contains PDK files provided by foundry, open_pdks that contains scripts to setup pdks for opensource tools, and sky130A which contains sky130 PDK files.

</details>
	
<details>
	
<summary> Codes </summary>
	
The used designs are taken from https://github.com/The-OpenROAD-Project/OpenLane
	
</details>
	
<details>
	
<summary> OpenLane, PDKs, and tools: Installation </summary>

To install OpenLane tools, I have used the following commands:

```bash	
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 
```

After reboot, I used this command: 

```bash
docker run hello-world
```	

To check dependencies, use the following commands:	
	
```bash
git --version
docker --version
python3 --version
python3 -m pip --version
make --version
python3 -m venv -h
```
	
I have used the below commands to install PDKs and tools:
	
```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```
	
As all the above steps were successful, I got the following terminal result:
	
<img width="653" alt="openlane1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/d92d7e22-8a80-44c0-b06b-088bb16c3ed1">
	
</details>
	
<details>
	
<summary> OpenLane: picorv32a  </summary>
	
To invoke OpenLane, I used the commands below in the OpenLane directory (note that without interactive switch, OpenLane will run in automatic mode):
	
```bash
make mount
./flow.tcl -interactive
package require openlane 0.9
```
	
To prepare the design, I used the following command (designs/picorv32a contains the verilog file, .sdc file, needed PDK, and config.json that has configurations for the design that will overwrite the default OpenLane settings. When the design is prepared, the LEF files are merged, and a "runs" directory is created inside the picorv32a directory, and inside it a directory with the current date is created. Inside that directory, all folder structures required by OpenLanes are present empty, except for temp folder. temp folder has the merged LEF files. Note that when synthesis is performed for example a file will be created inside the results/synthesis directory. Inside the runs/<RUN_today_date> directory there is a config.tcl file which contains the default OpenLane configuration settings, and it is important to check whether our modifications are reflected in it): 
	
```bash
prep -design picorv32a
```
	
To run the synthesis of the picorv32a design, I used the following command (During this step yosys and ABC tools are utilized to convert RTL design to the gate level netlist, which will be found in the folder runs/<RUN_today_date>/results/synthesis): 
	
```bash
run_synthesis
```
	
The obtained logs and reports are found in runs/<RUN_today_date>/logs/synthesis and runs/<RUN_today_date>/reports/synthesis respectively. Below are screenshots of the logs I obtained for STA results:
	
<img width="721" alt="stareport1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f6a68649-1104-4efd-a9aa-88e0d741794f">

<img width="723" alt="stareport2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2dcab5ea-0f64-416c-b951-18e647c60513">

<img width="513" alt="stareport3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5618e334-0611-4bbb-a6ea-94aa1586db60">

	
To calculate the flop ratio, I used the following formula, and the numbers are extracted from the report whose screenshot is included below:
	
```bash	
Flop ratio = # of D Flipflops / Total # of cells
dfxtp_2 = 1596,
Number of cells = 9541,
Flop ratio = 1596/9541 = 0.1673 = 16.73%	
```
	
<img width="510" alt="dff_formula1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/009c27f1-e108-4cb9-9c13-5bb436af71de">

<img width="513" alt="dff_formula2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/352f62ad-086d-472c-aa0f-216f301bb78f">

</details>
	
	
## Day 18

<details>
 <summary> Summary </summary>
	
I learned about chip floor planning. First step of floor planning is defining height and width of the core. Recall that logic cells are placed inside the core. Utilization factor of the core = Area (occupied by netlist)/Total area of the core. Ideally a 50-60% utilization (of cells only usually) is good. Aspect ratio = Height of core /width of core. The second step of floor planning is defining the locations of preplaced cells. We cut big logic cells into different blocks, we extended IO pins, block box the blocks, and then separate the black boxes as two different IPs or modules. IPs are implemented once and can be instantiated multiple times, and IPs are preplaced cells as their arrangement is done by user-defined locations and placed on the chip before automated placement-and-routing. The automatic placement-and-routing will place the remainingh logical cells on the chips. It is important to place the preplaced cells in locations that are relevant to the design as this lcoation won't change. Third step in floop planning is to define the decoupling capacitances around the preplaced cells. Decoupling capacitances are used to decouple circuits from the main supply, and they are placed closer to the cell. The decoupling capacitances are important during the switching activity as it makes sure signal is delivered with attentuation that lies in the noise margin regions (as opposed to huge attentuation that can take place because the main supply is physically far away from the cells. The decoupling capacitances replenish their own charge when there is no switching activity. The forth step is power planning. This is used for global communication between the different macros as the receiving macro (load) should receive the same signal sent from the sending macro (driver). Using one power supply to feen in the signal can cause problems in ground bounce or supply droop if multiple decoupling transistors try to charge or discharge at the same time. The solution to this problem is to ue multiple sources for the power supply, where each cell will take its power from the nearest supply. The problem of placing those multiple power supplies is called power planning. The fifth step in floor planning is pin placement. The connectivity between the cells is defined in the netlist, and pin placement is the problem of placing those pins on the chip's die. Note that clock pins are bigger than other pins as this pin drives more cells. The sixth step is logical cell placement blockage where a blockage is placed in die area outside core to present tools from placing cells in that area.

</details>
	
<details>
	
<summary> OpenLane: picorv32a  </summary>

To run the floorplanning after synthesis of the picorv32a design, I used the following command (During this, the 6 steps mentioned in summary are done, and a .def is created in the results/floorplan directory inside the chosen design directory. The results can be found in OpenLane/designs/<design name: picorv32a>/RUN_*/runs): 
	
```bash
run_floorplan
```
	
Note that some of the floorplan switches (can be included with the command above) are FP_CORE_UTIL (floorplan core utilization), FP_ASPECT_RATIO (floorplan aspect ratio), FP_CORE_MARGIN (Core to die margin area), FP_IO_MODE (defines pin configurations: 1 = equidistant and 0 = not equidistant), FP_CORE_VMETAL (vertical metal layer), and FP_CORE_HMETAL (horizontal metal layer). The default values of these are defined in OpenLane/configuration/floorplan.tcl. In order to overwite these, we can define those switches in OpenLane/designs/<design name: picorv32a>/config.json. Note that in OpenLane, horizontal and vertical metal are one value added to the value we specify.
	
To view the layout the floorplan in magic, I used the command below in the results/floorplan directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.min.lef def read picorv32a.def &
```
	
A screenshot of the obtained layout is below:
	
<img width="590" alt="floorplanlayout" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e8fdf4a3-d814-47a0-8716-74b53962bcb3">


After zooming in (left click, right click, z), below is the obtained screenshots (note that when we highlight (s after positioning the cursor), we can type "what" in the tkcon window and it will provide the layer of the highlighted object. The standard cells can be found on left bottom corner of the layout, as floorplan does not place those):
	
<img width="647" alt="highlight" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9997d9e1-4526-4642-806f-eb14c5dd6c36">
	

<img width="614" alt="standardcell_layout" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/713c5a4a-96fa-4133-9a55-c16a84dab523">

	
</details>
