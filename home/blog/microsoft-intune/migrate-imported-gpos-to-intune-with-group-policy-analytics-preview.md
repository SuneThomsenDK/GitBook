---
description: 31-05-2023 9:01 PM
---

# Migrate imported GPOs to Intune with Group Policy analytics (preview)

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1bnYjOREn0wQ6jzgmH1GHslM78TCmfQ3E" alt=""><figcaption><p>Migrate imported GPOs to Intune with Group Policy analytics (preview)</p></figcaption></figure>

## Introduction

In our previous blog post, where I wrote about [exporting GPOs from Group Policy management on-prem using PowerShell and doing a proper cleanup with Microsoft Graph](https://www.osdsune.com/home/blog/2022/group-policy-analytics-preview-made-a-bit-easier-with-powershell), I promised you an article about the new migration option within Group Policy analytics (preview). Using this new feature, you can create a Settings Catalog profile based on your imported GPOs and assign the profile to "All devices/All users" or your groups directly from Group Policy analytics (preview) in Intune.\
\
Read about the prerequisites and requirements for Group Policy analytics (preview) and how to use the tool in our original blog post here – [Analyze on-premises GPOs with MEM Group Policy analytics (preview).](https://www.osdsune.com/home/blog/2021/group-policy-analytics-preview)

## Migrate GPOs to a Settings Catalog profile

Alright, let’s assume that you have imported all of your GPOs and analyzed the result, and you know precisely which on-prem policies you will transition to Intune. What are your options, then?\
\
Well, before the migration option became available, you would have to search for an equivalent setting in the Endpoint Security blade, Settings Catalog, Administrative Template, or create a Custom profile, which can be a very time-consuming task. So, as mentioned in the introduction, we can now migrate imported GPOs to a Settings Catalog profile and assign "All device/All users" or a group to this profile directly from the Group Policy analytics (preview), which eases the burden a lot compared to doing it manually.\
\
Now, let’s take a closer look at this new migration option.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)\
\
Click **Devices | Group Policy analytics (preview)**

<figure><img src="https://drive.google.com/uc?id=1UcB3YvaBqFmCx6OKiWUEm-k4kA8vzfhB" alt=""><figcaption></figcaption></figure>

In the list of your imported GPOs, select the **Migrate** checkbox next to the GPO you want to include in your Settings Catalog profile.\
\
**Note**. You can choose to select one GPO or multiple GPOs.\
\
Click **Migrate.**

<figure><img src="https://drive.google.com/uc?id=1JLxbvpxVoyrEJ99YxoLx-ogbOupklJyo" alt=""><figcaption></figcaption></figure>

From the **Settings to migrate** page, you can select all settings or search and manually select the settings to transition to Intune. – I chose four random settings for this article.\
\
**Important note**. As mentioned above, you can migrate multiple GPOs to the same Settings Catalog profile, but the list may include identical settings with different values! – If you choose identical settings with different values, a conflict will occur, and an error will show with the following message:

{% hint style="danger" %}
&#x20;_<mark style="color:red;">Conflicts are detected for the following settings: \<setting name>. Select only one version with the value you prefer in order to continue.</mark>_
{% endhint %}

Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1Inwi2harkbo_yjag9R0pwrvvraRtMnmU" alt=""><figcaption></figcaption></figure>

On the **Configuration** page, you can review the selected settings and their values.\
\
Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1Io3h49jf0JKtGeueVWiz4AMLgNYveQZP" alt=""><figcaption></figcaption></figure>

On the **Profile info** page, fill in the required **Name** field. Although the **Description** field is optional, I would recommend filling it out. – It’s always a great idea to leave some breadcrumbs, so others know precisely why someone created the configuration profile.\
\
Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1x5xuNyekMeFGfyrpsZcCEGmTj5EbRoUT" alt=""><figcaption></figcaption></figure>

Choose either to assign the profile to "All devices/All users" or a group from the **Assignments** page. – I chose to assign this profile to "All devices", and then I’ve added a filter to only include corporate devices.\
\
**Note**. You do not have to configure the assignment at this point if your organization is not ready for it.\
\
Click **Next**.

<figure><img src="https://drive.google.com/uc?id=1NDLqXptMSE5FxDH33JnxkS43yP5TZyyK" alt=""><figcaption></figcaption></figure>

Please carefully review your configuration on the **Review + deploy** page and click **Deploy**.\
**Important note**. Some settings don’t migrate exactly and may use different settings or values. – Read more [here](https://docs.microsoft.com/en-us/mem/intune/configuration/group-policy-analytics-migrate#what-you-need-to-know)

<figure><img src="https://drive.google.com/uc?id=18zkZ7E3_WgYqKv7ZtcOAcjFYGWhZF6UQ" alt=""><figcaption></figcaption></figure>

The page will redirect you to an overview of your configuration profiles in Intune, and in the **Notifications** area, you should see that the migration was successful.&#x20;

<figure><img src="https://drive.google.com/uc?id=1C86nucplax_UUD5Ynjkyp5EYlKiQQwsk" alt=""><figcaption></figcaption></figure>

Select the newly created Settings Catalog profile from the overview and scroll down to the **Configuration settings** area. You will see the settings we chose during the profile creation. Shortly after creating and assigning the profile, the devices should start returning some data to the dashboard within the configuration profile.

<figure><img src="https://drive.google.com/uc?id=1xZX-MTN8N9hFkjvo7dyBXYnb8ixUoLC0" alt=""><figcaption></figcaption></figure>

## Summary

In this article, you learned how to use the new migration option within Group Policy analytics (preview) in Microsoft Endpoint Manager. This new possibility will, without a doubt, ease the burden of migrating on-prem policies to Intune. However, it’s not perfect, and you need to carefully review the settings you selected during the creation of the Settings Catalog profile.\
\
Read more at Microsoft docs about [what you need to know.](https://docs.microsoft.com/en-us/mem/intune/configuration/group-policy-analytics-migrate#what-you-need-to-know)\
\
That’s it, folks. Happy testing!\
If you have any questions regarding this topic, please feel free to reach out to me.
