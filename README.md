# lauterbah-log

A tutorial on how to set up Lauterbach for Xilinx ZYNQ Ultrascale+ MPSoC. ZCU102 is used in this documentation.

This tutorial covers **normal debug** and **trace with analyzer**. The board might run a standalone (bare-metal) application without an operation, or it might run an embedded linux. So this gives four situations.

## Current status
situation | status
----------| ------------------------
normal debug + standalone | success
normal debug + embedded linux | success
trace with analyzer + standalone | success on demo
trace with analyzer + embedded linux | success 

## Trace

In our project, the hardware for normal debug is PowerDebug PRO, and for trace with analyzer is PowerTrace-II AutoFocus-II. Even if no trace analyzer presents, the PowerDebug PRO can still perform trace. This type of trace is referred as **On-Chip trace**. Because the trace information generated by Embedded Trace Macrocells (ETM) is stored in the on-chip memory. ETB, ETF, ETR referred in some literatures are all On-Chip trace. Due to the limited size of the on-chip memory, the buffer would be filled up in no time, i.e. the trace can only record the information in a short period of time. 

When using an analyzer, the trace information can be exported via the equipment, thus a much larger buffer. This is referred as **Off-Chip trace**. Trace-port interface units (TPIU) on board is used in this case. To do so, the hardware design has to be configured accordingly. 

Read more from [Lauterbach manual](https://www2.lauterbach.com/pdf/training_arm_etm.pdf) 

> HINT: In PowerTrace32 GUI, use VERSION.HARDWARE and VERSION.HARDWARE2 to check your Lauterbach devices.
