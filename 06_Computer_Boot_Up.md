**Step-by-Step Process of What Happens When You Turn On a Computer**

### 1. Powering On the Computer

When you press the power button on your computer, the power supply unit (PSU) begins delivering electrical current to all essential components of the system. This initiates the startup process and effectively powers up the computer.

### 2. CPU Initialization and Locating BIOS/UEFI

After receiving power, the CPU initializes itself by setting up its internal state so that it can perform further tasks.

Next, the CPU looks for firmware stored on a dedicated chip on the motherboard. This firmware is typically known as the BIOS (Basic Input Output System), which resides in a ROM (Read-Only Memory) chip. The BIOS contains low-level software that helps initialize and manage communication with hardware.

Modern computers often use UEFI (Unified Extensible Firmware Interface) instead of traditional BIOS. UEFI is more advanced and flexible, providing additional features such as graphical interfaces, better security, and larger disk support.

### 3. Running BIOS/UEFI and Performing POST

The CPU begins executing the code found in the BIOS/UEFI. The primary task performed here is the Power-On Self-Test (POST).

During POST, the system checks the health and presence of essential hardware components:

* Ensures RAM is present and functional
* Verifies CPU and motherboard components
* Detects and checks storage drives
* Tests keyboard, mouse, and other peripherals

If any critical hardware is missing or faulty (e.g., RAM failure), the BIOS either displays an error message or produces a series of beep codes. In such cases, the boot process halts until the issue is resolved.

UEFI can act almost like a mini-operating system and offers more capabilities, such as network-based diagnostics and remote management features (e.g., Intel Management Engine in Intel CPUs).

### 4. BIOS/UEFI Hands Off Control to Bootloader

Once POST is successfully completed, BIOS or UEFI transfers control to the bootloader.

The bootloader is a small program stored at the beginning of a storage device. The BIOS checks for the MBR (Master Boot Record), which contains the bootloader code. In UEFI systems, it looks for the EFI system partition.

The bootloader is responsible for continuing the booting process by locating and loading the operating system.

### 5. Bootloader Loads the Operating System

The bootloader's job is to start the operating system by loading its kernel (the core part of the OS).

Once the kernel is loaded, it initializes the rest of the system — including user-space applications and background services.

Examples of bootloaders include:

* **Windows:** Windows Boot Manager (Bootmgr.exe)
* **Linux:** GRUB (Grand Unified Bootloader)
* **Mac:** boot.efi

### Summary

* Computer is powered on.
* CPU initializes and locates BIOS or UEFI firmware.
* BIOS/UEFI performs hardware checks using POST.
* If no issues are found, control is handed to the bootloader.
* The bootloader loads the operating system kernel and completes the boot process.

This entire chain of steps allows your computer to go from a powered-off state to a fully functional operating system ready for user interaction.

---