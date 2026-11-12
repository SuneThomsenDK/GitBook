---
description: 02-10-2021 9:42 PM
---

# Part 6 - Setting up Software Update Point

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

## SOFTWARE UPDATE POINT

In my previous blog post [Part 5](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-5) we completed the configuration of discovery methods and boundaries. In Part 6 I will be setting up the Software Update Point role in Microsoft Endpoint Configuration Manager and I will give you a walk-through of my maintenance configuration for SQL and WSUS.

{% hint style="info" %}
This blog post does not cover the Windows Server Update Services (**WSUS**) role configuration on the server, but it is covered in [Part 4](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-4/sql#wsus-server-role)
{% endhint %}

{% hint style="info" %}
#### WHAT IS A SOFTWARE UPDATE POINT?

A Software Update Point (**SUP**) is a role configured in Microsoft Endpoint Configuration Manager which interacts with the WSUS to configure the software update settings and to request synchronization of software updates metadata.

The software update point is required if you wish to enable software updates compliance assessment and to deploy updates to the clients through Microsoft Endpoint Configuration Manager. The SUP role must be installed and configured on the central administration site (**CAS**) first, then on the primary site server and optionally on a secondary site server.

Many organizations do not use central administration site, so when you have a stand-alone primary site, install and configure the software update point on the primary site server first, and then optionally, on a secondary site server.

Read more about Software Update Point [here](https://docs.microsoft.com/en-us/mem/configmgr/sum/get-started/install-a-software-update-point)
{% endhint %}

Since I've already prepared the Windows Server Update Services (**WSUS**), let's get started with configuring the software update point role in Microsoft Endpoint Configuration Manager.

### Software Update Point Role

**Step 1.** Type "**Configuration**" in the search line next to the start button, and click "**Configuration Manager Console**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/Boundary_Config_01.JPG)

**Step 2.** Navigate to "**Administration**" and expand the "**Site Configuration**", now select "**Servers and Site System Roles**", right-click on your site server name and select "**Add Site System Roles**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_01.JPG)

**Step 3.** Click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_02.JPG)

**Step 4.** Click "**Next**"

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_03 (1).JPG>)

**Step 5.** Select "**Software update point**" from the role list and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_04.JPG)

**Step 6.** Click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_05.JPG)

**Step 7.** Click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_06.JPG)

**Step 8.** Select "**Synchronize from Microsoft Update**" and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_07.JPG)

**Step 9.** Select "**Enable Synchronization on a schedule**", configure it to every 1 day and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_08.JPG)

**Step 10.** Set "**Supersedence behavior**" to 1 month or keep the default value (3 months) and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_09.JPG)

**Step 11.** Select all maintenance options and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_10.JPG)

**Step 12.** Click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_11.JPG)

**Step 13.** Select "**Download full files for all approved updates**" and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_12.JPG)

**Step 14.** Do not select any "**Classifications**" at this point, click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_13.JPG)

**Step 15.** Do not select any "**Products**" at this point, click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_14.JPG)

**Step 16.** Select the desired languages and click "**Next**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_15.JPG)

**Step 17.** Click "**Next**" and then click "**Close**" when the setup is complete.

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_16.JPG)

**Step 18.** Go to the Microsoft Endpoint Configuration Manager log location and review the **SUPSetup.log**

You should see a line in the log that says: **Installation was successful.**

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_17 (1).JPG>)

**Step 19.** In the console go to "**Software Library**" and expand "**Software Updates**", select "**All Software Updates**" which should be empty at this point. Now click on "**Synchronize Software Updates**"

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_18 (3).JPG>)

**Step 20.** Click "**Yes**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_19.JPG)

**Step 21.** Go to the Microsoft Endpoint Configuration Manager log location and review the **wsyncmgr.log**

You should see a line in the log that says: **Sync succeeded.**

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_20 (1).JPG>)

### Classifications & Products

We are now finally ready for the classifications and products configuration.

**Step 1.** Navigate to "**Administration**" and expand the "**Site Configuration**", select "**Sites**", right-click on your site name, expand the "**Configure Site Components**" and select "**Software Update Point**"

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_21.JPG)

**Step 2.** Select the "**Classifications**" tab and select the ones you need.

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_22.JPG)

