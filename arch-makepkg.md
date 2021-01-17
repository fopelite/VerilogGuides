# Installing SystemVerilog on Arch-based systems using Pacman and makepkg

In this guide we'll show you how to install all necessary tools for synthesizing or simulating your SystemVerilog projects.

> "[makepkg](https://git.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in) is a script to automate the
> building of packages. The requirements for using the script are
> a build-capable Unix platform and a [PKGBUILD](https://wiki.archlinux.org/index.php/PKGBUILD). 
> ([Arch Wiki](https://wiki.archlinux.org/index.php/Makepkg))

To use `makepkg` make sure you have `base-devel` installed
by running the following in a terminal (as root):
```sh
pacman -S base-devel
```

## Installing SystemVerilog toolchain

This guide has been tested on *5.10.6-arch1-1 x86_64 GNU/Linux*, but should work for all Arch-based systems.

### Getting the PKGBUILD and the SystemVerilog zip archive.
Either clone or download and unzip this repository.

You should have received a SystemVerilog zip archive:
Place the archive in the repository's directory.
**Don't** unzip it.
Rather make the name all lowercase,
remove all spaces and the part in parenthesis.
E.g. `SystemVerilog (Synthese und Simulation)-20210116.zip` becomes `systemverilog-20210116.zip`.

### Building and installing the package
Simply open a terminal in repository's directory and run:
```sh
makepkg -is
```
Pacman should prompt you a few times to install dependencies
and finally the package itself. Just hit enter each time.

You completed the installation of SystemVerilog. Now you can test it.

## Testing your installation

In the same terminal as before run:
```sh
# Copying examples
cp -r /usr/share/systemverilog/src/* .
cd comp
# Testing the synthesis
sv-synth example example.sv
# Testing the simulation
sv-sim example_tb example.sv example_tb.sv
```

Now there should be a new file in the same folder called `example.pdf` which is the result of the synthesis, 
and an application called GTKWave should open up, which displays measurements of the simulation.

Congratulations! All necessary tools for SystemVerilog are working properly.
