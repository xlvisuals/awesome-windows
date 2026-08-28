## How to upgrade Windows 10 IoT Enterprise (GAC) to Windows 11 IoT Enterprise LTSC:

If you are dealing with custom, legacy, or enterprise apps that cannot be pulled down from a public repository, losing them during a setup routine is a major headache.

There is some good news: **You _can_ keep your apps during this specific cross-channel upgrade**, provided you execute the registry override method correctly.

While standard Microsoft documentation claims cross-channel upgrades (GAC to LTSC) block application retention, field-tested deployment methods allow apps to carry over if the internal build architectures match closely enough.

### How to Force the Upgrade and Keep Your Custom Apps

1.  **Take a Full Backup First:** Before touching the registry or running setup, take a full system backup (using a tool like Macrium Reflect or Clonezilla). If something goes sideways, you can restore to your exact current state.
    
2.  **Mount the ISO:** Download and mount the official **Windows 11 IoT Enterprise LTSC 2024 ISO** by double-clicking it in File Explorer.
    
3.  **Apply the Registry Override:**
    
    *   Open **Command Prompt as Administrator**.
      
    *   Run this command to trick the system into matching the LTSC architecture:
        
        DOS
        
            reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /v EditionID /d IoTEnterpriseS /f
        
4.  **Launch Setup Immediately:**
    
    *   Open the mounted ISO drive in File Explorer and double-click **`setup.exe`**.
        
    *   _Crucial:_ Do not wait after running the command, or Windows will overwrite the registry key back to default.
        
5.  **Check the Prompts:**
    
    *   Proceed through the initial setup screens. When you reach the critical decision screen, look closely at what it allows you to keep.
        
    *   Under standard circumstances with this override, **"Keep personal files and apps"** should remain un-greyed and selectable. Select it.
        
6.  **Complete and Activate:** Let the upgrade finish. Once you land on the desktop, input your **Windows 11 IoT Enterprise LTSC 2024 license key** under Activation settings to finalize the transition.


### A Word of Caution for Custom Apps

Because these are custom/legacy/enterprise apps, test this process on a non-production test machine first if possible. 

While registry-forced upgrades usually migrate program files successfully, custom apps that rely heavily on specific Windows system hooks or low-level servicing filters should always be verified for functionality post-upgrade.

