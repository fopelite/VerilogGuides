# Installing SystemVerilog on Windows

In this guide we'll show you, how to install all necessary tools for synthesizing or simulating your SystemVerilog projects.

If you want to use a faster method of installing all tools and keeping them up-to-date automatically, 
check out the [installation using scoop](windows-scoop.md).

## Installing SystemVerilog toolchain

### Synthesis tools
Download the latest release of the GraphViz installer from 
[graphviz.org](https://www2.graphviz.org/Packages/stable/windows/10/cmake/Release/x64/).
While running the installer, it's important you select the option `Add Graphviz to the system PATH for current user` 
otherwise you have to do it [manually](https://www.java.com/en/download/help/path.html).

You find the latest version of YoSyS at [clifford.at](http://www.clifford.at/yosys/download.html).
Download the file which name starts with `yosys-win32-mxebin` and ends with `.zip`.
This is an archive file which you can extract using the Windows explorer.
Remember the directory where you extracted this file and [add it to the PATH](https://www.java.com/en/download/help/path.html).

At the end start a PowerShell console with privileged rights (right click and *run as administrator*) and run
```ps1
dot -c
```
to configure all plugins, otherwise there may be an error when generating `.pdf` files.

### Simulation tools
Download the latest installer (the file up top) of Icarus Verilog from [bleyer.org](http://bleyer.org/icarus/).
Start the installation progress and select a target directory *without spaces* in its name.
It's also important, that you select the option `Add executable folder(s) to the user PATH`. 
Otherwise, you have to add the subfolders `bin` and `gtkwave\bin` manually 
[to your PATH](https://www.java.com/en/download/help/path.html).

You completed the installation of SystemVerilog. Now you can test it.

## Testing your installation

Download and extract the .zip file from our Moodle course.

Then open the folder `SystemVerilog\src\comb` in PowerShell and run the following commands:
```ps1
# Testing the synthesis
..\..\bin\synth.bat example example.sv
# Testing the simulation
..\..\bin\sim.bat example_tb example.sv example_tb.sv
```

Now there should be a new file in the same folder called `example.pdf` which is the result of the synthesis, 
and an application called GTKWave should open up, which displays measurements of the simulation.

Congratulations! All necessary tools for SystemVerilog are working properly.
