---
description: 04-12-2020 5:39 PM
---

# Part 2 - The Host and Hyper-V Configuration

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

## HOST CONFIGURATION

In my previous blog post [Part 1](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-1) I did a quick hardware configuration walk-through and installed Windows 10 on my host. In Part 2, I will walk you through the Hyper-V configuration and build a Virtual Machine for my Domain Controller (**DC**) where we in [Part 3](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3) will be setting up Active Directory, DHCP, and DNS.

After finishing the Windows 10 installation the first thing I want to do is change the computer name to eg. OSDSUNE-LAB-01 and then check for Windows Updates. Since my Windows 10 image is offline serviced every month, Windows Updates won't find anything exciting!&#x20;

If you don't offline servicing your Windows 10 image, my recommendation is that you run Windows Updates and get the latest cumulative and other updates installed before moving forward with the configuration.

### Windows Update

Log into the host we created in [Part 1](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-1).

**Step 1.** Type "**Check for updates**" in the search line next to the start button, and click "**Check for updates**"

![Windows 10 (1909) - Windows Update](../../../.gitbook/assets/Step_01_windows_update.JPG)

**Step 2.** Click "**Check for updates**" and wait.

![Windows 10 (1909) - Windows Update](../../../.gitbook/assets/Step_02_windows_update.JPG)

**Step 3.** After a few seconds it should start downloading and install required updates for the host.

![Windows 10 (1909) - Windows Update](../../../.gitbook/assets/Step_04_windows_update.JPG)

**Step 4.** When it's done, reboot the host.

### Windows Features

After a reboot, log into the host again and we will now be adding the Hyper-V feature role to the host.

**Step 1.** In the search line, type "**Add features**" and click "**Turn Windows features on or off**"

![Windows 10 (1909) - Add Feature](../../../.gitbook/assets/Step_05_add_hyper-v_role.JPG)

**Step 2.** Check the "**Hyper-V**" box and click "**OK**"

![Windows 10 (1909) - Add Feature](../../../.gitbook/assets/Step_06_add_hyper-v_role.JPG)

**Step 3.** Click "**Restart now**"

![Windows 10 (1909) - Add Feature](../../../.gitbook/assets/Step_07_add_hyper-v_role.JPG)

**Step 4.** After a reboot, log into the host and check for Windows Updates once again. In the search line, type "**Check for updates**" and click "**Check for updates**". The reason for this is that since we have add a new feature to Windows it need to re-apply the cumulative update in order for the feature to function correct.

![Windows 10 (1909) - Windows Update](../../../.gitbook/assets/Step_08_add_hyper-v_role_windows_update.JPG)

**Step 5.** As mentioned it will re-apply the latest cumulative update. (And yes I has gone to the dark side...) reboot the host when it's done.

![Windows 10 (1909) - Windows Update](../../../.gitbook/assets/Step_09_add_hyper-v_role_windows_update.JPG)

## HYPER-V CONFIGURATION

After a reboot, log into the host again and we will start setting up the Hyper-V role.

{% hint style="info" %}
#### WHAT IS HYPER-V?

Hyper-V is Microsoft's Hypervisor, which give you the ability to run Virtual Machines (**Guests**) on a Physical Machine (**Host**).&#x20;

Hyper-V was introduced back in 2008, a lot has happened since then, and today Hyper-V is a great alternative to other Virtualization Technologies from eg. VMware and Citrix.
{% endhint %}

### Hyper-V NAT Virtual Switch

I will be using Windows PowerShell to create a Virtual Switch that uses Network Address Translation (**NAT**), this will keep the LAB environment separate from the rest of the network, but still provide internet access to the Virtual Machines.

