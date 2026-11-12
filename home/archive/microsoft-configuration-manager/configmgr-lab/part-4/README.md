---
description: 04-13-2020 11:25 AM
---

# Part 4 - Setting up Microsoft Endpoint Configuration Manager

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

### Recommended Reading

I've gathered some useful links below, that I've been using during creation of this blog post. I seriously recommend that you read the below Microsoft docs before installing SQL and Configuration Manager.

#### Downloads Sources

* [Download Windows 10 ADK](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install)
* [Download Microsoft SQL Server 2019 Reporting Services (SSRS)](https://www.microsoft.com/en-us/download/details.aspx?id=100122)
* [Download Microsoft SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)
* [Download Latest Microsoft SQL Server 2019 Updates ](https://sqlserverbuilds.blogspot.com/#sql2019x)
* [Download Kent Agerlund's "Estimate SQL Database" Excel File](https://blog.ctglobalservices.com/configuration-manager-sccm/kea/system-center-2012-configuration-manager-sql-recommendations/)

#### Microsoft Docs

* [Recommended Hardware for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/recommended-hardware)
* [Supported Operating Systems for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/supported-operating-systems-for-site-system-servers)
* [Prerequisites for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/site-and-site-system-prerequisites)
* [Supported SQL Server Versions for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/support-for-sql-server-versions)
* [Prepare Active Directory for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/plan-design/network/extend-the-active-directory-schema)
* [List of Prerequisite Checks for Configuration Manager](https://docs.microsoft.com/en-us/configmgr/core/servers/deploy/install/list-of-prerequisite-checks)

## CM PREPARATIONS

In my previous blog post [Part 3](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3) we completed the domain controller (**DC**) installation including DHCP and DNS configuration. In Part 4, I will walk you through the basic installation of Microsoft Endpoint Configuration Manager (**CM**) including the SQL, Distribution Point and Management Point configuration.

Since I've already prepared the Virtual Machine for my CM server and completed the OS installation, let's get started with the Windows Server configuration:sunglasses:

{% hint style="info" %}
If you need a complete walk-through of the Virtual Machine creation or OS installation, then take a look at my previous blog posts [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2) and [Part 3](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3).
{% endhint %}

Oh, there is actually one thing during creation of the Virtual Machine I should share with you, and that is that I've created additional Virtual Hard Disks, but more about that during the prerequisites step.

![Configuration Manager - Preparations](<../../../../.gitbook/assets/CM_WinConfig_01 (1).JPG>)

### Windows Server Configuration

The very first thing I like to do after a Windows Server 2019 installation and before adding server roles, is renaming the server and configure the network settings.

**Step 1.** Okay, so as mentioned above, I've already completed the installation and I should be able to log into the Windows Server 2019 for the first time by using a local Administrator account.

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_02.JPG)

**Step 2.** Click "**Yes**" to the "**Networks**" dialog box and close the Server Manager.

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_03.JPG)

**Step 3.** Type "**About**" in the search line next to the start button, and click "**About your PC**"

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_04.JPG)

**Step 4.** In the middle of the "**About**" page, click "**Rename this PC**", give it a new name and click "**Next**". You don't have to reboot at this point, because we will reboot the CM server after after running the Windows Update step.

![Configuration Manager - Preparations](<../../../../.gitbook/assets/CM_WinConfig_05 (1).JPG>)

**Step 5.** In the search line, type "**View network**" and click "**View network status and tasks**"

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_06.JPG)

**Step 6.** Click "**Ethernet**"

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_07.JPG)

**Step 7.** Click "**Properties**" and select "**Properties**" for "**Internet Protocol Version 4 (TCP/IPv4)**", add the IP address for the CM server and DNS address from the DC server. Click "**OK**" to complete the configuration.

{% hint style="info" %}
Give it a default gateway, subnet mask and a static IP address from the private IP range we created in [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2#hyper-v-nat-virtual-switch) during the Hyper-V configuration.
{% endhint %}

![Configuration Manager - Preparations](<../../../../.gitbook/assets/CM_WinConfig_08 (1).JPG>)

**Step 8.** Open the "**Server Manager**", select the "**Local Server**" tab and click on "**WORKGROUP**"

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_09.JPG)

**Step 9.** Click "**Change**" in the System Properties window. Select "**Domain**", enter your domain and click "**OK**". You don't have to reboot at this point, because we will reboot the CM server after running the Windows Update step.

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_10.JPG)

### Windows Update

So now that we have completed the above Windows Server configuration, I like to run a Windows Update scan before rebooting the server and continuing with the prerequisites step.

**Step 1.** Type "**Windows Update**" in the search line next to the start button, and click "**Windows Update settings**"

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_11.JPG)

**Step 2.** Click "**Check for updates**" and wait.

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_12.JPG)

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_13.JPG)

**Step 3.** When it's done, reboot the CM server.

![Configuration Manager - Preparations](../../../../.gitbook/assets/CM_WinConfig_14.JPG)

{% hint style="info" %}
I've decided, that since this would become a very large blog post, it would be best to split the **Prerequisites** and **SQL** step into sub-sections.

So please click on the desired step in the menu to the left, or click on the links below.
{% endhint %}

### Prerequisites

{% content-ref url="prerequisites.md" %}
[prerequisites.md](prerequisites.md)
{% endcontent-ref %}

### SQL Configuration

{% content-ref url="sql.md" %}
[sql.md](sql.md)
{% endcontent-ref %}

## CM INSTALLATION

