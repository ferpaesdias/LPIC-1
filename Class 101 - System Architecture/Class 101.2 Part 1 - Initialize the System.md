# Initialize the System

<br>

## Boot order

1. BIOS/MBR or UEFI
2. Boot Manager - GRUB2
3. Kernel
4. Init (runlevel)
5. DM
6. DE

<br>

## BIOS (MBR) / UEFI

**BIOS** => Basic Input/Output System   
**MBR** => Master Boot Record    
**UEFI** => Unified Extensible Firmware Interface    

**BIOS** is the program (firmware) stored on a non-volatile memory chip connected to the motherboard. The **BIOS** assumes that the first 440 bytes on the first storage device are the first stage of the bootloader (also called the *bootstrap*). The first 512 bytes of a storage device are what is called the **MBR** (Master Boot Record) of storage devices that use the standard DOS partition scheme, and in addition to the first stage of the boot loader, they contain the partition table . If the **MBR** does not contain the correct data, the system will not be able to boot unless an alternative method is employed.

<br>

The pre-operational steps to boot a **BIOS**-equipped system are:

1. The **POST (power-on self-test)** process is executed to identify simple hardware failures as soon as the machine is powered on.
2. The **BIOS** activates the basic system components, such as the video output, keyboard, and storage media.
3. The **BIOS** loads the first stage of the bootloader from the **MBR** (the first 440 bytes of the first device as defined in the **BIOS** setup utility).
4. The first stage of the bootloader calls the second stage, which is responsible for presenting boot options and loading the kernel.

<br>

Like BIOS, **UEFI** is also firmware, but it can identify partitions and read many file systems on them. **UEFI** does not depend on MBR, only taking into account settings stored in non-volatile memory (**NVRAM**) connected to the motherboard. These settings indicate the location of **UEFI**-compatible programs, called **EFI** applications, that will run automatically or be called from a boot menu. **EFI** applications can be boot loaders, operating system selectors, tools for system diagnosis and repair, etc.
The partition that contains **EFI** applications is called the **EFI** System Partition or just **ESP**. This partition should not be shared with other file systems on the system, such as the root file system or user data file systems. The **EFI** directory on the **ESP** partition contains the applications pointed to by entries saved in **NVRAM**.



In general, the pre-operating system boot steps on a **UEFI** system are:   

1. The **POST (power-on self-test)** process is executed to identify simple hardware failures as soon as the machine is powered on.
2. The **UEFI** activates the basic system components, such as the video output, keyboard, and storage media.
3. The **UEFI** firmware reads definitions stored in **NVRAM** to run the predefined EFI application stored in the ESP partition's systems file. Typically, the default EFI application is a bootloader.
4. If the default EFI application is a bootloader, it loads the kernel to boot the operating system.

The **UEFI** standard also supports a feature called Secure Boot, which only allows signed EFI applications to run, that is, EFI applications authorized by the hardware manufacturer. This feature increases protection against malicious software, but may make it difficult to install operating systems not covered by the manufacturer's warranty.

<br>

## Bootloader

**GRUB (Grand Unified Bootloader)** is the most popular bootloader for Linux (x86). As it is called by BIOS or UEFI, GRUB shows a list of operating systems available to boot.

Sometimes the list does not appear automatically, but can be invoked by pressing `Shift` while the system is being called by the BIOS. On UEFI systems, the key to use is `Esc`.