{% hint style="info" %}
I will not be diving deep into the details about Virtual Switch or NAT, so please read this excellent [blog](https://www.petri.com/using-nat-virtual-switch-hyper-v) on this topic by [Aidan Finn](https://twitter.com/joe_elway) if you need more information.
{% endhint %}

**Step 1.** Open Windows PowerShell in Administrator elevated mode.&#x20;

![PowerShell - NAT Virtual Switch](../../../.gitbook/assets/Step_10_PS_ExecutionPolicy.JPG)

**Step 2.** To create the Virtual Switch run the below New-VMSwitch command.

```
New-VMSwitch -SwitchName "NAT Switch" -SwitchType Internal
```

![PowerShell - NAT Virtual Switch](../../../.gitbook/assets/Step_11_PS_New-VMSwitch.JPG)

**Step 3.** The below New-NetIPAddress command, assigns an IP address to the Virtual NIC. Which also will be the default gateway IP address for the NAT Network that we are creating.

```
New-NetIPAddress -IPAddress 192.168.0.1 -PrefixLength 24 -InterfaceAlias "vEthernet (NAT Switch)"
```

![PowerShell - NAT Virtual Switch](../../../.gitbook/assets/Step_12_PS_New-NetIPAddress.JPG)

**Step 4.** The below New-NetNAT command assigns a private range of IP addresses that the Virtual Machines will use on the Virtual Switch we have just created.

```
New-NetNAT -Name "NAT Network" -InternalIPInterfaceAddressPrefix 192.168.0.0/24
```

![PowerShell - NAT Virtual Switch](../../../.gitbook/assets/Step_13_PS_New-NetNAT.JPG)

We have now create a NAT Virtual Switch that will keep the LAB environment separate from the rest of the network, but still provide internet access to the Virtual Machines - Now That's Awesome!:sunglasses:&#x20;

### Hyper-V Manager

Now that we have configured the Virtual Switch, it's time to launch the Hyper-V Manager and configure a Virtual Machine for the Domain Controller.

**Step 1.** In the search line, type "**Hyper-V**" and click "**Hyper-V Manager**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_14_hyper-v_manager.JPG)

**Step 2.** Right-click on the Hyper-V Server and click "**Hyper-V Settings...**"

![Windows 10 (1909) - Hyper-V Manager](<../../../.gitbook/assets/Step_15_hyper-v_manager_settings (1).JPG>)

**Step 3.** You don't have to perform this step, but by habit I like to change the default path for Virtual Hard Disks and Virtual Machines. Leave the rest as default and click "**OK**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_16_hyper-v_manager_VHD\&VM_Path.JPG)

**Step 4.** Open File Explorer and go to "**C:\Hyper-V**", confirm that the folders has been created.

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_17_hyper-v_manager_VHD\&VM_Path.JPG)

**Step 5.** Right-click on the Hyper-V Server again, but this time you click "**New**" and then "**Virtual Machine...**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_18_hyper-v_manager_new_vm.JPG)

**Step 6.** Click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_19_hyper-v_manager_new_vm_wizard.JPG)

**Step 7.** Enter a name for the Virtual Machine (**DC**) and leave "**Location**" as default and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_20_hyper-v_manager_new_vm_wizard.JPG)

**Step 8.** Select "**Generation 2**" and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_21_hyper-v_manager_new_vm_wizard.JPG)

**Step 9.** Type in the amount of memory (**RAM**) you want to dedicate to the Virtual Machine (I'll give a DC server, 4 GB of memory). Uncheck "**Use Dynamic Memory for this virtual machine**" and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_22_hyper-v_manager_new_vm_wizard.JPG)

**Step 10.** Now select the newly created "**NAT Switch**" from the drop-down menu and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_23_hyper-v_manager_new_vm_wizard.JPG)

**Step 11.** Select "**Create a virtual hard disk**" and enter a name (**DC.vhdx**). Leave the "**Location**" and "**Size**" as default and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_24_hyper-v_manager_new_vm_wizard.JPG)

**Step 12.** Select "**Install an operating system from a bootable image file**". Enter a path or browse to the "**Windows Server 2019**" ISO file and click "**Next**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_25_hyper-v_manager_new_vm_wizard.JPG)

**Step 13.** Review the settings and click "**Finish**" to create the Virtual Machine.

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_26_hyper-v_manager_new_vm_wizard08.JPG)

**Step 14.** We should now see a new Virtual Machine in the Hyper-V Manager.

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_27_hyper-v_manager_new_vm_done.JPG)

**Step 15.** Right-click on the Virtual Machine and then click "**Connect**"

![](../../../.gitbook/assets/Step_28_hyper-v_manager_new_vm_connect.JPG)

**Step 16.** Select "**File**" and click "**Settings...**" or click Ctrl+O to enter the settings for the Virtual Machine.

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_29_hyper-v_manager_new_vm_setting.JPG)

**Step 17.** Select "**Processor**" and change the "**Number of virtual processors**" to at least 2 and click "**OK**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_30_hyper-v_manager_new_vm_setting.JPG)

**Step 18.** Now click "**Start**"

![Windows 10 (1909) - Hyper-V Manager](../../../.gitbook/assets/Step_31_hyper-v_manager_new_vm_start.JPG)

**Step 19.** Windows Server 2019 are now ready to be installed on the Virtual Machine in [Part 3](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3).

![Windows Server 2019 - Installation](../../../.gitbook/assets/Step_32_hyper-v_manager_new_vm_start_install.JPG)

And that's it, folks! This should conclude the host and Hyper-V configuration. In [Part 3](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3) I will walk you through the installation of Windows Server 2019 on my Domain Controller and we will be setting up a basic Active Directory, DHCP, and DNS configuration.

If you have any questions regarding this topic, feel free to reach out to me. I am most active on [Twitter](https://twitter.com/SuneThomsenDK)!
