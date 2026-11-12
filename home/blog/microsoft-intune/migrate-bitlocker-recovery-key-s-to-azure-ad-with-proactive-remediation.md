---
description: 01-06-2023 8:09 PM
cover: ../../.gitbook/assets/Security_Encryption_Key.jpg
coverY: -4
---

# Migrate Bitlocker Recovery Key(s) to Azure AD with Proactive Remediation

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

## Introduction

Are you also in the middle of transitioning from on-premises to the cloud, or are you currently planning this journey? If so, you also want a modern way to migrate Bitlocker recovery key(s) to Azure AD when moving away from on-premises MBAM/Active Directory escrowing.\
\
I help our customers achieve this by using a proactive remediation script from Endpoint analytics in Microsoft Intune. It might sound like rocket science to you right now. However, getting started with Endpoint analytics and proactive remediation is pretty straightforward, and I’ll explain how it all works in this blog post so you will be the rocket scientist by the end of the post.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_01-1024x393.png" alt="Migrate Bitlocker recovery key(s) to Azure AD."><figcaption></figcaption></figure>

## Prerequisites

* The device must be Azure AD joined or Hybrid Azure AD joined.
* Intune enrolled or co-managed devices running the following:
  * Windows 10 version 1903 or later.
  * Enterprise, Professional, or Education edition.
  * The cumulative update from July 2021 or later.
* Devices enrolled into Endpoint analytics.
* Network connectivity from devices to the Microsoft public cloud.

## Licensing Requirements

* Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
* Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
* Windows 10/11 Virtual Desktop Access (VDA) per user
* Microsoft Intune or Microsoft Endpoint Configuration Manager

## Permissions

* A Microsoft Intune RBAC role that has the appropriate **Device Configurations** permissions or one of the following permissions in Azure AD
  * Global Administrator
  * Intune Administrator

{% hint style="warning" %}
&#x20;**Important:** An **Intune Service Administrator** is required to confirm licensing requirements before using Proactive remediations for the first time. – See the [what is Endpoint analytics?](https://learn.microsoft.com/en-us/mem/analytics/overview#proactive-remediations-permissions)
{% endhint %}

## Script Requirements

* You can have up to 200 script packages.
* A script package can contain a detection script (only) or both a detection and a remediation script.
* A remediation script only runs if the detection script uses exit code exit 1.
* Ensure the scripts are encoded in UTF-8, not UTF-8 BOM.
* The maximum allowed output size limit is 2048 characters.
* Don’t put secrets in scripts. Consider using parameters to handle secrets instead.
* Don’t put reboot commands in the detection or remediation scripts.

