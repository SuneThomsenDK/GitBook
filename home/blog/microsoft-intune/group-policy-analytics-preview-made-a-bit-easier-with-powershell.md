---
description: 31-05-2023 8:52 PM
---

# Group Policy analytics (preview) made a bit easier with PowerShell

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=17kL_rC8Y50DCoq-EsgbUsnfZS6V1n4iX" alt=""><figcaption><p><em>Group Policy analytics (preview) – Export linked and enabled GPOs.</em></p></figcaption></figure>

## Introduction

It has almost been a year since I wrote our original blog post about Group Policy analytics (preview) in Microsoft Endpoint Manager. Since then, several improvements have been added to the tool, but there are still a few areas lagging some attention, in my opinion! So, at our Modern Endpoint Management Summit 2022, I presented a live demo about how to export linked and enabled GPOs on-prem and perform a cleanup (bulk deletion) of the imported GPOs in Group Policy analytics after you have completed the analysis and transition to Intune.\
\
**Note**. The Group Policy analytics migration to device configuration profile feature was not generally available at our Modern Endpoint Management Summit, so I could unfortunately not demo that feature. Instead, I will be writing a blog post about that feature soon.\
\
Read about the prerequisites and requirements for Group Policy analytics (preview) and how to use the tool in our original blog post here – [Analyze on-premises GPOs with MEM Group Policy analytics (preview).](https://www.osdsune.com/home/blog/2021/group-policy-analytics-preview)

## Prerequisites and Requirements

* Access to Microsoft Graph &#x20;
* PowerShell scripts ([download](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/GroupPolicyAnalytics))

## Export linked and enabled GPOs as XML files

Let’s dive right into it. But first, you’ll need to download the PowerShell script from my GitHub repository.\
\
Download the GPO export script from the GitHub repository [here](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/GroupPolicyAnalytics)  \
\
\
Next, connect to your domain controller and copy the GPO export script to a folder (For example, C:Temp)  \
From the **Start Menu**, search for **PowerShell ISE** and select it in the list.

<figure><img src="https://drive.google.com/uc?id=1ZZNwJxjRagfe2tOZeLA7sHwBPkt-6BES" alt=""><figcaption></figcaption></figure>

Open the GPO export script and fill in the following variables:

* **OURoot** – Specify an Active Directory path.
* **OUName** – Specify a specific OU or add \* for all OUs.
* **GPOName** – Optional – Use this variable to export GPOs containing a particular keyword.
* **ExportPath** – Specify a path where to save the exported GPOs.

Hit **F5** or click on the **Run Script** button.

<figure><img src="https://drive.google.com/uc?id=1KAfkt6YcLeywNQuXsbDpUMHm0Ka4mgrx" alt=""><figcaption></figcaption></figure>

Go to your export folder, and you should see that all the GPOs linked and enabled on a specific OU or all OUs were exported and ready for import to Group Policy analytics in Intune.

<figure><img src="https://drive.google.com/uc?id=1xWmEF7gwP1wcs2hGL9phl1OeDFr3WTCR" alt=""><figcaption></figcaption></figure>

I have created this small GIF to show you the entire export process.

<figure><img src="https://drive.google.com/uc?id=1oB7I6SUjP5rdnq_OsYMvhUovKGYS7a_o" alt=""><figcaption></figcaption></figure>

## Perform a cleanup (bulk deletion) with Microsoft Graph

Once we have completed the GPO to Intune transition, we would probably like to clean up at some point in time. And as for now, the only option within Microsoft Endpoint Manager web portal is to delete each imported GPO manually. So, I’ve gathered some inspiration from our amazing community (Thank you, [Damien Van Robaeys](https://twitter.com/syst_and_deploy)) and came up with a few small scripts samples that will perform a bulk deletion based on a keyword or just delete everything.\
\
Download the cleanup script from the GitHub repository [here](https://github.com/SuneThomsenDK/OSDSUNE/tree/master/Scripts/GroupPolicyAnalytics)\
\
First, let’s go to [https://intune.microsoft.com](https://intune.microsoft.com)\
Click **Devices | Group Policy analytics (preview)**\
\
Okay, we have completed the GPO to Intune transition and now want to clean up in Microsoft Endpoint Manager. But as you can see from the below screenshot, we can only delete each imported GPO manually! That’s not a big deal if it’s only a few GPOs, but what if you have imported several hundred policies? Then it would turn out to be a much more cumbersome task to complete, Right?

<figure><img src="https://drive.google.com/uc?id=1s0coHR3yhprqELgE1FRLaZrcXMxOuGuZ" alt=""><figcaption></figcaption></figure>

Save the cleanup script somewhere on your local device (For example, C:Temp)\
Open the script in an elevated PowerShell ISE session.\
\
If this is your first time working with Microsoft Graph, you need to install and import the module before connecting to Microsoft Graph. – Read more about Microsoft Graph at [What is Microsoft Graph.](https://docs.microsoft.com/en-us/graph/overview)\
\
Mark the first three lines of the script and hit **F8** or click on the **Run Selection** button.

<figure><img src="https://drive.google.com/uc?id=1k42ZybzjNMhmFodYhbgEn_4gRo3chExH" alt=""><figcaption></figcaption></figure>

You will be prompt for authentication.

<figure><img src="https://drive.google.com/uc?id=1UAbB8z-N4AMsM6R0Xfs3POPmPI_nJ4-Z" alt=""><figcaption></figcaption></figure>

If the authentication is a success, you should see your UPN and Tenant ID, and we are ready to run our samples.

<figure><img src="https://drive.google.com/uc?id=19wVYxfBIUHVvs9ninUUuGUvy2PeqH-m3" alt=""><figcaption></figcaption></figure>

Mark a sample in the script. – I chose the sample that deletes every imported GPO in Group Policy analytics.\
Hit **F8** or click on the **Run Selection** button.\
\
You can see from the PowerShell output that all three GPOs are listed.

<figure><img src="https://drive.google.com/uc?id=1wvdcVDsJ4APlc7I4Sv83uZJMBKG93xes" alt=""><figcaption></figcaption></figure>

Let’s switch back to Microsoft Endpoint Manager and see if the imported GPOs have been deleted. – Success, they are all gone!

<figure><img src="https://drive.google.com/uc?id=1c-d0ZKEte2Oz-fTJn-KxuKkHtve9Cdhn" alt=""><figcaption></figcaption></figure>

I have created this small GIF to show you the cleanup process.

<figure><img src="https://drive.google.com/uc?id=1Jk5_7brbP7OI6ZNYcdtUyexELlS6zzRP" alt=""><figcaption></figcaption></figure>

## Summary

In this article, you learned how to export GPOs from Group Policy management on-prem using PowerShell and do a proper cleanup with Microsoft Graph after you have completed your GPO to Intune transition. – That’s it, folks. Happy testing!\
\
If you have any questions regarding this topic, please feel free to reach out to me.
