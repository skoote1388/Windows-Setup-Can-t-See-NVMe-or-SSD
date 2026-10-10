# Windows Setup Can't See NVMe or SSD

If Windows Setup cannot see your internal NVMe SSD or other storage drive, the problem may be related to the storage configuration in your BIOS.

I recently ran into this problem while reinstalling Windows. My SSD was installed and working, but Windows Setup could not properly access it because **Intel RST/RAID was enabled in the BIOS**.

If you are not using RAID, you may be able to disable the related setting in the BIOS. Another option is to leave RST enabled and provide Windows Setup with the appropriate Intel RST driver.

## Option 1 — Disable RAID/RST/VMD in BIOS

If you are not using RAID, check your BIOS for a storage setting related to:

- Intel RST
- Intel Rapid Storage Technology
- RAID
- Intel VMD
- VMD Controller
- Storage Controller

If the setting is enabled and you do not need it, disabling it may allow Windows Setup to see your SSD normally.

After changing the setting, save your BIOS changes and restart Windows Setup.

**Important:** Do not change storage-controller settings on an existing Windows installation without understanding the consequences. Changing between storage modes can prevent an existing Windows installation from booting if the appropriate driver or configuration is not available.

## Option 2 — Keep RST Enabled and Load the Driver

If you want or need to keep Intel RST/RAID/VMD enabled, you can provide Windows Setup with the appropriate **Intel Rapid Storage Technology (RST)** driver.

At the Windows installation screen:

1. Start Windows Setup from your installation USB.
2. Continue until you reach **Where do you want to install Windows?**
3. If your SSD is missing, select **Load driver**.
4. Browse to the extracted Intel RST driver files.
5. Select the appropriate storage-controller driver.
6. Allow Windows Setup to load the driver.
7. Check the drive list again.

Once the correct driver is loaded, Windows Setup should be able to access the storage controller and see the SSD.

## Intel RST Driver Files

I created a separate repository containing the Intel RST driver files I used:

**Intel Rapid Storage Technology (IRST) Driver Files — Version 18.7.6.1010.3**

[https://github.com/skoote1388/Intel-Rapid-Storage-Technology-IRST-Driver-Files-Version-18.7.6.1010.3](https://github.com/skoote1388/Intel-Rapid-Storage-Technology-IRST-Driver-Files-Version-18.7.6.1010.3)

The repository contains the extracted driver files needed for loading the storage driver directly from Windows Setup.

## Getting the Driver Files Yourself

If you already have the **SetupRST.exe** installer, you can extract the driver files yourself.

Open Command Prompt in the folder containing `SetupRST.exe` and run:

```cmd
SetupRST.exe -extractdrivers SetupRST_extracted
```

This creates a folder named:

```text
SetupRST_extracted
```

You can then copy that folder to your Windows installation USB and use **Load driver** in Windows Setup.

## Alternate Download

If you don't want to extract the files yourself, I also have a page where you can download the `SetupRST.exe` installer:

**Alternate download:**
[https://www.intel.com/content/www/us/en/download/19512/intel-rapid-storage-technology-driver-installation-software-with-intel-optane-memory-10th-and-11th-gen-platforms.html](https://www.intel.com/content/www/us/en/download/19512/intel-rapid-storage-technology-driver-installation-software-with-intel-optane-memory-10th-and-11th-gen-platforms.html)

You can download `SetupRST.exe` and use the extraction command above to obtain the driver files.

## What Happened in My Case

I was reinstalling Windows and ran into a problem where Windows Setup could not properly access my SSD.

My BIOS had **RAID/RST enabled**, even though I was not using a RAID configuration.

I was able to disable the setting because I did not need RAID. However, loading the Intel RST driver is another way to get Windows Setup to access the drive while keeping the storage configuration enabled.

I'm documenting both methods because the correct solution depends on how the computer is configured.

## Important

Before changing RAID, RST, or VMD settings, make sure you understand how your existing Windows installation is configured.

If you are performing a **clean Windows installation**, loading the correct storage driver may be preferable to changing the BIOS storage configuration.

If you are unsure which option applies to your computer, check your motherboard or computer manufacturer's documentation.

## Disclaimer

This is an independent community resource based on my own Windows installation experience. It is not affiliated with Intel or Microsoft.

Always verify the correct storage configuration and driver for your specific computer before making changes.

MIT License

Copyright (c) 2026 Stephen Dale Cothran

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Disclaimer

This is an independent, unofficial community resource based on my own Windows
installation experience. It is **not affiliated with, endorsed by, or sponsored
by** Intel Corporation, Microsoft Corporation, or any hardware manufacturer.

"Intel", "Intel Rapid Storage Technology", "Intel VMD", and "Windows" are
trademarks of their respective owners and are used here for identification only.

The guide text in this repository is licensed under the MIT License (see
`LICENSE`). Vendor files referenced or bundled in linked repositories remain
the property of their respective owners.

Always verify the correct storage configuration and driver for your specific
computer before making changes. Use at your own risk.
