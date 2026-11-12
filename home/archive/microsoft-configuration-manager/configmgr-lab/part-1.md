---
description: 04-12-2020 5:39 PM
---

# Part 1 - Installing Windows 10 (1909) on the Host

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

## HOST CONFIGURATION

### Hardware

* **DEVICE:** Intel NUC 8i7BEH  ([See more specification](https://ark.intel.com/content/www/us/en/ark/products/126140/intel-nuc-kit-nuc8i7beh.html))
* **CPU:** Intel® Core™ i7-8559U Processor (8 MB Cache, up to 4.50 GHz)
* **STORAGE 1:** Samsung 860 EVO SSD 500 GB
* **STORAGE 2:** Samsung 970 EVO Plus NVMe 2 TB
* **RAM:** Samsung DDR4-2400 64 GB (2x32 GB)

![Hardware - Intel NUC 8i7BEH](../../../.gitbook/assets/Front_Intel_NUC.jpg)

![Hardware - Intel NUC 8i7BEH](../../../.gitbook/assets/Top_Intel_NUC.jpg)

### Software

* **Operating System**: Windows 10 Enterprise 64-Bit (**1909**)
* **Hypervisor**: Microsoft Hyper-V

{% hint style="info" %}
The minimum hardware requirements to Install Windows 10 Enterprise 64-Bit are 1 GHz or faster processor speed (**CPU**), 2 GB Memory (**RAM**) and 32 GB of hard disk space (**HDD**).
{% endhint %}

I will be installing Windows 10 Enterprise 64-Bit **(1909)** on the host hardware mentioned above. Afterwards on the host I will add the Microsoft Hyper-V feature role and create a basic Microsoft Endpoint Configuration Manager LAB environment.

## HOST INSTALLATION

### DiskPart

{% hint style="info" %}
If you haven't customized the WinRE image, you could just skip this part.
{% endhint %}

Before I'll walk you through the Windows 10 Enterprise 64-Bit (**1909**) installation, then let's take a quick look at a small script that I've added to my bootable USB device and is used for disk partition.

Because I offline servicing my Windows 10 image and customizing WinRE to include DaRT, CMTrace and WMIExplorer, the default size of Recovery Partition (I believe the default size is 499 MB) is not enough, as my WinRE image becomes larger than 580 MB in size! So to fix this, I use the below DiskPart script to set the Recovery Partition to just under 1 GB _"There's a longer explanation for exactly why it has to be under 1 GB, but trust me on this and let's save that explanation for another day... Or you could just read about the drive partition rules_ [_here_](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-8.1-and-8/hh825146\(v=win.10\)?redirectedfrom=MSDN#drive-partition-rules) _and while you're at it, then read this_ [_blog post_](https://winpeguy.wordpress.com/2015/07/08/partitions-my-recommendations-for-windows-deployments/) _too - thanks_ [_David Segura_](https://twitter.com/SeguraOSD)_"_

{% hint style="info" %}
**DaRT** is not freely available.  It's part of the Microsoft Desktop Optimization Pack (**MDOP**)
{% endhint %}

**Script (CreatePartitions-UEFI.txt)**

```
rem ============================
rem == Create UEFI Partitions ==
rem ============================
  select disk 0
  clean
  convert gpt

rem =========================
rem == 1. System partition ==
rem =========================
  create partition efi size=260
  format quick fs=fat32 label="System"
  assign letter="S"

rem ===========================================
rem == 2. Microsoft Reserved (MSR) partition ==
rem ===========================================
  create partition msr size=128

rem ==========================
rem == 3. Windows partition ==
rem ==========================
  create partition primary 
  shrink minimum=980
  format quick fs=ntfs label="Windows"
  assign letter="W"

rem ==================================
rem === 4. Recovery tools partition ==
rem ==================================
  create partition primary
  format quick fs=ntfs label="Recovery"
  assign letter="R"
  set id="de94bba4-06d1-4d40-a16a-bfd50179d6ac"
  gpt attributes=0x8000000000000001

  list volume
  exit
```

### Windows 10 Installation

Now boot the device with a bootable Windows 10 media.

**Step 1.** Select language and click "**Next**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_01.JPG)

{% hint style="info" %}
If you haven't customized the WinRE image, you would just click "**Install now**" and go straight to step 4.
{% endhint %}

**Step 2.** Before clicking on the "**Install now**" press Shift + F10 to open a Command Prompt and execute the DiskPart Script as shown below.

```
DiskPart /s CreatePartitions-UEFI.txt
```

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_02.JPG)

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_03.JPG)

**Step 3.** Close the Command Prompt and click "**Install now**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_04.JPG)

**Step 4.** Read the License Terms _"Hmm... Yeah right, like people actually does that..."_ Anyway, click "**I accept the license terms**" and then click "**Next"**

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_05.JPG)

**Step 5.** Since this is a new installation, select "**Custom: Install Windows Only (advanced)**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_06.JPG)

**Step 6.** The partitions are already created because we used the DiskPart script in step 2. So all I have to do now is choose the partition with "**Windows**" in its name in this case it's "**Drive 0 Partition 3: Windows**" then click "**Next**"

{% hint style="info" %}
If you skipped step 2 you should instead see a "**Drive 0 Unallocated Space**" just leave everything default and then click "**Next**"
{% endhint %}

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_07.JPG)

**Step 7.** Windows 10 should now be installing and the device may restart a couple of times during this process.

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_08.JPG)

**Step 8.** After a couple of restarts you should now be presented with the OOBE (Out of Box experience) screen. Choose your region and click "**Yes**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_09.JPG)

**Step 9.** Choose keyboard layout and click "**Yes**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_10.JPG)

**Step 10.** I do not have a second keyboard layout to add, so I click "**Skip**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_11.JPG)

**Step 11.** Since this is a host I want to create a local user, to do so I click "**Domain join instead**" in the bottom left corner.

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_12.JPG)

**Step 12.** Give the local user account a name and click "**Next**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_13.JPG)

**Step 13.** Enter a password for the local user account and click "**Next**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_14.JPG)

**Step 14.** Create 3 security questions in case you forget your password. Click "**Next**" after each one.

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_15.JPG)

**Step 15.** Since this is my host I choose "**No**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_16.JPG)

**Step 16.** Since this is my host I choose "**Don't use online speech recognition**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_17.JPG)

**Step 17.** Since this is my host I choose "**No**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_18.JPG)

**Step 18.** Since this is my host I choose "**No**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_19.JPG)

**Step 19.** Since this is my host I just choose "**Basic**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_20.JPG)

**Step 20.** Since this is my host I choose "**No**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_21.JPG)

**Step 21.** Since this is my host I choose "**No**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_22.JPG)

**Step 22.** Since this is my host I choose "**No**" and click "**Accept**"

![Windows 10 (1909) - Installation](../../../.gitbook/assets/Win10_Install_23.JPG)

**Step 23.** Finally, the installation has completed successfully.

![Windows 10 (1909) - Desktop](../../../.gitbook/assets/Win10_Install_24.JPG)

This should conclude the Installation of Windows 10 Enterprise 64-Bit (**1909**) on my host. In [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2) I will be setting up the Hyper-V role and creating a NAT Switch by using PowerShell so that we can keep the LAB environment separate from the rest of the network, but still provide internet access to the VMs.

If you have any questions regarding this topic, feel free to reach out to me. I am most active on [Twitter](https://twitter.com/SuneThomsenDK)!