**Step 3.** Select the "**Products**" tab and select the ones you need.

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_23.JPG)

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_24.JPG)

**Step 4.** In the console go to "**Software Library**" and expand "**Software Updates**", select "**All Software Updates**" which should still be empty at this point. Now, click on "**Synchronize Software Updates**"

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_18 (3).JPG>)

**Step 5.** Click "**Yes**"

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_19 (1).JPG>)

**Step 6.** Go to the Microsoft Endpoint Configuration Manager log location and review the **wsyncmgr.log**

You should see a line in the log that says: **sync: Starting WSUS synchronization**

This **WILL** take a while to finish, so go grab a coffee, go for a walk or go to bed (I'll let you decide...):sunglasses:&#x20;

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_25.JPG)

**Step 7.** Okay, so almost 5 hours later and it is finally done!

You should see a line in the log that says: **Done synchronizing WSUS Server**

![Configuration Manager - Software Update Point](<../../../.gitbook/assets/SUP_26 (1).JPG>)

**Step 8.** You should now see the software updates in the console. Fantastic :star\_struck:

![Configuration Manager - Software Update Point](../../../.gitbook/assets/SUP_27.JPG)

## SQL & WSUS MAINTENANCE

Now that the software update point for this LAB has been configured and synchronized, let's continue with the SQL and WSUS maintenance which is important in order to prevent the whole house of cards from collapsing in the future - We have all been there at one point, right ?

{% hint style="info" %}
In my search for a maintenance solution, I found a blog post by [Kent Agerlund](https://twitter.com/agerlund) which led me to a PowerShell script created by [Kaido Järvemets](https://twitter.com/kaidja) and a SQL script created by [Ola Hallengren](https://twitter.com/olahallengren)

You can read Kent's entire blog post [here](https://blog.ctglobalservices.com/configuration-manager-sccm/kea/house-of-cardsthe-configmgr-software-update-point-and-wsus/)
{% endhint %}

### Prerequisites

* Download WSUS Script & Scheduled Task [here](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/WSUS_Maintenance)
* Download SQL Script [here](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html)

### SQL Maintenance

**Step 1.** Type "**SQL Server Management**" in the search line next to the start button, and click "**Microsoft SQL Server Management Studio 18**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_00.JPG)

**Step 2.** Click "**Connect**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_001.JPG)

**Step 3.** Click "**File**" -> "**Open**" -> "**File...**" or "**Ctrl+O**". Now, select the **MaintenanceSolution.sql** script previously downloaded from [Ola Hallengren's](https://twitter.com/olahallengren) website.

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_01 (2).JPG>)

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_02.JPG)

**Step 4.** Modify the configuration or keep the defaults and click "**Execute**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_03.JPG)

**Step 5.** You should see a line in the messages pane that says: **Commands completed successfully.**

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_04.JPG)

**Step 6.** Expand the "**SQL Server Agent**", right-click on "**Jobs**" and select "**Manage Schedules**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_05.JPG)

**Step 7.** Click "**New...**"

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_06 (1).JPG>)

**Step 8.** Configure the new job schedule to fit your needs or use my configuration in the below print screen and click "**OK**"

{% hint style="info" %}
**Note**. I recommend running the SQL maintenance before the WSUS maintenance.
{% endhint %}

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_07 (1).JPG>)

**Step 9.** Expand the "**Jobs**", right-click "**IndexOptimize - USER\_DATABASES**" and select "**Properties**"

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_08 (2).JPG>)

**Step 10.** On the "**Steps**" page, click "**New...**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_09.JPG)

**Step 11.** Give the step a name, add a command that the step should run once a week and click "**OK**"&#x20;

You can use my command below or find inspiration at [Ola Hallengren's](https://twitter.com/olahallengren) website [here](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html)

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_10 (1).JPG>)

```
EXECUTE dbo.IndexOptimize
@Databases = 'SUSDB',
@FragmentationLow = NULL,
@FragmentationMedium = 'INDEX_REORGANIZE,INDEX_REBUILD_ONLINE,INDEX_REBUILD_OFFLINE',
@FragmentationHigh = 'INDEX_REBUILD_ONLINE,INDEX_REBUILD_OFFLINE',
@FragmentationLevel1 = 5,
@FragmentationLevel2 = 30,
@UpdateStatistics = 'ALL',
@OnlyModifiedStatistics = 'Y',
@SortInTempdb = 'Y',
@MaxDOP = 0
```

