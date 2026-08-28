# Windows Update Cleanup Guide: DISM & ResetBase
    
This guide covers how to reclaim significant disk space on Windows by cleaning up the Component Store (`WinSxS` folder) and making current system updates permanent using the **DISM** (Deployment Image Servicing and Management) command-line tool.



## Overview

Over time, Windows accumulates superseded versions of system files and updates in the `WinSxS` folder. While this allows you to safely uninstall individual updates if something goes wrong, it consumes massive amounts of disk space. 

By running the `StartComponentCleanup` command with the `/ResetBase` switch, you prune these older files and permanently lock in your current update state, freeing up valuable storage.



## Prerequisites

* **Administrator Privileges:** You must run the Command Prompt or Windows Terminal with administrator rights.
* **Understanding the Trade-off:** Once `/ResetBase` is applied, **you will no longer be able to uninstall previous individual Windows updates**. Only proceed if your system is stable and working correctly.



## Step-by-Step Instructions

1. **Open Command Prompt as Administrator**
   * Press the `Windows Key`, type `cmd`.
   * Right-click on **Command Prompt** and select **Run as administrator**.

2. **Run the Cleanup Command**
   Copy and paste the following command into the prompt and press **Enter**:

   ```cmd
   DISM.exe /Online /Cleanup-Image /StartComponentCleanup /ResetBase
   ```
   
3.  **Wait for Completion**
    
    *   The process will take several minutes depending on your storage speed and the number of old update files.
        
    *   Do not close the window or interrupt the process until it reaches **100%** and confirms successful completion.
        

Summary of Switches Used
------------------------

*   `/Online`: Targets the currently running operating system.
    
*   `/Cleanup-Image`: Manages and repairs the Windows image.
    
*   `/StartComponentCleanup`: Cleans up superseded components and reduces the size of the WinSxS directory.
    
*   `/ResetBase`: Removes all base backups of superseded components, making the current update state permanent and maximizing disk space recovery. """
    

