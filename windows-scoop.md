# Installing SystemVerilog on Windows using scoop

In this guide we'll show you, how to install all necessary tools for synthesizing or simulating your SystemVerilog projects.

If you don't want to install scoop, check out our [manual guide](windows-manual.md).

## Installing scoop

[scoop](https://scoop.sh/) is a simple package manager for Windows.

You can install scoop using PowerShell.

```ps1
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

## Installing SystemVerilog toolchain

Now you can install the required packages for SystemVerilog.

```ps1
scoop install graphviz sed iverilog yosys
```

*sccop adds all installed packages automatically to the PATH.*

After everything is installed, run `dot -c` once to configure all plugins for graphviz. 

*This step may be optional in the future when a version including the pull request 
[1581](https://gitlab.com/graphviz/graphviz/-/merge_requests/1581) has been released.*

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

## Updates
This step is *optional*.

scoop can automatically update your installed packages. 
For this process the tool git is used, which you can install with

```ps1
scoop install git
```

Now you can update all of your installed packages at once
```ps1
scoop update *
```

I recommend that you run this command occasionally (maybe once a month). 

*Further information*

You can find a lot of useful tools in the scoop repositories (also called buckets), just search for it.
```
scoop search <package>
```

## Visual Studio Code
This step is *optional*.

Visual Studio Code is a lightweight code editor from Microsoft with lots of extensions.

You can download the software [here](https://code.visualstudio.com/) and once you installed it,
there's an extension for SystemVerilog called 
[`Verilog-HDL/SystemVerilog/Bluespec SystemVerilog`](https://marketplace.visualstudio.com/items?itemName=mshr-h.VerilogHDL). 
Open the sidebar, search for it and install it.

Using the extension you can easily edit highlighted `.sv` files.