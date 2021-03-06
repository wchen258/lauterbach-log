## Requirement

You should be able to establish linux debug session without trace first. Refer to the [Embedded_linux_debug](https://github.com/wchen258/lauterbach-log/blob/master/debug_linux/Embedded_Linux_debug.md). The onchip trace can be established quite straight forward based on that.

## Instructions

Lauterbach does not provide Linux trace scripts. However, they do provide many start-up scripts for bare-metal applications in 
```
t32/demo/arm64/hardware/zynq_ultrascale/zcu102-apu
```
Take a look at any of the onchip trace script, and take the codes relevent to the trace, and paste that to the proper location in the working `linux-attach.cmm`. Take a look at this [example script](linux-attch-traced.cmm). Again you need to modify the relevent parameters to your setting, including: the path to the vmlinux and the kernel specific parameters generated by `detect_translation.cmm`.

When you run the script, the onchip trace for linux should be ready to go. Watch [this](https://www.youtube.com/watch?v=ipgXGO6JKZE) to get a basic idea on what you can do.

Notice, in this video they are using an analyzer which enables a much larger buffer for the trace information. We are using the onchip buffer to store the trace information, thus the buffer is small.
