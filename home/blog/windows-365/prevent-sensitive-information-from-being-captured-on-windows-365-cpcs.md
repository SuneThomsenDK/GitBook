---
description: 30-05-2023 8:02 PM
---

# Prevent sensitive information from being captured on Windows 365 CPCs

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1urbk-LWuCtfkLGwB5NGgrlXp12Bl9URi" alt=""><figcaption><p><em>Prevent sensitive information from being captured on Cloud PCs with screen capture protection.</em></p></figcaption></figure>

## Introduction

In this blog post I will show you how to enable a feature called “**Screen Capture Protection**” which will prevent sensitive information from being captured on your Windows 365 Cloud PC(s), intentionally or by malicious software. This can be done in several ways, but in this post I will walk you through the Group Policy Object (**GPO**) and the PowerShell approach.

**Important note**. It is recommended to use this feature together with disabling clipboard, drive and printer redirection. Disabling redirection will help to prevent the user(s) from copying the captured screen content from the Cloud PC. However, there’s no guarantee that this feature will protect content in all scenarios, for example, where someone takes photography of the screen.

Source: [Microsoft Docs](https://docs.microsoft.com/en-us/azure/virtual-desktop/screen-capture-protection)<br>

## Prerequisites

Only clients that support this feature can connect to a Windows 365 Cloud PC.\
Following clients currently support screen capture protection:

* Windows Desktop Client version 1.2.1672 and above
* macOS client version 10.7.0 and above

\
**Get the Microsoft Remote Desktop client.**<br>

**macOS Client**\
Download the Microsoft Remote Desktop client from the [Mac App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) &#x20;

**Windows Desktop Client** (Supported on Windows 10, Windows 10 IoT Enterprise, and Windows 7)\
Download the Microsoft Remote Desktop client for [Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2068602)\
Download the Microsoft Remote Desktop client for [Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2098960)\
Download the Microsoft Remote Desktop client for [Windows ARM64](https://go.microsoft.com/fwlink/?linkid=2098961)  <br>

## Enable Screen Capture Protection with GPO

Okay, let’s get started! – The very first thing we need to do, is install the GPO administrative templates on our Domain Controller, which adds the Azure Virtual Desktop (**AVD**) settings to Group Policy Management.<br>

Download the [Azure Virtual Desktop administrative templates](https://aka.ms/avdgpo)\
Extract the contents of the downloaded cab file and zip archive.<br>

Copy the “**en-us**” folder and “**terminalserver-avd.admx**” file to the root of either the local or central store.

Group Policy Local Store: “**%windir%PolicyDefinitions**”\
Group Policy Central Store: “**%windir%SYSVOLsysvoldomain.localPoliciesPolicyDefinitions**”

<figure><img src="https://drive.google.com/uc?id=1agdl6Mb7hcuEFSxgeafMdRbrWEkUfv4F" alt=""><figcaption></figcaption></figure>

Open “**Group Policy Management**” and create or modify an existing GPO.

From “**Group Policy Management Editor**” navigate to **Computer Configuration | Policies | Administrative Templates | Windows Components | Remote Desktop Services | Remote Desktop Session Host | Azure Virtual Desktop**

Enable the “**Enable screen capture protection**” setting. – Don’t forget to link the GPO to the correct OU.

<figure><img src="https://drive.google.com/uc?id=1ktVg4o0Ju5-3eAVBRa2id5xwYCQNYgjL" alt=""><figcaption></figcaption></figure>

Now you just wait for the GPO to be applied on the Windows 365 Cloud PC or if you have local administrator privileges you can open Command Prompt in administrator elevated mode, and run the following command: “**gpupdate /force**”.

Open “**Registry Editor**” and navigate to “**HKLM:SOFTWAREPoliciesMicrosoftWindows NTTerminal Services**” and check that “**fEnableScreenCaptureProtect**” with value “**1**” exists.

Restart your Windows 365 Cloud PC.

<figure><img src="https://drive.google.com/uc?id=1MOVZ4wSay2aHldC8iAjJxCuj2X51bzwt" alt=""><figcaption></figcaption></figure>

The next time you try to capture the screen, the result should be a black window. Awesome, it works!

<figure><img src="https://drive.google.com/uc?id=1oRxrQw8eqyGqNGKUltd26wPvcXFd4YNX" alt=""><figcaption></figcaption></figure>

## Enable Screen Capture Protection with PowerShell

Now, let’s do it the PowerShell way.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
The proactive remediation script can be found in my [GitHub Repository](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/ProactiveRemediation)

Click on **Reports | Endpoint analytics | Proactive remediations | Create script package**.

<figure><img src="https://drive.google.com/uc?id=1hzQprZcJJQdrQYhn0CfnG8bJWt1OAmEB" alt=""><figcaption></figcaption></figure>

Fill in the required field and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1J_jnlISgP7o-1UeDFxUKa3sK61nKA2oJ" alt=""><figcaption></figcaption></figure>

Add the detection and remediation script, leave the rest as is and click **Next**.\
Set scope tags if needed and click **Next**.

<figure><img src="https://drive.google.com/uc?id=10enXaX_ynrITGTQoByG8sM4zJyFJewdA" alt=""><figcaption></figcaption></figure>

Assign it to a security group containing all or some of your Windows 365 Cloud(s).\
Click on the three dots to modify the schedule.\
Click **Apply** when you are done, and then click **Next**.

<figure><img src="https://drive.google.com/uc?id=1AoTcg152D8emRor5PkvaAYKN0LudHsZI" alt=""><figcaption></figcaption></figure>

Review your configuration and click **Create**.

<figure><img src="https://drive.google.com/uc?id=1ML39ugSdWkMWVPpTOrp-LOohEsgvHT0G" alt=""><figcaption></figcaption></figure>

After a while, the screen capture protection will be enabled on the Windows 365 Cloud PC, now set by the PowerShell script.

<figure><img src="https://drive.google.com/uc?id=1kOLhE6whK1haHN9tUcTnhmuB8n1uKu7A" alt=""><figcaption></figcaption></figure>

And once again, we can confirm that the end result is a black window, if we try to capture the screen.

<figure><img src="https://drive.google.com/uc?id=1BXX5Jd6psUKDum78T0a5u6xRItbYGDHo" alt=""><figcaption></figcaption></figure>

## Limitations and known issues

* This feature protects the Remote Desktop window from being captured through a specific set of public operating system features and APIs. However, there’s no guarantee that this feature will strictly protect content, for example, where someone takes photography of the screen.
* Customers should use the feature together with disabling clipboard, drive, and printer redirection. Disabling redirection will help to prevent the user from copying the captured screen content from the remote session.
* Users can’t share the Remote Desktop window using local collaboration software, such as Microsoft Teams, when the feature is enabled. If Microsoft Teams is used, both the local Teams app and Teams running with media optimizations can’t share the protected content.

Source: [Microsoft Docs](https://docs.microsoft.com/en-us/azure/virtual-desktop/screen-capture-protection)\
\
**Important note.** Please keep in mind that screen capture protection is only supported on Windows Desktop and macOS clients. This means that if you enable this feature, you will not be able to connect to your Windows 365 Cloud PC(s) from the web portal or other platforms (at least for now).

If screen capture protection is enabled, and you are trying to connect to a Windows 365 Cloud PC from the web portal, you will receive a message similar to the one below.

<figure><img src="https://drive.google.com/uc?id=16PHM6ALIVafHwcOtiOP2YWzIjXfIx3us" alt=""><figcaption></figcaption></figure>

## Summary

In this blog post you have learned how to enabled screen capture protection on your Windows 365 Cloud PC(s) with either GPO or proactive remediation script from Microsoft Endpoint Manager admin center.\
\
Personally I would very much appreciate if it was possible to set this setting through a configuration profile within Microsoft Endpoint Manager Intune (I haven’t found it yet, but please correct me if it already exists). And then it would be nice to see support for screen capture protections on other platforms in the near future or at least come up with a more user-friendly message than just “**Disconnected**” if you from the web portal are trying to connect to a Windows 365 Cloud PC where screen capture protection has been enabled.\
\
That was the final words. – Happy testing!\
As always, if you have any questions regarding this topic, feel free to reach out to me.