Once we have completed the Prerequisites and SQL step, we'll be ready to start the CM installation. But first we need to reboot the CM server to ensure that there is no pending reboot.

### Prerequisite Check

Before starting the setup wizard, I recommend running a prerequisite check utility to check that all prerequisites are installed and configured correctly. But first we'll have to mount the "**Configuration Manager**" media to the CM server.

Open a Command Prompt in Administrator elevated mode and follow the steps below.

**Step 1.** Navigate to "**.\SMSSETUP\BIN\X64\\**" on the mounted "**Configuration Manager**" media and execute "**Prereqchk.exe**" with the parameter "**/AdminUI**"

```
D:\SMSSETUP\BIN\X64\Prereqchk.exe /AdminUI
```

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_01.JPG)

**Step 2.** The Prerequisite Check should complete with success. If you are getting any errors or warnings at this step, it´s important that you read the details and fix it before proceeding with the installation.

{% hint style="info" %}
Click [here](https://docs.microsoft.com/en-us/configmgr/core/servers/deploy/install/list-of-prerequisite-checks) to see a list of prerequisite checks for Configuration Manager.
{% endhint %}

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_02.JPG)

### Setup Wizard

We are now finally ready for the CM installation, so navigate to the mounted "**Configuration Manager**" media and follow the steps below.

**Step 1.** Execute the "**splash.hta**" located in the root of the mounted "**Configuration Manager**" media.

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_03.JPG)

**Step 2.** Click "**Install**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_04.JPG)

**Step 3.** Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_05.JPG)

**Step 4.** Select "**Install a Configuration Manager primary site**" and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_06.JPG)

**Step 5.** Enter a product key or select the "**Evaluation**" edition which will expire after 180 days. Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_07.JPG)

**Step 6.** Check the "**I accept these License Terms and Privacy Statement**" and "**I accept these License Terms**" box and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_08.JPG)

**Step 7.** Select "**Download required files**" and specify a location where to download the files to. Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_09.JPG)

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_10.JPG)

**Step 8.** Select the server languages that Configuration Manager displays in the console and reports.

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_11.JPG)

**Step 9.** Select the client languages for Configuration Manager to support.

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_12.JPG)

**Step 10.** Provide the site code that we specified during the database creation, which in this case is "**PS1**". Give the site a name e.g. "**Test Site**" and change the drive letter of the installation path to "**E:\\**" which is the ConfigMgr drive. Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_13.JPG)

**Step 11.** Select "**Install the primary site as a stand-alone site**" and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_14.JPG)

**Step 12.** Click "**Yes**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_15.JPG)

**Step 13.** Verify that the information is correct. The database name has to match the database we created earlier and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_16.JPG)

**Step 14.** Ensure that the database and log file path is the same as specified during the SQL installation. Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_17.JPG)

**Step 15.** Leave everything default and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_18.JPG)

**Step 16.** Select "**Configure the communication method on each site system role**" and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_19.JPG)

**Step 17.** Leave everything default and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_20.JPG)

**Step 18.** Click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_21.JPG)

**Step 19.** Leave everything default and click "**Next**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_22.JPG)

**Step 20.** Verify that the selected settings is correct and click "**Next**"

![Configuration Manager - Installation](<../../../../.gitbook/assets/CM_Install_23 (1).JPG>)

**Step 21.** The Prerequisite Check completed with two warnings, which is weird because I ran it with success before starting the setup wizard.

I can verify, that the computer account does have full permissions to the "**System Management**" container in the Active Directory, so I can ignore that warning! The "**SQL Server security mode**" warning disappeared after running the check again. I guess it might be an bug:thinking:

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_24.JPG)

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_25.JPG)

{% hint style="info" %}
#### BONUS INFO

If you want to follow the Prerequisite Check or Core Setup progress in the background you can navigate to "**.\SMSSETUP\TOOLS\\**" on the mounted "**Configuration Manager**" media and copy the log viewer "**CMTrace.exe**" to e.g. "**C:\Temp\\**" run it and make it the default log viewer.

Open "**C:\ConfigMgrPrereq.log**" to follow the Prerequisite Check or "**C:\ConfigMgrSetup.log**" to follow the Core Setup progress.
{% endhint %}

**Step 22.** Click "**Begin Install**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_26.JPG)

**Step 23.** The installation progress will take between 15 and 30 minutes. Even though the core setup has completed there's still a few things happening in the background, but you should be able to open the Configuration Manger Console.

If you want to monitor what's happening in the background you can open the log file "**sitecomp.log**" from the following path "**.\Program Files\Microsoft Configuration Manager\Logs\\**"

Click "**Close**" when the core setup is done.

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_27.JPG)

**Step 24.** Type "**Configuration**" in the search line next to the start button, and click "**Configuration Manager Console**"

![Configuration Manager - Installation](<../../../../.gitbook/assets/CM_Install_28 (1).JPG>)

**Step 25.** Navigate to "**Monitoring**", expand "**System Status**" and verify that site systems and component status is "**OK**"

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_29.JPG)

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_30.JPG)

**Step 26.** Navigate to "**Administration**", expand "**Updates and Servicing**" and upgrade to the latest version

![Configuration Manager - Installation](../../../../.gitbook/assets/CM_Install_31.JPG)

Awesome! This should conclude the basic installation of Microsoft Endpoint Configuration Manager including the SQL, Distribution Point and Management Point configuration. In [Part 5](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-5) I'll be setting up the discovery methods and boundaries.

If you have any questions regarding this topic, feel free to reach out to me. I am most active on [Twitter](https://twitter.com/SuneThomsenDK)!
