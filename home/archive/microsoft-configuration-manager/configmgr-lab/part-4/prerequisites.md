# Prerequisites

{% hint style="info" %}
#### WHAT IS PREREQUISITES?

Prerequisites is something that must exist or happen before something else can exist or happen. So for example. The Active Directory Schema need to be extended before Microsoft Endpoint Configuration Manager can be installed on the server.
{% endhint %}

## INSTALLING PREREQUISITES

Log into to the CM server, and we will start installation and configuration of the required prerequisites for Microsoft Endpoint Configuration Manager.

### Disk Management

I've chosen to spread the load on multiple drives and as I mentioned in the beginning of Part 4, I have already prepared the Virtual Hard Disks. So the first thing we want to do here is make them online, assign drive letters and formatting them in NTFS file system.

{% hint style="info" %}
I would recommend formatting the SQL drives in NTFS file system and allocation unit size (block size) must be 64K (Default is 4K)
{% endhint %}

| **Drive** | **Content**     | **Size** |
| --------- | --------------- | -------- |
| C:\\      | Windows         | 127GB    |
| E:\\      | ConfigMgr       | 200GB    |
| F:\\      | SQL Database    | 75GB     |
| G:\\      | SQL Logs        | 50GB     |
| H:\\      | SQL TempDB      | 50GB     |
| I:\\      | Content Sources | 200GB    |
| J:\\      | Content Library | 200GB    |

#### **NO\_SMS\_ON\_DRIVE.SMS**

Place a file named "**NO\_SMS\_ON\_DRIVE.SMS**" in the root of each drive that shouldn’t be used by CM.

**Step 1.** Type "**Disk**" in the search line next to the start button, and click "**Create and format hard disk partitions**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_01.JPG)

**Step 2.** All the disks is in a Offline state. So right-click on "**Disk 1**" and select "**Online**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_02.JPG)

![Configuration Manager - Prerequisite](<../../../../.gitbook/assets/CM_PREREQUISITES_03 (1).JPG>)

**Step 3.** Right-click on "**Disk 1**" and select "**Initialize Disk**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_04.JPG)

**Step 4.** Leave everything default and click "**OK**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_05.JPG)

**Step 5.** Right-click the striped area and select "**New Simple Volume**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_06.JPG)

**Step 6.** Click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_07.JPG)

**Step 7.** Leave everything default and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_08.JPG)

**Step 8.** Assign the drive letter and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_09.JPG)

**Step 9.** Set file system to "**NTFS**", leave allocation unit size as "**Default**", give the volume label a descriptive name and click "**Next**"

{% hint style="info" %}
I would recommend formatting the SQL drives in NTFS file system and allocation unit size (block size) must be 64K (Default is 4K)
{% endhint %}

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_10.JPG)

**Step 10.** Verify the settings and click "**Finish**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_11.JPG)

**Step 11.** Repeat step 2 to 10 for all the remaining Virtual Hard Disks and you should end up with something similar to the images below.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_12.JPG)

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_13.JPG)

**Step 12.** Go to the "**SQL Database**" drive, create a folder called "**Database**" and add the "**NO\_SMS\_ON\_DRIVE.SMS**" file to the root of this drive.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_14-1.JPG)

**Step 13.** Go to the "**SQL Logs**" drive, create a folder called "**Logs**" and add the "**NO\_SMS\_ON\_DRIVE.SMS**" file to the root of this drive.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_14-2.JPG)

**Step 14.** Go to the "**SQL TempDB**" drive, create a folder called "**Database**" and add the "**NO\_SMS\_ON\_DRIVE.SMS**" file to the root of this drive.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_14-3.JPG)

**Step 15.** Add the "**NO\_SMS\_ON\_DRIVE.SMS**" file to the root of all remaining drives except the "**Content Library**" drive.

### Firewall Configuration

Make sure that Windows Firewall is turned on. We need to add some inbound rules and I've gathered a list of the CM rules that I add with an GPO, I would also recommend you to open for Echo Request (ping) and Remote Desktop.

| **Name**                                            | **Action** | **Protocol** | **Port**    |
| --------------------------------------------------- | ---------- | ------------ | ----------- |
| **ConfigMgr - Analysis Services**                   | Allow      | TCP          | 2382, 2383  |
| **ConfigMgr - Boot Information Negotiation Layer**  | Allow      | UDP          | 4011        |
| **ConfigMgr - Client notification**                 | Allow      | TCP          | 10123       |
| **ConfigMgr - Dynamic Host Configuration Protocol** | Allow      | UDP          | 67, 68      |
| **ConfigMgr - Hypertext Transfer Protocol**         | Allow      | TCP          | 80, 8530    |
| **ConfigMgr - Multicast Protocol**                  | Allow      | UDP          | 63000-64000 |
| **ConfigMgr - RPC Endpoint Mapper (TCP)**           | Allow      | TCP          | 135         |
| **ConfigMgr - RPC Endpoint Mapper (UDP)**           | Allow      | UDP          | 135         |
| **ConfigMgr - Secure Hypertext Transfer Protocol**  | Allow      | TCP          | 443, 8531   |
| **ConfigMgr - Server Message Block (SMB)**          | Allow      | TCP          | 445         |
| **ConfigMgr - SQL**                                 | Allow      | TCP          | 1433, 1434  |
| **ConfigMgr - SQL Broker**                          | Allow      | TCP          | 4022        |
| **ConfigMgr - Trivial File Transfer Protocol**      | Allow      | UDP          | 69          |
| **ConfigMgr - Wake-on-Lan (WOL)**                   | Allow      | UDP          | 9           |
| **ConfigMgr - Wake-up proxy**                       | Allow      | UDP          | 25536       |
| **ConfigMgr - Windows Update Delta Content**        | Allow      | TCP          | 8005        |

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_15.JPG)