**Step 12.** On the "**Schedules**" page, click "**New...**", select the job schedule previously created in step 8 and click "**OK**" twice.

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_11.JPG)

**Step 13.** Open the "**Job Activity Monitor**", right-click on "**IndexOptimize - USER\_DATABASES**" and select "**Start Job at Step...**"

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_12.JPG)

**Step 14.** Click "**Close**" when it's done.

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_13 (1).JPG>)

**Step 15.** Right-click on "**IndexOptimize - USER\_DATABASES**" again and now select "**View history**"

![SQL Maintenance](<../../../.gitbook/assets/SQL_Cleanup_14 (1).JPG>)

**Step 16.** Expand the log and review the details.

You should see that the last messages says: **The step succeeded.**

![SQL Maintenance](../../../.gitbook/assets/SQL_Cleanup_16.JPG)

### WSUS Maintenance

**Step 1.** Download the **WSUSCleanupTask.ps1** and **WSUSCleanupTask.xml** from my GitHub repository and place it somewhere on your WSUS server.&#x20;

**Important** - Before proceeding with step 2, you need to modify the **WSUSCleanupTask.ps1** configuration.

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_01.JPG)

```
#Configuration

$UseSSL = $False <-- HTTPS or HTTP (Mandatory)
$PortNumber = 8530 <-- Port for HTTPS or HTTP (Mandatory)
$Server = "cm.domain.local" <-- FQDN of the WSUS Server (Mandatory)
$ReportLocation = "E:\WSUS\CleanupReport.html" <-- Report location (Mandatory)
$SMTPServer = "mail.domain.com" <-- FQDN of the mail server (Optional)
$SMTPPort = 25 <-- SMTP Port (Optional)
$To = "Full Name <user@domain.com>" <-- Mail recipient (Optional)
$From = "System Notify <system.notify@domain.com>" <-- Mail sender (Optional)
```

**Step 2.** Type "**Task Scheduler**" in the search line next to the start button, and click "**Task Scheduler**"

![WSUS Maintenance ](../../../.gitbook/assets/Cleanup_02.JPG)

**Step 3.** Click "**Import Task...**" from the "**Actions**" pane and import the **WSUSCleanupTask.xml** previously downloaded from my GitHub repository. Make the necessary changes so it will fit your environment e.g. when should it run and where is the script located? Click "**OK**" when finish.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_03 (2).JPG>)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_03_1.JPG)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_03_2.JPG)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_03_3.JPG)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_03_4.JPG)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_03_5.JPG)

**Step 4.** Select the "**General**" tab and make sure that the configuration is correct for your environment.

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_04.JPG)

**Step 5.** Select the "**Triggers**" tab and make sure that the configuration is correct for your environment.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_05 (1).JPG>)

**Step 6.** Select the "**Actions**" tab and make sure that the configuration is correct for your environment.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_06 (2).JPG>)

**Step 7.** Select the "**Conditions**" tab and make sure that the configuration is correct for your environment.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_07 (1).JPG>)

**Step 8.** Select the "**Settings**" tab and make sure that the configuration is correct for your environment.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_08 (1).JPG>)

**Step 9.** Run the scheduled task and look for any issues in the "**History**" tab.

![WSUS Maintenance](<../../../.gitbook/assets/Cleanup_09 (1).JPG>)

**Step 10.** If the scheduled task ran successfully, you should see a **CleanupReport.html** in the location that you defined earlier in the **WSUSCleanupTask.ps1** configuration and if you open the report, you can see which job was performed by the script.

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_10.JPG)

![WSUS Maintenance](../../../.gitbook/assets/Cleanup_11.JPG)

This should conclude setting up the Software Update Point role in Microsoft Endpoint Configuration Manager and the maintenance configuration for SQL and WSUS.

Now, Part 7 was actually on the drawing board, but I've decided that Part 6 will be the last one in this blog series. I will continue to blog about Endpoint Management in the 2021 section, this has been an awesome and a long blog series but I know that it has helped others and that makes it all worthwhile to me :nerd:

If you have any questions regarding this topic, feel free to reach out to me. I am most active on [Twitter](https://twitter.com/SuneThomsenDK)!
