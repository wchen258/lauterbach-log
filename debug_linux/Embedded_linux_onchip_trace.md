## Requirement

You should be able to establish linux debug session without trace first. Refer to the [Embedded_linux_debug](https://github.com/wchen258/lauterbach-log/blob/master/debug_linux/Embedded_Linux_debug.md). The onchip trace can be established quite straight forward based on that.

## Instructions

Lauterbach does not provide Linux trace scripts. However, they do provide many start-up scripts for bare-metal applications in 
```
t32/demo/arm64/hardware/zynq_ultrascale/zcu102-apu
```
Take a look at any of the onchip trace script, and take the codes relevent to the trace, and paste that to the proper location in the working `linux-attach.cmm`. 
