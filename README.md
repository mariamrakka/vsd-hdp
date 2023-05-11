
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program.

## Day 0

I installed the following tools:
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
This is how I simulated and synthesized a 2x1 mux using iverilog and yosys respectively. iverilog generates from the RTL design and its testbench a value changing dump file (vcd). gtkwave is the tool used to plot the simulation results of the design. Yosys is a tool which synthesizes RTL designs into a netlist. It is also used to test the synthesized netlist when we provide it with a testbench.

<details>
 <summary> Verilog code </summary>
- The verilog code of the 2x1 mux is as follows:

```bash
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
- The verilog code of the testbench is as follows: 

```bash
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```
</details>

 <details>
 <summary> Simulation: iverilog and gtkwave </summary>
 
 I used the following commands to simulate and view the plots of the RTL design:
	
 ```bash
 iverilog good_mux.v tb_good_mux.v
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

I first synthesized a multiple module (made of two submodules) at the multiple module level (both in hierarchical and flattened forms) then at the submodule level. Synthesis at the submodule level is important for two reasons: 1-) when we have multiple instances of same module (we synthesize once and replicate this netlist multiple times and stitch together the replicas to get the multiple module netlist, and 2-) when we want to divide and conquer (in massive designs) so that the tool can generate a portion by portion of the overall netlist and then we can stitch together the netlist portions to get the multiple module netlist.

<details>
 <summary> Verilog code </summary>
- The verilog code of the multiple module (multiple_modules.v) is as follows:
	
```bash
module sub_module2 (input a, input b, output y);
	assign y = a | b;
endmodule
module sub_module1 (input a, input b, output y);
	assign y = a&b;
endmodule
module multiple_modules (input a, input b, input c , output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
endmodule
```
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
