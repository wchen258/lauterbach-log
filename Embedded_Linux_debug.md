## Linux Awareness

Awareness means the debugger need to be aware the existence of the Linux Kernel. To enable this, the Linux has to be compiled with certain configuration.

https://www2.lauterbach.com/pdf/training_rtos_linux.pdf see kernel configuration.

### Linux Kernel Requirement

Below is the summary of the Lauterbach manual on Linux kernel configuration 

```
cat /proc/config.gz | gunzip
```
The command above can list the current running kernel configuration. This command works if `CONFIG_IKCONFIG_PROC` is set during the kernel compilation (which is usually yes). Lauterbach can also obtain the configuration if this option is set.

The following options should be disabled

```
CONFIG_DEBUG_INFO_REDUCED
CONFIG_DEBUG_INFO_SPLIT
CONFIG_RANDOMIZE_BASE
CONFIG_SOFTLOCKUP_DETECTOR
CONFIG_DETECT_HUNG_TASK
CONFIG_CPU_IDLE
CONFIG_CPU_FREQ
CONFIG_UNMAP_KERNEL_AT_EL0
```
Notice `CONFIG_UNMAP_KERNEL_AT_EL0` is not available prior to kernel version 4.16. `CONFIG_SOFTLOCKUP_DETECTOR` and `CONFIG_DETECT_HUNG_TASK` are recommended to be disabled, might not be mandatory.
The following options should be set
```
CONFIG_KALLSYMS=y
CONFIG_DEBUG_INFO=y
```








