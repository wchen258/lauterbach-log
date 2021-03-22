## Requirement

### Hardware
You need corresponding analyzer hardware for this in addition to the PowerDebugger PRO. As in our lab, we are using PowerTrace-II Autofocus-II. 

> Use VERSION.HARDWARE to check your Luaterbach hardware info.

### Connection

For PowerTrace-II Autofocus-II, it provides Mictor-38, which would communicate with the board via EMIO after setting up the programming logic correctly. If you are using other analyzer (perhaps MIPI-60 connection?), take a look at [Lauterbach doc on ZYNQ trace](https://www2.lauterbach.com/pdf/app_xilinx_zynq.pdf).

Mictor-38 should connect to P6, the EMIO Arm Trace Port (P6 on the callout diagram). J6, ARM JTAG connector, connected as before. In addition to that J14 (Arm Debug VTREF), J38 (Arm Trace Power), and J88 (Arm Trace VTREF) should all be shorted (connected). All these information are available in the comment of each example script Lauterbach provided. The comments in Lauterbach example scripts are very useful.

Of course, the analyzer should also connected with the debugger, and there is only one way to connect these two side-by-side.

### Run the script

Now put the board in JTAG bootmode, and simply run any of the scripts with `offchip_trace`, it should workd! You can click the trace->configuration to see, the option is on the analyzer now, and the buffer size is much larger than those on-chip.

It's interesting to see the example script in fact loads a bitstream file. It's highly possible, the bistream is to set up the EMIO so that the ETM trace interface and export the trace data to the analyzer as Lauterbach describes in their documentations. 
