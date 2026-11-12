---
description: 19-01-2024 3:55 PM
cover: ../../.gitbook/assets/feature.png
coverY: -79.45767790262171
---

# The Concept of Windows 365 Switch

## BEFORE YOU BEGIN

{% hint style="warning" %}
<mark style="color:orange;">**Disclaimer:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.</mark>
{% endhint %}

In this blog post, I will explore the concept of Windows 365 Switch, a unique feature that became generally available (GA) in September 2023 and allows users to easily move between their local desktop and one of their Cloud PCs from Windows 11 via the Task view feature.

<figure><img src="../../.gitbook/assets/feature.png" alt=""><figcaption></figcaption></figure>

So, buckle up and join me as I explore this relatively new feature to see what the buzz is all about and what Windows 365 Switch adds to the experience. Also, let's look at how easy it is to set up on physical devices.

**In this post, I'll cover the following topics.**

* [**Prerequisites and Requirements**](the-concept-of-windows-365-switch.md#prerequisites-and-requirements)
* [**What is Windows 365 Switch?**](the-concept-of-windows-365-switch.md#what-is-windows-365-switch)
* [**Install the Windows App**](the-concept-of-windows-365-switch.md#install-the-windows-app)
* [**Test and Verification**](the-concept-of-windows-365-switch.md#test-and-verification)
* [**Summary**](the-concept-of-windows-365-switch.md#summary)

## Prerequisites and Requirements <a href="#prerequisites-and-requirements" id="prerequisites-and-requirements"></a>

* Windows 11-based devices (Pro & Enterprise).
* The physical device (and Cloud PCs) must be running Windows 11 version (22621.2361 or later).
* Windows App version (1.3.185.0 or later).
* You must have a Windows 365 Cloud PC license.

## What is Windows 365 Switch? <a href="#what-is-windows-365-switch" id="what-is-windows-365-switch"></a>

Windows 365 Switch lets users switch between their Cloud PC and their local desktop directly from the Windows 11 Task view using the same familiar keyboard commands, a mouse click, or a swipe gesture.

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Keyboard command example:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">Windows logo key 🪟 + Tab</mark>
{% endhint %}

A Windows 365 Cloud PC via the **Windows App** (_formerly known as the Windows 365 App_) is required on the physical device, and from there, Windows 365 Switch will (or it should) show up automatically in the Task view.

<figure><img src="../../.gitbook/assets/byod-bring-your-own-device-line-style_281653-4529.jpg" alt="" width="563"><figcaption></figcaption></figure>

### **What’s New for Windows 365 Switch**

Microsoft announced these new features in the service release 2312:

<details>

<summary><strong>Improved disconnect experience for Windows 365 Switch (preview)</strong></summary>

You can now disconnect from their Cloud PC directly from their local PC. This can be done by going to **Local PC** > **Task view** > **Right click on the Cloud PC button** > **Disconnect**. We have also added tooltips on disconnect and sign-out options in the Cloud PC Start menu so that you can differentiate between these functionalities.

</details>

<details>

<summary><strong>Desktop indicators to differentiate between Cloud PC and local PC for Windows 365 Switch (preview)</strong></summary>

You will now see the term “**Cloud PC**” and “**Local PC**” on the desktop indicator when you switch between your respective PCs.

</details>

<details>

<summary><strong>Gracefully handling increased connection time for Windows 365 Switch to Frontline Cloud PC (preview)</strong></summary>

You will now see updates regarding the Cloud PC connection status and the connection timeout indicator while waiting on the connection screen. In case there is an error, you will now be able to copy the correlation ID using the new copy button in the error screen for quicker resolution.

</details>

Source: [**What’s new in Windows 365 Enterprise**](https://learn.microsoft.com/en-us/windows-365/enterprise/whats-new#windows-365-switch)

### **The Use Case of Windows 365 Switch**

I can definitely see this unique feature as an ideal solution for **bring-your-own-device (BYOD)** scenarios when you connect from your personal-owned Windows device to a secure corporate-owned Cloud PC. Especially in these times when business wants to do more with less, this is a great experience.

## Install the Windows App <a href="#install-the-windows-app" id="install-the-windows-app"></a>

As briefly touched upon in the previous section, there’s not much to it configuration-wise! We must ensure that the physical device (and Cloud PCs) meets the Windows 365 Switch requirements and then install the Windows App. – And that’s it! Easy, huh?

### **Follow these steps to set up your physical devices for Windows 365 Switch.**

First, we must verify that the physical device is on the latest Windows 11 build version.\
Go to **System** and verify that Windows 11 is running version (22621.2361 or later).

<figure><img src="../../.gitbook/assets/W365_Switch_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_02.png" alt=""><figcaption></figcaption></figure>

Next, we’ll go to the Microsoft store and install the latest version of the Windows App.

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Note:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">The</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**Windows App**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">can, of course, also be delivered via</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**Microsoft Intune.**</mark>
{% endhint %}

Go to the **Microsoft Store** and search for the **Windows App.**\
Select the **Windows App** from the search overview and click **Install.**

<figure><img src="../../.gitbook/assets/W365_Switch_03.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_04.png" alt=""><figcaption></figcaption></figure>

Once installed, we can go ahead and run the **Windows App.**

<figure><img src="../../.gitbook/assets/W365_Switch_05.png" alt=""><figcaption></figcaption></figure>

We will go quickly through the first run experience.

<table data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/W365_Switch_06.png" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/W365_Switch_07.png" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/W365_Switch_08.png" alt="" data-size="original"></td></tr></tbody></table>

First, let’s verify that the Windows App version meets the minimum requirements.

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Minimum requirement:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">Windows App version (1.3.185.0 or later).</mark>
{% endhint %}

Click **Settings.**

<figure><img src="../../.gitbook/assets/W365_Switch_09.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_10.png" alt=""><figcaption></figcaption></figure>

We seem to meet all the Windows 365 Switch requirements and are now ready to switch between our Cloud PC and the local desktop directly from the Windows Task view feature.

<figure><img src="../../.gitbook/assets/W365_Switch_11.png" alt=""><figcaption></figcaption></figure>

However, as you can see in the screenshot above, our Cloud PC has yet to be added to the Task view!

Now, I’ve seen this happen a couple of times before, and the fix is to choose which Cloud PC to sign in to by selecting the **ellipses (…)** and clicking **Add to Task view.**

Go to **Devices** in the **Windows App.**

<figure><img src="../../.gitbook/assets/W365_Switch_12.png" alt=""><figcaption></figcaption></figure>

Select the **ellipses (…)** and click **Add to Task view.**

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Note:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">The</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**Windows 365 Frontline Cloud PCs**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">are also supported. However,</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**Windows 365 Switch**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">currently only supports one Switch-enabled Cloud PC!</mark>
{% endhint %}

<figure><img src="../../.gitbook/assets/W365_Switch_13.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_14.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_15.png" alt=""><figcaption></figcaption></figure>

Your preferred Windows 365 Cloud PC will now be available via the Windows Task view feature.

In the next section, we’ll verify that we can connect to the Cloud PC from the Task view and easily switch between our local desktop and the Cloud PC.

<figure><img src="../../.gitbook/assets/W365_Switch_16.png" alt=""><figcaption></figcaption></figure>

## Test and Verification <a href="#test-and-verification" id="test-and-verification"></a>

Now, let’s connect to my Cloud PC and verify that everything works as intended. If you have read my blog post about Windows 365 Boot, you will probably notice that the login experience looks similar.

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Note:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">Want to learn more about Windows 365 Boot? See</mark> [<mark style="color:blue;">**The Concept of Windows 365 Boot.**</mark>](https://blog.mindcore.dk/2023/12/the-concept-of-windows-365-boot/)
{% endhint %}

Hover over the Windows **Task view** icon in the taskbar and click on your Cloud PC.

<figure><img src="../../.gitbook/assets/W365_Switch_17.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
&#x20;<mark style="color:blue;">**Tip:**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">You can wait on the Local PC while connecting to your Cloud PC.</mark>
{% endhint %}

<figure><img src="../../.gitbook/assets/W365_Switch_18.png" alt=""><figcaption></figcaption></figure>

Success! We have now connected to the Cloud PC through the Windows Task view feature.

<figure><img src="../../.gitbook/assets/W365_Switch_19.png" alt=""><figcaption></figcaption></figure>

We can now easily switch between our local desktop and the Cloud PC.\
Hover over the Windows **Task view** icon in the taskbar and click **Local desktops** to switch back.

<figure><img src="../../.gitbook/assets/W365_Switch_20.png" alt=""><figcaption></figcaption></figure>

Here is the end-user experience shown in a short GIF.

<figure><img src="../../.gitbook/assets/Windows365Switch.gif" alt=""><figcaption></figcaption></figure>

If you hover over the Windows **Task view** icon in the taskbar and right-click on the Cloud PC, you will be presented with a couple of options. You can, for example, access the **Windows 365 app settings**, **Cloud PC privacy & security settings** or **Disconnect** the connection to your Cloud PC.

<figure><img src="../../.gitbook/assets/W365_Switch_24.png" alt=""><figcaption></figcaption></figure>

If we disconnect, we will return to the local desktop on the physical device.

<figure><img src="../../.gitbook/assets/W365_Switch_22.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/W365_Switch_23.png" alt=""><figcaption></figcaption></figure>

## Summary <a href="#summary" id="summary"></a>

In this blog post, you learned about the concept of Windows 365 Switch and how it can improve the end-user experience. I shared my view on the use case and showed you how easy it is to set up on physical devices.

That’s it, folks. Happy testing, and have fun exploring 🤓\
If you have any questions regarding this topic, please feel free to reach out to me.
