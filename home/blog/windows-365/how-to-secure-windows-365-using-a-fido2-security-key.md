---
description: 30-05-2023 8:2 PM
---

# How to secure Windows 365 using a FIDO2 security key

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1hRpOAo6splon7H-dCJaOGSmVaavcBMJz" alt=""><figcaption><p>Secure your Windows 365 Cloud PC(s) with Conditional Access and FIDO2 security keys.</p></figcaption></figure>

## Introduction

We have already written about FIDO2 security keys on several occasions (I will add the links below), which has inspired me to see how I could secure Windows 365 using Conditional Access and a FIDO2 security key.\
\
The scenario is that I connect to my Windows 365 Cloud PC from personally owned devices at home and on the go. I want to embrace the future of passwordless authentication to achieve a higher level of security for my Windows 365 environment.\
\
So, I will in this post walk you through how I secured my Windows 365 environment using Conditional Access and the FEITIAN AllinPass (K33) FIDO2 security key.\
\
\
Our other blog posts about FIDO2 security keys.

– [Passwordless using FIDO2 security key with HoloLens 2 by Mattias Melkersen](http://blog.mindcore.dk/2021/06/passwordless-using-fido2-security-key.html)\
– [Azure AD support for FIDO2 in hybrid environments by Lars Lohmann Blem](http://blog.mindcore.dk/2020/02/azure-ad-support-for-fido2-in-hybrid.html)\
– [Azure AD and password-less sign-in by Lars Lohmann Blem](http://blog.mindcore.dk/2019/07/azure-ad-and-password-less-sign-in.html)  \
&#x20;

As already mentioned, the security key used in this post is a [FEITIAN AllinPass (K33) FIDO2 security key.](https://www.ftsafe.com/Products/FIDO/Bio)

<figure><img src="https://drive.google.com/uc?id=1zugQgwTm0s5ZKc2PZqRQnSBUfJQRIzfX" alt=""><figcaption><p>Source: <a href="https://www.ftsafe.com/">FEITIAN Technologies</a> </p></figcaption></figure>

## Prerequisites and Requirements

* Azure Active Directory (**Azure AD**)
* Azure AD Multi-Factor Authentication (**MFA**)
* Azure AD Conditional Access (**CA**)
* Enable Combined security information registration \*
* Microsoft Endpoint Manager (**MEM**)
* Microsoft compatible FIDO2 security key
* For Azure AD joined devices, the best experience is on Windows 10 version 1903 or higher.
* Hybrid Azure AD joined devices must run Windows 10 version 2004 or higher.
* WebAuthN requires Windows 10 version 1903 or higher \*\*
* To use Windows 365 Enterprise, each user needs a license for Windows 10 or 11 Enterprise, Microsoft Endpoint Manager (**Intune**), and Azure AD P1 (e.g., Microsoft 365 E3 + Windows 365 Enterprise 4 vCPU, 16 GB, 128 GB)
  * Azure AD P1 license ([Azure Active Directory Premium licensing](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis#what-are-the-azure-ad-licenses))
  * Microsoft Intune supported license ([Microsoft Intune licensing](https://docs.microsoft.com/en-us/mem/intune/fundamentals/licenses))
  * Windows 365 license ([Microsoft Windows 365 licensing](https://www.microsoft.com/en-us/windows-365/all-pricing))

\* Starting on August 15th of 2020, all new Azure AD tenants will be automatically enabled for combined registration. – More details about [combined security information registration](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-registration-mfa-sspr-combined)

\*\* To use security keys for logging in to web apps and services, you must have a browser that supports the WebAuthN protocol. These include Microsoft Edge, Chrome, Firefox, and Safari.\
\
Source: [Microsoft](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-security-key)

### Supported FIDO2 security key providers

The following providers offer FIDO2 security keys that are known to be Microsoft compatible.

<figure><img src="https://drive.google.com/uc?id=1rVrGnHmHeRNlekR0hAEJrPGgyhVeb8XY" alt=""><figcaption><p>Source: <a href="https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-authentication-passwordless#fido2-security-key-providers">Microsoft</a></p></figcaption></figure>

## Enable FIDO2 Authentication method in Azure AD

Let’s enable the FIDO2 security key as an authentication method in Azure AD.\
Go to [https://portal.azure.com](https://portal.azure.com/)\
\
From **Security** in Azure AD, click **Authentication methods**.

<figure><img src="https://drive.google.com/uc?id=1X8BHT6apy9VOX4TIFKAzyQCdoVWK-lqM" alt=""><figcaption></figcaption></figure>

Click **Policies** and select **FIDO2 Security Key**.

<figure><img src="https://drive.google.com/uc?id=1ledeV3tSP-m2IcqWeUlSVD-7IyqdhYjg" alt=""><figcaption></figcaption></figure>

Set the settings as shown in the screenshot below.

<figure><img src="https://drive.google.com/uc?id=1Q6ZfhrlAPAIx0LY2ZZFOem2ateG0ggLg" alt=""><figcaption></figcaption></figure>

Go to the **Configure** tab, set the settings as shown in the screenshot below, and click **Save**.

<figure><img src="https://drive.google.com/uc?id=1JK2nFwqY_HCVqkBrvTtg9YokHqAzmG1F" alt=""><figcaption></figcaption></figure>

**FIDO2 Security Key** will now be available as an authentication method for all users.

<figure><img src="https://drive.google.com/uc?id=1222LUjRawkuGIZTzr8vjCRBv9pHs7_47" alt=""><figcaption></figcaption></figure>

## Create the Conditional Access policy in Azure AD

The end users can access their Windows 365 Cloud PC(s) in two different ways:

* [Windows 365 Web Site](https://windows365.microsoft.com/)
* [Microsoft Remote Desktop App](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients)

Let’s create a Conditional Access policy that will require MFA and set sign-in frequency for both cloud apps.\
Go to [https://portal.azure.com](https://portal.azure.com/)\
\
From **Security** in Azure AD, click **Conditional Access**.

<figure><img src="https://drive.google.com/uc?id=1DLrMbY9uqKmmzOwatE3sxAKuqdux2PAO" alt=""><figcaption></figcaption></figure>

Click **Policies | New Policy | Create new policy**

<figure><img src="https://drive.google.com/uc?id=1A8EGx-Z3awAPKroW-H6pzjS4WGKLwAwb" alt=""><figcaption></figcaption></figure>

Fill in the required **Name** field.\
Click **Users or workload identities** and choose which users or groups to include in this policy. – For example, I selected an AAD group containing users eligible for a Windows 365 Cloud PC.

<figure><img src="https://drive.google.com/uc?id=1F7ZuNLQHawn6GoM8XAlRGc_1j7b3p01M" alt=""><figcaption></figcaption></figure>

Click **Cloud apps or actions** and select the following two cloud apps:

* Windows 365 (**Web Site**)
* Windows Virtual Desktop (**Remote Desktop App**)

<figure><img src="https://drive.google.com/uc?id=1iBIW9WYSexggqjRClrh1c_-qBUPkl45f" alt=""><figcaption></figcaption></figure>

Click **Grant**, select **Grant access**, and tick the **Require multi-factor authentication** check box.\
Click **Select**.

<figure><img src="https://drive.google.com/uc?id=1ujd2h79UEbqz1urtupfnoXBO79mwZrfP" alt=""><figcaption></figcaption></figure>

Click **Session**, and configure the **Sign-in frequency**. I chose 8 hours in my policy, which matches a typical working day.\
Click **Select**. &#x20;

**Note**. The Sign-in frequency is the period before a user needs to sign in again when attempting to access a resource. The default setting is a rolling window of 90 days.

<figure><img src="https://drive.google.com/uc?id=1GyRDWEg0M97COl3BQWFJkfUZBSoIJ66Y" alt=""><figcaption></figcaption></figure>

Enable the policy and click **Create**.

<figure><img src="https://drive.google.com/uc?id=1dFTjgqdsYWKdf5G227pVk9Exkw2G6c_c" alt=""><figcaption></figcaption></figure>

## Configuring the security key

Adding the security key (in this case, a FEITIAN AllinPass (K33) FIDO2 security key) to my physical device was straightforward and can be done with either USB-C, NFC, or Bluetooth. I chose to demo the Bluetooth option for this post, but I have also tested the USB-C option, and it works perfectly as well.

{% hint style="warning" %}
&#x20;**Important:** Before using the security key, you need to set up a PIN and enroll a fingerprint onto the security key. See also the security key manufacturer’s user manual for additional guidance. For example, to find out how to turn on the Bluetooth and pair it with your device.
{% endhint %}

Windows 10 – Go to **Windows Settings | Devices | Bluetooth & other devices** and click **Add Bluetooth or other device**\
Windows 11 – Go to **Windows Settings | Bluetooth & devices** and click **Add device**\
&#x20;\
Select **Bluetooth** and prepare the security key for pairing.

<figure><img src="https://drive.google.com/uc?id=1DWLeh5XcCR6q3dwLUt5ezPq7rDdAOQsL" alt=""><figcaption></figcaption></figure>

Select the security key when it appears in the list. (in this case, the device pairing name is **FT\_XXXXXX**)

<figure><img src="https://drive.google.com/uc?id=1i1qpIsVyIQXFDpyUaLfr3UeVdbUqdn7s" alt=""><figcaption></figcaption></figure>

Once paired, click **Done**.

<figure><img src="https://drive.google.com/uc?id=18KUzmy-It0TdzgjzAq0LqnsCnlK0wj7g" alt=""><figcaption></figcaption></figure>

Go to **Windows Settings | Accounts | Sign-in options |** expand **Security key** and click **Manage.**

<figure><img src="https://drive.google.com/uc?id=1JToln-AAELuwYU1HzURHSAELt17Xz_HY" alt=""><figcaption></figcaption></figure>

Turn on your Bluetooth security key or insert it into the USB port.

<figure><img src="https://drive.google.com/uc?id=1kGHxN_LF0QdiiCiADXwF_4qs91Bv7-6G" alt=""><figcaption></figcaption></figure>

Tap the security key.

<figure><img src="https://drive.google.com/uc?id=16shmiE3-Rf0P3EEZ_fa-jZTX6HqhJ8oK" alt=""><figcaption></figcaption></figure>

Click **Add** to create a PIN.

<figure><img src="https://drive.google.com/uc?id=1W6fc2QFQbgdsjBMek3Kog0CQ0Qz49-PH" alt=""><figcaption></figcaption></figure>

Set up a PIN and click **OK**.

<figure><img src="https://drive.google.com/uc?id=1GF8aT9Hsn6AG5acNoZhlz-APCKWwO5JQ" alt=""><figcaption></figcaption></figure>

Click **Set up** to enroll your fingerprint(s).

<figure><img src="https://drive.google.com/uc?id=10_OEDJGiM7zDIIsmAarUcoo7zxAvamWH" alt=""><figcaption></figcaption></figure>

Enter the newly created PIN and click **OK**.

<figure><img src="https://drive.google.com/uc?id=1sJt78sq-brGwtUs4lGbPpltI14jFLMe4" alt=""><figcaption></figcaption></figure>

Enroll your fingerprint(s).

<figure><img src="https://drive.google.com/uc?id=1W5nuIOCBMEIhDAeJCbgQ1Eh7uQOkezc4" alt=""><figcaption></figcaption></figure>

Click **Done**.

<figure><img src="https://drive.google.com/uc?id=1rzBRVuJPxLnhHDYXPdsIWBe-IdtVFcOs" alt=""><figcaption></figcaption></figure>

Click **Close**.

<figure><img src="https://drive.google.com/uc?id=1EemH6d7qUHW0LMWUnzEIb132S02XKAjp" alt=""><figcaption></figcaption></figure>

## Register the security key to your Azure AD account

Once we have configured the security key, we can register it to our Azure AD account.\
Go to [https://aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo) or [https://mysignins.microsoft.com](https://mysignins.microsoft.com/)<br>

Click **Security info | Add method | Choose a method** and select **Security key**.

<figure><img src="https://drive.google.com/uc?id=1e9REN4eA-_e1XcVqj1VUGhLOjcB9LGMf" alt=""><figcaption></figcaption></figure>

Click **Add**.

<figure><img src="https://drive.google.com/uc?id=13lSr-gQCtlW7XelGVWoRRKmUxBo3VPJ9" alt=""><figcaption></figcaption></figure>

Select **USB device**.

<figure><img src="https://drive.google.com/uc?id=1eH1DFqhTLTrg-I-Tl6cH_fpbInn5lIbZ" alt=""><figcaption></figcaption></figure>

Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1gt30e1F5PyAWFzS75Wj332FOxZT3F6wr" alt=""><figcaption></figcaption></figure>

Click **OK**.

<figure><img src="https://drive.google.com/uc?id=1GasrHgV3voOtp7EVSGpZcE3aj417jscT" alt=""><figcaption></figcaption></figure>

Click **OK**.

<figure><img src="https://drive.google.com/uc?id=18vDnCFyqASl4yULhynLWXSGem_T9tUVB" alt=""><figcaption></figcaption></figure>

Turn on your Bluetooth security key or insert it into the USB port.

<figure><img src="https://drive.google.com/uc?id=1MBy1_Ij_8NZPdQEKI_n7aA507CybB8cY" alt=""><figcaption></figcaption></figure>

Rest your enrolled fingerprint on the security key sensor.

<figure><img src="https://drive.google.com/uc?id=1H8lPvMy-wmpM-M9V2luOanWGvXmWiaGr" alt=""><figcaption></figcaption></figure>

Name your security key and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1QiwssX4N6zl0Lzx_EHdzMoRJ7iyUzz7Y" alt=""><figcaption></figcaption></figure>

Click **Done**.

<figure><img src="https://drive.google.com/uc?id=1OZ--YRtfJxxkv96cE0iRrX-ISe75iLVP" alt=""><figcaption></figcaption></figure>

And the security key is now registered to your account as a sign-in method.

<figure><img src="https://drive.google.com/uc?id=1gsVS3R-KI2qRxQ7we4OnKswZFfvscIxC" alt=""><figcaption></figcaption></figure>

## Security key sign-in experience

Once we have configured the Conditional Access policy and set up the security key, we are ready to test the Windows 365 Cloud PC sign-in experience.

### Windows 365 Web Site

First, let’s try and sign in to the Windows 365 Web Site.\
Go to [https://windows365.microsoft.com](https://windows365.microsoft.com/)\
\
Click **Sign-in options**.

<figure><img src="https://drive.google.com/uc?id=1qsYVUU0iZ6WhV99ntVN5rB_eZQGKBOfO" alt=""><figcaption></figcaption></figure>

Select **Sign in with a security key**.

<figure><img src="https://drive.google.com/uc?id=1hLlRh4IEdJeAflsaoi0eerhfxIhRjzXR" alt=""><figcaption></figcaption></figure>

Turn on your Bluetooth security key or insert it into the USB port.

<figure><img src="https://drive.google.com/uc?id=1SL8MskYHSyr3FOnyWxsoKwPS2hKzjMYq" alt=""><figcaption></figcaption></figure>

Rest your enrolled fingerprint on the security key sensor.

<figure><img src="https://drive.google.com/uc?id=1lVXCI5Wj4TgNRbuew7UP8p95BbsfK8ni" alt=""><figcaption></figcaption></figure>

Click **Open in browser**.

<figure><img src="https://drive.google.com/uc?id=1U0MwdpV9Uv9t83x6MVYJmhGmuXvOxeKJ" alt=""><figcaption></figcaption></figure>

We now see the usual sign-in prompt for the Windows 365 Cloud PC.

Enter your password and click **Sign In**.

<figure><img src="https://drive.google.com/uc?id=1Tb9Kg_v88lV26eYlwQwsiAJRjKI6cc97" alt=""><figcaption></figcaption></figure>

And we are signed in.

<figure><img src="https://drive.google.com/uc?id=1MQL9XxbupmVgQev1EG3ecim9h3zeigmh" alt=""><figcaption></figcaption></figure>

### Microsoft Remote Desktop App

Next, let’s try and sign in to our Windows 365 Cloud PC using the Remote Desktop App.

Open **Remote Desktop App**.

<figure><img src="https://drive.google.com/uc?id=1cg9-XmPnHbWm7I5ewt6_5T3oZdy1NaTn" alt=""><figcaption></figcaption></figure>

Let’s look at my Windows 365 Cloud PC details. – Note the following status message “**We need your sign in information to refresh this feed**” that’s because the previous session has timed out due to the configuration I made in my Conditional Access policy, where I configured the sign-in frequency to be 8 hours.<br>

Double-click on your Windows 365 Cloud PC or click **Refresh** in the details.

<figure><img src="https://drive.google.com/uc?id=18hIoTcW3n-KhkG8AWdeuUX8YJiXzwmcb" alt=""><figcaption></figcaption></figure>

Select your account in the list.

<figure><img src="https://drive.google.com/uc?id=1YTITmLJZqq_--jz5-Sh3zQZnXDpcg9wJ" alt=""><figcaption></figcaption></figure>

Turn on your Bluetooth security key or insert it into the USB port.

<figure><img src="https://drive.google.com/uc?id=1jqMCtjqENxOyeZ3kEf7fC0woHOBbeRpZ" alt=""><figcaption></figcaption></figure>

Rest your enrolled fingerprint on the security key sensor.

<figure><img src="https://drive.google.com/uc?id=1IbRQmwp-Js3WjqEu_5kvXnzFQdkLOo8Z" alt=""><figcaption></figcaption></figure>

Once again, we see the usual Windows security prompt for the Windows 365 Cloud PC.

Enter your password and click **OK**.

<figure><img src="https://drive.google.com/uc?id=1zUvyF4w3lD3Gwjxt2lEMljuAfvRJCKqa" alt=""><figcaption></figcaption></figure>

And we are once again signed in. Awesome!

<figure><img src="https://drive.google.com/uc?id=1FcJeO96VOH4lqb-C2YBzlCUlvniCbQgU" alt=""><figcaption></figcaption></figure>

## Sign-in details in Azure AD

Once we have completed the configuration, you probably want to know which authentication methods are used in your environment, right? You can find this information in the end user’s sign-in details and the authentication methods activity dashboard in Azure AD.<br>

Go to **Users** in Azure AD and select a user.\
Click **Sign-in logs** in the **Activity** section and choose an activity from the list.\
Select the **Authentication Details** tab.

<figure><img src="https://drive.google.com/uc?id=1leJvJkmcIh5DpSXZM6QvqVVD11VFwSjB" alt=""><figcaption></figcaption></figure>

Go to **Security** in Azure AD and select **Authentication methods**.\
Click **Activity** in the **Monitoring** section and choose the **Usage** tab.

<figure><img src="https://drive.google.com/uc?id=1ahVCPK1iP-wsS4T3yA4_ITgmrrf_TyND" alt=""><figcaption></figcaption></figure>

## Summary

In this post, you learned how to secure your Windows 365 environment using Conditional Access and FIDO2 security keys. – Thanks to [Della Han](https://www.linkedin.com/in/della-han-081812200/) and [FEITIAN Technologies](https://www.ftsafe.com/) for providing me with the security key used in this post.\
\
&#x20;  \
Not only did I achieve a higher level of security for my Windows 365 environment by going passwordless. But it is also more convenient than Password + Two Factor Authentication, and I can access my applications and services much faster now (win-win).\
\
The future is passwordless! – More details about [passwordless](https://www.microsoft.com/en-us/security/business/identity-access-management/passwordless-authentication)\
\
\
That’s all, folks. Happy testing!\
As always, if you have any questions regarding this topic, feel free to reach out to me.
