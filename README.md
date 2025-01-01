Create a Vivado project
=======================

There are two ways to create a Vivado project

1. open xc7z015clg485-2.xpr
2. create a new project, add a ip: zynq7, and apply configuration of `zynq7.tcl`

Build PetaLinux
================

Remember to change the correct directory of the mount point and Xilinx tools.

```bash
source ~/tools/Xilinx/PetaLinux/settings.sh 
source ~/tools/Xilinx/Vivado/2024.2/settings64.sh 
petalinux-create project -n peta --template zynq
cd peta
petalinux-config --get-hw-description ../design_1_wrapper.xsa
petalinux-build
petalinux-package boot --fsbl images/linux/zynq_fsbl.elf --fpga --u-boot --force
rm -v /media/${USER}/boot/BOOT.BIN /media/${USER}/boot/image.ub /media/${USER}/boot/boot.scr
cp -v images/linux/BOOT.BIN images/linux/image.ub images/linux/boot.scr /media/${USER}/boot/
```
