This is more involved compared with other debug techniques. I am still trying to get it working. Notice you need the corresponding hardware for that. In our lab, we are using PowerTrace II autofocus II.

Since Lauterbach does not provide any scripts for this (they provide many related example and a document specific for this purpose), I propose the following general directions:

1. The ZYNQ board is somehow different from others while using the analyzer. Lauterbach dedicates a [document specifically for this purpose](https://www2.lauterbach.com/pdf/app_xilinx_zynq.pdf). 
2. Based on their description, it's recommanded to use EMIO and export the trace interface via the PL (this would take some PL resources but the throughput is 1000MB/s which is recommended by Lauterbach).
3. Indeed, in their example offchip trace example scripts, they all come in with a bitstream file to make the offchip working. This behavior is in agreement with their document.
4. In addition, Xilinx also provides an [example design](https://www.xilinx.com/support/answers/66669.html). This is also in agreement with the Lauterbach doc.

So 

1. try to use the Xilinx design exmaple to see whether you can use the analyzer to trace a bare-metal application you compiled. (since the example provided by Lauterbach is clearly working, we should try to reproduce what they have right now)
2. then use the xra (or hdf file) to compile a linux kernel to see whether it would open the trace for analyzer automatically.
