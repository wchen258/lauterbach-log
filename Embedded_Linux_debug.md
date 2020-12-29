Lauterbach is capable of debugging an embedded linux running on a development board. This is a guideline on how to set up. It's recommended to go through the run_demo session before setting the linux debug, as we will use some terminologies and conventions from that session. `rtos_linux_stop.pdf` is useful in the `pdf` folder.

## Quick start

### Requirements

Below is a sequence of setting up an embedded Linux debug session. We will use SDcard boot and use the linux on the same SDcard. You might want to use Xilinx Embedded Linux Build flows, the [PetaLinux](https://www.xilinx.com/products/design-tools/embedded-software/petalinux-sdk.html#tools) to faciliate the process. Also, save the corresponding vmlinux somewhere, as Lauterbach would need to load it to obtain the symbols. 

Again, we are working on zcu102

### Hardware setting

Use the plain JTAG debugger (do not connect with the trace debugger). Insert the SDcard, and toggle the SW6 to put the board into SDK boot mode. If you are unsure of that, take a look at Xilinx's [ZCU102 evaluation Board User Guide](https://www.xilinx.com/support/documentation/boards_and_kits/zcu102/ug1182-zcu102-eval-bd.pdf). Again, connect the debug cable to J6.

Verify the Linux can successfully boot from the SDcard. It's handy to connect the board to a host machine via USB, so that you can use things like minicom to communicate. 

### Software setting

Poweroff the target. Power on the Lauterbach debugger, and then USB launch the PowerView (if unsure, refer to the installation session). 

Power on the target, and wait for the Linux finishing the booting. Sometimes the minicom might appear to be frozen due to the target is stopped by the debugger. In this case, you can simply hit `Run` on the PowerView to resume the execution. 

Following scripts will be used

```
t32/demo/arm64/kernel/linux/board/generic-template/detect_translation.cmm
t32/demo/arm64/kernel/linux/board/zynq-ultrascale/linux-attach.cmm
```

`linux-attach.cmm` is the demo script that set up the debug session. However it has couple fields missing which users might need to fill in by themselves. Read the instruction in `linux-attach.cmm` carefully, it would guide you on how to find the missing field. 

`detect_translation.cmm` is designed to find the missing fields in `linux-attach.cmm`. Again read the instruction. 

In theory, if the missing fields are correctly filled in, by simply running the `linux-attach.cmm`, the debug session should be established. More details regarding the missing fields, refer to `rtos_linux_stop.pdf`.


## More things to consider

If the above steps do not go through, possible situations could be the following

1. It's possible Lauterbach by default only works well when the linux kernel maps to a continous physical memory address block. If there are holes presented in the kernel physical memory address, Lauterbach might 


## Linux Awareness

Awareness means the debugger need to be aware the existence of the Linux Kernel. To enable this, the Linux has to be compiled with certain configuration.

https://www2.lauterbach.com/pdf/training_rtos_linux.pdf see kernel configuration.

### Linux Kernel Requirement

Below is the summary of the Lauterbach manual on Linux kernel configuration.

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

> The Linux kernel CPU power management could cause for some processor architectures that single cores are not accessible by the debugger when in power saving state. CPU power management can be disabled in the Linux kernel configuration by disabling the options `CONFIG_CPU_IDLE` and` CONFIG_CPU_FREQ`.Idle states can also be disabled for single cores from the shell by writing to the file `/sys/devices/system/cpu/cpu<x>/cpuidle/state<x>/disable`. 

> Alternatively, you may remove the idle-states property from the device tree if available.On some Linux distributions, power management can be disabled using specific kernel command line parameters (e.g. “`jtag=on`” or “`nohlt`”). Please refer to the documentation of the kernel command line parameters of your Linux distribution for more information. 

So do something like
```
echo 1 | tee $(ls /sys/devices/system/cpu/cpu?/cpuidle/state?/disable)
```
On zcu quad core dev board, this should write to 8 files in total (each CPU has 2 idle states: state0 and state1).


