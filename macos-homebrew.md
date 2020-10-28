# Installing SystemVerilog on macOS using Homebrew

In this guide we'll show you how to install all necessary tools for synthesizing or simulating your SystemVerilog projects.

## Installing Homebrew
Homebrew is a package manager for macOS and will be used to install the majority of tools used.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)" 
```

## Installing SystemVerilog toolchain

This guide has been tested on macOS Catalina 10.15.7. Installation process and versions on older builds of macOS may vary.

### Synthesis & simulation tools
Just run the following commands in a terminal.
```sh
brew update
brew install yosys graphviz icarus-verilog gnu-sed dos2unix
```

### GTKWave
#### Method 1: Using Homebrew
*This, whyever, doesn't work all the time, which is why we created a second method to installing GTKWave below*.

```sh
brew cask install xquartz
brew cask install gtkwave
```


#### Method 2: Manually
First, download the GTKWave app:
https://netcologne.dl.sourceforge.net/project/gtkwave/gtkwave-3.3.107-osx-app/gtkwave.zip

After you've done that, unpack the zip-archive. An application called "gtkwave" should appear. Right-click on it and click "Open", then confirm your choice by clicking "Open" on the dialog that just popped up.

**Note: If no dialog popped up and you simply cannot open the application, you need to change a Setting. Go to System Settings - Security - General and set "Allow App-Downloads by:" to "App Store and verified developers". Now you should be able to follow the steps above.**

If gtkwave didn't open the first time, just double-klick on it once again. A new window should pop up showing you the user interface. Close the window and thereby the app. Now drag the gtkwave file (**not the gtkwave.zip file**) into your Applications Directory, shown on the lefthand side of Finder above "Documents". By doing so, gtkwave should now show up on Launchpad.


### Preparing files
Download and extract the .zip file from our Moodle course.
Now navigate to the `SystemVerilog/bin` directory and run
```sh
# Using the correct line ending for Unix
dos2unix sim.sh synth.sh
# Allow the shell scripts to be executed
chmod +x sim.sh synth.sh
```

You completed the installation of SystemVerilog. Now you can test it.

## Testing your installation

Go to the folder `SystemVerilog/src/comb` and run
```sh
# Testing the synthesis
../../bin/synth.sh example example.sv
# Testing the simulation
../../bin/sim.sh example_tb example.sv example_tb.sv
```

Now there should be a new file in the same folder called `example.pdf` which is the result of the synthesis, 
and an application called GTKWave should open up, which displays measurements of the simulation.

If GTKWave doesn't open up, don't panic. Open GTKWave manually and navigate to `SystemVerilog/src/comb` and open your `.vcd` file(s) manually. 

Congratulations! All necessary tools for SystemVerilog are working properly.
