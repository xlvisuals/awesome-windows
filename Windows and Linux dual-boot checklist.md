## Windows and Linux dual-boot checklist

Checklist and troubleshooting help for dual-booting Windows 11 and Linux on a **single-drive laptop**.

### Phase 1: Pre-Installation & Security Settings

*   **Disable Secure Boot:** Turn this off in your BIOS/UEFI settings. It prevents Windows updates or future system changes from breaking custom or third-party Linux drivers and eliminates a major source of silent boot failures.
    
### Phase 2: Partitioning & Single-Drive Management

*   **Back Up Your Data:** Always back up important personal files to an external drive or cloud storage _before_ tweaking partition tables on your only drive.

*   **Shrink the Windows Partition:** Use _Windows Disk Management_, _KDE Partition Manager__ (or a tool like Minitool Partition Wizard or GParted from a Live USB) to shrink your main OS partition and leave a block of "Unallocated Space" for the Linux or Windows partition.
    
*   **Share the Existing EFI Partition:** Do not try to create a brand-new EFI partition for Linux on a single-drive laptop. Install GRUB directly into the existing Windows EFI system partition (ESP), ensuring there is enough free space (usually 100MB–500MB is plenty).
    
*   **Map Your Partitions First:** Note down your partition layout (e.g., which partition is your Windows drive vs. recovery) so you don't accidentally select the wrong space during the Linux installation.
    

### Phase 3: Post-Installation

*   **Reconfigure the Bootloader & Order:**
    
    *   If Linux was pre-installed, or if Windows takes over upon finishing, use a live USB tool (like the Ubuntu Boot-Repair ISO) to reinstall GRUB.
        
    *   Change your boot order back in the BIOS/UEFI settings because Windows aggressively forces itself to the top priority position.
        
*   **Fix Time Drift (UTC vs. Local Time):** Windows tracks the hardware clock as Local Time, while Linux tracks it as UTC. Fix the resulting few-hour time shift between reboots by forcing Windows to use UTC via a registry entry, or setting Linux to use Local Time.
    

### Kubuntu-Specific Tips

*   **The "Something Else" Partitioning Menu:** When the Kubuntu installer asks how you want to install, choose **Manual partitioning** (often labeled _Something Else_). This ensures you explicitly point it to the **Unallocated Space** you carved out in Windows and prevents it from accidentally touching your Windows C: drive partition.
    
*   **Reusing the EFI Partition:** In that manual menu, when you select the existing Windows EFI partition (the small FAT32 partition usually around 100MB–260MB), set its mount point to `/boot/efi` (or just select it as the EFI boot partition) **without formatting it**. Formatting it would wipe your Windows bootloader, but leaving it unformatted allows Kubuntu's GRUB to live right alongside Windows peacefully.
    
*   **KDE Plasma and Time Drift:** If you notice your system clock is off by a few hours after switching between Windows and Kubuntu, you can easily fix it right from the Kubuntu system tray by right-clicking the clock, going to _Adjust Date & Time_, and checking the box to use UTC for the hardware clock (and applying the registry fix in Windows that we mentioned earlier).


### Windows-Specific Tips

During Windows setup, choose the following options when they are presented

*	**"Activate Windows"** - choose "I don't have a product key", the product key can be entered after installation.

*	**"Which type of installation do you want?"** - choose "Custom: Install Windows only (advanced)".

*	**"Where do you want to install Windows?"** - choose the unallocated space prepared earlier.

*   **Disable "Fast Startup":** Turn this off in Windows Power Options. If left on, Windows places the drive and hardware (like your Wi-Fi card) into a hybrid hibernation state, making them unavailable or read-only when you boot into Linux.
    
*   **Disable BitLocker:** Ensure device encryption/BitLocker is completely disabled in Windows. This avoids sudden lockout screens and 48-digit recovery key demands when you modify partition layouts or when Windows applies routine updates.
   
*   **Watch Out for Windows Feature Updates:** Major Windows updates can occasionally overwrite the EFI boot manager and hide GRUB. Keep a bootable Linux live USB handy just in case you ever need to quickly restore your bootloader.
    
