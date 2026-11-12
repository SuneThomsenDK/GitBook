---
description: 04-12-2020 5:39 PM
---

# Part 3 - Setting up the Domain Controller

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

## DC CONFIGURATION

In my previous blog post [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2) we created a NAT Switch for my Hyper-V LAB environment and prepared a Virtual Machine for the domain controller (**DC**) installation. In Part 3, I will walk you through the Windows Server 2019 installation for my DC server and we will be configuring Active Directory, DHCP and DNS.

{% hint style="info" %}
#### WHAT IS A DOMAIN CONTROLLER?

A server running Active Directory Domain Service (**AD DS**) is called a domain controller (**DC**) and it responds to security authentication requests within a Windows domain network. The domain controller is the centerpiece of the Active Directory Domain Services. It authenticate users, stores account information, and enforces security policies.

Read more about Active Directory Domain Services [here](https://docs.microsoft.com/en-us/windows/win32/ad/about-active-directory-domain-services)
{% endhint %}

Since the Virtual Machine for my DC server, has already been created in [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2) and the ISO image is mounted, let's get started with the Windows Server 2019 installation.

### Windows Server Installation

Start the Virtual Machine and boot from the mounted Windows Server 2019 ISO image.

**Step 1.** Select language and click "**Next**"

![Windows Server 2019 - Installation](../../../../.gitbook/assets/01_WinServer2019_Install.JPG)

**Step 2.** Click "**Install now**"

![Windows Server 2019 - Installation](../../../../.gitbook/assets/02_WinServer2019_Install.JPG)

**Step 3.** Select which server edition you want to install (I prefer one with "**Desktop Experience**") and click "**Next**"

{% hint style="info" %}
For a **Standard** vs. **Datacenter** comparison, please visit this [page](https://docs.microsoft.com/en-us/windows-server/get-started-19/editions-comparison-19)
{% endhint %}

![Windows Server 2019 - Installation](../../../../.gitbook/assets/03_WinServer2019_Install.JPG)

**Step 4.** Read the License Terms, check the "**I accept the license terms**" box and click "**Next"**

![Windows Server 2019 - Installation](../../../../.gitbook/assets/04_WinServer2019_Install.JPG)

**Step 5.** Select "**Custom: Install Windows Only (advanced)**"

![Windows Server 2019 - Installation](../../../../.gitbook/assets/05_WinServer2019_Install.JPG)

**Step 6.** Leave everything default and click "**Next**"

![Windows Server 2019 - Installation](../../../../.gitbook/assets/06_WinServer2019_Install.JPG)

**Step 7.** Windows Server 2019 should now start installing.

![Windows Server 2019 - Installation](../../../../.gitbook/assets/07_WinServer2019_Install.JPG)

**Step 8.** After a few minutes (_depending on hardware configuration..._) you should be presented with the "**Customize settings**" page. Enter a password for the local Administrator account and click "**Finish**"

![Windows Server 2019 - Installation](../../../../.gitbook/assets/08_WinServer2019_Install.JPG)

**Step 9.** The installation is now done and you can log into the Windows Server 2019 for the first time, with the local Administrator account.

![Windows Server 2019 - Installation](../../../../.gitbook/assets/09_WinServer2019_Install.JPG)

### Windows Server Configuration

The very first thing I like to do after a Windows Server 2019 installation and before adding server roles, is renaming the server and configure the network settings.

**Step 1.** Close the Server Manager.

![Windows Server 2019 - Configuration](../../../../.gitbook/assets/10_WinServer2019_Config.JPG)

**Step 2.** Type "**About**" in the search line next to the start button, and click "**About your PC**"

![Windows Server 2019 - Configuration](../../../../.gitbook/assets/11_WinServer2019_Config.JPG)

**Step 3.** In the middle of the "**About**" page, click "**Rename this PC**", give it a new name and click "**Next**". You don't have to reboot at this point, because we will reboot the server after configuring the network.

![Windows Server 2019 - Configuration](<../../../../.gitbook/assets/12_WinServer2019_Config (1).JPG>)

**Step 4.** In the search line, type "**View network**" and click "**View network status and tasks**"

![Windows Server 2019 - Configuration](../../../../.gitbook/assets/13_WinServer2019_Config.JPG)

**Step 5.** Click "**Ethernet**"

![Windows Server 2019 - Configuration](../../../../.gitbook/assets/14_WinServer2019_Config.JPG)

**Step 6.** Click "**Properties**", then select "**Properties**" for "**Internet Protocol Version 4 (TCP/IPv4)**", add the IP addresses for the DC server and click "**OK**" to complete the configuration.

{% hint style="info" %}
Give it a default gateway, subnet mask and a static IP address from the private IP range we created in [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2#hyper-v-nat-virtual-switch) during the Hyper-V configuration.
{% endhint %}

![Windows Server 2019 - Configuration](<../../../../.gitbook/assets/15_WinServer2019_Config (1).JPG>)

**Step 7.** Reboot the DC server, we will start adding the server roles to it afterwards.

## ADDING SERVER ROLES

{% hint style="info" %}
I've decided, that since this would become a very large blog post, it would be best to split the server role installations into sub-sections.&#x20;

So please click on the desired server role in the menu to the left, or click on the links below.
{% endhint %}

### Active Directory

{% content-ref url="active-directory.md" %}
[active-directory.md](active-directory.md)
{% endcontent-ref %}

### DHCP

{% content-ref url="dhcp.md" %}
[dhcp.md](dhcp.md)
{% endcontent-ref %}

### DNS

{% content-ref url="dns.md" %}
[dns.md](dns.md)
{% endcontent-ref %}

## Windows Update

So now that we have completed the above installation and configuration of my DC server, there's only one thing missing and that's Windows Update, so let's do that as the final step.

**Step 1.** Type "**Windows Update**" in the search line next to the start button, and click "**Windows Update settings**"

![Windows Server 2019 - Windows Update](../../../../.gitbook/assets/71_WinServer2019_Config_DNS.JPG)

**Step 2.** Click "**Check for updates**" and wait.

![Windows Server 2019 - Windows Update](../../../../.gitbook/assets/72_WinServer2019_Config_WU.JPG)

![Windows Server 2019 - Windows Update](../../../../.gitbook/assets/73_WinServer2019_Config_WU.JPG)

**Step 3.** When it's done, reboot the DC server.

![Windows Server 2019 - Windows Update](../../../../.gitbook/assets/74_WinServer2019_Config_WU.JPG)

This should conclude the domain controller (**DC**) installation and configuration. In [Part 4](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-4) I will walk you through the basic installation of Microsoft Endpoint Configuration Manager including the SQL, Distribution Point and Management Point configuration.

If you have any questions regarding this topic, feel free to reach out to me. I am most active on [Twitter](https://twitter.com/SuneThomsenDK)!
