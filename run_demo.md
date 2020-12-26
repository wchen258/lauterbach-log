## Obtain demo scripts

Lauterbach provides extensive demo scripts suitable for different boards and tasks. It suggests to start with a suitable demo script to set up your debug session.

For zcu102, the demo scripts come with the standard installation, which can be found in 

```
t32/demo/arm64/hardware/zynq_ultrascale
```

If you cannot find the demo scripts here, you can also downloaded them from this [link](https://www.lauterbach.com/frames.html?home.html)
Under the ARM64 section, download zynq_ultrascale for zcu102

## Run a demo script

In this session we will set up to run demo script `zcu102-apu_sieve_smp_sram.cmm` (cmm is extension for Lauterbach PRACTICE script) in `zcu102-apu` folder. This script set up a debug session for zcu102 and would debug `sieve_ram_aarch64_v8.elf`. You can find the source code `sieve.c` in the same directory. 

As the name suggests, this ELF runs [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes), a prime number finding algorithm. The cmm script would invoke other cmm scripts (responsible for board setting-up like booting cores and etc.) in the directory to set up the debug session, you can also find the command that load the ELF in this script. 

It's a good idea to single step through this script (will discuss how to shortly) to see how the debug session is established. 

### hardware setup

Simply open the PowerView application, `File -> Run script`, and choose the .cmm file. If an error occurs, try to run the reset script in `./scripts` folder. 

In principle, a start-up script should be run first to set up the correct environment. It can be seen that the demo script internally invoke the `zynq-ultrascale_kick_bootcore.cmm` script in the `./scripts` folder to do the set up.
