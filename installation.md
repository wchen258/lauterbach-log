## Installation on pc_linux64

Most of the instructions are provided within the installation package.
1. Unzip the downloaded file
2. run setup_linux.sh
3. follow and prompts and install the USB-driver related files along the way.
4. When the installation is done. Use the following commands to start the PowerView
```
/home/zcu1023/t32/bin/pc_linux64/t32marm64 -c "/home/zcu1023/t32/config_usb.t32"
/home/zcu1023/t32/bin/pc_linux64/t32mppc -c "/home/zcu1023/t32/config_sim.t32"
```
The first command starts ARM 64bit Debugger. If the LauterBach USB cable is not connect with PC, it would trigger an error.
The second command starts the simulator.

More examples on config files are as below
```
#     To start TRACE32 you will find 4 example configuration files in the
#     installation directory:
#     - config.t32          explaining general config-file syntax.
#     - config_usb.t32      example to start USB-Debugger configurations
#     - config_eth.t32      example to start Ethernet-Debugger configurations
#                           (adapt the debugger IP-address inside!)
#     - config_hostmci.t32  example to start HostMCI configurations
#     - config_sim.t32      example to start Simulator configurations
#
#     Please note: Installed udev rules require a system reboot or
#                  'udevadm control --reload-rules' / similar command

```
