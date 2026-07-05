## Windows 11 IoT Enterprise LTSC 24H2 for older hardware

Windows 11 IoT Enterprise LTSC 24H2 functions identically to Windows 11 Home and Pro in terms of interface and core usability. But unlike Home and Pro, it offers full flexibility in deployment environments, supporting older, embedded, or specialised hardware without enforcing modern hardware requirements such as TPM and Secure Boot.

Windows 11 IoT Enterprise LTSC was designed for secure and low-maintenance systems such as industrial PCs, ATMs, and privacy-focused users. 

While it was not originally intended for general consumer use, it is well suited for professional work and gaming alike and is very popular among advanced users due to its minimalism and control.

### Key Features

- Does not include Copilot, Recall, or other AI/cloud-driven features found in consumer editions
- No Microsoft Account required — allows full local account setup by default
- No pre-installed consumer apps or bloatware
- Optional Secure boot, BitLocker, Hyper-V, domain join
- Lightweight and resource-efficient
- Locked-down update cycle (security updates only, no feature updates)
- Built-in ability to disable telemetry (recommended)
- Built-in ability to disable Windows Defender (not recommended)
- 10 year support for security updated until 10 Oct 2034
- Full Group Policy and Registry customization


### Hardware requirements

- Processor: 1GHz (2 Cores)
- Memory: 4GB
- Storage: 64GB
- Storage type: SSD, HDD, SSHD, eMMC, SD, USB
- Firmware: UEFI or BIOS
- TPM: Not required
- Secure Boot: Not required


### Install and activate Windows 11 IoT Enterprise LTSC 24H2

#### 1. Download the Windows 11 IoT Enterprise LTSC .iso image

Directly from Microsoft:

