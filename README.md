# Freedom_zybo Repository
=======

This repository contains the RTL created by SiFive for its Freedom E300 and U500
platforms. The Freedom E310 Arty FPGA Dev Kit and Freedom E310 Zybo FPGA Dev Kit 
implement the Freedom E300 Platform. The Freedom U500 VC707 FPGA Dev Kit implements
the Freedom U500 Platform.

Please read the section corresponding to the kit you are interested in for
instructions on how to use this repo.

Software Requirement
--------------------
To compile the bootloaders for Freedom E300 Zybo, Arty and U500 VC707
FPGA dev kits, the RISC-V software toolchain must be installed locally and
set the $(RISCV) environment variable to point to the location of where the
RISC-V toolchains are installed. You must pay attention to the version, or 
you may meet much trouble.

First, you should download the repository(it may take much time):
```sh
$ git clone --recursive https://github.com/gongqingfeng/freedom_zybo.git
```

Second, you should enter the work dir like this:
```sh
$ cd freedom_zybo/freedom
```

Optionally, if you did not compile the toolchain and you do like this(it will take much time):
```sh
$ cd rocket-chip/riscv-tools
$ export RISCV=/yout/install/toolchain/location
$ ./build.sh
```
OK! Let's go ahead!

Freedom E300 Zybo FPGA Dev Kit
------------------------------

The Freedom E300 Zybo FPGA Dev Kit implements a Freedom E300 chip.

### How to build

The Makefile corresponding to the Freedom E300 Zybo FPGA Dev Kit is
`Makefile.e300zybodevkit` and it consists of several targets:

- `verilog`: to compile the Chisel source files and generate the Verilog files.
- `project`: to compile the Chisel source files and generate the vivado project.
- `vivado`: to launch the vivado project with GUI mode. So you can systhesis, implement and generate bitstream by yourself.

To execute these targets, you can run the following commands:

```sh
$ make -f Makefile.e300zybodevkit verilog
$ make -f Makefile.e300zybodevkit project
$ make -f Makefile.e300zybodevkit vivado
```
Note1: This lab tested within vivado 2016.2.
Note2: Before you generate bitstream, you are supposed to add the `freedom_zybo/freedom/fpga-shells/xilinx/zybo/tcl/no_connect.tcl` file to your Bitstream Settings's tcl.pre blank line. Otherwise, you will get errors.

The vivado project files place under `builds/e300artydevkit` and the *.v files place under `builds/e300artydevkit/obj`.

Note that in order to run the `projest` and `vivado`target, you need to have the `vivado`
executable on your `PATH`.

### Bootrom

The default bootrom consists of a program that can blink tree LED from address 0x0001FFFF on the Zybo board.


Freedom E300 Arty FPGA Dev Kit
------------------------------

The Freedom E300 Arty FPGA Dev Kit implements a Freedom E300 chip.

### How to build

The Makefile corresponding to the Freedom E300 Arty FPGA Dev Kit is
`Makefile.e300artydevkit` and it consists of two main targets:

- `verilog`: to compile the Chisel source files and generate the Verilog files.
- `mcs`: to create a Configuration Memory File (.mcs) that can be programmed
onto an Arty FPGA board.

To execute these targets, you can run the following commands:

```sh
$ make -f Makefile.e300artydevkit verilog
$ make -f Makefile.e300artydevkit mcs
```

Note: This flow requires vivado 2017.1. Old versions are known to fail.

These will place the files under `builds/e300artydevkit/obj`.

Note that in order to run the `mcs` target, you need to have the `vivado`
executable on your `PATH`.

### Bootrom

The default bootrom consists of a program that immediately jumps to address
0x20400000, which is 0x00400000 bytes into the SPI flash memory on the Arty
board.

### Using the generated MCS Image

For instructions for getting the generated image onto an FPGA and programming it with software using the [Freedom E SDK](https://github.com/sifive/freedom-e-sdk), please see the [Freedom E310 Arty FPGA Dev Kit Getting Started Guide](https://www.sifive.com/documentation/freedom-soc/freedom-e300-arty-fpga-dev-kit-getting-started-guide/).

Freedom U500 VC707 FPGA Dev Kit
-------------------------------

The Freedom U500 VC707 FPGA Dev Kit implements the Freedom U500 platform.

### How to build

The Makefile corresponding to the Freedom U500 VC707 FPGA Dev Kit is
`Makefile.u500vc707devkit` and it consists of two main targets:

- `verilog`: to compile the Chisel source files and generate the Verilog files.
- `mcs`: to create a Configuration Memory File (.mcs) that can be programmed
onto an VC707 FPGA board.

To execute these targets, you can run the following commands:

```sh
$ make -f Makefile.u500vc707devkit verilog
$ make -f Makefile.u500vc707devkit mcs
```

Note: This flow requires vivado 2016.1. Newer versions are known to fail.

These will place the files under `builds/u500vc707devkit/obj`.

Note that in order to run the `mcs` target, you need to have the `vivado`
executable on your `PATH`.

### Bootrom

The default bootrom consists of a bootloader that loads a program off the SD
card slot on the VC707 board.
