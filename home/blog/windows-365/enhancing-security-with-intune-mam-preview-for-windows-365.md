---
description: 23-08-2024 08:42 AM
cover: ../../.gitbook/assets/Designer (6) (1).jpeg
coverY: 46
---

# Enhancing Security With Intune MAM (preview) for Windows 365

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

Hey, folks! - It’s been a while since I last wrote a blog post. A lot has happened in my personal life over the past six months that is beyond my control, which has forced me to prioritize my family above everything else.

But now I'm back with a backpack full of topics for upcoming blog posts - so stay tuned!

In this blog post, we'll look at **Microsoft Intune Mobile Application Management (MAM)** for **Windows 365** and **Azure Virtual Desktop (AVD)**, which is now in public preview.

## What is Intune MAM?

Intune MAM allows us to manage and protect our organization's data within an application. Many productivity apps, such as the **Microsoft 365 Apps**, can be managed by Intune MAM.

{% hint style="info" %}
See the official list of [**Microsoft Intune protected apps**](https://learn.microsoft.com/mem/intune/apps/apps-supported-intune-apps) available for public use.
{% endhint %}

Intune MAM supports two configurations:

* **Intune Mobile Device Management (MDM) + MAM:** IT admins can manage apps using MAM on devices enrolled with Intune MDM.
* **Unenrolled devices with MAM managed applications:** IT admins can manage apps using MAM on unenrolled devices, which typically are employees’ preferred personal devices.

<figure><img src="../../.gitbook/assets/byod-concept-illustration_1284-6467.jpg" alt="" width="470"><figcaption></figcaption></figure>

Intune MAM for unenrolled devices is commonly used to protect against data loss on personal devices or in **bring-your-own-device (BYOD)** scenarios. To protect against data loss, Intune MAM for unenrolled devices uses app configuration policies combined with app protection policies and conditional access.

**For unenrolled devices, Intune MAM allows IT admins to:**

* Disable specific redirections on personal devices.
* Require PIN access to app.
* Block third-party keyboards.
* Specify a minimum device operating system version.
* Specify a minimum app version.
* Block jailbroken/rooted devices.
* Require a mobile threat defense (MTD) solution on devices, with no threats detected.

So, buckle up and join me as I explore Intune MAM for **Windows 365** and **Azure Virtual Desktop**. In this post, I will configure the **Windows App (iOS/iPadOS)** and the **Remote Desktop (iOS/iPadOS)** app on unenrolled iOS devices to block drive redirection and restrict cut, copy, and paste between other apps.

**In this post, I'll cover the following topics.**

* [**Prerequisites and Requirements**](enhancing-security-with-intune-mam-preview-for-windows-365.md#prereq)
* [**Managed App Filter**](enhancing-security-with-intune-mam-preview-for-windows-365.md#managedappfilter)
* [**App Configuration Policy for Managed Apps**](enhancing-security-with-intune-mam-preview-for-windows-365.md#appconfigpolicy)
* [**App Protection Policy**](enhancing-security-with-intune-mam-preview-for-windows-365.md#appprotectpolicy)
* [**App-based Conditional Access Policy**](enhancing-security-with-intune-mam-preview-for-windows-365.md#capolicy)
* [**Test and Verification**](enhancing-security-with-intune-mam-preview-for-windows-365.md#testverification)
* [**Summary**](enhancing-security-with-intune-mam-preview-for-windows-365.md#summary)

## Prerequisites and Requirements <a href="#prereq" id="prereq"></a>

* A valid and working Microsoft Entra and Intune tenant.
* **Azure Virtual Desktop** host pool with session hosts or **Windows 365** Cloud PCs.
* At least one security group containing users to which the policies apply.
* Client devices running one of the following versions of **Windows App** or the **Remote Desktop** app.
  * **Windows App:**
    * iOS and iPadOS: 10.5.2 or later.
  * **Remote Desktop:**
    * iOS and iPadOS: 10.5.8 or later.
    * Android: 10.0.0.19.1279 or later.
* Before you create an app-based Conditional Access policy, you must have:
  * **Enterprise Mobility + Security (EMS)** or a **Microsoft Entra ID P1 or P2 subscription**.
  * Users must be licensed for EMS or Microsoft Entra ID.
* Conditional Access Administrator and Microsoft Intune Administrator rights.

## Managed App Filter <a href="#managedappfilter" id="managedappfilter"></a>

First, we must create a managed app filter in Intune, which narrows the assignment scope of the app configuration and app protection policies to unenrolled devices.

{% hint style="warning" %}
**Important:** Managed app filters apply to app configuration and app protection policies. They don't apply to other policies, like compliance or device configuration profiles.
{% endhint %}

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com)\
In the left pane, select **Tenant administration** | **Filters** to create a managed app filter for unenrolled devices.

<div data-full-width="false"><figure><img src="../../.gitbook/assets/managed app filter_01.jpg" alt="Managed app filter"><figcaption></figcaption></figure></div>

On the **Basics** tab, fill in the required **Filter name** field and select the **Platform** to which this filter applies.

Your platform options:

* Android
* iOS/iPadOS
* Windows

Click **Next.**

{% hint style="info" %}
**Tip:** Although the **Description** field is optional, I recommend filling it out. Leaving some breadcrumbs is always a great idea, so others know precisely why someone created the filter(s).
{% endhint %}

<figure><img src="../../.gitbook/assets/managed app filter_02.jpg" alt="Managed app filter"><figcaption></figcaption></figure>

There are two ways to create a filter rule: Either by using the **Rule builder** or the **Rule syntax.**

* **Rule builder:** Select the following options for the rule expression.
  * Property: <mark style="background-color:blue;">deviceManagementType (Device Management Type)</mark>
  * Operator: <mark style="background-color:blue;">Equals</mark>
  * Value: <mark style="background-color:blue;">Unmanaged</mark>
* **Rule syntax:** Select **Edit** and past in this rule expression: <mark style="background-color:blue;">(app.deviceManagementType -eq "Unmanaged")</mark>

Click **Next.**

<figure><img src="../../.gitbook/assets/managed app filter_03.jpg" alt="Managed app filter"><figcaption></figcaption></figure>

Review that everything is correct and click **Create.**

<figure><img src="../../.gitbook/assets/managed app filter_04.jpg" alt="Managed app filter"><figcaption></figcaption></figure>

## App Configuration Policy for Managed Apps <a href="#appconfigpolicy" id="appconfigpolicy"></a>

Next, we must create an app configuration policy for managed apps targeting the **Windows App** and the **Remote Desktop** app, which enable us to provide configuration settings to unenrolled devices.

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com)\
In the left pane, select **Apps** | **App configuration policies** (under **Policy**), choose **Add**, and select **Managed apps.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_01.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Basics** tab, fill in the required **Name** field and target the policy to **Selected apps.**\
Next, do the following to target both apps.

* For the **Windows App**, choose **Select custom apps**, then for **Bundle or Package ID**, enter <mark style="background-color:blue;">com.microsoft.rdc.apple</mark>, and for **Platform**, select **iOS/iPadOS.**
* For the **Remote Desktop** app, choose **Select public apps**, then search for and select **Remote Desktop** for **iOS/iPadOS.**

Click **Next.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_02.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Settings catalog** tab, click **Next.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_03.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Settings** tab, expand **General configuration settings** and enter the name and value below.

* Name: <mark style="background-color:blue;">drivestoredirect</mark>
* Value: <mark style="background-color:blue;">0</mark>

{% hint style="info" %}
**Note:** The above configuration setting corresponds to the RDP properties listed on [**Supported RDP properties**](https://learn.microsoft.com/en-us/azure/virtual-desktop/rdp-properties#device-redirection), but the syntax is slightly different.
{% endhint %}

Click **Next.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_04.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Assignments** tab, assign the policy to a security group containing the users to which it applies. Next, select the filter we created earlier to narrow the policy's assignment scope to unenrolled devices.

Click **Next.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_05.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

Review that everything is correct and click **Create.**

<figure><img src="../../.gitbook/assets/AppConfigPolicy_06.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

### **Beware of the check-in interval**

{% hint style="warning" %}
**Important:** Intune managed apps will check in with an interval of 30 minutes for app configuration policy status, when deployed in conjunction with an app protection policy. If an app protection policy isn't assigned to the user, then the app configuration policy check-in interval is set to 720 minutes.\
\
Source: [**App configuration policies for Microsoft Intune**](https://learn.microsoft.com/en-us/mem/intune/apps/app-configuration-policies-overview#managed-apps)
{% endhint %}

If blocking local drive redirection satisfies your needs, you could stop here and wait 12 hours (720 minutes) for the policy to apply on unenrolled devices. However, I wanted to take it one step further by configuring an app protection policy and two Conditional Access policies. These policies will give us greater control over our security, allowing us to require a minimum app and OS version, restrict cut, copy, and paste between other apps, limit access to the remote session, etc. - it also reduces check-in interval to 30 minutes.

## App Protection Policy <a href="#appprotectpolicy" id="appprotectpolicy"></a>

First, we must create an app protection policy for the **Windows App** and the **Remote Desktop** app, which will enable us to control how data is accessed and shared by apps on unenrolled devices.

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com)\
In the left pane, select **Apps** | **App protection policies** (under **Policy**), choose **Create policy**, and select the **Platform** to which this policy applies.

<figure><img src="../../.gitbook/assets/AppProtectPolicy_01.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Basics** tab, fill in the required **Name** field.

Click **Next.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_02.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Apps** tab, target the policy to **Selected apps** and do the following to target both apps.

* For the **Windows App**, choose **Select custom apps**, then for **Bundle ID**, enter <mark style="background-color:blue;">com.microsoft.rdc.apple</mark> and click **Select.**
* For the **Remote Desktop** app, choose **Select public apps**, then search for and select **Remote Desktop.**

Click **Next.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_03.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Data protection** tab, only the following settings are relevant to the **Windows App** and the **Remote Desktop** app. The other settings don't apply as the **Windows App** and the **Remote Desktop** app interact with the Cloud PC or session host and not with data in the app.

* For **iOS/iPadOS**, you can configure the following settings:
  * Restrict cut, copy, and paste between other apps
  * Third-party keyboards
* For **Android**, you can configure the following settings:
  * Restrict cut, copy, and paste between other apps
  * Screen capture and Google Assistant
  * Approved keyboards

{% hint style="info" %}
**Tip:** If you disable clipboard redirection in an app configuration policy, you should set **Restrict cut, copy, and paste between other apps** in the app protection policy to **Blocked**.
{% endhint %}

{% hint style="info" %}
**Tip:** To allow users to copy phone numbers and/or credit card numbers, you should set the **Cut and copy character limit for any app** in the app protection policy to **19**.
{% endhint %}

Click **Next.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_04.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Access requirements** tab, configure the PIN and credential requirements to fit your organization's needs and click **Next.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_05.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Conditional launch** tab, I recommend the following conditions:

### **App conditions:**

| Setting              | Value          | Action                 |
| -------------------- | -------------- | ---------------------- |
| Max PIN attempts     | 5 (default)    | Reset PIN              |
| Offline grace period | 1440 (default) | Block access (minutes) |
| Offline grace period | 90 (default)   | Wipe data (days)       |
| Min app version      | 10.5 (1        | Block access           |

_(1. This will allow Windows App v10.5.2 and Remote Desktop v10.5.9_

{% hint style="info" %}
**Note:** If you add MTD conditions under **Conditional launch**, you must set up an MTD connector in MS Intune. For **Microsoft Defender for Endpoint**, see [**Configure Microsoft Defender for Endpoint in Intune**](https://learn.microsoft.com/en-us/mem/intune/protect/advanced-threat-protection-configure)
{% endhint %}

### **Device conditions:**

| Setting                         | Value                              | Action       |
| ------------------------------- | ---------------------------------- | ------------ |
| Jailbroken/rooted devices       | N/A                                | Block access |
| Min OS version                  | 17.5 (1                            | Block access |
| Max allowed device threat level | Secured (2                         | Block access |
| Primary MTD service             | Microsoft Defender for Endpoint (3 | N/A          |

_(1. This will allow iOS v17.5.1_\
_(2. This level is the most secure. - For more information, see_ [_**Create Mobile Threat Defense app protection policy with Intune**_](https://learn.microsoft.com/en-us/mem/intune/protect/mtd-app-protection-policy)\
_(3. I'm using MDE as my Mobile Threat Defense partner. - However, this configuration should be based on your requirements._

<figure><img src="../../.gitbook/assets/AppProtectPolicy_06.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

On the **Assignments** tab, assign the policy to a security group containing the users to which it applies. Next, select the filter we created earlier to narrow the policy's assignment scope to unenrolled devices.

Click **Next.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_07.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

Review that everything is correct and click **Create.**

<figure><img src="../../.gitbook/assets/AppProtectPolicy_08.jpg" alt="Enhancing security with Intune MAM"><figcaption></figcaption></figure>

## App-based Conditional Access Policy <a href="#capolicy" id="capolicy"></a>

Lastly, I will create two **Conditional Access** policies, enabling us to restrict access to a remote session only when an app protection policy is applied with the **Windows App** and the **Remote Desktop** app and block access to **Windows 365** and **Azure Virtual Desktop** using a web browser.

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com) or [**https://entra.microsoft.com**](https://entra.microsoft.com)

* For **Microsoft Intune admin center**: In the left pane, select **Endpoint security** and **Conditional access** (under **Manage**).

<figure><img src="../../.gitbook/assets/CAPolicy_01.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

* For **Microsoft Entra admin center**: In the left pane, expand **Protection** and select **Conditional Access.**

<figure><img src="../../.gitbook/assets/CAPolicy_02.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

Choose **Create new policy.**

<figure><img src="../../.gitbook/assets/CAPolicy_03.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

### **Conditional Access policy: Require app protection policy for Windows 365 and AVD**

For the first policy, we will grant access to **Windows 365** and **Azure Virtual Desktop** only when an app protection policy is applied with the **Windows App** and the **Remote Desktop** app.

{% hint style="warning" %}
**Important:** When you target **Cloud apps** under **Target resources** in **Conditional Access** policies, you will only find **Azure Virtual Desktop** in the list if you registered the **Microsoft.DesktopVirtualization** resource provider on a subscription in your **Microsoft Entra** tenant.
{% endhint %}

Fill in the required **Name** field.\
Under **Assignments**, include a security group containing the users to which the policy applies.

<figure><img src="../../.gitbook/assets/CAPolicy_05.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

For **Target resources**, choose **Cloud apps**, then for **Include**, select **Select apps**. Search for and select **Azure Virtual Desktop** and **Windows 365**.

<figure><img src="../../.gitbook/assets/CAPolicy_06.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

For **Conditions**:

* Choose **Device platforms**, then select **iOS** and/or **Android**.

<figure><img src="../../.gitbook/assets/CAPolicy_07.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

* Choose **Client apps**, then select **Mobile apps and desktop clients.**

<figure><img src="../../.gitbook/assets/CAPolicy_08.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

Under **Access controls**, select **Grant access**, then check the box for **Require app protection policy** and select the radio button for **Require all the selected controls**. - For **Enable policy**, set it to **On** and click **Create.**

<figure><img src="../../.gitbook/assets/CAPolicy_09.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

### **Conditional Access policy: Block access to Windows 365 and AVD via web browsers**

For the second policy, we will block access to **Windows 365** and **Azure Virtual Desktop** via web browsers.

Fill in the required **Name** field.\
Under **Assignments**, include a security group containing the users to which the policy applies.

<figure><img src="../../.gitbook/assets/CAPolicy2_01.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

For **Target resources**, choose **Cloud apps**, then for **Include**, select **Select apps**. Search for and select **Azure Virtual Desktop** and **Windows 365**.

<figure><img src="../../.gitbook/assets/CAPolicy2_02.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

For **Conditions**:

* Choose **Device platforms**, then select **iOS** and/or **Android**.

<figure><img src="../../.gitbook/assets/CAPolicy2_03.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

* Choose **Client apps**, then select **Browser.**

<figure><img src="../../.gitbook/assets/CAPolicy2_04.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

Under **Access controls**, select **Block access**, then select the radio button for **Require all the selected controls**.\
For **Enable policy**, set it to **On** and click **Create.**

<figure><img src="../../.gitbook/assets/CAPolicy2_05.jpg" alt="Enhancing security with Conditional Access"><figcaption></figcaption></figure>

## Test and Verification <a href="#testverification" id="testverification"></a>

Now it's time to treat yourself to a well-deserved cup of perfectly brewed coffee or tea, sit back, and admire the fantastic work you've accomplished in strengthening your environment's security.

Let’s open the **Windows App** on my iPhone and verify that everything works as intended. The initial indication that the policies have been applied to my unenrolled iPhone is a message indicating that your organization is now protecting its data in this app.

Once the app has been restarted, you should see your **Windows 365 Cloud PCs** and/or **Azure Virtual Desktop** session host.



<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/IMG_1760.PNG" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/IMG_1761.PNG" alt="" data-size="original"></td></tr></tbody></table>



When I connect to my **Windows 365 Cloud PC**, I'm being asked to configure **Microsoft Defender for Endpoint.**\
Click **Download from App Store**, then download and open the app.

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/IMG_1762.PNG" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/IMG_1763.PNG" alt="" data-size="original"></td></tr></tbody></table>

Check the box for **Terms of Use** and click **Accept.** Next, allow **Microsoft Defender** to set up a VPN connection.

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/IMG_1764.PNG" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/IMG_1765.PNG" alt="" data-size="original"></td></tr></tbody></table>



**Microsoft Defender** is now set up, and your device is protected. Now, return to the **Windows App**.\
You will now be asked to enter your **PIN** to access your **Cloud PC.**



<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/IMG_1766.PNG" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/IMG_1767.PNG" alt="" data-size="original"></td></tr></tbody></table>



**WOOHOO!** - I'm connected to my **Windows 365 Cloud PC.**

<figure><img src="../../.gitbook/assets/IMG_1768.PNG" alt="Unenrolled iPhone"><figcaption></figcaption></figure>

If I open **File Explorer**, we can see that no local drives are being redirected.

<figure><img src="../../.gitbook/assets/IMG_1769.PNG" alt="Unenrolled iPhone"><figcaption></figcaption></figure>

Let's copy a number in the format of a credit card number and see if we can paste it into a note on my iPhone.

<figure><img src="../../.gitbook/assets/IMG_1770.PNG" alt="Unenrolled iPhone"><figcaption></figcaption></figure>

We can confirm that it’s allowed. However, we can also verify that if we attempt to paste a longer number, it gets replaced by a message indicating that only 19 characters are allowed.

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th></tr></thead><tbody><tr><td align="center"><img src="../../.gitbook/assets/IMG_1771.PNG" alt="" data-size="original"></td></tr><tr><td align="center"><img src="../../.gitbook/assets/IMG_1773.PNG" alt="" data-size="original"></td></tr></tbody></table>

Finally, we can verify that **Conditional Access** blocks access to **Windows 365 Cloud PCs** and **Azure Virtual Desktop** through web browsers.

<figure><img src="../../.gitbook/assets/IMG_1774.PNG" alt="" width="375"><figcaption></figcaption></figure>

Let’s finish with a short video of the end-user experience.

{% embed url="https://youtu.be/Ce0D9b1dtcM" %}

## Summary <a href="#summary" id="summary"></a>

In this blog post, you learned about **Intune MAM** (preview) for **Windows 365** and **Azure Virtual Desktop** and how it can help protect against data loss on unenrolled iOS/iPadOS and/or Android devices by blocking local drive redirection via an app configuration policy.

I explained how we achieve greater control over our security by configuring an app protection policy and two Conditional Access policies, allowing us to require a minimum app and OS version, restrict cut, copy, and paste between apps, limit access to the remote session, and more.

That's it, folks. Happy testing, and have fun exploring 🤓\
If you have any questions regarding this topic, please feel free to reach out to me.
