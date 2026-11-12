# DHCP

## SETTING UP DHCP

{% hint style="info" %}
#### WHAT IS DHCP?

Microsoft Windows Server operating systems includes Dynamic Host Configuration Protocol (**DHCP**), which is an optional networking server role that you can deploy on your network to lease IP addresses and other information to DHCP clients. All Microsoft Windows client operating systems include the DHCP client as part of TCP/IP, and it's enabled by default.

Read more about Dynamic Host Configuration Protocol [here](https://docs.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top)
{% endhint %}

After installing the Active Directory server role on my DC server, it's time to install and configure the DHCP server role, so log into the DC server again, and we will start setting up the DHCP server role for my LAB environment.

### Installing DHCP

**Step 1.** Click "**Add roles and features**" in the Server Manager.

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/36_WinServer2019_Config_DHCP.JPG)

**Step 2.** Click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/37_WinServer2019_Config_DHCP.JPG)

**Step 3.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/38_WinServer2019_Config_DHCP.JPG)

**Step 4.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/39_WinServer2019_Config_DHCP.JPG)

**Step 5.** Select "**DHCP Server**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/40_WinServer2019_Config_DHCP.JPG)

**Step 6.** Leave everything default and click "**Add Features**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/41_WinServer2019_Config_DHCP.JPG)

**Step 7.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/42_WinServer2019_Config_DHCP.JPG)

**Step 8.** Click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/43_WinServer2019_Config_DHCP.JPG)

**Step 9.** Check the "**Restart the destination server automatically if required**" box and click "**Install**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/44_WinServer2019_Config_DHCP.JPG)

**Step 10.** Click "**Close**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/45_WinServer2019_Config_DHCP.JPG)

### Configuring DHCP

**Step 1.** When the server role installation is done, we should now see a yellow triangle with an exclamation mark in the Server Manager, click on it and then click "**Complete DHCP configuration**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/46_WinServer2019_Config_DHCP.JPG)

**Step 2.** Click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/47_WinServer2019_Config_DHCP.JPG)

**Step 3.** The "**User Name**" is populated automatically, so leave everything as default and click "**Commit**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/48_WinServer2019_Config_DHCP.JPG)

**Step 4.** Click "**Close**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/49_WinServer2019_Config_DHCP.JPG)

### **Configuring DHCP Scope**

**Step 1.** Type "**DHCP**" in the search line next to the start button, and click "**DHCP**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/50_WinServer2019_Config_DHCP.JPG)

**Step 2.** Right-click on "**IPv4**" and then click "**New Scope**"

![Windows Server 2019 - DHCP](<../../../../.gitbook/assets/51_WinServer2019_Config_DHCP (1).JPG>)

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/52_WinServer2019_Config_DHCP.JPG)

**Step 3.** Click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/53_WinServer2019_Config_DHCP.JPG)

**Step 4.** Enter a name and description for the scope and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/54_WinServer2019_Config_DHCP.JPG)

**Step 5.** Enter start and end IP address (**IP range**), a subnet mask and click "**Next**"

{% hint style="warning" %}
Give it a subnet mask and a range of address from the private IP range we created in [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2#hyper-v-nat-virtual-switch) during the Hyper-V configuration.
{% endhint %}

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/55_WinServer2019_Config_DHCP.JPG)

**Step 6.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/56_WinServer2019_Config_DHCP.JPG)

**Step 7.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/57_WinServer2019_Config_DHCP.JPG)

**Step 8.** Select "**Yes, I want to configure these options now**" and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/58_WinServer2019_Config_DHCP.JPG)

**Step 9.** Enter a Router (**Default Gateway**) IP address and click "**Next**"

{% hint style="warning" %}
The Router (**Default Gateway**) IP address is the IP address of the Virtual NIC that we created in [Part 2](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2#hyper-v-nat-virtual-switch) during the Hyper-V configuration.
{% endhint %}

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/59_WinServer2019_Config_DHCP.JPG)

**Step 10.** It should populate the IP address of the DC server automatically. But if that's not the case, then enter a server name and click "**Resolve**". Click "**Add**" to add the IP Address and then click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/60_WinServer2019_Config_DHCP.JPG)

**Step 11.** Leave everything default and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/61_WinServer2019_Config_DHCP.JPG)

**Step 12.** Select "**Yes, I want to activate this scope now**" and click "**Next**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/62_WinServer2019_Config_DHCP.JPG)

**Step 13.** Click "**Finish**"

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/63_WinServer2019_Config_DHCP.JPG)

**Step 14.** Expand the scope and click on "**Address Pool**" to confirm that the IP range has been created.

![Windows Server 2019 - DHCP](<../../../../.gitbook/assets/64_WinServer2019_Config_DHCP (1).JPG>)

**Step 15.** Click "**Scope Options**" to confirm that the Router and DNS settings are configured correct.

![Windows Server 2019 - DHCP](../../../../.gitbook/assets/65_WinServer2019_Config_DHCP.JPG)

This concludes the DHCP installation and configuration on my DC server, let's configure the DNS server role. Click "**Next**" below or click "**DNS**" in the menu to the left.
