---
description: 01-06-2023 7:55 PM
cover: ../../.gitbook/assets/logo_new.png
coverY: -1.4492254733218637
---

# Fix the Hyper-V virtual switches after updating to Windows 11 (22H2)

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

## Introduction

Are you running Hyper-V on your Windows 11 device, and are the virtual switches broken after installing the Windows 11 version 22H2 feature update? – Then read this small post, as it might help you fix the issue.\
\
Last night I noticed that the Windows 11 version 22H2 feature update was available on a device that I use for pretty much everything in my daily life, including a Hyper-V lab environment. So, I went ahead and installed the feature update, and everything seemed to be okay afterward (Phew! What a relief…). But that was until I turned on my lab environment and noticed that none of my VMs had Internet connectivity.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/02-1.png" alt="Windows 11 version 22H2."><figcaption></figcaption></figure>

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/01-1024x576.png" alt="VM with no internet connectivity."><figcaption></figcaption></figure>

## Okay, what’s going on with those virtual switches?

So, the first thing I had to confirm was that the virtual switches had not been changed or deleted during the feature update, and thank goodness, it turned out that they were still present in Hyper-V Manager.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/02.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure>

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/04-1024x978.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure>

Okay, what’s going on then? – Well, let’s find out! Luckily, this is not my only lab environment! So, I started an investigation by comparing the virtual switches with those in another lab environment, which led to the discovery of a switch extension called “**Microsoft Azure VFP Switch Filter Extension**“.\
\
I suspect that the feature update has caused the “**Microsoft Azure VFP Switch Filter Extension**” to be enabled!

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/05.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure>

{% hint style="info" %}
&#x20;**Note:** In Windows Server 2016, HNVv2 is implemented using the Azure Virtual Filtering Platform (VFP) which is a NDIS filtering extension within the Hyper-V Switch. – [**See the Hyper-V Network Virtualization Technical Details in Windows Server**](https://learn.microsoft.com/en-us/windows-server/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server)
{% endhint %}

## How to fix the broken virtual switches

The fix is pretty easy! Just untick the **Microsoft Azure VFP Switch Filter Extension** for each virtual switch.\
\
Type **Hyper-V** in the search line next to the start button and click **Hyper-V Manager**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/06.png" alt="Hyper-V Manager."><figcaption></figcaption></figure>

Next, right-click on the **Hyper-V Server** and select **Virtual Switch Manager…**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/07-1024x544.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure>

Expand the **Virtual Switches** and select **Extensions**.\
Untick the **Microsoft Azure VFP Switch Filter Extension** and click **OK**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/08.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure>

Click **Yes** if you see the below warning.

<div align="left"><figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/09_new.png" alt="Hyper-V Virtual Switches."><figcaption></figcaption></figure></div>

Now, reboot your VMs, and that’s it! – Everything should now function as normal again. Awesome!

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/10-1024x576.png" alt="VM with internet connectivity."><figcaption></figcaption></figure>

## Bonus info – Re-enable the processor resource control feature

After installing the feature update, I noticed that the feature **processor resource control** had been disabled.

{% hint style="info" %}
&#x20;**Note:** Hyper-V host CPU resource controls introduced in Windows Server 2016 or later allow Hyper-V administrators to better manage and allocate host server CPU resources between the “root”, or management partition, and guest VMs. – [**See the Hyper-V Host CPU Resource Management**](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016)
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/11.png" alt="Hyper-V VM settings."><figcaption></figcaption></figure>

Run the below command if you want to re-enable this feature.

```
bcdedit /set hypervisorschedulertype classic
```

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/12-1024x576.png" alt="Enable processor resource controls feature."><figcaption></figcaption></figure>

Reboot the device hosting your Hyper-V environment to complete the re-enablement of this feature.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2022/09/13.png" alt="Hyper-V VM settings."><figcaption></figcaption></figure>

## Summary

In this blog post, you learned how to fix your Hyper-V virtual switches if they broke during the Windows 11 version 22H2 feature update.\
\
I hope this can help others, so they don’t have to spend time investigating this issue.\
\
That’s it, folks. Happy fixing!\
If you have any questions regarding this topic, please feel free to reach out to me.
