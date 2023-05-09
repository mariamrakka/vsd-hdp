
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program.

## Day 0

I installed the following tools:
 - Yosys
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


 - OpenSTA
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


 - ngspice
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


 - iverilog
 I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="iverilog-installation" src="https://user-images.githubusercontent.com/49097440/236971696-39580165-f629-4404-bef8-45ebfbedcdcd.png">


 Below is the screenshot showing sucessful launch:
 
 <img width="560" alt="iverilog" src="https://user-images.githubusercontent.com/49097440/236971782-a5ae1815-7ca0-4514-8b9c-6464b012b5c7.png">


 - gtkwave
 I installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="gtkwave-installation" src="https://user-images.githubusercontent.com/49097440/236971803-bae61afb-35d0-4548-84f8-a687f552500c.png">


Below is the screenshot showing sucessful launch:

<img width="572" alt="gtkwave" src="https://user-images.githubusercontent.com/49097440/236971818-0c6906c4-2839-4913-8d1e-fc173c5d9251.png">


 - magic
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




