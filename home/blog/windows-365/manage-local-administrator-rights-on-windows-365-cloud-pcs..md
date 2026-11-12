---
description: 24-05-2023 10:37 PM
---

# Manage local administrator rights on Windows 365 Cloud PCs.

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1cMvf6ThHg26HlwBCOVDt5chiSwoiRt-w" alt=""><figcaption><p><em>Managing local administrator rights on Windows 365 Cloud PCs.</em></p></figcaption></figure>

## Introduction

I’ve been writing about Windows 365 over the past few months, and in the original Windows 365 blog post I quickly mentioned that users by default doesn’t have local admin rights on their Cloud PC(s), and how to grant users local administrator privileges. The weather is cold and it’s raining today, and now that I’m just sitting here in my home office with a freshly brewed cup of coffee, why not write a post about how to manage local administrator rights on Windows 365 Cloud PCs.

I know that it can be done with a Group Policy Object (GPO) and via PowerShell, but in this blog post, I will be focusing on a custom configuration profile and the Windows 365 user settings.\
\
The original blog post about – [How to configure Windows 365 Enterprise in Microsoft Endpoint Manager](https://www.osdsune.com/home/blog/2021/configure-windows-365-enterprise)

## Managing local admin rights on Windows 365 Cloud PCs

Like in every great cooking show on television I’ve cheated a bit, and already prepared a security group within my on-prem Active Directory and it has been synced with AD Connect to Azure AD.\
\
This security group is named “**W365\_Enterprise\_Local\_Admin**” and will only contain users that I will grant local admin rights.



<figure><img src="https://drive.google.com/uc?id=1jO0XWcKJfVk0Kb3gnU2FImBBRTVDP79P" alt=""><figcaption></figcaption></figure>



### Manage local admin rights with a configuration profile

\
Let’s get started by visiting the Microsoft Endpoint Manager admin center.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
First, we will create a filter for Cloud PCs.\
Click on **Devices | Filters (preview) | Create**

<figure><img src="https://drive.google.com/uc?id=18sasTDORPbVtIPt4_L4QPlXCisIbIk_2" alt=""><figcaption></figcaption></figure>

I already created a filter for Windows 365 Cloud PCs, but you can copy the rule syntax used in my filter.\
**(device.model -contains “Cloud PC”)**

<figure><img src="https://drive.google.com/uc?id=104CwolbR0QDo3quFStzZTbB74OFJqetD" alt=""><figcaption></figcaption></figure>

Once you have created the Windows 365 Cloud PC filter, you can go ahead and create the custom configuration profile.\
Click on **Devices | Configuration profiles | Create profile**\
Select **Windows 10 and later** in the drop-down menu.\
Select **Templates** in the drop-down menu.\
Select **Custom** on the list and click **Create**.

<figure><img src="https://drive.google.com/uc?id=1Mce3Si0m-dYFXK5H3RRhKi-MtvpSTnzw" alt=""><figcaption></figcaption></figure>

Fill in the required field and click **Next**.

<figure><img src="https://drive.google.com/uc?id=15wTIRrKEzzNBXbS76eO5xCFS2I7as-Rk" alt=""><figcaption></figcaption></figure>

Click **Add**.

<figure><img src="https://drive.google.com/uc?id=12qqYcgcOJtMQahVYuJvlfUgkpv5snVi5" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=1K7if4Px756zOLvoZaa3ZeOstTMqifoK3" alt=""><figcaption><p>Source: <a href="https://docs.microsoft.com/en-us/windows/client-management/mdm/policy-csp-localusersandgroups#localusersandgroups-policies">Microsoft</a></p></figcaption></figure>

<table data-header-hidden><thead><tr><th width="187"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Add Domain Group to Local Administrator Group</td></tr><tr><td><strong>Description</strong></td><td>This is optional.</td></tr><tr><td><strong>OMA-URI</strong></td><td>./Vendor/MSFT/Policy/Config/LocalUsersAndGroups/Configure</td></tr><tr><td><strong>Data type</strong></td><td>String</td></tr><tr><td><strong>Value</strong></td><td>&#x3C;GroupConfiguration><br>    &#x3C; accessgroup desc = “S-1-5-32-544”><br>        &#x3C;group action = “U”/><br>            &#x3C;add member = “MINDCORELABW365_Enterprise_Local_Admin”/><br>    &#x3C;/accessgroup><br>&#x3C;/GroupConfiguration></td></tr></tbody></table>

**Note**. For adding Azure AD users and/or groups please read more about that in the [LocalUsersAndGroups CSP policy.](https://docs.microsoft.com/en-us/windows/client-management/mdm/policy-csp-localusersandgroups)  \
**Tip**. You can use SID S-1-5-32-544 instead of the group name (**Administrators**). – I would especially recommend it if you are managing a multi-language environment since the SID is not language dependent.  \
&#x20;\
Fill in all the required fields and click **Save**.

<figure><img src="https://drive.google.com/uc?id=1tJCk3onhcP9AKlP8l3gaqjtM4agi4zIY" alt=""><figcaption></figcaption></figure>

Click **Next**.\
Set scope tags if needed and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1wCjqpmRUNk6OJ_EOMTq0mKtZ0AE5iTlX" alt=""><figcaption></figcaption></figure>

Add the security group and filter as **Include** in filter mode.\
Click **Next**.\
Set applicability rules if needed and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1b4SvW_7i27lh7cacQtdkDSYutTepMhEQ" alt=""><figcaption></figcaption></figure>

Review your configuration and click **Create**.

<figure><img src="https://drive.google.com/uc?id=10Q0vcwoVs0hZ2qfN-3BJaC4atQA8kiA-" alt=""><figcaption></figcaption></figure>

To monitor the status of the configuration profile, click on **Devices | Configuration profiles** and select the profile.

<figure><img src="https://drive.google.com/uc?id=1x1IdJkM6YYUbXNLuFS35qPDkySH1oGU_" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=1g0mJucFMF8yEy5CUtKOHK43ikxQ2V_MX" alt=""><figcaption></figcaption></figure>

To check the filter evaluation on a Windows 365 Cloud PC, click on **Devices | Windows** and choose the Cloud PC.\
Click on **Filter evaluation (preview)** and select the configuration profile from the list.

<figure><img src="https://drive.google.com/uc?id=1Eeg-9xRYmUiuywVn0-IeAU_-OQlKYVRY" alt=""><figcaption></figcaption></figure>

If I connect to my Cloud PC, I can confirm that the security group has been added to the local administrator group. Awesome!

<figure><img src="https://drive.google.com/uc?id=1OrCjxh9c6vFS1vdgVO2nKjZQKL4slnT5" alt=""><figcaption></figcaption></figure>

### Manage local admin rights with Windows 365 user settings



<figure><img src="https://drive.google.com/uc?id=1gs_t7KK66gBCXNvgWmitq5FyUb9K2fOl" alt=""><figcaption></figcaption></figure>



Another way to grant a user local administrator privileges, is to create a Windows 365 user setting.

The main difference between the two approaches is that the custom configuration profile adds a domain security group (which probably contains several users) to the local administrator group, and the Windows 365 user setting adds the logged-on user directly to the local administrator group (if that user is a member of the domain security group used in the user setting).

Both scenarios are quite dynamic as you only need to remove the user from the domain security group to take away the local administrator privileges from the end-user.\
\
Click on **Devices | Windows 365 | User settings**\
Click on **Add**.

<figure><img src="https://drive.google.com/uc?id=14eW1jYXLAQ1aaeHrpyNnU71w5DPr1VzO" alt=""><figcaption></figcaption></figure>

Fill in the required field, tick the **Enable Local admin** check box, and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1vhkt5S0ljAacYzf2xZ-e0vnkNv-c3puj" alt=""><figcaption></figcaption></figure>

Add the security group and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1pZHIv2KmN5MzcrgUGedASgHEJuWOYmH2" alt=""><figcaption></figcaption></figure>

Review your configuration and click **Create**.

<figure><img src="https://drive.google.com/uc?id=1OEmF_FIwie-odikkXv0NEUV80Htmnycm" alt=""><figcaption></figcaption></figure>

The Windows 365 user setting didn’t add the logged-on user to the local administrator group, on my current Windows 365 Cloud PC, probably because it was provisioned with a custom Windows 11 image where I changed the system locale language to Danish before sysprep (which also translates the local group names to Danish during provisioning of new Cloud PCs).

If I reprovision my Windows 365 Cloud PC with a standard gallery Windows 11 image (which is in English), I can confirm that my user account has been added to the local administrator group, which kind of strengthens my suspicion that Windows 365 user settings are currently not working on custom images where you have changed the system locale language.

<figure><img src="https://drive.google.com/uc?id=1U9_ulkowrvm9dr5ni0YnVB5VWJ-uY0Ss" alt=""><figcaption></figcaption></figure>

After a while, the custom configuration profile will also be applied to my Cloud PC if the profile still has an assignment.

<figure><img src="https://drive.google.com/uc?id=1c_3vXgWOVDA8spiCfXUtiWootdTukEw4" alt=""><figcaption></figcaption></figure>

## Summary

In this blog post you have learned how to grant a user local administrator privileges on their Windows 365 Cloud PC. If you are using a custom image and you have changed the system locale language, the Windows 365 user settings will probably not work, but by the time of reading this blog post, it may have been fixed by Microsoft. Happy testing!

As always, if you have any questions regarding this topic, feel free to reach out to me.
