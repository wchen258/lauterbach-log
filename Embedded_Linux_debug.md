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
The `CONFIG_CPU_IDLE` and `CONFIG_CPU_FREQ` might be set. In the manual, the following instructions could be referenced without recompile the kernel.

The Linux kernel CPU power management could cause for some processor architectures that single cores are not accessible by the debugger when in power saving state. CPU power management can be disabled in the Linux kernel configuration by disabling the options `CONFIG_CPU_IDLE` and` CONFIG_CPU_FREQ`.Idle states can also be disabled for single cores from the shell by writing to the file `/sys/devices/system/cpu/cpu<x>/cpuidle/state<x>/disable`. 

Alternatively, you may remove the idle-states property from the device tree if available.On some Linux distributions, power management can be disabled using specific kernel command line parameters (e.g. “`jtag=on`” or “`nohlt`”). Please refer to the documentation of the kernel command line parameters of your Linux distribution for more information. 








