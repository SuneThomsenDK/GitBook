---
description: 02-06-2023 10:08 AM
cover: ../../.gitbook/assets/Part2.jpg
coverY: 8
---

# Windows 365 End-User Experience (Tips & Tricks) – Part 2. Teams Optimization, SSO, and Localization

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

Welcome to **Part 2** in this new **Windows 365 End-User Experience** blog series. This series will be an educational journey exploring several features that can potentially help improve the end-user experience.\
\
**Below you’ll find all parts of this blog series.**

* [Windows 365 End-User Experience (Tips & Tricks) – Part 1. Connection Experience](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-1.-connection-experience)
* [**Windows 365 End-User Experience (Tips & Tricks) – Part 2. Teams Optimization, SSO, and Localization**](windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization.md)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 3. Multimedia Redirection](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-3.-multimedia-redirection)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 4. Windows 365 app and Cloud PC reporting](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting)

**In this part, I’ll cover the following topics.**

* [**Microsoft Teams Optimization**](windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization.md#teamsoptimization)
* [**Azure AD Join Single Sign-on (SSO)**](windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization.md#sso)
* [**Localized Windows 365 Experience**](windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization.md#localization)

## Microsoft Teams Optimization <a href="#teamsoptimization" id="teamsoptimization"></a>

Windows 365 uses media optimization provided by Azure Virtual Desktop (AVD). This optimization ensures a great Microsoft Teams experience from the Windows 365 Cloud PCs. In other words, with media optimization for Microsoft Teams, the Remote Desktop client or the Windows 365 app handles audio and video locally for Teams calls and meetings by redirecting and rendering it directly onto the physical endpoint, which ensures that the audio and video quality remains high and avoids latency issues that may arise due to the Cloud PCs’ virtual nature.

{% hint style="info" %}
&#x20;**Note:** Using Microsoft Teams on a Cloud PC differs from using it on a physical endpoint. Therefore, you must read about the requirements and limitations to provide the best Microsoft Teams experiences from Cloud PCs.\
\
See [**Microsoft Teams on Cloud PCs | Microsoft Learn**](https://learn.microsoft.com/en-us/windows-365/enterprise/teams-on-cloud-pc)
{% endhint %}

The Windows 365 gallery images with pre-installed Microsoft 365 Apps already include Microsoft Teams and the optimization components. So there is actually nothing to configure. – It just works!

{% hint style="warning" %}
&#x20;**Important:** If you create custom images for your Windows 365 Cloud PCs, you need additional steps to ensure your image has the correct registry configuration and includes the optimization components.\
\
See [**Create a custom Cloud PC image to support Microsoft Teams | Microsoft Learn**](https://learn.microsoft.com/en-us/windows-365/enterprise/create-custom-image-support-teams)
{% endhint %}

To verify that the registry setting and optimization components are up to date and included in the image, you can check the **Registry Editor** and **Installed apps** on the Cloud PC.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/MSTeamsOptimization02-1024x732.png" alt="Windows 365 - Teams Optimization Registry"><figcaption></figcaption></figure>

{% hint style="warning" %}
&#x20;**Required components for Microsoft Teams optimizations to work.**\
– The latest version of the Microsoft Visual C++ Redistributable 2015-2022\
– The latest version of the Remote Desktop WebRTC Redirector Service
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/02/MSTeamsOptimization03-1024x728.png" alt="Windows 365 - Teams Optimization Components"><figcaption></figcaption></figure>

We can confirm that Microsoft Teams is media optimized by clicking on the **ellipsis (…)** **|** **About |** **Version**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/02/MSTeamsOptimization01-1024x701.png" alt="Windows 365 - Teams Optimized"><figcaption></figcaption></figure>

### **Remote Desktop WebRTC Redirector Service**

The Remote Desktop WebRTC Redirector Service client is a critical component in optimizing the Microsoft Teams experience on Windows 365 Cloud PCs. That’s because it facilitates peer-to-peer streaming (Audio/Video) and renders it directly onto the endpoints.\
\
Unfortunately, the WebRTC Redirector Service is not updated automatically, which can result in customers having older versions of the client in their production – and thereby a degraded end-user experience. In addition, upgrading this client will cause the Microsoft Teams application to restart automatically, disrupting the end users who are using Teams at the installation time.\
\
[**Donna Ryan**](https://twitter.com/TheNotoriousDRR), a Senior PM at Microsoft, has created a scripted solution to resolve these challenges by detecting both the latest and installed versions of the Remote Desktop WebRTC Redirector Service client. Then, if an upgrade is required, the script automatically downloads and installs the latest version. – However, the script detects whether the user state is active or disconnected and only installs the upgrade when the user state is disconnected – avoiding end-user disruption.

{% hint style="info" %}
&#x20;**Note:** You can find the **WebRTC Auto Updater** scripts in Donna’s [**GitHub repository**](https://github.com/microsoft/Windows365-PSScripts/tree/main/WebRTC%20Auto%20Updater)**.**
{% endhint %}

Media optimization for Microsoft Teams is only available for the Windows and macOS endpoints and requires one of the following clients.

* Windows 365 app for Windows through the Microsoft Store
* Remote Desktop client for Windows, version 1.2.1026.0 or later
* Remote Desktop client for macOS, version 10.7.7 or later

That concludes the section about Microsoft Teams Optimization. – In this section, we learned that the Windows 365 gallery images with pre-installed Microsoft 365 Apps include Microsoft Teams and the optimization components. We also learned that the Remote Desktop WebRTC Redirector Service client is a critical component in optimizing the Microsoft Teams experience that needs to be kept up to date, which we can accomplish through a scripted solution like Donna’s **WebRTC Auto Updater**.

## Azure AD Join Single Sign-on (SSO) <a href="#sso" id="sso"></a>

Single Sign-on (SSO) is one of those pieces of the puzzle that provide the end users with the best possible sign-in experience on their Windows 365 Cloud PCs.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/02/logo-1024x575.jpeg" alt="Azure AD Join Single Sign-on"><figcaption></figcaption></figure>

You might be thinking, why is SSO support that interesting? It’s interesting because until recently, the user had to sign in twice, first to the Windows 365 service and then again to their Windows 365 Cloud PC, either through the Web Portal, the Remote Desktop client, or the Windows 365 app.\
\
To know more about this topic, see [**Configuring Windows 365 Azure AD Join Single Sign-on (SSO).**](https://www.osdsune.com/home/blog/windows-365/how-to-configure-windows-365-azure-ad-join-single-sign-on-sso)

## Localized Windows 365 Experience <a href="#localization" id="localization"></a>

A localized Windows 365 experience is very important for some users to be productive. Configuring the language and region settings in the Windows 365 provisioning policy will provide those users with a great experience when they see a familiar language immediately at first sign-in.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/02/Localized01-1-1024x575.png" alt="PowerShell - Culture and TimeZone"><figcaption></figcaption></figure>

To know more about this topic, see [**Providing end users with a localized Windows 365 experience.**](https://www.osdsune.com/home/blog/windows-365/provide-the-end-users-with-a-localized-windows-365-cloud-pc-experience)\
\
That’s it for **Part 2**. Please join me in [**Part 3**](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-3.-multimedia-redirection), where we explore **Multimedia Redirection (MMR)**.
