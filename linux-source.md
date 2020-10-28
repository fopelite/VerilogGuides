# Building SystemVerilog tools from source on Linux

## Abstract
We will build all the tools we need from source, which ensures that we will always have the most up-to-date versions installed and thus reduces the risk of running into problems because of conflicting versions or similar while using these tools.
This guide should work on all Linux distributions but has its focus on Arch-based (Arch, Manjaro, ...) and Debian-based (Debian, Ubuntu, Mint, ...) operating systems.

## Prerequisites
To be able to follow each and every step as instructed in this guide, you need to have some programs and toolchains already installed. This includes:
* a working C compiler toolchain such as `clang` or `gcc`
* a package manager such as `apt`, `pacman`, `rpm` or similar (in the following guide we will use `pacman` and `apt`, but using other managers should work equally well with some tweaks ans changes)
* `wget`

Create a new folder to save all downloads by running
`mkdir system_verilog_tools`
and enter the newly created directory by running
`cd system_verilog_tools`

## Installing Git
Install git, a program used for version control:
* Arch: `sudo pacman -S git`
* Debian: `sudo apt install git`.

## Installing GraphViz
### Install dependencies:
Arch:
```sh
sudo pacman -S base-devel cairo expat freetype2 fontconfig glib2 libpng pango zlib gts gtk3 gtkglext glade glut autoconf ghostscript pkg-config swig
```
Debian:
```sh
sudo apt install build-essential libcairo2-dev expat libfreetype-dev fontconfig libglib2.0-dev libpng-dev libpango-1.0-0 libpango1.0-dev zlib1g-dev libgts-dev libgtk-3-dev libgtkglext1 libgtkglext1-dev freeglut3-dev autoconf ghostscript pkg-config swig libperl-dev
```
### Source download
Download the GraphViz source package by entering
`wget https://www2.graphviz.org/Packages/stable/portable_source/graphviz-2.44.1.tar.gz`
and unpack by running 
`tar -xzvf graphviz-2.44.1.tar.gz`

Enter the freshly unpacked directory using `cd graphviz-2.44.1`.

### Configuration, compilation and installation
Now configure, compile and uninstall GraphViz by running the follwing commands in the provided order:
1. `./configure`
2. `make -j$(nproc)`
    * *if you run into an error here just try to run* `make` *without any arguments, as these do the following:*
        * `-j` essentially lets you define the number of cores to run the compilation on (parallelized)
        * `nproc` outputs the number of usable cores on your processor
4. `sudo make install`

### Testing
Last but certainly not least, test your installation by running `dot -v`. If you can spot any output, especially something such as `dot - graphviz version 2.44.1 (20200629.0846)` in the first line of output.

## Installing yosys
### Install dependencies
Arch:
```sh
sudo pacman -S bison flex readline gawk tcl libffi xdot pkg-config python3 boost boost-libs zlib --assume-installed=graphviz
```
Debian:
```sh
sudo apt install bison flex libreadline-dev gawk tcl-dev libffi-dev xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev
```

### Source download
Now go back to the root directory by entering `cd ..` and proceed to downloading the yosys source code by running:
`git clone https://github.com/YosysHQ/yosys.git`

Navigate to the directory by typing `cd yosys`.

### Configuration, compilation and installation
Now, depending on whether you use clang or gcc as a compiler toolchain, run either of the following:
* `make config-gcc` *or*
* `make config-clang`

Now compile and install again by entering `make -j$(nproc)` (or simply `make` if you run into issues) and finally `sudo make install`.

### Testing
Test your installation by entering `yosys --version`.

If you see the version number and some additional text, you're fine

## Installing Icarus-Verilog
### Install dependencies
Arch:
```sh
sudo pacman -S gperf
```
Debian:
```sh
sudo apt install gperf
```
### Source download
Download the Icarus-Verilog source by running:
`cd .. && wget https://github.com/steveicarus/iverilog/archive/v11_0.tar.gz`

Unpack the downloaded source and navigate to the newly created directory:
`tar -xzvf v11_0.tar.gz && cd iverilog-11_0`

### Configuration, compilation and installation
Now, create your `configure` file by running `sh autoconf.sh`. After that, enter the following commands once again to configure, compile and install:
1. `./configure`
2. `make -j$(nproc)` - *if you run into an error here just try to run* `make` *without any arguments*
3. `sudo make install`

### Testing
Finally, test your installation by running `iverilog -v`

## Installing GTKWave
### Install dependencies
Arch:
```sh
sudo pacman -S tk
```
Debian:
```sh
sudo apt install tk tk-dev liblzma-dev
```

### Source download
Download the GTKWave source:
`cd .. && wget http://gtkwave.sourceforge.net/gtkwave-3.3.107.tar.gz`

Unpack the source and navigate to the newly created directory:
`tar -xzvf gtkwave-3.3.107.tar.gz && cd gtkwave-3.3.107`

### Configuration, compilation and installation:
Configure, compile and install:
1. `./configure`
2. `make -j$(nproc)` - *if you run into an error here just try to run* `make` *without any arguments*
3. `sudo make install`

### Testing
Lastly, test your installation by running `gtkwave --version`

## After-build cleanup
If you're here, you made it. You successfully built all tools you need from source and installed them.
Now, if you want to free some space on your disk, simply run:
`cd ../.. && rm -rf system_verilog_tools`

This deletes all the downloaded source files as we technically don't need them any longer. However, if you want to keep the files, you're of course free to do so.

## Testing the installation
### Attention
We highly recommend you to test your installation. At least, follow the first few steps to convert the line-endings and adjust the permissions as this will ensure that future sythesizations will work and thus is crucial.

### Install dependencies:
Arch:
```sh
sudo pacman -S dos2unix
```
Debian:
```sh
sudo apt install dos2unix
```

### Preparing files
Download and extract the .zip file from our Moodle course.
Now navigate to the `SystemVerilog/bin` directory and run
```sh
# Using the correct line ending for Unix
dos2unix sim.sh synth.sh
# Allow the shell scripts to be executed
chmod +x sim.sh synth.sh
```

### Actual testing
Go to the folder `SystemVerilog\src\comb` and run
```sh
# Testing the synthesis
../../bin/synth.sh example example.sv
# Testing the simulation
../../bin/sim.sh example_tb example.sv example_tb.sv
```

Now there should be a new file in the same folder called `example.pdf` which is the result of the synthesis and GTKWave should open up, which displays measurements of the simulation.

Congratulations! All necessary tools for SystemVerilog are working properly.
