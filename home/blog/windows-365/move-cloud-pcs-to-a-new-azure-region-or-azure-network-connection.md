---
description: 17-07-2023 8:20 PM
cover: ../../.gitbook/assets/logo_01.jpg
coverY: -6
---

# Move Cloud PCs to a new Azure Region or Azure Network Connection

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

Until recently, you had to reprovision existing Windows 365 Cloud PCs if you changed the Azure region of the Microsoft Hosted Network or the Azure Network Connection (ANC) in your provisioning policy – only new Cloud PCs would honor these changes! But this has changed with the recent Service Release 2305! Now, it is possible to move up to 100 Cloud PCs at a time to another Azure region or ANC.

– So, buckle up and join me as I explore this new feature to see if it adds more value and flexibility to the Windows 365 service. Also, let’s find out what’s happening in the backend and when it’s most optimal to move Cloud PCs.

**In this post, I’ll cover the following topics.**

* [**How to move Cloud PCs**](move-cloud-pcs-to-a-new-azure-region-or-azure-network-connection.md#move)
* [**What’s happening in the backend?**](move-cloud-pcs-to-a-new-azure-region-or-azure-network-connection.md#backend)
* [**Summary**](move-cloud-pcs-to-a-new-azure-region-or-azure-network-connection.md#summary)

## How to move Cloud PCs <a href="#move" id="move"></a>

Before moving Cloud PCs to a new Azure region or ANC, it’s important to highlight a few things first!

In preview, you can move up to 100 Cloud PCs at a time from their current Azure region or ANC to a new one. You can change the network type from Microsoft Hosted Network to ANC or vice versa.

{% hint style="warning" %}
&#x20;**Important:** If you change the **Azure Network Connection (ANC)** for **Hybrid Azure AD Join**, the domain defined in the new ANC must match the domain of the Cloud PC(s) you want to move. The domain used in the original ANC must be reachable from the new ANC.
{% endhint %}

As moving the Cloud PCs involves a shutdown, which can take several hours, it’s best to perform the move of Cloud PCs outside working hours to ensure minimal user impact. For this reason, it’s also advisable to notify your users in advance so that they can save their work and sign out.

Let’s visit **Microsoft Intune** to change the Azure region of the Microsoft Hosted Network in one of my current Windows 365 provisioning policies.

{% hint style="info" %}
&#x20;**Note:** It’s a similar approach for changing the current Azure Network Connection (ANC) for **Hybrid Azure AD Join** and **Azure AD Join** to a new ANC. See [**Move a Cloud PC (preview) | Microsoft Learn**](https://learn.microsoft.com/en-us/windows-365/enterprise/move-cloud-pc#move-a-cloud-pc)
{% endhint %}

### **Changing the Azure region**

Go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)

In the left pane, click **Devices | Windows 365 | Provisioning policies**\
Select an existing policy in the list of provisioning policies.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_00-1024x480.png" alt="Move Cloud PCs to a new Azure Region"><figcaption></figcaption></figure>

On the overview page, look for **General** and click **Edit.**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_01-710x1024.png" alt="Changing to a new Azure Region"><figcaption></figcaption></figure>

Choose a new **Geography** and **Region** or a new **Region** within the already selected **Geography** and click **Next**.

– I expanded the **Region** drop-down menu to see all available Azure regions within my current **Geography** and chose **Sweden Central** as the new Azure region for my Cloud PCs.

{% hint style="info" %}
&#x20;**Tip:** You can use [**Azure Speed Test 2.0**](http://azurespeedtest.azurewebsites.net/) to measure the latency from your web browser to the Blob Storage Service in each of the Microsoft Azure Data Centers.
{% endhint %}

{% hint style="info" %}
&#x20;**Note:** Starting with Service Release 2304, **Windows 365** now supports the **South Africa North** and **Sweden Central** regions. See [**Supported Azure regions for Cloud PC provisioning**](https://learn.microsoft.com/en-us/windows-365/enterprise/requirements?tabs=enterprise,ent#supported-azure-regions-for-cloud-pc-provisioning)
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_03-752x1024.png" alt="Changing to a new Azure Region"><figcaption></figcaption></figure>

Review the configuration and click **Update**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_04-717x1024.png" alt="Changing to a new Azure Region"><figcaption></figcaption></figure>

When you are ready to move the existing Cloud PCs, select **Apply region change to existing Cloud PCs**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_05-764x1024.png" alt="Apply region change to existing Cloud PCs"><figcaption></figcaption></figure>

## What’s happening in the backend? <a href="#backend" id="backend"></a>

As mentioned, click **Apply region change to existing Cloud PCs** when ready.

{% hint style="info" %}
&#x20;**Note:** A message explaining what will happen appears, and you can choose between **Apply** or **Cancel**.
{% endhint %}

Click **Apply**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_06.png" alt="Apply region change to existing Cloud PCs"><figcaption></figcaption></figure>

What happens next in the backend involves backing up the Cloud PCs before moving them to the new Azure region. This backup, which may take some time, can begin even though the user is still signed in and active.

After completing the backup, the Cloud PC is shut down and moved to the new Azure region, which may take several hours. The Cloud PC is inaccessible during this time, so the best time to perform the move is outside working hours to ensure minimal user impact.

You can monitor the move status by navigating to the **All Cloud PCs** tab.\
You will see the following status during the move: **Moving region or network**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_07-1-1024x396.png" alt="Monitor the Cloud PC move."><figcaption></figcaption></figure>

The move is complete when the status changes to **Provisioned**.\
Users can sign in once the move is complete and continue working where they left off.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_08-1-1024x411.png" alt="Monitor the Cloud PC move."><figcaption></figcaption></figure>

## Summary

In this blog post, you learned how to change the Azure region of the Microsoft Hosted Network in an existing Windows 365 provisioning policy. I also shared some advice about what to be aware of before moving Cloud PCs to a new Azure region or ANC and where to monitor the Cloud PC move status.

This addition to the Windows 365 service is a fantastic enhancement that adds more flexibility to Cloud PC management. However, there is room for some minor improvements. For instance, let the IT admins choose which individual Cloud PCs to move and make it possible to observe the number of Cloud PCs being moved.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/06/CPC_Policy_09-1024x130.png" alt="Monitor the Cloud PC move."><figcaption></figcaption></figure>

That’s it, folks. Happy testing, and have fun exploring 🤓\
If you have any questions regarding this topic, please feel free to reach out to me.
