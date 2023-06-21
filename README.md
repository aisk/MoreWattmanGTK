# MoreWattmanGTK

This is a fork of WattmanGTK with a few changes.

This is a Python3 program which uses a simple GTK gui to view, monitor and in the future overclock a Radeon GPU on Linux. 
![Main screen](https://i.imgur.com/ahrQrEO.png)
## What can it do?
 * View memory and GPU P-states including voltages.
 * Ability to monitor signals from GPU sensors by means of plotting
 * Write a bash file with overclock settings
 * Multi GPU support in top dropdown list
## What can't it do?
 * ~~Directly apply values from GUI (this will be a future addition)~~ --Added
 * Fan control (this will be a future addition)
 * Monitor multiple GPU's

## Hardware Requirements

* A Radeon card which uses the AMDGPU kernel driver

## OS Requirements

* Linux kernel 4.8+ (Ubuntu 16.10 or newer)
* The overdrive kernel parameter must be set.
* Python3 (3.6+)

## To Run

```
    pip install pygobject matplotlib pycairo
```

```
    python3 run.py
```

## Contributing & Donations
Contributions can be made in terms of:
 ## FAQ
 ### How do I know my card has the overdrive bit enabled
 **Just try to run WattmanGTK.**
 It will tell you if your card does not 
 support overdrive. Even if this is not the case you can set a kernel 
 parameter to force overdrive to be enabled (may not work on all cards).
 For more information on how to set the parameter check the [Arch Wiki](https://wiki.archlinux.org/index.php/kernel_parameters)

 For GRUB based systems (like ubuntu): edit the /etc/default/grub file and edit the line:
```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```
And change it to:
```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amdgpu.ppfeaturemask=<the suggested value by WattmanGTK>"
```
Then grub needs to be updated, for ubuntu this is done by running
```
    sudo update-grub
```
For distro agnostic updating this can be done by running

on BIOS systems: ```# grub2-mkconfig -o /etc/grub2.cfg```

on UEFI systems: ```# grub2-mkconfig -o /etc/grub2-efi.cfg```

Then reboot the machine. Once rebooted you can check the current featuremask by 
```
   printf "0x%08x\n" $(cat /sys/module/amdgpu/parameters/ppfeaturemask)
```
 ### Setting the kernel parameter causes artifacts and glitching
 It could be that setting the kernelparameter can enable features that 
 should not be enabled which could be the cause.
 
 ### The program can not find a certain senor path and fails
Please refer to: https://github.com/BoukeHaarsma23/WattmanGTK/issues/1

