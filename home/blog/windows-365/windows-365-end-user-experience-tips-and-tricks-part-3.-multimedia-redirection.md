---
description: 02-06-2023 2:06 PM
cover: ../../.gitbook/assets/Part3.jpg
coverY: 13
---

# Windows 365 End-User Experience (Tips & Tricks) – Part 3. Multimedia Redirection

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

Welcome to **Part 3** in this new **Windows 365 End-User Experience** blog series. This series will be an educational journey exploring several features that can potentially help improve the end-user experience.\
\
**Below you’ll find all parts of this blog series.**

* [Windows 365 End-User Experience (Tips & Tricks) – Part 1. Connection Experience](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-1.-connection-experience)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 2. Teams Optimization, SSO, and Localization](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization)
* [**Windows 365 End-User Experience (Tips & Tricks) – Part 3. Multimedia Redirection**](windows-365-end-user-experience-tips-and-tricks-part-3.-multimedia-redirection.md)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 4. Windows 365 app and Cloud PC reporting](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting)

**In this part, I’ll cover the following topics.**

* [**Multimedia Redirection (MMR)**](windows-365-end-user-experience-tips-and-tricks-part-3.-multimedia-redirection.md#mmr)

## Multimedia Redirection (MMR) <a href="#mmr" id="mmr"></a>

Let’s face it, video playback on Windows 365 Cloud PCs is not a smooth experience without multimedia redirection (MMR). This is because media content is rendered once on the Cloud PC and then again on the local endpoint. However, you’ll get that smooth video playback with MMR when watching videos in a supported browser on your Cloud PC. MMR makes this possible because it redirects the media content from the Cloud PC to your local endpoint for faster processing and rendering.

In the following two video samples, you can clearly see a difference.

**Multimedia redirection is disabled.**\
**Quality**: 1080p

{% embed url="https://youtu.be/5l3CHr0qAW4" %}

**Multimedia redirection is enabled.**\
**Quality**: 1080p

{% embed url="https://youtu.be/gVj26jppTtk" %}

{% hint style="info" %}
&#x20;**Note:** Both **Microsoft Edge** and **Google Chrome** support multimedia redirection.
{% endhint %}

MMR for Windows 365 Cloud PCs is only available for Windows 11, Windows 10, or Windows 10 IoT Enterprise devices and requires one of the following clients.

* Windows 365 app for Windows through the Microsoft Store
* Remote Desktop client for Windows, version 1.2.3916 or later

{% hint style="warning" %}
&#x20;**Required components for Multimedia Redirection to work.**\
– Microsoft Visual C++ Redistributable 2015-2022 version 14.32.31332.0 or later\
– Remote Desktop Multimedia Redirection Service (aka the MMR host MSI installer)\
– Multimedia redirection browser extension for Microsoft Edge or Google Chrome \*\*
{% endhint %}

_\*\* Installing the **Remote Desktop Multimedia Redirection Service** also installs the browser extension._

### **Websites that work with multimedia redirection**

For now, MMR works by default with the following websites.

<table data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><p></p><ul><li>AnyClip</li><li>AWS Training</li><li>BBC</li><li>Big Think</li><li>Bleacher Report</li><li>Brightcove</li><li>CNBC</li><li>Coursera</li><li>Daily Mail</li><li>Facebook</li><li>Fidelity</li><li>Flashtalking</li><li>Fox Sports</li><li>Fox Weather</li><li>IMDB</li></ul></td><td></td><td></td></tr><tr><td><p></p><ul><li>Infosec Institute</li><li>LinkedIn Learning</li><li>Microsoft Learn</li><li>Microsoft Stream</li><li>NBC Sports</li><li>The New York Times</li><li>Pluralsight</li><li>Politico</li><li>Reddit</li><li>Reuters</li><li>Skillshare</li><li>The Guardian</li><li>Twitch</li><li>Twitter</li><li>Udemy</li></ul></td><td></td><td></td></tr><tr><td><p></p><ul><li>UMU</li><li>U.S. News</li><li>Vidazoo</li><li>Vimeo</li><li>The Wall Street Journal</li><li>Yahoo</li><li>Yammer</li><li>YouTube (including sites with embedded YouTube videos).</li></ul></td><td></td><td></td></tr></tbody></table>

{% hint style="info" %}
&#x20;**Note:** A new feature is in beta that enables video playback for all sites.\
\
See [**Enable video playback for all sites | Microsoft Learn**](https://learn.microsoft.com/en-us/azure/virtual-desktop/multimedia-redirection?tabs=edge#enable-video-playback-for-all-sites)
{% endhint %}

{% hint style="info" %}
&#x20;**Tip:** Did you know that Microsoft Teams live events aren’t media optimized for Windows 365 Cloud PCs when using the native Teams app? However, if you use Teams live events with a supported browser, MMR is a workaround that provides smoother Teams live events playback on Cloud PCs.\
\
_&#x53;ource:_ [_**Microsoft Learn**_](https://learn.microsoft.com/en-us/azure/virtual-desktop/multimedia-redirection?tabs=edge#teams-live-events)
{% endhint %}

### **Multimedia redirection status icons**

You can check MMR status by visiting a website with media content that works with MMR. To see the status hover your mouse cursor over the multimedia redirection extension icon in your browser. A message will appear and tell you about the current MMR status, as shown in the following screenshot.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-mouse-hover-2-1024x619.png" alt="Windows 365 - Multimedia redirection"><figcaption></figcaption></figure>

You’ll see one of these icon states when visiting a website in your browser.

<table><thead><tr><th width="139">Icon</th><th>Description</th></tr></thead><tbody><tr><td><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-extension-unsupported.png" alt="" data-size="original"></td><td>A greyed-out icon means that multimedia content on the website can’t be redirected or the extension isn’t loading.</td></tr><tr><td><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-extension-disconnect-1.png" alt="" data-size="original"></td><td>The red square with an “X” inside of it means that the client can’t connect to multimedia redirection. You may need to uninstall and reinstall the extension, then try again.</td></tr><tr><td><img src="../../.gitbook/assets/mmr-extension-supported.png" alt="" data-size="original"></td><td>The default icon appearance with no status applied. This icon state means that multimedia content on the website can be redirected and is ready to use.</td></tr><tr><td><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-extension-playback.png" alt="" data-size="original"></td><td>The green square with a play button icon inside of it means that the extension is currently redirecting video playback.</td></tr><tr><td><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-extension-webrtc.png" alt="" data-size="original"></td><td>The green square with a phone icon inside of it means that the extension is currently redirecting a WebRTC call.</td></tr></tbody></table>

Clicking on the MMR icon in your browser will display a menu listing the features supported on the current website. For example, you can enable or disable video playback for all sites (beta) and collect logs. It also lists the version numbers for each component of the service.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr-settings-1-1024x619.png" alt="Windows 365 - Multimedia redirection"><figcaption></figcaption></figure>

### **Use multimedia redirection on Windows 365 Cloud PCs**

Like with Microsoft Teams optimization, all necessary components for multimedia redirection to work are already included in the Windows 365 gallery images. So it should work on a newly provisioned Windows 365 Cloud PC, right? – Nope! The thing is that the components built into the gallery image need to be updated for MMR to function as intended!\
\
Let’s examine a real-life example where I sign in to a newly provisioned Windows 365 Cloud PC and notice the outdated and missing components. Next, I’ll show you how we comply with the minimum version requirements listed on Microsoft Learn.\
\
Sign in to the Windows 365 Cloud PC and open the Microsoft Edge browser.\
Go to [**edge://extensions**](edge://extensions)

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr01-1024x627.png" alt="Windows 365 - Installed Extensions"><figcaption></figcaption></figure>

That’s weird because I expected the MMR extension to be part of the Windows 365 gallery image.\
Oh, well. – Let’s install it manually!\
\
Open one of the following links in your browser, depending on which browser you’re using.

* For Microsoft Edge: [**Microsoft Multimedia Redirection Extension**](https://microsoftedge.microsoft.com/addons/detail/wvd-multimedia-redirectio/joeclbldhdmoijbaagobkhlpfjglcihd)
* For Google Chrome: [**Microsoft Multimedia Redirection Extension**](https://chrome.google.com/webstore/detail/wvd-multimedia-redirectio/lfmemoeeciijgkjkgbgikoonlkabmlno)

Click **Get**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr02-1024x627.png" alt="Windows 365 - Installed Extensions"><figcaption></figcaption></figure>

Hmm… It turns out that a policy is blocking this extension from being installed.\
Please take note of the App ID, as we need it later when we add it to an allowlist in a Microsoft Edge policy.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr03-1024x627.png" alt="Windows 365 - Extension Blocked"><figcaption></figcaption></figure>

#### **Security baseline and extension allowlist**

I began examining which policy in my tenant blocked Microsoft Edge extensions. Eventually, I came across my **Windows 365 Security Baseline** and discovered it is configured to block all extensions by default.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr04-1024x422.png" alt="Microsoft Intune - Security Baseline"><figcaption></figcaption></figure>

At this point, I knew I had to modify the security baseline or add the MMR extension App ID to an allowlist in my current Microsoft Edge device configuration profile.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr05-1024x436.png" alt="Microsoft Intune - Security Baseline"><figcaption></figcaption></figure>

After adding the MMR extension App ID to the allowlist in my Microsoft Edge policy, I waited a few minutes before attempting the MMR extension installation again.\
\
Once applied, I could successfully install the MMR extension on my Windows 365 Cloud PC.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr06-1024x634.png" alt="Windows 365 - Add Extension"><figcaption></figcaption></figure>

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr07-1024x634.png" alt="Windows 365 - Add Extension"><figcaption></figcaption></figure>

Unfortunately, I received the following status when I tested the multimedia redirection on YouTube afterward.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr08-1024x576.png" alt="Windows 365 - Video redirection failed."><figcaption></figcaption></figure>

#### **Prehistoric (outdated version) multimedia redirection components**

After further investigation, I discovered that the required components were older than the minimum requirements and the latest available online. It’s worth noting that Microsoft Learn only specifies a minimum version for the **Microsoft Visual C++ Redistributable 2015-2022** component and the **Remote Desktop client**, not for the **Remote Desktop Multimedia Redirection Service (also known as the MMR host MSI installer)** component.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr09-1024x627.png" alt="Windows 365 - Old components."><figcaption></figcaption></figure>

Out of curiosity, I chose to update the pre-installed **MsMmrHostMsi**. Unfortunately, it resulted in the removal of the MMR extension, which I had to reinstall again afterward. – But it solved the issue!

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr11-1024x576.png" alt="Windows 365 - Video is redirected."><figcaption></figcaption></figure>

The following screenshot shows that the **Remote Desktop Multimedia Redirection Service** replaced the **MsMmrHostMsi**. However, the **Microsoft Visual C++ Redistributable 2015-2022** version still does not comply with the minimum requirements listed on Microsoft Learn.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr10-1-1024x602.png" alt="Windows 365 - Components updated."><figcaption></figcaption></figure>

{% hint style="info" %}
&#x20;**Note:** I recommend updating the **Microsoft Visual C++ Redistributable 2015-2022** to the latest version to resolve other known issues.\
\
See [**Known issues and limitations | Microsoft Learn**](https://learn.microsoft.com/en-us/azure/virtual-desktop/troubleshoot-multimedia-redirection#known-issues-and-limitations)
{% endhint %}

Oh man, I’m exhausted already! So how can we simplify the following task from Microsoft Intune?

* Install the Remote Desktop Multimedia Redirection Service.
* Add the MMR extension App ID to the Microsoft Edge allowlist.
* Automatically install the MMR extension without user interaction but let the end-user disable it.

### **Simplify the multimedia redirection configuration from Microsoft Intune.**

Let’s look at how I simplified those tasks in my Microsoft Intune tenant. First, we’ll look at the app deployment and then the Microsoft Edge policy.

{% hint style="warning" %}
&#x20;**Important:** Before continuing, please download the [**Remote Desktop Multimedia Redirection Service**](https://aka.ms/avdmmr/msi) .MSI file.
{% endhint %}

#### **Deploy the multimedia redirection app through Microsoft Intune**

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Apps | Windows**\
Click **Add**.\
Select the **Line-of-business app** in the app type drop-down menu and click **Select**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_App01-1-1024x527.png" alt="Microsoft Intune - App deployment"><figcaption></figcaption></figure>

Click **Select app package file** on the **App information** page, choose the Remote Desktop Multimedia Redirection Service .MSI file, and click **OK**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_App02-1024x490.png" alt="Microsoft Intune - App deployment"><figcaption></figcaption></figure>

Fill in the required **Publisher** field.\
Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_App03-1024x935.png" alt="Microsoft Intune - App deployment"><figcaption></figcaption></figure>

On the **Assignments** page, we configure this to be a required deployment. Select **Add all devices** and a filter to include only Windows 365 Cloud PCs.\
Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_App04-1024x683.png" alt="Microsoft Intune - App deployment"><figcaption></figcaption></figure>

Review the configuration and click **Create**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_App05-1018x1024.png" alt="Microsoft Intune - App deployment"><figcaption></figcaption></figure>

This configuration ensures that the Remote Desktop Multimedia Redirection Service will replace the pre-installed **MsMmrHostMsi**. So, let’s move on to the Microsoft Edge policy.

#### **Deploy the Microsoft Edge policy from Microsoft Intune**

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Devices | Windows | Configuration profiles**\
Click **Create profile**.\
Select **Windows 10 and later** in the platform drop-down menu.\
Select **Settings catalog** in the profile type drop-down menu and click **Create**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify01-1024x644.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

On the **Basics** page, fill in the required **Name** field. Although the **Description** field is optional, I recommend filling it out.

{% hint style="info" %}
&#x20;**Tip:** Leaving some breadcrumbs is always a great idea, so others know precisely why someone created the configuration profile.
{% endhint %}

Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify02-1024x555.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

#### **Extension management settings**

Click **Add settings** on the **Configuration settings** page and search for **Microsoft Edge** in the **Settings picker**.\
Choose **Microsoft Edge\Extensions**, and select the following two settings.

* **Allow specific extensions to be installed**
* **Configure extension management settings**

{% hint style="warning" %}
&#x20;**Important:** By configuring the **extension management settings**, end users can disable the extension, which can be particularly useful when switching between Windows and macOS endpoints.\
\
Remember that multimedia redirection is only available for Windows 11, Windows 10, or Windows 10 IoT Enterprise devices.
{% endhint %}

Close the **Settings picker**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify03-1024x635.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

Enable both settings and add the extension App ID “**joeclbldhdmoijbaagobkhlpfjglcihd”** to the allowlist.\
Next, add the following compact JSON data string to the **Configure extension management settings** field.

```
Example JSON data:
------------------
{
   "joeclbldhdmoijbaagobkhlpfjglcihd": {
     "installation_mode": "normal_installed",
     "update_url": "https://edge.microsoft.com/extensionwebstorebase/v1/crx"
   }
}

Compact JSON data:
------------------
{"joeclbldhdmoijbaagobkhlpfjglcihd":{"installation_mode":"normal_installed","update_url":"https://edge.microsoft.com/extensionwebstorebase/v1/crx"}}
```

Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify04-1-1024x892.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

Select scope tags if needed and click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify05-1024x607.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

On the **Assignments** page, select **Add all devices** and a filter to include only Windows 365 Cloud PCs.\
Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify06-1024x426.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

Review the configuration and click **Create**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/mmr_simplify07-1009x1024.png" alt="Microsoft Intune - Edge Policy"><figcaption></figcaption></figure>

That brings us to the end of the Multimedia Redirection (MMR) section. Throughout this section, we’ve explored how MMR can enhance the video playback experience while watching videos in a supported browser on your Windows 365 Cloud PC. However, we’ve also discovered that the pre-installed components in the Windows 365 gallery image are outdated and require additional steps to be updated. In addition, we also needed a few extra Microsoft Edge configurations to provide a great end-user experience.\
\
That’s it for **Part 3**. Please join me in [**Part 4**](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting), where we’ll explore **Windows 365 app and Cloud PC reporting.**