### Server Roles & Features

We need to add a few Server Roles and Features to the CM server. Before adding the "**.NET Framework 3.5**" feature, we need to mount the "**Windows Server 2019**" media because we need a file from it.&#x20;

Open Windows PowerShell in Administrator elevated mode and follow the steps below.

**Step 1.** To add the "**.NET Framework 3.5**" feature, run the below command. The source is the "**Windows Server 2019**" media, and the drive letter may therefore be different from the example below.

```
Install-WindowsFeature NET-Framework-Features -source D:\sources\sxs
```

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_16.JPG)

**Step 2.** To add the remaining Server Roles and Features, run the below command.

```
Install-WindowsFeature Web-Static-Content,Web-Default-Doc,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Redirect,Web-Net-Ext,Web-ISAPI-Ext,Web-Http-Logging,Web-Log-Libraries,Web-Request-Monitor,Web-Http-Tracing,Web-Windows-Auth,Web-Filtering,Web-Stat-Compression,Web-Mgmt-Tools,Web-Mgmt-Compat,Web-Metabase,Web-WMI,BITS,RDC
```

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_17.JPG)

**Step 3.** Ensure that the exit code says "**Success**" before moving on.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_18.JPG)

### Windows 10 ADK & WinPE

{% hint style="info" %}
Windows 10 ADK and WinPE can be download from [here](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install) (_They are two separate downloads..._)
{% endhint %}

**Step 1.** Start the Windows 10 ADK installation. Leave everything default and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_19.JPG)

**Step 2.** Select "**No**" and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_20.JPG)

**Step 3.** Click "**Accept**" to the License Agreement.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_21.JPG)

**Step 4.** Select "**Deployment Tools**" and "**User State Migration Tool (USMT)**" and click "**Install**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_22.JPG)

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_23.JPG)

**Step 5.** Click "**Close**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_24.JPG)

**Step 6.** Start the WinPE installation. Leave everything default and click "**Install**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_25.JPG)

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_26.JPG)

**Step 7.** Click "**Close**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_27.JPG)

### ConfigMgr Accounts & Groups

Before we continue it's important that we create a few accounts and groups in our Active Directory. I'll be referring to the following accounts and groups throughout the blog post.

| **Name**              | **Type** | **Description**                                                        |
| --------------------- | :------: | ---------------------------------------------------------------------- |
| **Svc.ClientPush**    |   User   | Service Account for Client Push Installation                           |
| **Svc.NetworkAccess** |   User   | Service Account for Accessing Network Resources                        |
| **Svc.Sql**           |   User   | Service Account for SQL/Reporting                                      |
| **Svc.TaskSequence**  |   User   | Service Account for Task Sequence/Domain Join                          |
| **CM Administrators** |   Group  | Members in this group grants full permissions in Configuration Manager |
| **CM Servers**        |   Group  | This group contains all site system servers                            |

{% hint style="info" %}
Add "**CM Administrators**" and "**CM Servers**" to the local administrator group on the site server. If you got multiple site servers I'll recommend you adding them with an GPO.
{% endhint %}

### AD Schema Extension

Since this is a new environment with no previous Configuration Manager installations, we need to extend the Active Directory Schema, but first we'll have to mount the "**Configuration Manager**" media to the DC server.

**Step 1.** Add the "**Configuration Manager**" media to the DC server.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_28.JPG)

**Step 2.** Log into to the DC server with an account that is a member of the security group Schema Admins. Navigate to "**.\SMSSETUP\BIN\X64\\**" on the mounted "**Configuration Manager**" media and execute "**extadsch.exe**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_29.JPG)

**Step 3.** Verify that Active Directory Schema were successfully extended by checking the "**ExtADSch.log**" file which is located in the root of the system drive.

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_30.JPG)

**Step 4.** Type "**ADSI**" in the search line next to the start button, and click "**ADSI Edit**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_31.JPG)

**Step 5.** Right-click on "**ADSI Edit**" and select "**Connect to...**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_32.JPG)

**Step 6.** Leave everything default and click "**OK**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_33.JPG)

**Step 7.** Right-click on "**CN=System**" and create a new "**Object...**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_34.JPG)

**Step 8.** Select the "**Container**" class and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_35.JPG)

**Step 9.** Type "**System Management**" as the value and click "**Next**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_36.JPG)

**Step 10.** Click "**Finish**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_37.JPG)

**Step 11.** Right-click on "**CN=System Management**" and select "**Properties**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_38.JPG)

**Step 12.** Go to the "**Security**" tab and click on "**Advanced**". Add the primary site server "**CM**" and the security group "**CM Servers**" that we created in our Active Directory earlier. Give them both "**Full Control**" and select "**This object and all descendant objects**" in the "**Applies to:**" list.

Click "**Apply**" and close the "**ADSI Edit**"

![Configuration Manager - Prerequisite](../../../../.gitbook/assets/CM_PREREQUISITES_39.JPG)

![Configuration Manager - Prerequisite](<../../../../.gitbook/assets/CM_PREREQUISITES_40 (1).JPG>)

## Windows Update

Before continuing with the SQL installation and configuration, it´s important to check for Windows Updates once again. The reason for this is that Windows Server 2019 probably need to re-apply the cumulative update in order for the new server roles and features to function correct.

{% hint style="info" %}
The Windows Update process is covered in the main section. Click "**Previous**" below or click "**Part 4 - Setting up Microsoft Endpoint Configuration Manager**" in the menu to the left.
{% endhint %}

Now that we have successfully installed and configured the required prerequisites for Microsoft Endpoint Configuration Manager, let's move on to the SQL installation and configuration.&#x20;

Click "**Next**" below or click "**SQL**" in the menu to the left.
