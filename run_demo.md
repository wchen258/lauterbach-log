## Download necessary scripts

Scripts could be downloaded here. https://www.lauterbach.com/frames.html?home.html

Under the ARM64 section, download zynq_ultrascale

## Run script

Demo run for zcu102-apu_sieve_smp_sram.cmm (Lauterbach PRACTICE script) in zcu102-apu folder.

Simply open the PowerView application, File -> Run script, and choose the .cmm file. If an error occurs, try to run the reset script in ./scripts folder. 

In principle, a start-up script should be run first to set up the correct environment. It can be seen that the demo script internally invoke the zynq-ultrascale_kick_bootcore.cmm script in the ./scripts folder to do the set up.
