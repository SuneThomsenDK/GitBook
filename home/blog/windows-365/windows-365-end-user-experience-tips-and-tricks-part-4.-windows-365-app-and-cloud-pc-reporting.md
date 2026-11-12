---
description: 02-06-2023 2:40 PM
cover: ../../.gitbook/assets/Part4.jpg
coverY: -37
---

# Windows 365 End-User Experience (Tips & Tricks) – Part 4. Windows 365 app and Cloud PC reporting

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

Welcome to **Part 4** in this new **Windows 365 End-User Experience** blog series. This series will be an educational journey exploring several features that can potentially help improve the end-user experience.\
\
**Below you’ll find all parts of this blog series**.

* [Windows 365 End-User Experience (Tips & Tricks) – Part 1. Connection Experience](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-1.-connection-experience)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 2. Teams Optimization, SSO, and Localization](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-2.-teams-optimization-sso-and-localization)
* [Windows 365 End-User Experience (Tips & Tricks) – Part 3. Multimedia Redirection](https://www.osdsune.com/home/blog/windows-365/windows-365-end-user-experience-tips-and-tricks-part-3.-multimedia-redirection)
* [**Windows 365 End-User Experience (Tips & Tricks) – Part 4. Windows 365 app and Cloud PC reporting**](windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting.md)

**In this part, I**‘**ll cover the following topics**.

* [**The Windows 365 App**](windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting.md#w365app)
* [**Endpoint Analytics & Cloud PC Performance**](windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting.md#reporting)
* [**Summary**](windows-365-end-user-experience-tips-and-tricks-part-4.-windows-365-app-and-cloud-pc-reporting.md#summary)

## The Windows 365 app <a href="#w365app" id="w365app"></a>

Microsoft announced the general availability (GA) of the Windows 365 app for Windows 10/11 in February 2023.\
\
With the Windows 365 app, you have a direct path to your Windows 365 Cloud PC straight from the taskbar or the Start menu, which provides a seamless end-user experience while switching between your local desktop and Cloud PCs.\
\
The Windows 365 app provides several key value-adds and enhanced user experiences, such as:

* Multiple monitor support, which is enabled by default.
* Support for fullscreen and window mode with dynamic resizing.
* Self-servicing capabilities like Restart, Restore, Rename, and troubleshooting.
* Support for RDP Shortpath, Microsoft Teams Optimization, and Multimedia redirection (MMR).
* Support for Azure Active Directory (Azure AD) Multi-Factor Authentication (MFA).
* Single sign-on experience.
* And more…

{% hint style="info" %}
&#x20;**Note:** By default, the restore self-servicing option is not available. You must configure a user setting policy in your environment to enable this functionality for the end users.
{% endhint %}

The Windows 365 app lets you access details about the Cloud PC assigned to your account, connect, and utilize self-servicing features by clicking on the ellipsis symbol (three dots). If you have used Cloud PCs before through a web browser, the Windows 365 app experience should feel familiar.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App01-1024x624.png" alt="Windows 365 app - User Actions"><figcaption></figcaption></figure>

### **How to get the Windows 365 app**

The Windows 365 app is available through the Microsoft Store on Windows endpoints. The Microsoft Store will ensure you always use the most up-to-date version of the app. To get the Windows 365 app:

#### **Get it from the Microsoft Store**

1. Go to **Microsoft Store** for Windows.
2. Search for the Windows 365 app.
3. Click **Get** to install the Windows 365 app.
4. When the installation is complete, click **Open** to launch the app.

#### **Get it from the Windows 365 Web Portal**

1. Go to [**https://windows365.microsoft.com**](https://windows365.microsoft.com/)
2. From the **Download** page, click **Go to Microsoft Store**.
3. Click **Get** to install the Windows 365 app.
4. When the installation is complete, click **Open** to launch the app.

{% hint style="info" %}
&#x20;**Note:** In the future, Microsoft will ship the Windows 365 app with Windows 11.
{% endhint %}

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App02-1024x461.png" alt="Windows 365 app - Microsoft Store"><figcaption></figcaption></figure>

### **Deploy the Windows 365 app through Microsoft Intune**

IT admins do also have the option to deploy the Windows 365 app through Microsoft Intune, which allows for easy distribution to Windows endpoints. Let’s explore how to achieve this in this section.\
\
Go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Apps | Windows**\
Click **Add**.\
Select the **Microsoft Store app (new)** in the app type drop-down menu and click **Select**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App03-1024x497.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

Click **Search the Microsoft Store app (new)** on the **App information** page and search for **Windows 365**. Next, choose the app from the list and click **Select**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App04-1024x499.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App05-1024x918.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

Select scope tags if needed and click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App06-1024x609.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

On the **Assignments** page, we configure this to be a required deployment. Select **Add group** and choose an Azure AD group containing users with a Windows 365 license. We will also apply a filter to exclude Windows 365 Cloud PCs from this deployment.\
Click **Next**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App07-1024x606.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

Review the configuration and click **Create**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/W365App08-1024x993.png" alt="Microsoft Intune - Windows 365 app deployment."><figcaption></figcaption></figure>

That concludes the section on the Windows 365 app. – In this section, we learned that the Windows 365 app provides a direct path from your Windows endpoints to the Windows 365 Cloud PCs and offers various value-adds, including self-service capabilities and support for some of the features covered in this blog series. We also learned that we could deploy the app through Microsoft Intune, allowing easy distribution to your Windows endpoints.

## Endpoint Analytics & Cloud PC Performance <a href="#reporting" id="reporting"></a>

As stated at the beginning of this blog series, we will now examine which tools are available for monitoring Cloud PC performance, connection quality, and utilization in your environment. Please note that this section will not provide any technical depth into the tools mentioned. Instead, I will highlight what’s available and where to find it in Microsoft Intune, which should enable you to explore these tools in greater depth on your own.

### **Endpoint analytics | Resource performance report**

The resource performance report in **Endpoint analytics** helps you optimize CPU and RAM resources on the Cloud PC devices in your organization.\
\
To get to the resource performance report, go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Reports** | **Endpoint analytics** | **Resource performance**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Resouce_Performance01-1024x640.png" alt="Resource performance report"><figcaption></figcaption></figure>

#### **Resource performance score tab**

The resource performance score is an overall performance rating (from 0 to 100) for all the Cloud PCs that you manage. This score is a weighted average of CPU and RAM Spike time scores.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Resouce_Performance02.png" alt="Resource performance report"><figcaption></figcaption></figure>

#### **Model performance tab**

Review the CPU and RAM spike time score and percentage per Cloud PC model type (SKU) in your organization.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Resouce_Performance03-1024x387.png" alt="Resource performance report"><figcaption></figcaption></figure>

#### **Device performance tab**

Review the CPU and RAM spike time score and percentage per Cloud PC in your organization.&#x20;

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Resouce_Performance04-1-1024x392.png" alt="Resource performance report"><figcaption></figcaption></figure>

#### &#x20;**Device history**

If the device score for a particular device falls below the baseline, you can improve its performance and score by allocating more resources to the device. – This is done by performing a resize action.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Resouce_Performance05-1024x468.png" alt="Resource performance report"><figcaption></figcaption></figure>

_Source:_ [_**Microsoft Learn**_](https://learn.microsoft.com/en-us/windows-365/enterprise/report-resource-performance)

### **Endpoint analytics | Remoting connection report**

The remoting connection report in **Endpoint analytics** helps you monitor key performance metrics for connecting to the Cloud PCs.\
\
To get to the remoting connection report, go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Reports** | **Endpoint analytics** | **Remoting connection**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Remoting_Connection01-1024x574.png" alt="Remoting connection report"><figcaption></figcaption></figure>

#### **Remoting connection tab**

Review key performance metrics for connecting to your Cloud PCs and how it impacts user connectivity. With sign-in time, we provide the time it takes to connect to the Cloud PC. Round trip time (RTT) provides insights into the speed and reliability of network connections from the user location.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Remoting_Connection02.png" alt="Remoting connection report"><figcaption></figcaption></figure>

#### **Model performance tab**

Review the round trip time (RTT) and Cloud PC sign-in time per Cloud PC model type (SKU) in your organization.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Remoting_Connection03-1024x509.png" alt="Remoting connection report"><figcaption></figcaption></figure>

#### **Device performance tab**

Review the round trip time (RTT) and Cloud PC sign-in time per Cloud PC in your organization.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Remoting_Connection04-1024x471.png" alt="Remoting connection report"><figcaption></figcaption></figure>

#### **Device history**

To assess the speed and quality of the connection for this Cloud PC, review the average daily sign-in and round trip time for the last 14 days.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/EA_Report_Remoting_Connection05-1024x355.png" alt="Remoting connection report"><figcaption></figcaption></figure>

_Source:_ [_**Microsoft Learn**_](https://learn.microsoft.com/en-us/windows-365/enterprise/report-remoting-connection)

### **Cloud PC | Utilization report**

You can use the Cloud PC utilization report to ensure your licenses are assigned to active users. Reviewing Cloud PCs with low usage lets you decide if a Windows 365 license would better serve other users who might use these resources more often.\
\
To get to the Cloud PC utilization report, go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Devices | Overview | Cloud PC performance (preview) | View report**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance01-1024x450.png" alt="Cloud PC Utilization report"><figcaption></figcaption></figure>

Review data from the last 28 days to decide how to allocate Cloud PCs and use your license effectively.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance02-1024x439.png" alt="Cloud PC Utilization report"><figcaption></figcaption></figure>

_Source:_ [_**Microsoft Learn**_](https://learn.microsoft.com/en-us/windows-365/enterprise/report-cloud-pc-utilization)

### **Cloud PC | Connection quality report**

The Cloud PC connection quality report helps you evaluate your users’ connection experiences on their Cloud PCs.\
\
To get to the Cloud PC connection quality report, go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Devices | Overview | Cloud PC performance (preview) | View report**

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance03-1024x450.png" alt="Cloud PC Connection quality report"><figcaption></figcaption></figure>

Review the speed and quality of connection for your Cloud PCs.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance04-2-1024x745.png" alt="Cloud PC Connection quality report"><figcaption></figcaption></figure>

_Source:_ [_**Microsoft Learn**_](https://learn.microsoft.com/en-us/windows-365/enterprise/report-cloud-pc-connection-quality)

### **Cloud PC | Performance (preview)**

You can see similar quality data per Cloud PC.\
\
To get to the Cloud PC performance report, go to [**https://intune.microsoft.com**](https://intune.microsoft.com/)\
\
In the left pane, click **Devices | Windows | Windows Devices**\
Select a Cloud PC to review and click **Cloud PC performance (preview)** under **Monitor**.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance05-1024x498.png" alt="Cloud PC Performance (preview)"><figcaption></figcaption></figure>

Review the performance and connection metrics and trends for the Cloud PC.

<figure><img src="http://blog.mindcore.dk/wp-content/uploads/2023/03/CloudPC_Performance06-1024x659.png" alt="Cloud PC Performance (preview)"><figcaption></figcaption></figure>

## Summary <a href="#summary" id="summary"></a>

Wow, what an incredible educational journey this has been for me! Congratulations if you read my entire blog series without losing your sanity. – You deserve a medal!\
\
In this blog series, you learned about the importance of selecting the closest Azure region to where your end users are physically located around the world to provide them with the best possible connection experiences on their Cloud PCs. Throughout this blog series, we’ve explored several features that can potentially help improve the end-user experience, such as:

* Remote Desktop Protocol (RDP) Shortpath
* Microsoft Teams Optimization
* Multimedia redirection (MMR)
* And more…

I could have added many other end-user experience-related topics, but there should also be content for future blog posts, and I had to stop somewhere.\
\
However, here are a few suggestions for other topics you can note down and explore on your own.

* Change google search language in your Cloud PC.
* Notifying end-users when their Cloud PC is provisioned and ready.
* Device and Resource Redirection.
* Enrollment Status Page (ESP)
* Remote Desktop client and auto-subscribe.
* Point in time restore.
* Log collection
* Hardware acceleration

As promised, we concluded this blog series by examining which tools we have at our disposal for monitoring Cloud PC performance, connection quality, and utilization in your environment.\
\
That’s it, folks. Happy testing, and have fun exploring 🤓\
If you have any questions regarding this topic, please feel free to reach out to me.
