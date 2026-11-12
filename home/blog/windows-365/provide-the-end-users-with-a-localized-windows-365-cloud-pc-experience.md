---
description: 31-05-2023 9:11 PM
cover: ../../.gitbook/assets/logo.png
coverY: -240
---

# Provide the end-users with a localized Windows 365 Cloud PC experience

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

## Introduction

A few months back, I wrote a post about [localizing a custom image for Windows 365 Cloud PCs.](https://www.osdsune.com/home/blog/2021/how-to-create-a-custom-image-for-windows-365-enterprise-cloud-pcs) Back then, the Windows 365 Cloud PCs were only provisioned in English (United States). – Microsoft has since then made it possible to configure the language and region directly in the provisioning policy, with support for more than 30 languages.\
\
Some users prefer that Windows is in a language they are comfortable with to be productive. – Configuring the language and region settings in the provisioning policy will provide those users with a great experience when they see the correct language immediately at first sign-in.\
\
So with that in mind, in this article, I will show you how to configure the language, region, and time zone of your Windows 365 Cloud PCs. – Let’s get started!\
\
Read about the prerequisites and requirements for Windows 365 Cloud PCs in our original blog post here – [How to configure Windows 365 Enterprise in Microsoft Endpoint Manager.](https://www.osdsune.com/home/blog/2021/configure-windows-365-enterprise)

## Configure Language and Region

First, let’s visit the Microsoft Endpoint Manager Admin center and change the language and region settings within my current provisioning policy from English (United States) to Danish (Denmark).\
\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
Click **Devices | Windows 365 | Provisioning policies**   \
Create a new policy or select an existing policy in the list of provisioning policies. – For this article, I chose to modify my current provisioning policy.

<figure><img src="https://drive.google.com/uc?id=1RqUv4rBspTwq2Pz1WDINhY8D-KWMKsn0" alt=""><figcaption></figcaption></figure>

On the overview page, look for **Configuration** and click **Edit.**

<figure><img src="https://drive.google.com/uc?id=1d9hP0Ok8hkXgxCL2H18WvPMOPFXQw1b2" alt=""><figcaption></figcaption></figure>

Change the **Language & Region (preview)** from English (United States) to the language of your preference. For example, I chose Danish (Denmark).

<figure><img src="https://drive.google.com/uc?id=1j-bp-lWTwXDt7zr8XrLDbxwuZa7ek_En" alt=""><figcaption></figcaption></figure>

Click **Next.**

<figure><img src="https://drive.google.com/uc?id=1L9fg7fkLnnK20DIfpLydjrjc8hmuKm80" alt=""><figcaption></figcaption></figure>

Click **Update.**

<figure><img src="https://drive.google.com/uc?id=15w2G6uF3L2t16b8L7EfVTiBjJDC5Ob_Y" alt=""><figcaption></figcaption></figure>

From **Devices | Windows 365,** click the **All Cloud PCs** tab.\
\
If you are provisioning a new Cloud PC, it will show in the list after approx. 20-30 minutes.\
Otherwise, select an existing Cloud PC to reprovision. – For this article, I chose to reprovision an existing Cloud PC.

<figure><img src="https://drive.google.com/uc?id=1vwC4fEhLzxJajMQqGkiuqZ8JN2T4nh0x" alt=""><figcaption></figcaption></figure>

Click **Reprovision.**\
If all goes well, the Cloud PC should appear in the **All Cloud PCs** list after approx. 20-30 minutes.

<figure><img src="https://drive.google.com/uc?id=1-6rchp3yj6szatElnf4JW8YqjsBFje05" alt=""><figcaption></figcaption></figure>

Let’s sign in to my newly reprovisioned Windows 365 Cloud PC and confirm the configuration changes.\
Go to [https://windows365.microsoft.com](https://windows365.microsoft.com/)\
&#x20;

From a **Windows PowerShell** session, we can confirm that the language and region on my Cloud PC have been configured to Danish (Denmark) and that the time zone is correct.

<figure><img src="https://drive.google.com/uc?id=1otp5u9uz-GCnMfMimjHA_Gbbrvm46_Sk" alt=""><figcaption></figcaption></figure>

We can also confirm this from the **Windows Settings.**

<figure><img src="https://drive.google.com/uc?id=1kbXuWsDf6UqhBsCozNh6MHJ-xycyVyaI" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=1VAQfWXPqtlPotfXnYKmhbBxkA_mGCQL6" alt=""><figcaption></figcaption></figure>

The time zone redirection is enabled by default, allowing clients capable of time zone redirection to send their time zone information to the Windows 365 Cloud PCs.\
&#x20;\
You can go to the below path in the **Registry Editor** on your Windows 365 Cloud PC to confirm that time zone redirection is enabled.

```
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services
```

<figure><img src="https://drive.google.com/uc?id=1kO_UULiuKHfy9qCnkL35EgbsC6LTXhvT" alt=""><figcaption></figcaption></figure>

Success! – We now have a localized Windows 365 Cloud PC.\
But wait, what if the time zone redirection is not configured on my Cloud PC by default? – If that’s the case, continue reading this article.

## Configure Time Zone Redirection

Is time zone redirection not configured on your Cloud PCs by default? No worries! – We can configure that with a device configuration profile or a proactive remediation script.\
\
**We have a couple of options to choose from when it comes to setting the time zone on your Windows 365 Cloud PCs:**

* Let the users change the time zone themselves. – _Possible on Cloud PCs provisioned after April 18, 2022._
* Create a Settings Catalog profile that sets the time zone.
* Create a Settings Catalog profile that configures time zone redirection.
* Create a Custom CSP that sets the time zone.
* Create a Proactive Remediation script that sets the time zone.
* Etc.

{% hint style="info" %}
&#x20;**Tip:** To get a list of available time zones, run **Get-TimeZone -ListAvailable** in PowerShell.
{% endhint %}

Let me show you how to configure the time zone redirection on Windows 365 Cloud PCs.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
Click **Devices | Configuration profiles**\
Click **Create profile.**

<figure><img src="https://drive.google.com/uc?id=1J_ntLycHA8Nd0duoIUx3zvHFQOQwVHyR" alt=""><figcaption></figcaption></figure>

Select **Windows 10 and later** as the platform and **Settings catalog (preview)** as the profile type.\
Click **Create.**

<figure><img src="https://drive.google.com/uc?id=1ohO0qcz6Q93YtySRFdnUmsdTYd_J_se1" alt=""><figcaption></figcaption></figure>

Fill in the required **Name** field. Although the **Description** field is optional, I would recommend filling it out. – It’s always a great idea to leave some breadcrumbs, so others know precisely why someone created the configuration profile.\
\
Click **Next.**

<figure><img src="https://drive.google.com/uc?id=1zpIJguMAxQZx9zEksleJrEf9JKCUSwx_" alt=""><figcaption></figcaption></figure>

Click **Add settings.**\
\
In the **Settings picker**, search for “**time zone redirection**” and select the setting **Allow time zone redirection** in the **Device and Resource Redirection** category.&#x20;

<figure><img src="https://drive.google.com/uc?id=1peBBVa8LBx0u1MAEgziXF8VtMZMQ1ymO" alt=""><figcaption></figcaption></figure>

Enable the setting **Allow time zone redirection.**\
Click **Next.**

<figure><img src="https://drive.google.com/uc?id=1QrmbfMQfMS-aAvqblZnmX2M3mvnVStHg" alt=""><figcaption></figcaption></figure>

Choose either to assign the profile to “All devices/All users” or a group. – I chose to assign this profile to “All users”, and then I’ve added a filter to only include Windows 365 Cloud PCs.\
\
Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1WwRMhbalSu6YZVXe0T4xGM93PS88sXIt" alt=""><figcaption></figcaption></figure>

Click **Next.**

<figure><img src="https://drive.google.com/uc?id=1bfP5tjFzjQ68cOtCHDidouXPUQSB0Baq" alt=""><figcaption></figcaption></figure>

Review the configuration and click **Create.**

<figure><img src="https://drive.google.com/uc?id=1q2mlad3HN5BZYP7utt8U1my1PCWpxcYO" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=1LJUKxViKQwf6fNET0yTO-iF0GzSN2Bgc" alt=""><figcaption></figcaption></figure>

This configuration is all it takes to enable time zone redirection on your Windows 365 Cloud PCs.

## Summary

In this article, you learned how to change the language and region settings of your Windows 365 Cloud PCs. In my provisioning policy, we changed the language and region settings from English (United States) to Danish (Denmark) and confirmed the results on a reprovisioned Cloud PC.\
\
One thing worth mentioning is that, while preparing for this article, I noticed that the Windows 11 welcome screen was in English during the first sign-in, but after a reboot, it was in Danish.\
\
That’s it, folks. Happy testing!\
If you have any questions regarding this topic, please feel free to reach out to me.
