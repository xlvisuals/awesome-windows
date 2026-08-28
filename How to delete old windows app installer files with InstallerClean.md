# InstallerClean Guide: Cleaning Orphaned MSI/MSP Files

This guide covers how to reclaim disk space from the `C:\Windows\Installer` folder using **InstallerClean** (from `no-faff`), which targets orphaned installer files left behind by third-party applications.

---

## Overview

Every time you install, update, or patch third-party desktop applications (such as Microsoft Office, Adobe Creative Cloud, games, and various utilities), Windows stores the original `.msi` or `.msp` installer files in a hidden system directory: `C:\Windows\Installer`. 

Over the years, as programs are uninstalled or updated, many of these files become **orphaned**—no longer tied to any active program on your system. Windows rarely cleans this folder automatically, causing it to bloat to massive sizes (often 10GB to 50GB+).

`InstallerClean` safely queries the Windows Installer database to distinguish between active installer files and dead/orphaned files, allowing you to reclaim that lost space.


## Important Distinction: InstallerClean vs. DISM

* **InstallerClean (`C:\Windows\Installer`):** Cleans cached installation files for **third-party desktop apps and programs**.
* **DISM (`WinSxS` folder):** Cleans up **core Windows operating system updates and system files**. 

   ```cmd
   DISM.exe /Online /Cleanup-Image /StartComponentCleanup /ResetBase
   ```

Using both tools provides a thorough cleanup of both types of installer clutter.


## How to Use InstallerClean Safely

1. **Get the Tool**
   * Download the utility from the official repository: [github.com/no-faff/InstallerClean](https://github.com/no-faff/InstallerClean)

2. **Run as Administrator**
   * Because `C:\Windows\Installer` is a protected system directory, you must run the tool with administrative privileges.

3. **Scan and Review**
   * Run the tool to analyze the directory. It will cross-reference files against the Windows Installer database to identify safe-to-delete orphaned files.
   * Review the scan results before confirming deletion.

4. **Clean**
   * Proceed with deleting the confirmed orphaned files to recover disk space.


## Safety Precautions

* **Do not manually delete files** from `C:\\Windows\\Installer` using File Explorer. Deleting active `.msi` files manually will break your ability to uninstall, repair, or update those applications later.
* Always rely on specialized utilities like `InstallerClean` that verify the Windows Installer database state before removing anything.