Read this [Microsoft Learn](https://learn.microsoft.com/en-us/mem/analytics/proactive-remediations#bkmk_prereq) article for more information about prerequisites, permissions, and requirements.

## What is Proactive Remediation in Endpoint Analytics?

Proactive remediations in Endpoint analytics are script packages that detect and remediate issues or configure Windows 10/11 settings on devices. An example of this could be settings that I call **non-supported MDM settings**, which are settings or GPO preferences that are unsupported and do not exist in Microsoft Intune (For example, Registry Settings, Shortcuts, File Download, etc.)

{% hint style="info" %}
&#x20;**Info:** Proactive remediations in **Endpoint analytics** help you fix common support issues before end-users notice issues. – See the [Tutorial: Proactive remediations](https://learn.microsoft.com/en-us/mem/analytics/proactive-remediations)
{% endhint %}

Each script package can consist of a detection script (only) for monitoring purposes or both a detection and a remediation script to remediate issues or configure Windows 10/11 settings, as explained above. You assign and monitor the status of these script packages through Endpoint analytics in Microsoft Intune.

## The Bitlocker Backup to AAD Detection and Remediation Script

{% hint style="warning" %}
&#x20;**Important:** Please download the [**detection**](https://github.com/SuneThomsenDK/OSDSUNE/blob/master/Scripts/ProactiveRemediation/BitLockerBackupToEntraID/Detect_BitLockerBackupToEntraID.ps1) and [**remediation**](https://github.com/SuneThomsenDK/OSDSUNE/blob/master/Scripts/ProactiveRemediation/BitLockerBackupToEntraID/Remediate_BitLockerBackupToEntraID.ps1) script from my [**GitHub repository**](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/ProactiveRemediation/BitLockerBackupToEntraID) before continuing.
{% endhint %}

The detection and remediation scripts contain a detailed description, notes, changelog, CMTrace-friendly log functionality, several functions, and the main script within a script block.

<table><thead><tr><th width="145">Action</th><th>Description</th></tr></thead><tbody><tr><td>Detection</td><td>The detection script will run a prerequisite check and detect whether or not Bitlocker protects the device. If the device is protected, the script will check the local event log or registry to see if the Bitlocker recovery key(s) exist in Azure AD.</td></tr><tr><td>Remediation</td><td>The remediation script will run a prerequisite check and detect whether or not Bitlocker protects the device. If the device is protected, the script will check the local event log and registry to confirm that the Bitlocker recovery key(s) does not exist in Azure AD and then attempt to back up the Bitlocker recovery key(s) to Azure AD.</td></tr></tbody></table>

Getting started with these proactive remediation scripts requires very little effort. Since the event log time variable is optional, you only need to add a name of your choice to the registration path before uploading it to Endpoint analytics in Microsoft Intune. – It’s that easy, folks!\
\
Let’s look at the script structure from a high-level perspective. – I’ve split it into these four sections:\
\
**Section 1** – A detailed description, notes, and changelog.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Script_01-1024x507.png" alt="The proactive remediation script."><figcaption></figcaption></figure>

**Section 2** – The global variables used throughout the scripts.\
As mentioned, you only need to change the “**CompanyName**” in the registry path to a name of your choice (for example, your company name).

{% hint style="info" %}
&#x20;**Tip:** Although changing the event log time variable is optional, I suggest you change it to the date you plan to put the scripts into production.
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Script_02-1024x425.png" alt="The proactive remediation script."><figcaption></figcaption></figure>

**Section 3** – The script block that contains the main script.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Script_03-1024x539.png" alt="The proactive remediation script."><figcaption></figcaption></figure>

**Section** 4 – The functions used throughout the scripts.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Script_04-1024x356.png" alt="The proactive remediation script."><figcaption></figcaption></figure>

## Configure the Proactive Remediation Script Package in Endpoint Analytics

Once you have downloaded the required scripts from my [**GitHub repository**](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/ProactiveRemediation) and modified the registry path with a name of your choice, we can now upload it to Endpoint analytics in Microsoft Intune.\
\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
In the left pane, click **Reports** | **Analytics** | **Endpoint analytics**\
Select the **Proactive remediations** “report” and then select **Create script package**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_02-1-1024x500.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

Fill in the required **Name** field. – Although the **Description** field is optional, I recommend filling it out.\
Click **Next**.

{% hint style="info" %}
&#x20;**Tip:** It’s always a great idea to leave some breadcrumbs so others know precisely why someone created the script package.
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_03-1024x659.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

Add your **detection** and **remediation** script files, then configure the script package to run in **64-bit PowerShell**.\
Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_04.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_05-1024x942.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

Choose either to assign the script package to “**All devices**/**All users**” or to a specific security group and then select a schedule. – For example, I assigned this script package to “**All devices**“, scheduled it to run once every day, and then added a filter not to include **Windows 365 Cloud PCs**.\
Click **Next**.

{% hint style="info" %}
&#x20;**Tip: Bitlocker is not a supported** encryption option for **Windows 365 Cloud PCs**, so I recommend excluding them from this particular script package. See the [Data encryption in Windows 365](https://learn.microsoft.com/en-us/windows-365/enterprise/encryption)
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_06.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

Review the configuration and click **Create.**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_07.png" alt="The proactive remediation script package."><figcaption></figcaption></figure>

And that’s it, folks. – Once the scripts run on the devices according to the defined schedule, we should start seeing some results from the Proactive remediation blade in Endpoint analytics, but more about that in the next section.

## Monitor, Verify, and Troubleshoot

This section will be about where to monitor the Proactive remediation status in Endpoint analytics and how to troubleshoot with the help of script and log output.

Go to [https://intune.microsoft.com](https://intune.microsoft.com)

In the left pane, click **Reports** | **Analytics** | **Endpoint analytics**\
Select the **Proactive remediations** “report”, which gives you a nice status overview of your script packages.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Monitor_01-1024x428.png" alt="Proactive remediation monitoring."><figcaption></figcaption></figure>

Choose your **Bitlocker Backup to AAD** script package from the list, which gives you an even more awesome overview of the detection and remediation status and the daily remediation trends.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Monitor_02-1024x590.png" alt="Proactive remediation monitoring."><figcaption></figcaption></figure>

Select **Device status** from the overview page in the script package to see the status per device.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Monitor_03-1024x395.png" alt="Proactive remediation monitoring."><figcaption></figcaption></figure>

### **Scenarios and Script Output**

**Scenario 1** – Bitlocker recovery key(s) exists in Azure AD.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/06/Bitlocker_Endpoint_Analytics_Output_01-1024x393.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Script output."><figcaption></figcaption></figure>

**Scenario 2** – Bitlocker does not protect the system drive.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Output_02-1024x393.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Script output."><figcaption></figcaption></figure>

**Scenario 3** – The script is not running in 64-bit PowerShell.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Output_03-1024x393.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Script output."><figcaption></figcaption></figure>

**Scenario 4** – Bitlocker recovery key(s) does not exist in Azure AD.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Output_04-1024x372.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Script output."><figcaption></figcaption></figure>

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_Output_04-Post-1024x372.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Script output."><figcaption></figcaption></figure>

### **Log Output**

{% hint style="info" %}
&#x20;**Info:** By default, the log file is located in the **IntuneManagementExtension** folder so that it can be collected via remote actions in Microsoft Intune.
{% endhint %}

If we reuse the above scenarios, we will see the following output in the log file.\
\
**Scenario 1** – Bitlocker recovery key(s) exists in Azure AD.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogOutput_04-1024x314.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Scenario 2** – Bitlocker does not protect the system drive.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogOutput_02-1024x328.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Scenario 3** – The script is not running in 64-bit PowerShell.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogOutput_03-1024x328.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Scenario 4** – Bitlocker recovery key(s) does not exist in Azure AD.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogOutput_01-1024x708.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

The detection and remediation scripts will also catch errors and provide good information about what went wrong. – Here are a couple of error scenarios and the log output.\
\
**Error scenario 1** – The registry key parameter is null or empty.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogErrorOutput_01-1024x382.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Error scenario 2** – The registry key is not valid.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogErrorOutput_02-1024x382.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Error scenario 3** – The event provider name does not exist.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogErrorOutput_03-1024x357.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

**Error scenario 4** – The event ID parameter is null or empty.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/12/Bitlocker_Endpoint_Analytics_LogErrorOutput_04-1024x354.png" alt="Migrate Bitlocker recovery key(s) to Azure AD - Log output."><figcaption></figcaption></figure>

### Summary

Congratulation, you are now a Proactive remediation rocket scientist! Because in this blog post, you learned how to migrate Bitlocker recovery key(s) to Azure AD with the help of my proactive remediation scripts and how to deploy and monitor it from Endpoint analytics in Microsoft Intune.\
\
That’s it, folks. Happy testing, and merry Christmas!\
As always, if you have any questions regarding this topic, feel free to reach out to me.
