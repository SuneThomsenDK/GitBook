---
description: 30-05-2023 8:46 PM
---

# How to configure Windows 365 Enterprise Azure AD join

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1Yyx_YFfgGrQiJ-BT1T3yP1fIGr98Fdao" alt=""><figcaption><p><em>Windows 365 Enterprise Azure AD join – Microsoft Hosted Network.</em></p></figcaption></figure>

## Introduction

Many of us have been waiting for native Azure AD join for Windows 365 Enterprise since its release in August 2021. But wait no longer! The native Azure AD join support has finally become a reality. In this article, I will guide you through the whole process of how to configure both the **Built in Network** (Referred to as **Microsoft Hosted Network** in this article) and the **On-premises network connection** provisioning policy in the Microsoft Endpoint Manager admin center.\
\
Read about the prerequisites and requirements for Windows 365 Enterprise Cloud PC and how to configure **Hybrid Azure AD join** in the original blog post here – [How to configure Windows 365 Enterprise in Microsoft Endpoint Manager.](https://www.osdsune.com/home/blog/2021/configure-windows-365-enterprise)

## Azure AD join (Microsoft Hosted Network)

First, let’s configure the **Microsoft Hosted Network** provisioning policy by visiting the Microsoft Endpoint Manager admin center. The Cloud PCs based on this policy will be Azure AD joined, and they will run in a network hosted by Microsoft, which is perfect for cloud-only customers without an Azure or on-premises infrastructure.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
Click **Devices | Windows 365 | Provisioning policies**

<figure><img src="https://drive.google.com/uc?id=1MBfJy5UyaeYqFkbUC1NLKv_umWkgITw9" alt=""><figcaption></figcaption></figure>

Click **Create policy.**

<figure><img src="https://drive.google.com/uc?id=10Q9XzcbDv7woii0JeqYsBQSufqI6n60N" alt=""><figcaption></figcaption></figure>

Fill in the required **Name** field.\
Choose **Join type**, **Network**, **Region,** and click **Next.**

<figure><img src="https://drive.google.com/uc?id=1-geCv1_ZocITPL5Pe9me_7Fr8b3p9Ya2" alt=""><figcaption></figcaption></figure>

Select **Image type** and click **Next.** I chose **Windows 11 Enterprise + Microsoft 365 Apps 21H2** from the **image gallery.**

<figure><img src="https://drive.google.com/uc?id=1ZID3S_gY55tdlXUECgbQFm00_sjyCtoZ" alt=""><figcaption></figcaption></figure>

Add a user-based Azure AD security group containing users eligible for a Windows 365 Enterprise Cloud PC, and click **Next.**

<figure><img src="https://drive.google.com/uc?id=18npE7H0n9SNmQ0fer0vKEL0vZ-3Ridn7" alt=""><figcaption></figcaption></figure>

Review the configuration and click **Create.**

<figure><img src="https://drive.google.com/uc?id=1APdCeZSf8whbuozBxJIUWV7PMhiSGE4x" alt=""><figcaption></figcaption></figure>

From **Devices | Windows 365,** click the **All Cloud PCs** tab.\
If all goes well, the Cloud PCs should appear in the list with the status shown as **Provisioned** after approx. 20-30 minutes.

<figure><img src="https://drive.google.com/uc?id=1ONmFUFssxwG_w8p1bjhAj5X7jcpdmX7j" alt=""><figcaption></figcaption></figure>

Let’s try and sign in to the newly created Azure AD joined Windows 365 Enterprise Cloud PC.   \
Go to [https://windows365.microsoft.com](https://windows365.microsoft.com/)\
&#x20;\
I can confirm from an elevated Command Prompt that the Cloud PC is Azure AD joined, and it’s running in a Microsoft hosted network.

<figure><img src="https://drive.google.com/uc?id=1gd91CGo8HePR60cW2wvA-rjrp3jHUnp5" alt=""><figcaption></figcaption></figure>

## Azure AD join (On-premises network connection)

Next, let’s configure the **On-premises network connection** provisioning policy. The Cloud PCs based on this policy will be Azure AD joined and connected to your Virtual Network, perfect for customers with an existing Azure or on-premises infrastructure that they need to reach from their Cloud PCs for several reasons.\
\
From **Devices | Windows 365,** click the **On-premises network connection** tab.\
Click **Create** and choose **Azure AD join (preview)** in the list.

<figure><img src="https://drive.google.com/uc?id=1ldL8YUrOuUu--WNOtMJeL-0FE8Q85oSO" alt=""><figcaption></figcaption></figure>

Fill in the required **Name** field.\
Choose **Subscription**, **Resource group**, **Virtual network**, **Subnet,** and click **Next.**

<figure><img src="https://drive.google.com/uc?id=178xaXetvHS7grSQH2Fh_gLg9SzAAiSBi" alt=""><figcaption></figcaption></figure>

Review the configuration and click **Review + Create.**

<figure><img src="https://drive.google.com/uc?id=1OvTlny1AQMIKDqbCzaNAR64mtJ4nBzs2" alt=""><figcaption></figcaption></figure>

After approx. 5-10 minutes, we should be able to check the status of the on-premises network connection.\
Luckily for me, everything passed! Next, click the **Provisioning policies** tab.

<figure><img src="https://drive.google.com/uc?id=1fWUf2rYz1Gx5CI1OUGWGpDBK2Bp7svL7" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=18fMKXl7FmuyuV_U2KR7MKLU8Nut4YiFP" alt=""><figcaption></figcaption></figure>

Click **Create policy.**

<figure><img src="https://drive.google.com/uc?id=1iiqiW26IJsrPBToKR2I8WXgiCI8NughR" alt=""><figcaption></figcaption></figure>

Fill in the required **Name** field.\
Choose **Join type**, **Network,** and click **Next.**

<figure><img src="https://drive.google.com/uc?id=1E92wVB4Pvc2uex7JiCXU0VutppKjXuUg" alt=""><figcaption></figcaption></figure>

Select **Image type** and click **Next**.\
Once again, I chose **Windows 11 Enterprise + Microsoft 365 Apps 21H2** from the **image gallery.**

<figure><img src="https://drive.google.com/uc?id=1b8u6SgAGmITXXjKTmETyBXdjqiOlstKH" alt=""><figcaption></figcaption></figure>

Add a user-based Azure AD security group containing users eligible for a Windows 365 Enterprise Cloud PC, and click **Next.**&#x20;

<figure><img src="https://drive.google.com/uc?id=1DkzGENaQCT3Mc5Ek4vx18RMDrXuZnZ6n" alt=""><figcaption></figcaption></figure>

Review the configuration and click **Create.**

<figure><img src="https://drive.google.com/uc?id=1bdsG-iiGs1YkgWUMcrZlrsoekdOx0bUK" alt=""><figcaption></figcaption></figure>

From **Devices | Windows 365,** click the **All Cloud PCs** tab.\
If all goes well, the Cloud PCs should appear in the list with the status shown as **Provisioned** after approx. 20-30 minutes.

<figure><img src="https://drive.google.com/uc?id=1dq3PppP9MyMxAY_YhoNBhRWgot5hvPT0" alt=""><figcaption></figcaption></figure>

Let’s try and sign in to the newly created Azure AD joined Windows 365 Enterprise Cloud PC.\
Go to [https://windows365.microsoft.com](https://windows365.microsoft.com/)\
\
Once again, I can confirm from an elevated Command Prompt that the Cloud PC is Azure AD joined. However, it’s connected to the newly created on-premises network connection, and I can communicate with an on-premises server.

<figure><img src="https://drive.google.com/uc?id=1uPYXrgJ18GYgKA0_gfpgNisVa1Fm5h3d" alt=""><figcaption></figcaption></figure>

## Summary

In this article, you learned how to configure Windows 365 Enterprise Azure AD join based on a **Microsoft Hosted Network** or an **On-premises network connection** provisioning policy in the Microsoft Endpoint Manager admin center.\
\
The capability to provision Windows 365 Enterprise Cloud PCs without the need for a connection to an on-premises domain controller is finally a reality. As already mentioned at the beginning of this article, native Azure AD join is something many of us have been looking forward to for several months, especially cloud-only customers! So this is something that I’m very excited to see available in public preview. – Happy testing, everyone!\
\
As always, if you have any questions regarding this topic, don’t hesitate to reach out to me.
