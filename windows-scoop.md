# Installing SystemVerilog using scoop

## Installing scoop

[scoop](https://scoop.sh/) is a simple package manager for Windows.

You can install scoop using PowerShell.

```ps1
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

## Installing SystemVerilog

Now you can install the required packages for SystemVerilog.

```ps1
scoop install graphviz sed iverilog
```

*sccop adds all installed packages automatically to the PATH.*

Sadly there's no package for *yosys*. You have to download the file [`yosys-win32-mxebin-0.9.zip`](http://www.clifford.at/yosys/nogit/win32/yosys-win32-mxebin-0.9.zip), extract it somewhere and the new folder to your  PATH.

After everything is installed, run `dot -c` once to configure all plugins for graphviz. 

*This step may be optional in the future when a version including the pull request [1581](https://gitlab.com/graphviz/graphviz/-/merge_requests/1581) has been released.*

## Testing your installation

Download and extract the .zip file from our Moodle course.

Then open the folder `SystemVerilog\src\comb` in PowerShell and run the following commands:
```ps1
# Testing the synthesis
..\..\bin\synth.bat example example.sv
# Testing the simulation
..\..\bin\sim.bat example_tb example.sv example_tb.sv
```

Now there should be a new file in the same folder called `example.pdf` which is the result of the synthesis and an application called GTKWave should open up, which displays measurements of the simulation.

## Updates
This step is *optional*.

If you want to keep your packages installed via scoop up-to-date, 
you have to download the package git, so you have to run once:

```ps1
scoop install git
```

Now you can update all of your packages at once (except `yosys`):
```ps1
scoop update *
```

I recommend that you run this command occasionally (maybe once a month). 

*Further information*

You can find a lot of useful tools in the scoop repository, just search for it.
```
scoop search <package>
```

## Visual Studio Code
This step is *optional*.

Visual Studio Code is a lightweight code editor from Microsoft with lots of extensions.

You can download the software [here](https://code.visualstudio.com/) and once you installed it,
there's an extension for SystemVerilog called [`Verilog-HDL/SystemVerilog/Bluespec SystemVerilog`](https://marketplace.visualstudio.com/items?itemName=mshr-h.VerilogHDL). 
Open the sitebar, search for it and install it.

Now you can easily edit highlighted `.sv` files.