- [X23-81951\_26100.1742.240906-0331.ge\_release\_svc\_refresh\_CLIENT\_ENTERPRISES\_OEM\_x64FRE\_en-us.iso](https://oemsoc.download.prss.microsoft.com/dbazure/X23-81951_26100.1742.240906-0331.ge_release_svc_refresh_CLIENT_ENTERPRISES_OEM_x64FRE_en-us.iso_640de540-87c4-427f-be87-e6d53a3a60b4?t=2c3b664b-b119-4088-9db1-ccff72c6d22e&P1=102816950270&P2=601&P3=2&P4=OC448onxqdmdUsBUApAiE8pj1FZ%2BEPTU3%2BC6Quq29MVwMyyDUtR%2Fsbiy7RdVoZOHaZRndvzeOOnIwJZ2x3%2BmP6YK9cjJSP41Lvs0SulF4SVyL5C0DdDmiWqh2QW%2BcDPj2Xp%2BMrI9NOeElSBS5kkOWP8Eiyf2VkkQFM3g5vIk3HJVvu5sWo6pFKpFv4lML%2BHaIiTSuwbPMs5xwEQTfScuTKfigNlUZPdHRMp1B3uKLgIA3r0IbRpZgHYMXEwXQ%2FSLMdDNQthpqQvz1PThVkx7ObD55CXgt0GNSAWRfjdURWb8ywWk1gT7ozAgpP%2FKNm56U5nh33WZSuMZIuO1SBM2vw%3D%3D)

  - Note: the file might end with .iso\_640de540-87c4-427f-be87-e6d53a3a60b4 instead of .iso
  - Just rename the ending to .iso

The Massgrave website has published the download links from the official Microsoft servers:

- [https://massgrave.dev/windows\_ltsc\_links](https://massgrave.dev/windows_ltsc_links)

A copy is also available to download from Archive.org:

- [https://archive.org/details/Windows11LTSC](https://archive.org/details/Windows11LTSC)

#### 2. Burn ISO to USB

- Burn the downloaded .iso file to a USB stick or memory card with [Rufus](https://rufus.ie/en/).
  - Alternatively, you can prepare a USB stick or memory card with [Ventoy](https://www.ventoy.net/en/index.html) and then just copy the .iso file on it.

#### 3. Boot from USB and install

- Insert the USB Stick and turn on or restart your computer.
- You can turn off secure boot and TMP in your PC BIOS, the LTSC version of Windows 11 doesn't need it.
- Follow on-screen instructions to install Windows 11 IoT Enterprise LTSC

#### 4. Activate Windows

If you are in an organizational/corporate environment, your company likely uses a KMS host to activate machines automatically.

If you have a Multiple Activation Key (MAK) from your Visual Studio Subscription (formerly MSDN), Volume Licensing Service Center (VLSC), or Microsoft Microsoft 365 Admin Center, you can activate it directly via the Settings app or the command line.

For alternative activation methods see [https://massgrave.dev/](https://massgrave.dev/) for details, and follow "Method 1: PowerShell (Recommended)".

- Click the Start button (Windows logo).
- Search for **PowerShell** in the Start menu, right-click it, and select "**Run as administrator**."
- Copy and paste this command and hit enter:
```powershell
    irm \[[https://get.activated.win](https://get.activated.win/)\]([https://get.activated.win/](https://get.activated.win/)) | iex
```


### Configure Windows 11 IoT Enterprise LTSC 24H2

#### 1. Restore the full Explorer context menu

Windows 11 has hidden many useful context items in a 2nd window (e.g. delete, properties). But you can restore the classic context menu behaviour with a single command:

- Click the Start button (Windows logo).
- Search for **cmd** in the Start menu, right-click it, and select "**Run as administrator**."
- Copy and paste this command and hit enter:
```cmd
    reg.exe add "HKCU\\\\Software\\\\Classes\\\\CLSID\\\\\\\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2\\\}\\\\InprocServer32" /f /ve
```
- In the menu that appears, press 1 for "HWID".
- Then press the number corresponding to "Activate Windows".

#### 2. Disable Windows 11 Memory Integrity on Intel 6th Gen & older

Windows 11 includes two additional security layers to prevent malware from injecting code into high-priority processes. These are called **Virtualization-Based Security (VBS)** and **Hypervisor-protected Code Integrity (HVCI)**.

- These features are only fully supported by Intel Kaby Lake (7th Gen, iX-7xxx) and AMD Zen 2 (Ryzen 3000) and newer
- Older CPUs like Intel Skylake (6th Gen, iX-6xxx) and AMDs Zen1, Zen+ (Ryzen 2000) lack the necessary instruction sets (MBEC and GMET)
- Without these, Windows must emulate the instructions in software, which comes with a performance drop of 10% to 30%.
  - This is noticeable in system responsiveness, especially gaming and photo and video editing.
- Disabling VBS and HVCI removes this emulation overhead, making a Windows 11 installation on older systems feel significantly faster and more like Windows 10.

  
**Disable VBS and HVCI**

- Click the Start button (Windows logo).
- Search for **cmd** in the Start menu, right-click it, and select "**Run as administrator**."
- Paste this command and hit enter:
```cmd
    reg add "HKLM\\SYSTEM\\CurrentControlSet\\Control\\DeviceGuard\\Scenarios\\HypervisorEnforcedCodeIntegrity" /v "Enabled" /t REG\_DWORD /d 0 /f
```
- The setting will take effect after you restart Windows


**Uninstall Virtual Machine Platform and Windows Hypervisor Platform**

To ensure the VBS/HVCI stack is fully unloaded, you can disable the underlying virtualization platform.

- Click the Start button (Windows logo).
- Search for **optionalfeatures.exe** in the Start menu, click-it.
- Uncheck *Virtual Machine Platform* and *Windows Hypervisor Platform*.


#### 3. Remove remaining bloat and telemetry settings

Although Windows 11 IoT Enterprise LTSC comes with a lot less clutter, bloat and telemetry than the regular Windows 11 Pro, it still can be much improved. **Win11Debloat** is a lightweight, easy to use PowerShell script that allows you to quickly declutter and customize your Windows experience

- [https://github.com/Raphire/Win11Debloat](https://github.com/Raphire/Win11Debloat)
- Click the Start button (Windows logo).
- Search for **PowerShell** in the Start menu, right-click it, and select "**Run as administrator**."
- Copy and paste this command and hit enter:
```powershell
        & (\[scriptblock\]::Create((irm ["https://debloat.raphi.re/"](https://debloat.raphi.re/))))
```
- Wait for the script to automatically download Win11Debloat.
- Carefully read through and follow the on-screen instructions.


#### 4. Install Better Windows Software

The default Microsoft Apps seem more interested in selling you things than doing their job. The programs below are replacements that share a common thread: open source or at least privacy-respecting, no upsell popups, and they just *do the thing*.

#### Must replace

| Category | Replace | With | Why |
| - | - | - | - |
| Browser | Edge | [Firefox](https://www.mozilla.org/firefox/) + [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/), or just [Brave](https://brave.com/) | No tracking, no ads, blocks the web's worst behaviour |
| Search Engine | Bing | [DuckDuckGo](https://duckduckgo.com/) | Fast; just search, not news/ads |
| PDF Viewer | Adobe Acrobat | [SumatraPDF](https://www.sumatrapdfreader.org/) | Fast, tiny, opens instantly — no subscription nags |
| File Search | Windows Explorer Search | [Everything](https://www.voidtools.com/) | Finds any file on your PC instantly, no indexing wait |
| Email | Outlook / Windows Mail | [Thunderbird](https://www.thunderbird.net/) | Fully featured, no Microsoft account required |


#### Recommended

| Category | Replace | With | Why |
| - | - | - | - |
| Photo Preview | Windows Photos | [IrfanView](https://www.irfanview.com/) | Lightweight, fast, no AI features you didn't ask for |
| Notes | Notepad | [Notepad++](https://notepad-plus-plus.org/downloads/) | Tabs, syntax highlighting, actually useful |
| Screenshot | Snipping Tool | [ShareX](https://getsharex.com/) | Screenshots, recording, annotation — all in one |
| Video Editor | Clipchamp | [OpenShot](https://www.openshot.org/) or [Kdenlive](https://kdenlive.org/) | Cut and export - no learning curve, no account, no nags |
| Media Player | Windows Media Player | [VLC](https://www.videolan.org/vlc/) | Plays everything, no codec packs needed |
| Start Menu | Windows Start | [Open-Shell](https://open-shell.github.io/Open-Shell-Menu/) | Classic menu without ads or recommended content |
| Office Suite | Microsoft Office | [LibreOffice](https://www.libreoffice.org/) | Full Word/Excel/PowerPoint replacement, free forever |
| Cloud Storage | OneDrive | [Proton Drive](https://proton.me/drive) | End-to-end encrypted, not harvested for ads |
| Format SD Cards | Explorer | [SD Card Formatter](https://www.sdcard.org/downloads/formatter/) | Official tool from the SD Association, does it properly |
| Unzip | — | [7-Zip](https://www.7-zip.org/) | Handles every archive format, no bloat |
| Password Manager | — | [Proton Pass](https://proton.me/pass) | Encrypted, syncs across devices, no upselling |
| Ebooks | — | [Calibre](https://calibre-ebook.com/) | Manages your library and converts between formats |
| Write Disk Images | — | [Rufus](https://rufus.ie/) | Creates bootable USB drives quickly and reliably |
| Download Manager | — | [AB Download Manager](https://abdownloadmanager.com/) | Modern, free, open source, browser integration works well |


These are the top tools to improve your computing experience significantly, just by not getting in the way.

