
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)

[Day 6: My Design Part 1](#day-6)

[Day 7](#day-7)

[Day 8](#day-8)

[Day 9: My Design Part 2](#day-9)

[Day 10](#day-10)

[Day 11](#day-11)

[Day 12](#day-12)

[Day 13](#day-13)

[Day 14](#day-14)

[Day 15](#day-15)

[Day 16: My Design Part 3](#day-16)

[Day 17](#day-17)

[Day 18](#day-18)

[Day 19](#day-19)

[Day 20](#day-20)

[Day 21](#day-21)

[Day 22: My Design Part 4](#day-22)

[Day 23: My Design Part 5](#day-23)

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
	
<summary> OpenLane (synthesis): picorv32a  </summary>
	
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
	
I learned about chip floor planning and placement and routing. First step of floor planning is defining height and width of the core. Recall that logic cells are placed inside the core. Utilization factor of the core = Area (occupied by netlist)/Total area of the core. Ideally a 50-60% utilization (of cells only usually) is good. Aspect ratio = Height of core /width of core. The second step of floor planning is defining the locations of preplaced cells. We cut big logic cells into different blocks, we extended IO pins, block box the blocks, and then separate the black boxes as two different IPs or modules. IPs are implemented once and can be instantiated multiple times, and IPs are preplaced cells as their arrangement is done by user-defined locations and placed on the chip before automated placement-and-routing. The automatic placement-and-routing will place the remainingh logical cells on the chips. It is important to place the preplaced cells in locations that are relevant to the design as this lcoation won't change. Third step in floop planning is to define the decoupling capacitances around the preplaced cells. Decoupling capacitances are used to decouple circuits from the main supply, and they are placed closer to the cell. The decoupling capacitances are important during the switching activity as it makes sure signal is delivered with attentuation that lies in the noise margin regions (as opposed to huge attentuation that can take place because the main supply is physically far away from the cells. The decoupling capacitances replenish their own charge when there is no switching activity. The forth step is power planning. This is used for global communication between the different macros as the receiving macro (load) should receive the same signal sent from the sending macro (driver). Using one power supply to feen in the signal can cause problems in ground bounce or supply droop if multiple decoupling transistors try to charge or discharge at the same time. The solution to this problem is to ue multiple sources for the power supply, where each cell will take its power from the nearest supply. The problem of placing those multiple power supplies is called power planning (in OpenLane, this is done post placement). The fifth step in floor planning is pin placement. The connectivity between the cells is defined in the netlist, and pin placement is the problem of placing those pins on the chip's die. Note that clock pins are bigger than other pins as this pin drives more cells. The sixth step is logical cell placement blockage where a blockage is placed in die area outside core to present tools from placing cells in that area.
	
Placement is perfomed in two stages: global amd detailed. In global placement, tool finds optimal position for all cells which may not be legal and cells may overlap. Optimization is done through reduction of half parameter wire length. In detailed placement, the tool changes the position of cells post global placement so as to legalise them. The first step in placement and routing is binding the netlist with physical cells. This means taking every component in the netlist and giving them a proper width and height. These widths and heights are taken from the library. The library has various options of widths and heights for the same cell (bigger is faster). The second step in placement and routing is placement. In this step, the netlist is placed on the floor plan (which already has the preplaced cells by now). The placement is important as it affects the delays. The third step is optimized placement, where the wire capacitances are estimated and the placement is optimized by adding buffers (repeaters that replicate the original signal) where needed to maintain the integrity of the signal. The distances for signals are calculated according to slew values and transition delay. Criss cross can occur when placing, and should be avoided. 
	
All stages of floorplanning and place and route need library characterization. Standard cells are placed inside libraries, which defines their functionalities and their different versions: different sizes and threshold voltages. For one standard cell, the cell design flow defined in the library consists of:
	
1-) inputs: pdks from foundary: DRC and LVS rules, SPICE models, library and user-defined specs 
	
2-) design steps: circuit design where sizing takes place, layout design (where the function is implemented via pmos and nmos connections, then the pmos and nmos network graphs are derived, then the Euler's path is determined, then a stick diagram is drawn, then stick diagram is converted to layout by sticking to the DRC rules defined by the foundary), and characterization
	
3-) Outputs: circuit description language, GDSII, LEF, extracted spice netlist (.cir) which includes the parasitics, timing, noise, power .libs, function

	
Characterization flow (part of 2-) above): firdst step is to read the models, second step is to read the extracted spice netlist, third step is to define the behaviour of the circuit, the fourth step is to read the subcircuits, fifth step is to attach the necessary power sources, sixth step is to apply the stimulus, seventh step is to provided needed capacitances for output, and finally eighth step is to provide the necessary simulation command. These 8 steps are fed via a configuration file to the characterization software called "GUNA". And the software will generate timing, noise, power .libs, function (part of 3-) above). There are hence three characterization types: timing characterization, power characterization, and noise characterization.
	
Timing characterization: timing threshold definitions are points whose definitions help us calculate slew from the waveforms (definitions are for slew_low_rise_thr, slew_high_rise_thr, slew_low_fall_thr, and slew_high_fall_thr), and the delay of the cell between input and output plots (definitions are for in_rise_thr, in_fall_thr, out_rise_thr, and out_fall_thr). The choice of the threshold definitions is important to get correct propagation delay and transition time. Propagation delay = time(out_*_thr) - time(in_*_thr). Fall/Rise Transition time = time(slew_high_*_thr) - time(slew_low_*_thr). Typical values: slew_low_rise_thr=20%, slew_high_rise_thr=80%, slew_low_fall_thr=20%, slew_high_fall_thr=80%, in_rise_thr=50%, in_fall_thr=50%, out_rise_thr=50%, and out_fall_thr=50%. 
	
	
</details>
	
<details>
	
<summary> Codes </summary>
	
The used designs are taken from https://github.com/The-OpenROAD-Project/OpenLane
	
</details>
	
<details>
	
<summary> OpenLane (floorplan, placement): picorv32a  </summary>

To run the floorplanning after synthesis of the picorv32a design, I used the following command (During this, the 6 steps mentioned in summary are done, and a .def is created in the results/floorplan directory inside the chosen design directory. The results can be found in OpenLane/designs/<design name: picorv32a>/RUN_*/runs): 
	
```bash
run_floorplan
```
	
Note that some of the floorplan switches (can be included with the command above) are FP_CORE_UTIL (floorplan core utilization), FP_ASPECT_RATIO (floorplan aspect ratio), FP_CORE_MARGIN (Core to die margin area), FP_IO_MODE (defines pin configurations: 1 = equidistant and 0 = not equidistant), FP_CORE_VMETAL (vertical metal layer), and FP_CORE_HMETAL (horizontal metal layer). The default values of these are defined in OpenLane/configuration/floorplan.tcl. In order to overwite these, we can define those switches in OpenLane/designs/<design name: picorv32a>/config.json. Note that in OpenLane, horizontal and vertical metal are one value added to the value we specify.
	
To view the layout of the floorplan in magic, I used the command below in the results/floorplan directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.min.lef def read picorv32.def &
```
	
A screenshot of the obtained layout is below:
	
<img width="590" alt="floorplanlayout" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e8fdf4a3-d814-47a0-8716-74b53962bcb3">


After zooming in (left click, right click, z), below is the obtained screenshots (note that when we highlight (s after positioning the cursor), we can type "what" in the tkcon window and it will provide the layer of the highlighted object. The standard cells can be found on left bottom corner of the layout, as floorplan does not place those):
	
<img width="647" alt="highlight" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9997d9e1-4526-4642-806f-eb14c5dd6c36">
	

<img width="614" alt="standardcell_layout" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/713c5a4a-96fa-4133-9a55-c16a84dab523">

To run the placement after floorplanning of the picorv32a design, I used the following command (If overflow value progressively reduces during the placement run, this means the design will converge and placement will be successful): 
	
```bash
run_placement
```

To view the layout after placement in magic, I used the command below in the results/placement directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.max.lef def read picorv32.def &
```
	
A screenshot of the obtained layout is below:	
	
<img width="447" alt="placement1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9bba4567-34b2-4fe0-aa18-1ba30d1bd388">


After zooming in, this is the obtained placement: 
	
<img width="441" alt="placement2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/26a3b489-ec94-49df-b69a-205d3579a740">

	
</details>
	
## Day 19

<details>
<summary> Summary </summary>
	
I have learned about CMOS inverter ngspice simulations, the CMOS fabrication process (and how layout helps with it), and the sky130 technology file. OpenLane allows users to make changes on the fly, using the following command before rerunning the design step (for example floorplanning):

```bash
set ::env(<name of variable that can be extracted from OpenLane/configurations/<design step: floorplan>.tcl: FP_IO_MODE>) <value: 2>
```

To simulate the inverter, first its spice needs to be created. Recall that a spice deck includes component connectivity, component values, nodes. The netlist to simulate includes model description, netlist description, simulation type and parameters, and needed libraries. Recall that the switching threshold (Vm, used to evaluate static behavior) of a CMOS inverter is the point on the voltage transfer characteristic curve where input voltage equals output voltage: at which both PMOS and NMOS are in saturation region which gives rise to a leakage current. 
	
16-mask CMOS process steps:
	
1-) Selecting a substrate: selecting body/substrate material (P-substrate)

2-) Creating active region for transistors: first create isolation between active region pockets by SiO2, then perform Si3N4 deposition, then photoresist deposition, and then apply photolithography (part of photoresist is covered by mask to protect it against UV light). Areas that are not protected against UV light are then washed out using developing solution and etching is done, then photoresist is chemically removed. Then we place CMOS in oxidation furnace,and field oxide is grown (process is called LOCOS or Local Oxidation of Silicon). After that, Si3N4 is stripped using hot phospheric acid. 
	
3-) N-well and P-well formation: Photoresist is deposited and mask is used to define the protected area. UV light reacts with exposed area, and then we wash the area which is unprotected. After that, the mask is removed (this is lithography). Ion implemention by Boron for P-well is then done, followed by ion implementation of Phosphorous for N-well formation (after photoresist, mask application, and wash out). Then the CMOS is put in a high temperature furnace for a high temperature for a long time, which will diffuse the N-well and P-well (the pockets). In N-well the pmos will be created and in P-well the nmos will be created.

4-) Formation of gate terminal: the nmos and pmos gates are formed by depositing photoresist, using mask, exposing UV, applying wash out, removing the mask, doping with Boron to modify the doping concentration in the P-well. Similar steps are repeated for P-well to control the threshold voltage or doping concentration in the N-well. Extra oxide is diluted then re-grown again to give high quality oxide. A polisilicon layer is then deposited to form the gate, then N-type material is doped on the gate to make it low resistance. Then photoresist is dumped, mask is used, unprotected material is washed out, mask is removed, and the remaining areas of polisilicon are etched away.  

5-) Lightly Doped Drain (LDD) formation: LDD is formed to prevent hot electron effect and short channel effect: P+, P-, P doping profile is needed for pmos and N+, N-, N profile is needed for nmos. Photolithography is applied, Phosphorous is doped to create N- implants on P-well side. The lithography is repeated for N-well side and we get P- implant after doping Boron. A thick Si3N4 or SiO2 is deposited on whole material and plasma anisotropic etching takes place  to create the side-wall spacers where source and drain will be later affected in next step.

6-) Source and drain formation: think layer of screen oxide is added to avoid channelling during implantation. Then after photolithography, Aresenic implantation/doping takes place above P-well (below side-wall spacers). Then after photolithography, Boron implantation/doping takes place above N-well (below side-wall spacers). The material is put in high temperature furnace (called high temperature annealing).

7-) Contacts and local interconnect formation: Etching/removal of screen oxide by HF solution. Then Ti is deposited on material for low resistant contacts using sputtering (hitting Ti by Ar+ and the then Ti will be deposited on the substrate with heating). Then lithograpphy is used, and RCA cleaning is used to etch TiN. Result = TiN used only for local communication. 

8-) Higher level metal formation: A thick layer of SiO2 doped with phosphorous or boron is deposited on the material. CMP is used for planarizing the wafer (polishing it), then photolithograpphy is used in areas where we want the metal to be formed, then TiN is deposited. Tungsten is then deposited, followed by CMP again. Al is then deposited on the material, and photolithography is used. Result is we get the first layer of metal. To get higher layers, SiO2 is deposited again, CMP is used, lithography is used, TiN is deposited, Tungsten is deposited, followed by CMP again. Al is then deposited on the material, and photolithography is used. The result is a metal layer which is higher and thicker (thicker Al). Si3N4 is deposited on top to protect the whole chip. Finally, mask16 is used to open contact holes on this top layer and connect the highest metal layer to the top. 
	
Below is the obtained CMOS after finishing the fabrication process explained above:
	
<img width="1003" alt="fabrication" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/50be3978-5069-416f-ad7b-2145f26da6d6">

In CMOS magic layout the first layer is called the local interconnect layer or Locali. The P diffusion and N diffusion regions with Polysilicon verify that this is the layout of a CMOS inverter. Also, drain and source connections are another sanity cehck: drains of both pmos and nmos are connected to output port (Y) and the sources of nmos/pmos are connected to  GND/VDD respectively (moving cursor and clicking S twice helps us identify the connections in magic).

Library Exchange Format (LEF): A format that tells us about cell pins and boundaries, VDD and GND lines. It contains no information about the logic of circuit and is also used to protect the IP.
	
The technology file is a one setup file that tells magic everything it needs to know about a project (all layer types, patters, connectvitity, DRC rules, GDS generation rules, rules to read LEF and Def files, rules for interactive wiring, etc...). There are two sections: CIF and GDS styles. CIF is human readable. 
	
</details>

<details>
	
<summary> Codes </summary>
	
The used designs are taken from https://github.com/The-OpenROAD-Project/OpenLane, https://github.com/nickson-jose/vsdstdcelldesign.git, and http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
	
</details>
	
<details>
	
<summary> OpenLane: sky130_inv.mag, sky130_inv.spice </summary>
	
To get the technology file inside the cloned github, I used the following commands (inside OpenLane directory):	
	
```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
cp /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech ./vsdstdcelldesign 
```

To view the layout of the CMOS inverter, I used the following command (inside vsdstdcelldesign directory):
	
```bash
magic -T sky130A.tech sky130_inv.mag &	
```
	
The obtained layout design can be found below (this layout will be used to intergate the inverter with the picorv32a design): 
	
<img width="392" alt="cmoslayout" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/d84d23e2-2f45-43fd-9cb8-ed9c4f8e0cca">

Using the magic environment, I used the following commands in tkcon to extract .spice from .mag (this generates the sky130_inv.spice file in the same directory. This SPICE deck is edited to include pshort.lib and nshort.lib which are the pmos and nmos libraries respectively. The minimum grid size of inverter is measured from the magic layout and incorporated into the deck as: .option scale=10m. The model names in the MOSFET definitions are changed to pshort.model.0 and nshort.model.0 for pmos and nmos respectively):

```bash
extract all
ext2spice cthresh 0 rethresh 0
ext2spice
```

I modified the extracted netlist to include the library files and define the power supply, ground and input pulses, and specify the type of analysis. The lines I added are found below (note that I commented .subckt and .ends, and I changed names of pmos and nmos to pshort_model.0 and nshort_model.0 respectively, and I changed x0 and x1 to M1000 and M1001):
	
```bash
.include ./libs/pshort.lib
.include ./libs/nshort.lib
VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)
.tran 1n 20n
.control 
run
.endc
.end
```
	
The final netlist looks like this:
	
<img width="452" alt="netlist_new_cmos" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/795fb39f-a0dc-4b2d-b2bb-9e05fb7cda53">


In the same directory of the netlist (sky130_inv.spice), I used the following commands to run the simulation:
	
```bash
ngspice sky130_inv.spice
plot <output: y> vs time <input: a>
```

The obtained simulation is shown below:
	
<img width="336" alt="netlist_sim_cmos" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/fb326174-f01f-4cca-a659-c4b850567a28">


The cell chacarterization is done via the waveforms obtained from spice simualtion, and the results are noted below:
	
The above timing parameters can be computed by noting down various values from the ngspice waveform (recall that Rise transition: Time taken for the output to rise from 20% of max value to 80% of max value, Fall transition: Time taken for the output to fall from 80% of max value to 20% of max value, Cell rise delay: time(50% output rise) - time(50% input fall), Cell fall delay: time(50% output fall) - time(50% input rise)):

```bash
Rise transition = (2.1957e-9 - 2.15099e-9) = 44.71 ps
Fall transition = (4.06461e-9 - 4.03953e-9) = 25.08 ps
Cell rise delay = (2.17613e-9 - 2.15e-9) = 26.13 ps
Cell fall delay = (4.05241e-9 - 4.04991e-9) = 25.00 ps
```
	
</details>
	
<details>
	
<summary> OpenLane: drc_tests </summary>
	
To download the needed files, I used the following commands:

```bash
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
```
	
To invoke magic, I used the following commands in the /drc_tests directory:
	
```bash
magic -d XR
```

To load the sky130 tech-rules, I clicked on (in the magic wizard) file, open, and I selected "met3.mag" which has the rules for layer3. Below is a screenshot of the layout I obtained (there are layout geometries with DRC errors, and each component of layout is named after a DRC rule number in the google documentation. Selecting the component and writing "drc why" in the tkcon shows the rules that has been violated):
	
<img width="363" alt="drc1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b1e9d6d4-cd84-429a-83b2-27aa9abfbe79">

To fix poly.9 error in magic's layout, first I loaded the file using magic's tkcon as follows:
	
```bash
load poly.mag
```
	
I then edited the sky130A.tech file to add the following two highlighted commands:
	
<img width="462" alt="tech1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c2e442a2-a6bc-4f84-874f-5219cde8fa40">
	
<img width="454" alt="tech2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/34b859d0-1a0b-447a-8eca-3c679684c15a">
	
I then used the following commands in the tkcon window to load the updated sky130A.tech file (this will lead to the correct implementation of the drc rule and an error being flagged in magic):
	
```bash
tech load sky130A.tech
drc check
```
	
The resulting layout with the flagged violation is shown below:

<img width="407" alt="drc2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/bf55097f-252f-47bf-8e26-c3b6585cb4fc">
	
To implement poly resistor spacing to diff and tap, I modified a rule in the sky130A.tech file, as highlighted below:	

<img width="451" alt="tech3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c662e26a-67c4-4259-8859-a2989ced2c2c">
	
I then used the following commands in the tkcon window to load the updated sky130A.tech file:

```bash
tech load sky130A.tech
drc check
```
	
The resulting layout with the flagged violation is shown below:

<img width="517" alt="drc3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ba80a8a8-7089-4575-b763-54918204aa9e">	
	
Note that challenging DRC rules are described as geometric constructs (rather than in simple commands as shown above). Templayers can be used as building bloks for other layers (but are not present in output of GDS file). There are two modes defined in the tech file for drc rules, fast and full. Fast is used when the user does not require magic to look below the metal layer for drc checking (as that would slow the iteractive wizard), and full makes magic look at all the layers and check them.
	
To add the challenging drc rule in the tech file (only checked in full variant style so it does not create a burden), I first loaded the file in magic's tkcon as follows:
	
```bash
load nwell.mag
```
	
I then added the following highlighted commands to the sky130A.tech file:
	
<img width="452" alt="tech4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ca7690af-9b97-4491-92f4-5afd92db8779">
	
<img width="451" alt="tech5" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/d47a980f-8dc0-4a55-9239-c2547f7d4f53">

I then used the following commands in the tkcon window to load the updated sky130A.tech file:

```bash
tech load sky130A.tech
drc check
drc style drc(full)
drc check
```
	
We can then see the error in magic as shown below:
	
<img width="396" alt="drc4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e4190164-bc7b-4d64-a295-270350d99726">
	
The problem goes away when nsubstrate constact is added in the nwell as shown below:
	
<img width="215" alt="drc5" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ce78a294-1afc-45d4-a498-d6ecbc9a63fa">

</details>
	
## Day 20

<details>
<summary> Summary </summary>
	
I first leaned how to extarct a LEF file (defining a port and their purpose) (the LEF file is used in picorv32a design), then I learned about pre-layout timing analysis, CTS, and post-CTS timing analysis. Recall that in delay tables, there are delay values for varying input transition and output load. For CTS: Delay tables for all buffers with their different sizes compose the timing models. To find a delay of a certain path, the delay tables of buffers on that path are used to find individual delays then those delays are added up. If two paths have the same buffer as load in turn driving the same load, then the signal comming out of those two buffers will have a skew of 0 (ensuring this will not lead to problems). For power-aware CTS, one of paths would be activated at a time. 
	
Setup timing analysis (single clock, ideal scenario where clk is not built yet): the internal delay (finite time) in the capture flop which has to be subtracted from period, and the variation of time that a clock edge can can undergo when it arrives to the launch flop and capture clock (called uncertainty) which has to be also subtracted from period, so D (combinational delay)< T (period) - SUT (setup) - U (uncertainty). Using this analysis, the combinational delay should be considered when placing the cells. 

Clock Tree Synthesis (CTS): goal is to make the clock reach all flipflops with minimum skew. H-tree calculates the path from all flops and connects the clock to the midpoint of the flops. Buffers (with equal rise and fall time) are added on the H-tree path. The CTS run adds clock buffers, so buffer delays are taken into consideration, and the analysis now deals with real clocks. Setup and hold time slacks can be then analyzed in the post-CTS STA analysis using OpenROAD. All critical (as shielding all is sometimes not possible) clock nets are shielded to prevent coupling with other components, and hence reducing potential of a glitch. A glitch is a serious problem as it can reset memory system and can lead to incorrect functionality in the whole system activity. Crosstalk leads to exponential delta skew, and this is another reason shielding nets is important.    

Setup timing analysis (single clock, real clock scenario): nw clk goes through real wires and buffers, which cause delays. D (combinational delay)+ del1 (time for clk to reach launch flop) < T (period) + del2 (time for clk to reach capture flop) - SUT (setup: D to clk delay in capture flop) - U (uncertainty). del1-del2 is known as skew (difference in time the clk reaches the two flops). D+del1=data required time, T+del2-SUT-U is data arrival time, and slack= data required time - data arrival time => slack should be +ve. 

Hold timing analysis (single clock, ideal scenario): D > H (hold time: clk to Q in capture flop) + HU (hold uncertainty). 
	
Hold timing analysis (single clock, real clock scenario): D + del1 > H (hold time: clk to Q in capture flop) + del2. The keft hand side is called data arrival time while right hand side is called data required time. In this case, slack = data arrival time - data required time, and slack here should be +ve too. 
	
Del 1nad del2 need to be identified for both setup and hold time analysis. Del1/del2 = sum of RC wire delays on path + sum of buffer delays on the path. The difference is that del1 goes to launch flop, while del2 goes to capture flop (see picture below to understand the difference).

<img width="684" alt="realclock" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/34a1ad05-87b9-40c2-ae36-9058aba5dd79">
	

</details>

<details>
	
<summary> Codes </summary>
	
The used designs are taken from https://github.com/The-OpenROAD-Project/OpenLane and https://github.com/nickson-jose/vsdstdcelldesign.git
</details>
	
<details>
	
<summary> OpenLane (synthesis, floorplan, placement): picorv32a with sky130_vsdinv </summary>
	
Ports should be at intersection of horizontal and vertical tracks. The CMOS ports A and Y are on li1 layer. A and Y must be on the intersection of horizontal and vertical tracks. I accessed the tracks.info file for the pitch and direction information by using the commands below:

```bash
vi /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/openlane/sky130_fd_sc_hd/tracks.info
```	
	
Below is a screenshot of the obtained file:
	
<img width="352" alt="tracksfile" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/625f35d0-0902-4d9c-8eb0-23ddbd35fee0">

To force ports to lie on the intersection point, I used the following commmands in tkcon:

```bash
grid 0.46um 0.34um 0.23um 0.17um
save sky130_vsdinv.mag
```	

The resulting layout is shown in the screenshot below (grids will be used for routing):
	
<img width="363" alt="grid" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4a160df0-6f17-480a-bd25-ef28ed4188bc">
	

To extract LEF (In a LEF file, a cell that contains ports is written as a macro, and the ports are declared pins of the macro) from a given layout in standard format, one must first define ports. To define a port through magic's wizard first source the .mag file for the design, then click "Edit, Text" which opens up a dialogue box. Use the box to input a label name along with a sticky label of the layer name with which the port needs to be associated. Note that I have not done this step for the CMOS because it is already done for us.
	
The next step in extracting LEF is defining the purpose of ports. For example to define that of A, use the following commands in tkcon: 1-) port class input
2-) port use signal. To define that of  VGND, use the following commands in tkcon: 1-) port class inout 2-) port use ground. Note that I have not done this step for the CMOS because it is already done for us.
	
To write the LEF file, I first invoked magic using the below command:
	
```bash
magic -T sky130A.tech sky130_vsdinv.mag &	
```
	
Then, I used the following command in the tckon window:
	
```bash
lef write	
```
	
A screenshot of the obtained LEF is shown below:
	
<img width="447" alt="lef" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2e299eae-b576-4c2a-a528-54660c30680b">

	
To include the generated LEF with the picorv32a design, I used the following commands in the OpenLane/designs/picorv32a/src (I also copied sky130_fd_sc_hd__*.lib file from vsdstdcelldesign/libs directory since abc maps the standard cell to a library):
	
```bash
cp /home/mariam/OpenLane/vsdstdcelldesign/sky130_vsdinv.lef . 
cp /home/mariam/OpenLane/vsdstdcelldesign/libs/sky130_fd_sc_hd__typical.lib .
cp /home/mariam/OpenLane/vsdstdcelldesign/libs/sky130_fd_sc_hd__fast.lib .
cp /home/mariam/OpenLane/vsdstdcelldesign/libs/sky130_fd_sc_hd__slow.lib .
```	

I then modified OpenLane/designs/picorv32a/runs/ as follows: 
	
```bash
"LIB_SYNTH": "/home/mariam/OpenLane/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib",
    "LIB_SLOWEST": "/home/mariam/OpenLane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib",
    "LIB_FASTEST": "/home/mariam/OpenLane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib",
    "LIB_TYPICAL": "/home/mariam/OpenLane/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib",
    "EXTRA_LEFS": "/home/mariam/OpenLane/designs/picorv32a/src/sky130_vsdinv.lef",	
```

The modified config.jason file is below:
	
<img width="491" alt="jasonfile" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4147ca05-0b7f-4374-a697-ef44321d70cf">

I then invoked OpenLane from the already used OpenLane Container then ran synthesis (note that in my case no slack violations were reported after synthesis), floorplan, and placement as follows:

```bash
exit
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
run_floorplan
run_placement
```
	
To view the layout after placement in magic, I used the command below in the results/placement directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.max.lef def read picorv32.def &
```
	
A screenshot of the obtained layout is below, zoomed in to see one of the custom CMOS added (custom CMOS is selected in screenshot):	
	
<img width="397" alt="vsdinvplacement" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9c2875bf-378d-4ae1-bf76-78c5dbb60e72">
	

</details>
	
<details>
	
<summary> OpenLane, OpenSTA: picorv32a with sky130_vsdinv </summary>
	
Again, in my case no negative slack was reported post synthesis. The slack value is the difference between data required time and data arrival time. The worst slack value must be greater than or equal to zero. If a negative slack is obtained, one can do the following steps: change synthesis strategy, enable buffering (in OpenLane) and upsizing buffers: review maximum fanout of cells replacing those with high fanout (in OpenSTA). When edits are done in OpenLane, the synthesis should be rerun.
To apply these, OpenSTA will be used iteratively (it displaying the changes, and OpenLane applying some changes), and one starts by writing a configuration file (that sets the units, reads liberty for bpth fast and slow sky130 technologies, reads the verilog for the synthesized picorv32a found in results/synthesis, links the design, reads the sdc file that specifies the constraints based on base.sdc in /scripts (i.e. to produce same slack initially seen in OpenLane inside the OpenSTA) and has some environemnt definitions brought from OpenLane and library files, and reports the delays). OpenSTA can then be invoked as follows (recall that CTS is not done yet, so this is done for ideal clock assumed, and only setup analysis is included):
 
```bash
sta pre_sta.conf
```
	
Note that each time a change is done in OpenLane, the netlist (.v) with same name gets updated, and hence OpenSTA must be invoked again to reflect the salck of the applied changes (that is why it is an iterative approach). Now if changes for timing where done within OpenSTA (like upsizing buffers), we need to reflect those to the OpenLane tool and the way we do this is via an echo the new timing: use "write_verilog" command in OpenSTA dumping file in the results/synthesis directory. Then rerun the synthesis, floorplan and placement again.
	
</details>
	
</details>
	
<details>
	
<summary> OpenLane, OpenROAD (CTS): picorv32a with sky130_vsdinv </summary>
	
Having reran synthesis, floorplan, and placement if needed to rerun (due to timing fixes, but I did not need that), I used the following command to carry out CTS analysis:
	
```bash
run_cts
```
	
Note that even though CTS was successful, this did not generate a .v file in the result/synthesis directory or anywhere else (even time stamp on the .v file in synthesis directory was not updated meaning cts did not overwrite that file). When I looked at OpenLane/scripts/openroad it had a cts.tcl file that did not use write_verilog!. Also, no reports where generated for cts inside reports/cts, but there were logs generated in logs/cts, and these showed no errors or warnings. The results/cts directory contained .odb, .def, and .sdc files.

Note that I did not need to invoke OpenROAD for post-CTS STA, I found the reports already in the reports/cts directory. 
	
Below are the hold and setup STA analysis results respectively (both slacks are met):
	
<img width="490" alt="cststa1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/a13d9431-e81b-40c0-bf55-8a7df3729e2a">

<img width="452" alt="cststa2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/63aa417d-193e-40f0-ac7d-9958b1050d7c">
	
<img width="493" alt="cststa3" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/f7113b99-5fd5-439a-945e-b71ee7182c8c">

<img width="491" alt="cststa4" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/c24d3c4d-2549-4336-a2cd-70af82d982f5">

</details>
	
## Day 21
	
<details>
<summary> Summary </summary>
	
I learned about creating Power Distribution Network (PDN) in OpenLane, routing, design rule check (drc), and PNR interactive flow. In an ASIC flow, PDN generation is part of floorplan. In OpenLane, however, this is not the case and PDN must be generated after CTS and post-CTS STA analysis. 
	
During routing, algorithm tries to find the best possible connection between points. One such algorithm is maze routing also known as Lee's algorithm. This algorithm, find the minimum distance between points by 1-) creating a routing grid, 2-) labels source and target points, 3-) labels edge grids of source point as 1 (horizontal and vertical), then labels unlabeled edge grids of those grids as 2 and so on and so forth until we hit the target grid, 3-) Now all enumarated pathes in order that take from source to target grid are identified as options, 4-) L shaped routes (if found) would be chosen, otherwise any other identified option is chosen (the lower the number of pins found the better). Lee's algorithm is shown below. 
	
<img width="848" alt="mazeroute" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/879d8b61-fa68-4bca-985c-2c31520021ac">
	
There are 2 stages of routing: global (routing region is divided into rectangle grids which are represented as course 3D routes via FastRoute tool) and detailed (finer grids and routing guides are used to implement physical wiring via TritonRoute tool). OpenLane uses the TritonRoute tool (an inter-layer sequential, intra-layer parallel routing framework that honours pre-processed route guides, assumes that each net satisfies inter-guide connectivity, and uses MILP based panel routing scheme) for detailed routing. The preprocessed route guides and inter-guide connectivity are found below.
	
<img width="465" alt="preprocessedrouteguides" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/949c70c5-9c7c-469f-b1e3-6ba621fbdf71">
	
<img width="419" alt="interguideconnectivity" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9948f8dc-66d8-4721-9cfb-0f8045fbb4ec">

Design rule check (drc) are rules that need to be followed when routing. Some rules define: minimum wire width, minimum wire pitch (distance between two wires from midpoints), and minimum wire spacing (distance between two wires from inner points). One violation is signal short when two wires meet: to solve it, one wire is put on another metal layer, but in this case two new rules are created and need to be checked: 1-) via width (inner square width) and 2-) via spacing (from inner close sides). 
	
</details>

<details>
	
<summary> Codes </summary>
	
The used designs are taken from https://github.com/The-OpenROAD-Project/OpenLane and https://github.com/nickson-jose/vsdstdcelldesign.git

</details>
	
<details>
	
<summary> OpenLane (power distribution network): picorv32a with sky130_vsdinv </summary>
	
To generate PDN in OpenLane then verify its success, I used the commands below (PDN takes <name of design>_cts.def as input def file. During this step, the grid is created grid along with straps for the power supply and ground. These are then placed around the standard cells. A standard cell is designed such that the height is a multiple of the space between the power supply and ground rails (pitch is 2.72 here). Standard cells are powered only if the above conditions are satisfied. Power reaches the chip through the power pads, then the rings (through the via). The power supply and ground straps are connected to the power supply and ground rings, so power is then supplied to standard cells through the straps. If there are macros, then the straps attach to the rings of the macros via the macro pads and the pdn for the macro is pre-done. In this design straps are at metal layer 4 and 5 and the standard cell rails are at metal layer 1):
	
```bash
gen_pdn
echo $::env(CURRENT_DEF)
```

The generated logs and results are found in logs/floorplan and results/floorplan respectively. Hence, the "echo $::env(CURRENT_DEF)" post PDN must point to the def file in the results/floorplan directory. 
	
</details>

<details>
	
<summary> OpenLane (routing, GDSII): picorv32a with sky130_vsdinv </summary>
	
To run routing in OpenLane (via TritonRoute), I used the command below (options for routing can be specified in config.jason file, and there is a trade-off between the optimized route and the runtime according to routing strategy):
	
```bash
run_routing
```
	
Below is the screenshot of the global routing log (found in logs/routing):
	
<img width="651" alt="globalpicorv32a" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/82ba2e0d-ddc6-4f6f-98c8-d0059b19cac0">


Below is the screenshot of the detailed routing log (found in logs/routing):	

<img width="722" alt="detailedpicorv32a" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/91525c12-53cf-497b-ab5e-9e2dfbd35caa">

	
To generate the GDSII file, I used the following commands (SPEF extraction, IR drop analysis, streaming out GDSII and generating LEF with magic, lvs, drc, antenna check, erc):

```bash	
run_parasitics_sta
run_irdrop_report
run_magic
run_magic_spice_export
run_lvs
run_magic_drc
run_antenna_check
run_erc
```
	
To view the GDSII file in magic, in OpenLane I used the command:
	
```bash	
magic
```

The GDSII file is generated in the results/signoff/magic directory, so I selected it from there in the wizard.

The layout screenshots are shown below:
	
<img width="334" alt="picorv32routing" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6b243cc8-b43c-418b-b9c6-f10f0fa28f88">

After zooming in:

<img width="526" alt="picorv32routing2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0470770e-a790-4443-acc5-009142d79544">

	
</details>
	

	
## Day 22
	
<details>
 <summary> Summary </summary>
	
I performed all the ASIC Design Flow steps on my design (the updown counter) using OpenLane, OpenSTA, and OpenRoad.
	
</details>
	
<details>
 <summary> Synthesis: mariam_updown_counter </summary>
	
After multiple trials of running the ASIC design flow on my designs, I kept encountering an error with pitch value during floorplan step, and I had to fix the jason.config file of my design to include the following command:
	
```bash
"FP_PDN_AUTO_ADJUST": 0
```

The above command allowed me to carry out the whole design flow successfully starting from synthesis and ending at routing.
	
To run synthesis (after I invoked OpenLane as usual), I used the command:
	
```bash
run_synthesis
```	

The obtained STA report is below (hold (met slack), setup (met slack), and power): 
	
<img width="485" alt="mydesign_slackmin_synth" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/a74016a9-078e-4cde-97d6-ca7fd2fa63ab">
	
<img width="490" alt="mydesign_slackmax_synth1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/af42e5b7-3a5b-4373-9d8d-ad18731083f3">
	
<img width="492" alt="mydesign_slackmax_synth2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/13d0c6c2-93e3-4593-b699-da87dc51ba8e">
	
<img width="489" alt="mydesign_power" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9d43c82c-c906-44a7-bbe5-ce548a5dd2fb">
	

To calculate the flop ratio, I used the following formula, and the numbers are extracted from the report whose screenshot is included below:
	
```bash	
Flop ratio = # of D Flipflops / Total # of cells
Flop ratio = 4/21 = 0.1904 = 19.04%
```
	
<img width="491" alt="mydesign_flopratio" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e395168d-3212-4506-952c-2980f7da8973">
	
</details>
	
<details>
	
<summary> Floorplan: mariam_updown_counter </summary>
	
To run the floorplanning after synthesis, I used the following command: 
	
```bash
run_floorplan
```
	
To view the layout of the floorplan in magic, I used the command below in the results/floorplan directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.min.lef def read mariam_updown_counter.def &
```
	
A screenshot of the obtained layout is below:	
	
<img width="785" alt="mydesign_floorplan" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ac220133-5a0f-4ef9-9318-b5611dd18dce">
	
After zooming in:
	
<img width="950" alt="mydesign_floorplan2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/66f88730-524e-4fe7-81ba-2d28f0e350b5">


	
</details>
	
<details> 
	
<summary> Placement: mariam_updown_counter </summary>
	
To run the placement after floorplanning, I used the following command: 
	
```bash
run_placement
```

To view the layout after placement in magic, I used the command below in the results/placement directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):
	
```bash
magic read -T /home/mariam/Desktop/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.max.lef def read mariam_updown_counter.def &
```
	
A screenshot of the obtained layout is below:	
	
<img width="757" alt="mydesign_placement" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/55cb4983-d007-4c4b-bb0f-8117c1712c88">

After zooming in:
	
<img width="747" alt="mydesign_placement2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b08281be-100e-41fb-bdd1-2ac8699374fa">
	
</details>
	
<details>
	
<summary> CTS: mariam_updown_counter </summary>	
	
After synthesis, floorplan, and placement, I used the following command to carry out CTS analysis:
	
```bash
run_cts
```
	
Note that even though CTS was successful, this did not generate a .v file in the result/synthesis directory or anywhere else (even time stamp on the .v file in synthesis directory was not updated meaning cts did not overwrite that file). When I looked at OpenLane/scripts/openroad it had a cts.tcl file that did not use write_verilog!. Also, no reports where generated for cts inside reports/cts, but there were logs generated in logs/cts, and these showed no errors or warnings. The results/cts directory contained .odb, .def, and .sdc files.

Note that I did not need to invoke OpenROAD for post-CTS STA, I found the reports already in the reports/cts directory. 
	
Below are the hold and setup STA analysis results respectively (both slacks are met):

<img width="949" alt="mydesign_cts_hold1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/fe71d61e-ba99-4485-8a90-e94554dbd815">

<img width="953" alt="mydesign_cts_hold2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6dfa62cc-d626-4aa4-af03-50ce3b9f721c">

<img width="954" alt="mydesign_cts_setup1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/eeead678-2715-40d2-99cf-fbdf4ba14155">

<img width="953" alt="mydesign_cts_setup2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/26e6eb14-f2ca-4873-91ce-f79c8f2d8ea2">

	
</details>
	
<details>
	
<summary> PDN and Routing: mariam_updown_counter </summary>
	
After CTS, I ran PDN and routing using the following commands:
	
```bash
gen_pdn
run_routing
```

Below is the screenshot of the global routing log (found in logs/routing):
	
<img width="950" alt="my_design_global" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/4b2f45fa-87a7-4f69-80be-f19f2b782c8e">

Below is the screenshot of the detailed routing log (found in logs/routing):	

<img width="950" alt="mydesign_detailed" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0014843d-979e-4343-8138-d98c61d64ab2">
	

</details>	
	
<details>
	
<summary> GDSII: mariam_updown_counter </summary>
	
To generate the GDSII file, I used the following commands (SPEF extraction, IR drop analysis, streaming out GDSII and generating LEF with magic, lvs, drc, antenna check, erc):

```bash	
run_parasitics_sta
run_irdrop_report
run_magic
run_magic_spice_export
run_lvs
run_magic_drc
run_antenna_check
run_erc
```
	
To view the GDSII file in magic, in OpenLane I used the command:
	
```bash	
magic
```

The GDSII file is generated in the results/signoff/magic directory, so I selected it from there in the wizard.

The layout screenshots are shown below (No DRC errors are found, mariam_updown_counter.magic.gds):
	
<img width="708" alt="gds1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2e3c55aa-46a7-4671-a4f3-844570cee236">

After zooming in:
	
<img width="758" alt="gds2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/3fb5ff34-a569-4104-9ae3-5d8855cbc031">

The LEF file shows as below in magic (mariam_updown_counter.lef.mag):
	
<img width="742" alt="leffile_mydesign" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/bb79ce33-8fce-4e16-b5a4-4a3c2aee7a31">

	
</details>

<details>
	
<summary> Noninteractive mode: mariam_updown_counter </summary>
	
To also ran the flow for my design in noninteractive mode. Below is the copied history of my terminal showing sucessful execution of all the ASIC Design Flow steps:

```bash		
OpenLane Container (e910d11):/openlane$ ./flow.tcl -design mariam_updown_counter
OpenLane e910d115dc75c51407f652330bce8ed997c45946
All rights reserved. (c) 2020-2022 Efabless Corporation and contributors.
Available under the Apache License, version 2.0. See the LICENSE file for more details.

[INFO]: Using configuration in 'designs/mariam_updown_counter/config.json'...
[INFO]: PDK Root: /home/mariam/.volare
[INFO]: Process Design Kit: sky130A
[INFO]: Standard Cell Library: sky130_fd_sc_hd
[INFO]: Optimization Standard Cell Library: sky130_fd_sc_hd
[INFO]: Run Directory: /openlane/designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30
[INFO]: Saving runtime environment...
[INFO]: Preparing LEF files for the nom corner...
[INFO]: Preparing LEF files for the min corner...
[INFO]: Preparing LEF files for the max corner...
[INFO]: Running Verilator (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/synthesis/verilator.log)...
[INFO]: 0 errors found by Verilator
[INFO]: 0 warnings found by Verilator
[STEP 1]
[INFO]: Running Synthesis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/synthesis/1-synthesis.log)...
[STEP 2]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/synthesis/2-sta.log)...
[STEP 3]
[INFO]: Running Initial Floorplanning (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/floorplan/3-initial_fp.log)...
[INFO]: Floorplanned with width 26.22 and height 24.48.
[STEP 4]
[INFO]: Running IO Placement...
[STEP 5]
[INFO]: Running Tap/Decap Insertion (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/floorplan/5-tap.log)...
[INFO]: Power planning with power {VPWR} and ground {VGND}...
[STEP 6]
[INFO]: Generating PDN (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/floorplan/6-pdn.log)...
[STEP 7]
[INFO]: Running Global Placement (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/placement/7-global.log)...
[STEP 8]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/placement/8-gpl_sta.log)...
[STEP 9]
[INFO]: Running Placement Resizer Design Optimizations (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/placement/9-resizer.log)...
[STEP 10]
[INFO]: Running Detailed Placement (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/placement/10-detailed.log)...
[STEP 11]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/placement/11-dpl_sta.log)...
[STEP 12]
[INFO]: Running Clock Tree Synthesis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/cts/12-cts.log)...
[STEP 13]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/cts/13-cts_sta.log)...
[STEP 14]
[INFO]: Running Placement Resizer Timing Optimizations (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/cts/14-resizer.log)...
[STEP 15]
[INFO]: Running Global Routing Resizer Design Optimizations (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/15-resizer_design.log)...
[STEP 16]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/16-rsz_design_sta.log)...
[STEP 17]
[INFO]: Running Global Routing Resizer Timing Optimizations (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/17-resizer_timing.log)...
[STEP 18]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/18-rsz_timing_sta.log)...
[STEP 19]
[INFO]: Running Global Routing (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/19-global.log)...
[INFO]: Starting OpenROAD Antenna Repair Iterations...
[STEP 20]
[INFO]: Writing Verilog (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/19-global_write_netlist.log)...
[STEP 21]
[INFO]: Running Single-Corner Static Timing Analysis (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/21-grt_sta.log)...
[STEP 22]
[INFO]: Running Fill Insertion (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/22-fill.log)...
[STEP 23]
[INFO]: Running Detailed Routing (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/23-detailed.log)...
[INFO]: No DRC violations after detailed routing.
[STEP 24]
[INFO]: Checking Wire Lengths (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/routing/24-wire_lengths.log)...
[STEP 25]
[INFO]: Running SPEF Extraction at the min process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/25-parasitics_extraction.min.log)...
[STEP 26]
[INFO]: Running Multi-Corner Static Timing Analysis at the min process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/26-rcx_mcsta.min.log)...
[STEP 27]
[INFO]: Running SPEF Extraction at the max process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/27-parasitics_extraction.max.log)...
[STEP 28]
[INFO]: Running Multi-Corner Static Timing Analysis at the max process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/28-rcx_mcsta.max.log)...
[STEP 29]
[INFO]: Running SPEF Extraction at the nom process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/29-parasitics_extraction.nom.log)...
[STEP 30]
[INFO]: Running Multi-Corner Static Timing Analysis at the nom process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/30-rcx_mcsta.nom.log)...
[STEP 31]
[INFO]: Running Single-Corner Static Timing Analysis at the nom process corner (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/31-rcx_sta.log)...
[WARNING]: Module sky130_fd_sc_hd__tapvpwrvgnd_1 blackboxed during sta
[WARNING]: Module sky130_fd_sc_hd__fill_1 blackboxed during sta
[WARNING]: Module sky130_ef_sc_hd__decap_12 blackboxed during sta
[WARNING]: Module sky130_fd_sc_hd__fill_2 blackboxed during sta
[STEP 32]
[INFO]: Creating IR Drop Report (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/32-irdrop.log)...
[STEP 33]
[INFO]: Running Magic to generate various views...
[INFO]: Streaming out GDSII with Magic (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/33-gdsii.log)...
[INFO]: Generating MAGLEF views...
[INFO]: Generating lef with Magic (/openlane/designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/33-lef.log)...
[STEP 34]
[INFO]: Streaming out GDSII with KLayout (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/34-gdsii-klayout.log)...
[STEP 35]
[INFO]: Running XOR on the layouts using KLayout (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/35-xor.log)...
[INFO]: No XOR differences between KLayout and Magic gds.
[STEP 36]
[INFO]: Running Magic Spice Export from LEF (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/36-spice.log)...
[STEP 37]
[INFO]: Writing Powered Verilog (logs: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/37-write_powered_def.log, designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/37-write_powered_verilog.log)...
[STEP 38]
[INFO]: Writing Verilog (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/37-write_powered_verilog.log)...
[STEP 39]
[INFO]: Running LVS (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/39-lvs.lef.log)...
[STEP 40]
[INFO]: Running Magic DRC (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/40-drc.log)...
[INFO]: Converting Magic DRC database to various tool-readable formats...
[INFO]: No DRC violations after GDS streaming out.
[STEP 41]
[INFO]: Running OpenROAD Antenna Rule Checker (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/41-antenna.log)...
[STEP 42]
[INFO]: Running Circuit Validity Checker ERC (log: designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/logs/signoff/42-erc_screen.log)...
[INFO]: Saving current set of views in 'designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/results/final'...
[INFO]: Saving runtime environment...
[INFO]: Generating final set of reports...
[INFO]: Created manufacturability report at 'designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/reports/manufacturability.rpt'.
[INFO]: Created metrics report at 'designs/mariam_updown_counter/runs/RUN_2023.06.07_03.20.30/reports/metrics.csv'.
[INFO]: There are no max slew, max fanout or max capacitance violations in the design at the typical corner.
[INFO]: There are no hold violations in the design at the typical corner.
[INFO]: There are no setup violations in the design at the typical corner.
[SUCCESS]: Flow complete.
[INFO]: Note that the following warnings have been generated:
[WARNING]: Module sky130_fd_sc_hd__tapvpwrvgnd_1 blackboxed during sta
[WARNING]: Module sky130_fd_sc_hd__fill_1 blackboxed during sta
[WARNING]: Module sky130_ef_sc_hd__decap_12 blackboxed during sta
[WARNING]: Module sky130_fd_sc_hd__fill_2 blackboxed during sta
```	
	
</details>

	
## Day 23
	
<details>
	
<summary> Summary </summary>
	
I learned how to integrate my design in the user projext wrapper as part of efabless's caravel.

</details>
	
<details>
	
<summary> Links </summary>
	
The followed links are found in https://github.com/efabless/caravel/, https://github.com/efabless/caravel_mgmt_soc_litex, https://github.com/efabless/caravel_user_project/blob/main/docs/source/index.rst#section-quickstart, and https://github.com/efabless/caravel/blob/main/openlane/README.rst 

</details>
	
<details>
	
<summary> Caravel integration: management SoC core instantiation </summary>
	
To clone the directory I used the following command:

```bash	
git clone https://github.com/efabless/caravel_mgmt_soc_litex.git
```
	
First, I had to modify caravel.py inside the /litex directory of the cloned directory to remove the line that imports SpiFlash.
	
To install dependencies and build the management core, I used the following commands:
	
```bash
cd caravel_mgmt_soc_litex
cd litex
make setup
pip3 install git+https://github.com/litex-hub/pythondata-software-compiler_rt.git
make
```
	
The screenshot below shows the successful build of the management core:
	
<img width="952" alt="sucessfulbuildsoc" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/208c577b-d30a-4a62-a3d8-46200b5ced90">


</details>
	
<details>
	
<summary> Caravel integration: hardening with OpenLane </summary>

	
I first created a new repo using the below link:
	
```bash
https://github.com/efabless/caravel_user_project/generate
```
	
Then, I set up the environment using the commands below

```bash
git clone https://github.com/mariamrakka/updown_counter_openlane.git
cd updown_counter_openlane
mkdir dependencies
export OPENLANE_ROOT=$(pwd)/dependencies/openlane_src # you need to export this whenever you start a new shell
export PDK_ROOT=$(pwd)/dependencies/pdks # you need to export this whenever you start a new shell
export PDK=sky130A
make setup
make pdk
make openlane
```
	
To prepare for hardening my design, I first used the following commands:
	
```bash 
cd openlane
cp -r user_proj_example/ mariam_updown_counter 
cd ..
cd verilog/rtl/
cp /home/mariam/OpenLane/designs/mariam_updown_counter/src/mariam_updown_counter.v .
```

I then modified my verilog file has shown below (to accomodate for io_oeb which is driven low to enable the output):

<img width="488" alt="final_mydesign_verilog" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/192bb585-a46e-4685-a12f-492206163f41">


I also modified the verilog/rtl/user_project_wrapper.v as shown in the screenshot below:

<img width="944" alt="final_wrapper" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/93e3891b-107e-4b61-825b-04a8f85d402c">


After that, I modified the includes.rtl.caravel_user_project in the verilog/includes/ directory as shown below:

<img width="484" alt="final_includes" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e085dd36-ded5-4ec0-be9c-2c921c81accd">

I adapted the tests found in verilog/dv/io_ports/ using the commands below:

```bash
cp -r io_ports/ mariam_updown_counter
cd mariam_updown_counter
rename s/io_ports/mariam_updown_counter/ *
```

I modified the .c file in the verilog/dv/mariam_updown_counter/ directory as follows:

<img width="490" alt="file_cfile" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/5b530514-61dc-4d02-8f76-3f757bc672c9">

I also modified the _tb.v file in the verilog/dv/mariam_updown_counter/ directory by chaging all names as needed and applying following modifications:

<img width="490" alt="final_tb" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ce860217-23b6-421b-add5-f0fb7ed7eb03">


<img width="485" alt="final_tb1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b63866e9-72f3-419f-9c6e-f77bf6479e90">


<img width="498" alt="final_tb2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/37cf6796-6cd1-4594-89b7-bc783b01dbe2">


To test the design, I used the following command in the updown_counter_openlane/ directory: 

```bash
make verify-mariam_updown_counter-rtl 
```

And below was the screenshot of the obtained traces (as we can see test has passed):

<img width="490" alt="final_tbpass" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/05e09671-b851-4a27-b1e4-8310d6086100">
	
In the updown_counter_openlane/openlane/mariam_updown_counter directory, I modified the configuration file as shown in the screenshot below:

<img width="488" alt="final_config" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/2ad78a62-3653-44bd-a8c9-102d695de669">

To harden my design, I used the command below in updown_counter_openlane/openlane directory:
	
```bash
make mariam_updown_counter
```

Below is the screenshot showing a successful flow completion:

<img width="730" alt="final_successful" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/99b1033b-1865-40a3-953d-3d870cc6d462">


Below is the GDSII layout picture:

<img width="222" alt="final_counter_gds" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/efaeff1f-f809-4a2f-b68d-473ae22af1b1">

<img width="569" alt="zoomed_final_gds_counter" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/6257f3ca-fb7c-47f0-9630-0a61dd2b6097">


Below is the LEF screenshot:

<img width="440" alt="final_lef_counter" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/b0e56e81-ab6d-4613-9af6-b179ead7da51">

	
Then, I modified the config.json file found in openlane/user_project_wrapper/directory as shown in the screenshot below:
	
<img width="953" alt="final_config_wrapper" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/0dc9e620-e440-45d2-8fed-95d5caebad63">


I also modified the macro.cfg file as follows:

<img width="499" alt="final_macro" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ddac09bf-965c-444d-ba1b-04a537dafb31">


I then hardened the user_project_wrapper by using the command below in updown_counter_openlane/openlane directory:
	
```bash
make user_project_wrapper
```
	
I got a successful flow as shown in the screenshot below:
	
<img width="796" alt="Screen Shot 2023-06-30 at 9 59 15 AM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/9c63ddff-fbe4-4917-a60e-f76c8e3dc355">

Note that the slew violations are for io pins as shown also below, so we ignore these violations:

<img width="594" alt="pin_slew_violations" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/68b65a05-7007-4d5f-8307-c449da08dbb0">


Below is the final GDS file I obtained:

<img width="907" alt="Screen Shot 2023-06-22 at 12 37 51 AM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/cfcf6718-c84c-4972-a395-96b9a3e487cc">

<img width="716" alt="Screen Shot 2023-06-22 at 12 38 38 AM" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/079864db-9f0c-4255-971e-59c28ac1dd77">

Below is the final LEF file I obtained:

<img width="554" alt="final_wrapper_lef" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/e8ec8570-dbe9-46bd-bc56-4355e98a1939">

To run the precheck locally, I used the following commands:

```bash
make precheck
make run-precheck
```

Below is a screenshot of the obtained result (0 DRC violations, only 2 out of 14 tests failed: default and gpio-defines):

<img width="572" alt="final_precheck1" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/158646ac-53a5-4973-a578-e652f11f79d1">

<img width="728" alt="final_precheck2" src="https://github.com/mariamrakka/vsd-hdp/assets/49097440/ab97261c-11c8-40ac-ad47-83113245dd9d">



</details>
	
