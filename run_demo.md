## Obtain demo scripts

Lauterbach provides extensive demo scripts suitable for different boards and tasks. It suggests to start with a suitable demo script to set up your debug session.

For zcu102, the demo scripts come with the standard installation, which can be found in 

```
t32/demo/arm64/hardware/zynq_ultrascale
```

If you cannot find the demo scripts here, you can also downloaded them from this [link](https://www.lauterbach.com/frames.html?home.html)
Under the download/ARM64 section, download zynq_ultrascale for zcu102

## Run a demo script

In this session we will set up to run demo script `zcu102-apu_sieve_smp_sram.cmm` (cmm is extension for Lauterbach PRACTICE script) in `zcu102-apu` folder. This script set up a debug session for zcu102 and would debug `sieve_ram_aarch64_v8.elf`. You can find the source code `sieve.c` for the ELF in the same directory. 

As the name suggests, this ELF runs [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes), a prime number finding algorithm. The cmm script would invoke other cmm scripts (responsible for board setting-up like booting cores and etc.) in the directory to set up the debug session, in this script you can also find the command that loads the ELF. 

It's a good idea to single step through this script (will discuss how to shortly) to see how the debug session is established. 

### hardware setup

Xilinx's [ZCU102 evaluation Board User Guide](https://www.xilinx.com/support/documentation/boards_and_kits/zcu102/ug1182-zcu102-eval-bd.pdf) contains two callout diagrams where you can conveniently find the location of each component. 

Lauterbach debugger's USB cable should connect to the host machine, and the debugger's JTAG cable should connect to J6 (you can find J6 in the User Guide above, it is numbered 39 on the callout diagram). The board should be in the JTAGE boot mode. This is achieved by toggle on all siwtches on the SW6 (switch 6 callout number 44). In practice, if you put SW6 in SDcard boot mode, you can still run this demo script, but you have to execute the demo script before the bootloader in SDcard loads anything. Thus unless you want to debug something on the SDcard (e.g. a Linux on the card), you should put SW6 into JTAG boot mode. 


### run the script

The recommended steps for powering up is: power up the Lauterbach debugger hardware, start the Lauterbach debugger software (PowerView 32) through USB, and finally power up the zcu102 board. To start Latuerbach debugger software, you can refer to the installation in this tutorial. 

Now on the host machine, you should be able to see the PowerView32 GUI. From the menu `File -> Open script`, and choose `zcu102-apu_sieve_smp_sram.cmm`. On the top right corner of the popped up window, you can choose "DO" to run the script from start to the end, or choose "DEBUG" to have more control over the process. 

By simply hitting "DO", the debug session should be successfully established.

To see in details how the debug session is established, hitting "DEBUG" instead of "DO". A new window should pop up, and you can now debug this debug script such as setting breakpoints, single step, and etc.. It's very helpful to run the script in debug mode, so that the step by step configuration can be studied. 

## useful tips

### convenient command

The PowerView32 accept command line input at the bottom. `reset` each time when you want to run a new script. `winclear` can clear all the windows. `area` output all the useful information. You can add ` \spotlight` to a command, e.g. `register \spotlight` so that each time when the values in registers changes, the values would be highlighted. 

Bottom right of the window, a number indicates which core all the information belongs to. Windows would also change background color to indicate the core it runs on. You can right click the number to switch core. 










