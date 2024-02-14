# Class 101.1 Part 1 - Hardware configuration

## Glossary

**BIOS** => Basic Input Output System   
**UEFI** => Unified Extensible Firmware Interface   
**PCI** => Peripheral Component Interconnect   
**USB** => Universal Serial Bus

<br>

## Commands

`lspci` => Shows all equipment connected to the PCI bus.    
`lsusb` => Shows all equipment connected to the USB.   
`lsmod` => Shows the modules loaded by the system.   

<br>

```shell
lspci
0000:00:00.0 Host bridge: Intel Corporation 12th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
0000:00:01.0 PCI bridge: Intel Corporation 12th Gen Core Processor PCI Express x16 Controller #1 (rev 02)
0000:00:02.0 VGA compatible controller: Intel Corporation Alder Lake-P GT1 [UHD Graphics] (rev 0c)
0000:00:04.0 Signal processing controller: Intel Corporation Alder Lake Innovation Platform Framework Processor Participant (rev 02)
0000:00:06.0 System peripheral: Intel Corporation RST VMD Managed Controller
0000:00:07.0 PCI bridge: Intel Corporation Alder Lake-P Thunderbolt 4 PCI Express Root Port #0 (rev 02)
```

`0000:00:02.0` => The first numbers are hexadecimal addresses of the device.   

<br>

```shell
lspci -s 0000:00:02.0 -v
0000:00:02.0 VGA compatible controller: Intel Corporation Alder Lake-P GT1 [UHD Graphics] (rev 0c) (prog-if 00 [VGA controller])
	DeviceName: Onboard - Video
	Subsystem: ASUSTeK Computer Inc. Alder Lake-P GT1 [UHD Graphics]
	Flags: bus master, fast devsel, latency 0, IRQ 191, IOMMU group 0
	Memory at 612e000000 (64-bit, non-prefetchable) [size=16M]
	Memory at 4000000000 (64-bit, prefetchable) [size=256M]
	I/O ports at 5000 [size=64]
	Expansion ROM at 000c0000 [virtual] [disabled] [size=128K]
	Capabilities: [40] Vendor Specific Information: Len=0c <?>
	Capabilities: [70] Express Root Complex Integrated Endpoint, MSI 00
	Capabilities: [ac] MSI: Enable+ Count=1/1 Maskable+ 64bit-
	Capabilities: [d0] Power Management version 2
	Capabilities: [100] Process Address Space ID (PASID)
	Capabilities: [200] Address Translation Service (ATS)
	Capabilities: [300] Page Request Interface (PRI)
	Capabilities: [320] Single Root I/O Virtualization (SR-IOV)
	Kernel driver in use: i915
	Kernel modules: i915
```

`Kernel driver in use: i915` => Kernel module used by the device.   

<br>

```shell
lspci -s 0000:01:00.0 -k
0000:01:00.0 VGA compatible controller: NVIDIA Corporation GA107M [GeForce RTX 3050 Mobile] (rev a1)
	Subsystem: ASUSTeK Computer Inc. GA107M [GeForce RTX 3050 Mobile]
	Kernel driver in use: nvidia
	Kernel modules: nvidiafb, nouveau, nvidia_drm, nvidia
```

`lspci -s 0000:01:00.0 -k` => The *-k* option shows the module used by device.   
`Kernel modules: nvidiafb, nouveau, nvidia_drm, nvidia` => Other modules associated with the device.   

<br>

```shell
lsusb
Bus 004 Device 002: ID 0bda:0329 Realtek Semiconductor Corp. USB3.0 Card Reader
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 003: ID 3277:0021 Sonix Technology Co., Ltd. USB2.0 FHD UVC WebCam
Bus 003 Device 015: ID 2808:a658 Realtek USB2.0 Finger Print Bridge FocalTech Fingerprint Device
Bus 003 Device 004: ID 8087:0033 Intel Corp. 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

`lsusb -v -d 2808:a658` => Shows device data in detail. Use the *-d* option for identify the device.   

`lsusb -t` => Shows devices in a tree format.   
```shell
lsusb -t
/:  Bus 04.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 10000M
    |__ Port 2: Dev 2, If 0, Class=Mass Storage, Driver=usb-storage, 5000M
/:  Bus 03.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/12p, 480M
    |__ Port 5: Dev 15, If 0, Class=Vendor Specific Class, Driver=, 480M
    |__ Port 8: Dev 3, If 0, Class=Video, Driver=uvcvideo, 480M
    |__ Port 8: Dev 3, If 1, Class=Video, Driver=uvcvideo, 480M
    |__ Port 10: Dev 4, If 0, Class=Wireless, Driver=btusb, 12M
    |__ Port 10: Dev 4, If 1, Class=Wireless, Driver=btusb, 12M
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/2p, 20000M/x2
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/1p, 480M
```
`Driver=xhci_hcd/1p` => Module used by device.   
`Class=Wireless` => Device Class.    

```shell
lsusb -s 03.3
Bus 003 Device 003: ID 3277:0021 Sonix Technology Co., Ltd. USB2.0 FHD UVC WebCam
```
`lsusb -s 03.3` => Show only devices with specified device and/or bus numbers (in decimal). Use the format [[bus]:][devnum].

<br>

```shell
lsmod
Module                  Size  Used by
ccm                    20480  6
vboxnetflt             36864  0
vboxdrv               741376  2 vboxnetadp,vboxnetflt
snd_ctl_led            24576  0
snd_soc_skl_hda_dsp    24576  4
snd_soc_hdac_hdmi      45056  1 snd_soc_skl_hda_dsp
algif_skcipher         12288  1
af_alg                 32768  6 algif_hash,algif_skcipher
snd_hda_codec_realtek   192512  1
snd_hda_codec_generic   122880  1 snd_hda_codec_realtek
```

`Module` => Name of module.   
`Size`=> Amount of RAM, in bytes, used by the module.   
`Used by` => Dependent modules.

`modprobe -r snd` => The *-r* option unloads a module.   
`modinfo nvidia` => Shows information about a module.  

`/etc/modprobe.d/` => Module configuration directory.
`/etc/modprobe.d/blacklist.conf` => Doesn't load the module listed in this file.   

