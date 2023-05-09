
# VSD-HDP

This github repository summarized the progress made in the VSD-HDP tapeout program.

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
<img width="642" alt="yosys-installation" src="https://user-images.githubusercontent.com/49097440/236970377-90dc784f-934b-4268-9d05-766f01d0ec52.png">
Below is the screenshot showing sucessful launch:
<img width="568" alt="yosys" src="https://user-images.githubusercontent.com/49097440/236970455-639c2d86-1982-4473-9fe6-656909ef4597.png">
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

<img width="644" alt="OpenSTA-installation" src="https://user-images.githubusercontent.com/49097440/236970483-93e5af93-b6b6-4ec7-b235-282e258e7a9c.png">

Below is the screenshot showing sucessful launch:

<img width="570" alt="OpenُSTA" src="https://user-images.githubusercontent.com/49097440/236970494-db1af91a-ff50-4e1b-a78a-f2f2352d451e.png">
 
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

<img width="641" alt="ngspice-installation" src="https://user-images.githubusercontent.com/49097440/236970506-7a163ce6-b326-4264-9a7c-d698868ac30a.png">

Below is the screenshot showing sucessful launch:

<img width="573" alt="ngspice" src="https://user-images.githubusercontent.com/49097440/236970522-7d74c109-739c-4755-88e5-3a478ba33383.png">
 
- iverilog
I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
Below is the screenshot showing sucessful installation:
<img width="568" alt="iverilog-installation" src="https://user-images.githubusercontent.com/49097440/236970545-d39310e7-cb8d-4fb6-beb5-098f21bd08fb.png">
Below is the screenshot showing sucessful launch:
<img width="560" alt="iverilog" src="https://user-images.githubusercontent.com/49097440/236970564-1d7d0d50-f901-42d5-b060-64c30175cb14.png">
 - gtkwave
 I installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
Below is the screenshot showing sucessful installation:
<img width="568" alt="gtkwave-installation" src="https://user-images.githubusercontent.com/49097440/236970581-9f8dbd1e-f93a-41de-8f5a-5717656364e3.png">
Below is the screenshot showing sucessful launch:
<img width="572" alt="gtkwave" src="https://user-images.githubusercontent.com/49097440/236970625-ddb68424-25d8-4031-aea7-da6e6c760934.png">
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
<img width="570" alt="magic-installation" src="https://user-images.githubusercontent.com/49097440/236970651-2375e6dc-df76-4bd8-aec9-0f9423bf042b.png">
Below is the screenshot showing sucessful launch:
<img width="635" alt="magic" src="https://user-images.githubusercontent.com/49097440/236970669-bfc9c632-a0a0-42af-bb4d-4c8fc95d9875.png">

