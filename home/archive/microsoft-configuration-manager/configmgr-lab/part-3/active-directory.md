# Active Directory

## SETTING UP ACTIVE DIRECTORY

{% hint style="info" %}
#### WHAT IS ACTIVE DIRECTORY?

Active Directory Domain Service (**AD DS**) is a directory service developed by Microsoft for Windows domain network. It is included in most Microsoft Windows Server operating systems as a set of processes and services. Initially, Active Directory was only in charge of centralized domain management.&#x20;

Starting with Windows Server 2008, however, Active Directory became an umbrella title for a broad range of directory-based identity-related services.

Read more about Active Directory Domain Services [here](https://docs.microsoft.com/en-us/windows/win32/ad/about-active-directory-domain-services)
{% endhint %}

Log into the DC server, and we will start setting up the Active Directory server role for my LAB environment.

### Installing Active Directory

**Step 1.** Click "**Add roles and features**" in the Server Manager.

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/16_WinServer2019_Config_AD.JPG)

**Step 2.** Click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/17_WinServer2019_Config_AD.JPG)

**Step 3.** Leave everything default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/18_WinServer2019_Config_AD.JPG)

**Step 4.** Leave everything default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/19_WinServer2019_Config_AD.JPG)

**Step 5.** Select "**Active Directory Domain Services**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/20_WinServer2019_Config_AD.JPG)

**Step 6.** Leave everything default and click "**Add Features**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/21_WinServer2019_Config_AD.JPG)

**Step 7.** Leave everything default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/22_WinServer2019_Config_AD.JPG)

**Step 8.** Click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/23_WinServer2019_Config_AD.JPG)

**Step 9.** Check the "**Restart the destination server automatically if required**" box and click "**Install**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/24_WinServer2019_Config_AD.JPG)

**Step 10.** This might take a while, so click "**Close**" and go grab a cup of coffee:sunglasses:&#x20;

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/25_WinServer2019_Config_AD.JPG)

### Configuring Active Directory

**Step 1.** When the server role installation is done, we should now see a yellow triangle with an exclamation mark in the Server Manager, click on it and then click "**Promote this server to a domain controller**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/26_WinServer2019_Config_AD.JPG)

**Step 2.** Check "**Add a new forest**", enter a "**Root Domain Name**" and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/27_WinServer2019_Config_AD.JPG)

**Step 3.** Enter a password for DSRM, leave the rest as default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/28_WinServer2019_Config_AD.JPG)

**Step 4.** Leave everything default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/29_WinServer2019_Config_AD.JPG)

**Step 5.** The NetBIOS domain name is populated automatically after a few second, it is possible to change the NetBIOS domain name, but I choose to leave it as default for my LAB environment.

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/30_WinServer2019_Config_AD.JPG)

**Step 6.** Leave everything default and click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/31_WinServer2019_Config_AD.JPG)

**Step 7.** Click "**Next**"

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/32_WinServer2019_Config_AD.JPG)

{% hint style="info" %}
#### BONUS INFO

If you click "**View script**" you can actually save it as a PowerShell script and re-use it the next time you have to create a new Active Directory Forest.
{% endhint %}

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/33_WinServer2019_Config_AD.JPG)

**Step 8.** The system will now verify all the prerequisites, this might take a few seconds to validate. You will see the message "**All prerequisite checks passed successfully.**" if everything went as it should.&#x20;

The yellow triangle with an exclamation mark is okay since this is a new LAB environment. For example, I do not have any existing Windows DNS server in my environment, so I can just ignore that "warning".

Click "**Install**" (_The system should reboot automatically during this process..._)

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/34_WinServer2019_Config_AD.JPG)

**Step 9.** After a reboot the Active Directory installation is done and you should be able to log on to the domain for the first time.

![Windows Server 2019 - Active Directory](../../../../.gitbook/assets/35_WinServer2019_Config_AD.JPG)

Now that we have successfully installed and configured the Active Directory server role on my DC server, let's move on to the DHCP server role installation. Click "**Next**" below or click "**DHCP**" in the menu to the left.
