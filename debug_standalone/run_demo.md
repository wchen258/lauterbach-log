## Obtain demo scripts

Lauterbach provides extensive demo scripts suitable for different boards and tasks. It suggests to start with a suitable demo script to set up your debug session.

For zcu102, the demo scripts come with the standard installation, which can be found in 

```
t32/demo/arm64/hardware/zynq_ultrascale
```

If you cannot find the demo scripts here, you can also downloaded them from this [link](https://www.lauterbach.com/frames.html?home.html)
Under the download/ARM64 section, download zynq_ultrascale for zcu102

## Run a JTAG debug demo script

In this session we will set up to run demo script `zcu102-apu_sieve_smp_sram.cmm` (cmm is extension for Lauterbach PRACTICE script) in `zcu102-apu` folder. This script set up a debug session for zcu102 and would debug `sieve_ram_aarch64_v8.elf`. You can find the source code `sieve.c` for the ELF in the same directory. 

As the name suggests, this ELF runs [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes), a prime number finding algorithm. The cmm script would invoke other cmm scripts (responsible for board setting-up like booting cores and etc.) in the directory to set up the debug session, in this script you can also find the command that loads the ELF. 

It's a good idea to single step through this script (will discuss how to shortly) to see how the debug session is established. 

### Hardware setup

Xilinx's [ZCU102 evaluation Board User Guide](https://www.xilinx.com/support/documentation/boards_and_kits/zcu102/ug1182-zcu102-eval-bd.pdf) contains two callout diagrams where you can conveniently find the location of each component. 

Lauterbach debugger's USB cable should connect to the host machine, and the debugger's JTAG cable should connect to J6 (you can find J6 in the User Guide above, it is numbered 39 on the callout diagram). The board should be in the JTAGE boot mode. This is achieved by toggle on all switches on the SW6 (switch 6 callout number 44). In practice, if you put SW6 in SDcard boot mode, you can still run this demo script, but you have to execute the demo script before the bootloader in SDcard loads anything. Thus unless you want to debug something on the SDcard (e.g. a Linux on the card), you should put SW6 into JTAG boot mode. 


### Run the script

The recommended steps for powering up is: power up the Lauterbach debugger hardware, start the Lauterbach debugger software (PowerView 32) through USB, and finally power up the zcu102 board. To start Latuerbach debugger software, you can refer to the installation in this tutorial. 

Now on the host machine, you should be able to see the PowerView32 GUI. From the menu `File -> Open script`, and choose `zcu102-apu_sieve_smp_sram.cmm`. On the top right corner of the popped up window, you can choose "DO" to run the script from start to the end, or choose "DEBUG" to have more control over the process. 

By simply hitting "DO", the debug session should be successfully established.

To see in details how the debug session is established, hitting "DEBUG" instead of "DO". A new window should pop up, and you can now debug this debug script such as setting breakpoints, single step, and etc.. It's very helpful to run the script in debug mode, so that the step by step configuration can be studied. 

## Useful tips

### Convenient command

The PowerView32 accept command line input at the bottom. `reset` each time when you want to run a new script. `winclear` can clear all the windows. `area` output all the useful information. You can add ` \spotlight` to a command, e.g. `register \spotlight` so that each time when the values in registers changes, the values would be highlighted. 

Bottom right of the window, a number indicates which core all the information belongs to. Windows would also change background color to indicate the core it runs on. You can right click the number to switch core. 

In `/t32/pdf`, you can find many useful documentations.

## Run a trace demo script

In this session, we will set up a debug session with trace port in use. It's highly suggested to successfully set up the plain JTAG debug explained above, since running trace script only requires miniminum modificatoin. You can find more information from `trace_arm_etm.pdf` and `training_arm_etm.pdf` from `pdf` folder. ETM is an optional component, standing for Embedded Trace Macrocell which allows the reconstruction of the program execution. You need to have corresponding hardware to utilize this component. 

### Hardware setup

Make sure the target and the debugger is power off. Connect the trace debugger to the the JTAG debugger. There is only one way to connect these two together. If you are still not sure, refer to the tutorial video we have. To get started, first power on the debugger. Then start the PowerView32 software on the host machine, you can use the exact same USB start command. The time to launch the software should be longer due to the extra trace configuration. Finally start the target. 

Notice, beside putting the board into JTAG boot mode and connecting to J6, some scripts also requires shorting J14 (By default, the board should short J14 already).

### Run demo script

In `zcu102-apu` folder, you can find many scripts with keyword `trace`. Usually the starting of the scripts contain useful summary regarding the setup and usage. Run any one of these through PowerView32. Upon finishing, you can see a trace window. This window should automatically log all the trace information. If not, click the `init` button on the trace window. 





