---
description: 24-05-2023 9:34 PM
---

# How to create a custom image for Windows 365 Enterprise Cloud PCs

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer:** All information and content in this blog post is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should the mentioned persons or vendors, the author, or anyone else involved in creating these blog posts be held liable for any damage or data loss.
{% endhint %}

<figure><img src="https://drive.google.com/uc?id=1nlWjM-mbY23cEV5zDlk7PRRgETH4vy2_" alt=""><figcaption><p><em>Windows 365 Enterprise Cloud PC with a custom Windows 11 image on my son’s iPad.</em></p></figcaption></figure>

## Introduction

A few months back I wrote a blog post about how to configure Windows 365 Enterprise in Microsoft Endpoint Manager, which was provisioned with a standard gallery Windows 10 image and after Windows 11 became generally available, my Cloud PC was successfully reprovisioned with a standard gallery Windows 11 image. – It just works!

But what if you would like to provision your Cloud PC(s) with a custom image (also known as a Golden Image)? Well Microsoft understand the need for this and since it is supported in Windows 365 I believe it’s time for yet another Windows 365 post and this time I will walk you through the process of how to provision your Cloud PC(s) with a custom Windows 11 image.\
\
The original blog post about – [How to configure Windows 365 Enterprise in Microsoft Endpoint Manager](https://www.osdsune.com/home/blog/2021/configure-windows-365-enterprise)\
The blog post about – [How to reprovision existing Cloud PC (Windows 365) to Windows 11](https://www.osdsune.com/home/blog/2021/how-to-reprovision-existing-cloud-pc-windows-365-to-windows-11)

## Creating a custom image for Windows 365 Enterprise

If I connect to my current Windows 365 Cloud PC we can see that it is running Windows 11 and the system locale is “**en-US**” at the moment and no extra application has been installed since this Cloud PC is provisioned with a standard gallery image.

<figure><img src="https://drive.google.com/uc?id=1tPChl6MW_ytxWd0Ic_oKdfKsgiXOV3LR" alt=""><figcaption></figcaption></figure>

Let’s create a custom Windows 11 image for Windows 365 Cloud PCs.\
Go to [https://portal.azure.com](https://portal.azure.com/)\
\
Search for “**Virtual Machines**” and select the service from the list.

<figure><img src="https://drive.google.com/uc?id=1uuW-8KmoVKlPL1DjnA0k9DiYIKWNs-Nu" alt=""><figcaption></figcaption></figure>

Click **Create** and select **Virtual machine**.

<figure><img src="https://drive.google.com/uc?id=1RelojcHFFIjmDl8I23IfjuQbtInfAykf" alt=""><figcaption></figcaption></figure>

Fill in all the required fields and click on “**See all images**”

<figure><img src="https://drive.google.com/uc?id=1A5IsTy0qv5B9forPidWQa3lKDY_NSLxJ" alt=""><figcaption></figcaption></figure>

Search for “**Cloud PC**” and click **Select**.

<figure><img src="https://drive.google.com/uc?id=1cCma2d2vW6E4rLOdyh9JqhIOzvIFwG7O" alt=""><figcaption></figcaption></figure>

Select “**Windows 11 Enterprise Cloud PC + Microsoft 365 Apps – Gen 2**” from the list.

<figure><img src="https://drive.google.com/uc?id=1K5j0uHx2n2SkrvB2eWmF3NOkD59dKrBG" alt=""><figcaption></figcaption></figure>

Fill in the rest of the required fields.\
**Note**. It’s important that security type is set to “**Standard**” and that VM generation is “**Gen 2**”. – Microsoft does not support Gen 1 images as part of Windows 365 Enterprise.

Click on **Next**.

<figure><img src="https://drive.google.com/uc?id=1z-p3n59SiSOjIaSjIs4b0sW3C9h0HzoW" alt=""><figcaption></figcaption></figure>

Select “**Standard SSD**” as the OS disk type and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1pNxHyRyAZ801uN21v91adp2W4PoMsgBa" alt=""><figcaption></figcaption></figure>

Configure the network interface and click **Next**.

<figure><img src="https://drive.google.com/uc?id=1-8sZ7UAXscgqcseN-k1UylcCFLbDPOWe" alt=""><figcaption></figcaption></figure>

Configure the monitoring and management options and click **Review + Create**.

<figure><img src="https://drive.google.com/uc?id=173wwQPuxBZNDIXB4pwtXddF_ptDTk02m" alt=""><figcaption></figcaption></figure>

Review your configuration and click **Create**.

<figure><img src="https://drive.google.com/uc?id=1eg0TI5PMKmx0WjObsRQQ_pimdfZthIia" alt=""><figcaption></figcaption></figure>

After a few minutes you should see that the deployment has completed.\
Click on “**Go to resource**”

<figure><img src="https://drive.google.com/uc?id=1KlJd09X7W2WTeGa3bcl0NZPOxPov6qUs" alt=""><figcaption></figcaption></figure>

Once the VM has been created, you should see that the VM is running and that it is assigned a private IP address. Make note of the assigned private IP address, you will need it to connect to the VM via RDP.

<figure><img src="https://drive.google.com/uc?id=1xVLrYyTc3DYz1gVTqI7mjPm1FqEXqPmk" alt=""><figcaption></figcaption></figure>

Connect to the VM with either Azure Bastion or RDP.

<figure><img src="https://drive.google.com/uc?id=1mlvjsFwSD0T18okqbRDNYOq3VYsf-hpg" alt=""><figcaption></figcaption></figure>

I’ve added a Danish language pack and installed the latest OS updates to the image.\
For the purpose of this blog post I’ve added a few applications: **7-Zip** | **Adobe Acrobat Reader DC** | **Notepad++**

<figure><img src="https://drive.google.com/uc?id=1cFVGpkyjavBnj_eKLXPekltq55QDXyr3" alt=""><figcaption></figcaption></figure>

Once you are done with the customizations, run this sysprep command:\
**sysprep.exe /generalize /shutdown /oobe**

<figure><img src="https://drive.google.com/uc?id=1JQ66rEkxlg3ry4JrJ_5RMS698ydlPYPA" alt=""><figcaption></figcaption></figure>

Go to “**Virtual Machines**” in the Azure Portal and put the VM into a stopped (deallocated) state.\
Click on **Capture**.

<figure><img src="https://drive.google.com/uc?id=1MJOhnf0dfVbTuMLKfj6iaFnPi_EN92qv" alt=""><figcaption></figcaption></figure>

Create or choose an existing resource group, select “**No, capture only a managed image.**” give the image a name and click **Review + create**.

<figure><img src="https://drive.google.com/uc?id=1oDIbU0-114Y03hlSZLq949qrOM7XzzaL" alt=""><figcaption></figcaption></figure>

Click on **Create**.

<figure><img src="https://drive.google.com/uc?id=1UqJdOBqv3E9_ujYqRr7TsbUL2CR6Lshn" alt=""><figcaption></figcaption></figure>

After a few minutes you should see that the deployment has completed.

<figure><img src="https://drive.google.com/uc?id=1EeOQvhttemq2RFFOsRLT5UTBMz-Qidmx" alt=""><figcaption></figcaption></figure>

## Provision the custom image to your Windows 365 Enterprise Cloud PC(s)

Let’s add the new custom Windows 11 image to our provisioning policy.\
Go to [https://intune.microsoft.com](https://intune.microsoft.com)

Click on **Devices | Windows 365 | Device images**.

<figure><img src="https://drive.google.com/uc?id=151Jj_Om7MVdHz5_CeASde52iyTxWY4D6" alt=""><figcaption></figcaption></figure>

Click on **add**, fill in the required fields and click **Add** again.\
**Note**. The upload process will take approx. 30 minutes to complete.

<figure><img src="https://drive.google.com/uc?id=1l3CT_kFdg0wwFcr--8_H8OWWK7mZYkck" alt=""><figcaption></figcaption></figure>

Once the upload process is completed, click on the “**Provisioning policies**” tab.

<figure><img src="https://drive.google.com/uc?id=1zuGdiCeVB66a5b5_xYCCJM1ud8zZIZgs" alt=""><figcaption></figcaption></figure>

Create a new provisioning policy or modify an existing policy.\
I chose to modify an existing policy and then I reprovisioned my Windows 365 Cloud PC.

**Note**. Creating a new provisioning policy is described in our original Windows 365 blog post.\
[How to configure Windows 365 Enterprise in Microsoft Endpoint Manager](https://www.osdsune.com/home/blog/2021/configure-windows-365-enterprise)

Select your provisioning policy.

<figure><img src="https://drive.google.com/uc?id=1EiVFzAidOMnPd5n-cG0DmJ6ghhUbdYlu" alt=""><figcaption></figcaption></figure>

Click on **Edit**.

<figure><img src="https://drive.google.com/uc?id=1Gsu6EpIuachOPly3pFmVaP8EeiDjAfX3" alt=""><figcaption></figcaption></figure>

Change the image type to “**Custom image**” and click on **Select.**\
Select your custom Windows 11 image, click **Select** and then click **Next**.

<figure><img src="https://drive.google.com/uc?id=140zxX5ohlBPoPN8xbLh5xibY1Mfqgls7" alt=""><figcaption></figcaption></figure>

Click on **Update**.

<figure><img src="https://drive.google.com/uc?id=1dVAR2AaxCflpG6kEXHDt144O_-Wl8dBJ" alt=""><figcaption></figcaption></figure>

Click on **Devices | Windows 365 | All Cloud PCs** or **Devices | Windows.** \
Select your Cloud PC from the list of devices and click on **Reprovision**.\
Click **Yes**.

<figure><img src="https://drive.google.com/uc?id=1JqRjfl4FdQt5ducy1Pa4vHBAU4aWL8Ys" alt=""><figcaption></figcaption></figure>

<figure><img src="https://drive.google.com/uc?id=1Ft5w-uNR_CAV3xXtH_1icKJULczi4pIj" alt=""><figcaption></figcaption></figure>

Approximately 1 hour later and your new Cloud PC with a custom Windows 11 image will be ready for use.\
Success! My Windows 365 Cloud PC is now in Danish and the added applications are still present for the user logged on…

<figure><img src="https://drive.google.com/uc?id=1dlnNQ_SwBxena7q7jPW9Ki2NnPkn37VZ" alt=""><figcaption></figcaption></figure>

## Summary

Now you know how to create a custom Windows 11 image for your Windows 365 Cloud PC(s). I do understand the need and why Microsoft support custom images in Windows 365, and I think it makes great sense in scenarios where you want to apply a few baseline applications and/or language packs to your custom image. But it is also my recommendation that you keep the image as clean as possible to leave a very small footprint and then let Microsoft Endpoint Manager and Intune add other applications, and configuration settings. Happy testing!

As always, if you have any questions regarding this topic, feel free to reach out to me.
