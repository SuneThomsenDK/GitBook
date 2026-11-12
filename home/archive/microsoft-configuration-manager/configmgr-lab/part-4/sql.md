# SQL

{% hint style="info" %}
#### WHAT IS SQL?

Structured Query Language (**SQL**) lets you access and manipulate databases. It became a standard of the American National Standards Institute (**ANSI**) in 1986, and of the International Organization for Standardization (**ISO**) in 1987.

Read more about SQL [here](https://en.wikipedia.org/wiki/SQL)
{% endhint %}

## SQL SERVER 2019 INSTALLATION

After installing and configuring the required prerequisites for Microsoft Endpoint Configuration Manager, it's time to install and configure the SQL Server 2019, so log into to the CM server, and we'll get started.

{% hint style="info" %}
SQL Server 2019 has some known issues, for more information about that or supported SQL versions click [here](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/support-for-sql-server-versions)
{% endhint %}

**Step 1.** Mount the "**SQL Server 2019**" media to the CM server. Execute the "**Setup.exe**" from the media and click "**New SQL Server stand-alone installation or add features to an existing installation**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_01.JPG)

**Step 2.** Enter a product key or select the "**Evaluation**" edition which will expire after 180 days. Click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_02.JPG)

**Step 3.** Check the "**I accept the license terms and Privacy Statement**" box and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_03.JPG)

**Step 4.** Check the "**Use Microsoft Update to check for updates (recommended)**" box and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_04.JPG)

**Step 5.** The below "**Windows Firewall**" warning is OK! But if you are getting any errors or warnings at this step, I would always advise you to read the details before proceeding with the installation.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_05.JPG)

**Step 6.** Select "**Database Engine Services**" and change the directory drive letter to "**E:\\**" which is the ConfigMgr drive.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_06.JPG)

**Step 7.** Leave everything default and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_07.JPG)

**Step 8.** Set the "**SQL Server Agent**" and "**SQL Server Database Engine**" services to run with the SQL service account that we created earlier and set the startup type to "**Automatic**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_08.JPG)

**Step 9.** Click on the "**Collation**" tab. Set "**Database Engine:**" to use "**SQL\_Latin1\_General\_CP1\_CI\_AS**" and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_09.JPG)

**Step 10.** Select "**Windows authentication mode**". Add the "**Current User**" and "**CM Administrators**" group as SQL Server administrators.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_10.JPG)

**Step 11.** Click on the "**Data Directories**" tab and change the path for "**User database**" and "**User database log**" directory. Also make sure that the "**Data root**" and "**Backup**" directory is set to use the drive letter "**E:\\**" which is the ConfigMgr drive.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_11-1.JPG)

**Step 12.** Click on the "**TempDB**" tab and change the path for "**Data**" and "**Log**" directory. During this step I made an mistake with the database sizing and I will show you how to correct it in the step "**TempDB Correction**" further down in this post.&#x20;

Here's the correct approach during the setup wizard.

{% hint style="info" %}
For estimating the database size, I am using a Excel file created by [Kent Agerlund](https://twitter.com/agerlund) which can be downloaded [here](https://blog.ctglobalservices.com/configuration-manager-sccm/kea/system-center-2012-configuration-manager-sql-recommendations/)
{% endhint %}

I will create an database for 2000 Clients, 1 Processor, 8 Cores and 32 GB of Memory.

![Configuration Manager - SQL](<../../../../.gitbook/assets/CM_SQL_35 (1).JPG>)

According to the Excel calculations, the TempDB values should be as shown in the table below. So, as already mentioned, change the path for "**Data**" and "**Log**" directory, add the below values and click "**Next**"

| **TempDB Data files**  | **Value** |
| ---------------------- | --------- |
| **Number of files:**   | 8         |
| **Initial size (MB):** | 567       |
| **Autogrowth (MB):**   | 256       |

| **TempDB Log file**    | **Value** |
| ---------------------- | --------- |
| **Initial size (MB):** | 2268      |
| **Autogrowth (MB):**   | 512       |

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_13.JPG)

**Step 13.** Verify that the SQL Server 2019 features to be installed is correct and click "**Install**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_14.JPG)

**Step 15.** Everything should be completed successfully. Click "**Close**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_15.JPG)

### SQL Management Studio

SQL Server Management Studio (**SSMS**) can be downloaded from [here](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)

**Step 1.** Download and execute "**SSMS-Setup-ENU.exe**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_16.JPG)

**Step 2.** Change the drive letter of the location to "**E:\\**" which is the ConfigMgr drive. Click "**Install**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_17.JPG)

**Step 3.** Click "**Restart**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_18.JPG)

### SQL Reporting Services

SQL Server 2019 Reporting Services (**SSRS**) can be downloaded from [here](https://www.microsoft.com/en-us/download/details.aspx?id=100122)

**Step 1.** Log into to the CM server. Download and execute "**SQLServerReportingServices.exe**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_16.JPG)

**Step 2.** Click "**Install Reporting Services**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_19.JPG)

**Step 3.** Enter a product key or select the "**Evaluation**" edition which will expire after 180 days. Click "**Next**"

{% hint style="info" %}
#### BONUS INFO

If you didn't note down the product key during SQL installation, you can actually find it in the "**.\x64\DefaultSetup.ini**" file on the "**SQL Server 2019**" media.
{% endhint %}

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_20.JPG)

**Step 4.** Check the "**I accept the license terms**" box and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_21.JPG)

**Step 5.** Click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_22.JPG)

**Step 6.** Change the drive letter of the location to "**E:\\**" which is the ConfigMgr drive. Click "**Install**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_23.JPG)

**Step 7.** Click "**Close**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_24.JPG)

### SQL Server 2019 Update

Latest Microsoft SQL Server 2019 Updates can be downloaded from [here](https://sqlserverbuilds.blogspot.com/#sql2019x)

**Step 1.** Download and execute "**SQLServer2019-KBXXXXXXX-x64.exe**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_16.JPG)

**Step 2.** Check the "**I accept the license terms and Privacy Statement**" box and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_25.JPG)

**Step 3.** Leave everything default and click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_26.JPG)

**Step 4.** Click "**Next**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_27.JPG)

**Step 5.** Click "**Update**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_28.JPG)

**Step 6.** Click "**Close**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_29.JPG)

### Service Principal Names

When configuring the SQL server to use a domain account instead of the local system account, you must manually register the Service Principal Name (**SPN**) for the domain account.

**Step 1.** Log into the CM server with an Domain Administrator account. Type "**CMD**" in the search line next to the start button, and click "**Command Prompt**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_30.JPG)

**Step 2.** Run the below commands to create the SPN.

```
# Change the HOST, DOMAIN and ACCOUNT name for each command
# Run the following commands to create the SPN

setspn -A MSSQLSVc/HOST:1433 DOMAIN\ACCOUNT
setspn -A MSSQLSVc/HOST.DOMAIN.LOCAL:1433 DOMAIN\ACCOUNT

# Run this command to verify the SPN creation

setspn –L DOMAIN\ACCOUNT
```

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_31.JPG)

## SQL Server Configuration

Now that we are done with the SQL server installation, it's time to configure it:sunglasses:

**Step 1.** Type "**Microsoft SQL Server**" in the search line next to the start button, and click "**Microsoft SQL Server Management Studio 18**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_32.JPG)

**Step 2.** Right-click on the "**CM (SQL Server...)**" node and select "**Properties**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_33.JPG)

**Step 3.** Select the "**Memory**" page and set "**Minimum server memory**" to 8192 MB and the "**Maximum server memory**" to 25600 MB which is 80% of the total system memory.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_34.JPG)

### CM Database Creation

It´s not required, but I recommend creating the CM database before installing CM. As mentioned during the SQL server installation, I'm using a Excel file to estimate the database size.

{% hint style="info" %}
For estimating the database size, I am using a Excel file created by Kent Agerlund which can be downloaded [here](https://blog.ctglobalservices.com/configuration-manager-sccm/kea/system-center-2012-configuration-manager-sql-recommendations/)
{% endhint %}

I will create an database for 2000 Clients, 1 Processor, 8 Cores and 32 GB of Memory.

![Configuration Manager - SQL](<../../../../.gitbook/assets/CM_SQL_35 (1).JPG>)

According to the Excel calculations, the ConfigMgr DB values should be as shown in the table below.

| **ConfigMgr DB**    | **Value** |
| ------------------- | --------- |
| **Number of files** | 8         |
| **Size per file**   | 1890      |
| **Autogrowth**      | 624       |

| **ConfigMgr Log** | **Value** |
| ----------------- | --------- |
| **Size per file** | 4990      |
| **Autogrowth**    | 512       |

With that in mind I've modified a SQL query created by [SystemCenterDudes](https://twitter.com/scdudes) to fit my needs.

I'm using "**PS1**" as my site code, but if you are going to use another site code or path for the database and log file, then please remember to change it in the SQL query below before executing it.

{% hint style="info" %}
I've found my inspiration to this SQL query on a [blog post](https://www.systemcenterdudes.com/complete-sccm-installation-guide-and-configuration/) created by [SystemCenterDudes](https://twitter.com/scdudes) but please keep in mind that I'm no SQL query guru and it ain't perfect but it'll do:nerd:
{% endhint %}

```
USE master
GO
CREATE DATABASE CM_PS1 ON ( NAME = CM_PS1_1, FILENAME = 'F:\Database\CM_PS1_1.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
LOG ON ( NAME = PS1_log, FILENAME = 'G:\Logs\CM_PS1.ldf', SIZE = 4990, MAXSIZE = 25600, FILEGROWTH = 512)
GO
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_2, FILENAME = 'F:\Database\CM_PS1_2.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_3, FILENAME = 'F:\Database\CM_PS1_3.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_4, FILENAME = 'F:\Database\CM_PS1_4.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_5, FILENAME = 'F:\Database\CM_PS1_5.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_6, FILENAME = 'F:\Database\CM_PS1_6.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_7, FILENAME = 'F:\Database\CM_PS1_7.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
ALTER DATABASE CM_PS1 ADD FILE ( NAME = CM_PS1_8, FILENAME = 'F:\Database\CM_PS1_8.mdf', SIZE = 1890, MAXSIZE = Unlimited, FILEGROWTH = 624)
```

**Step 1.** Open "**Microsoft SQL Server Management Studio 18**" and click on "**New Query**" from the toolbar. Copy / Paste my SQL query and make your changes before executing it.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_36.JPG)

**Step 2.** Verify that the database and log file has been created.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_37.JPG)

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_38.JPG)

**Step 3.** From "**Microsoft SQL Server Management Studio 18**" right-click on the database "**CM\_PS1**" and select "**Properties**". Verify that the collation is set to "**SQL\_Latin1\_General\_CP1\_CI\_AS**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_39.JPG)

**Step 4.** Click on the "**Files**" page and change the owner to "**SA**". Verify that the Size, Autogrowth / Maxsize and Path is correct.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_40.JPG)

**Step 5.** Click on the "**Options**" page, change "**Recovery model**" to use "**Simple**" and click "**OK**"

![Configuration Manager - SQL](<../../../../.gitbook/assets/CM_SQL_41 (1).JPG>)

### TempDB Correction

{% hint style="warning" %}
#### You can skip this step, if you didn't make the same mistake as i did:laughing:
{% endhint %}

Okay, as I mentioned during the SQL server installation, I made a mistake with the TempDB creation, so here's my way to correct this afterwards.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_35.JPG)

According to the Excel calculations, the TempDB values should be as shown in the table below. Take these values an add them to the below SQL query.

| **TempDB DB**     | **Value** |
| ----------------- | --------- |
| **Size per file** | 567       |
| **Autogrowth**    | 256       |

| **TempDB Log**    | **Value** |
| ----------------- | --------- |
| **Size per file** | 2268      |
| **Autogrowth**    | 512       |

```
USE master
GO
ALTER DATABASE tempdb MODIFY FILE (NAME = tempdev, FILENAME = 'H:\Database\tempdb.mdf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp2, FILENAME = 'H:\Database\tempdb_mssql_2.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp3, FILENAME = 'H:\Database\tempdb_mssql_3.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp4, FILENAME = 'H:\Database\tempdb_mssql_4.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp5, FILENAME = 'H:\Database\tempdb_mssql_5.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp6, FILENAME = 'H:\Database\tempdb_mssql_6.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp7, FILENAME = 'H:\Database\tempdb_mssql_7.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
ALTER DATABASE tempdb MODIFY FILE (NAME = temp8, FILENAME = 'H:\Database\tempdb_mssql_8.ndf', SIZE = 567, MAXSIZE = Unlimited, FILEGROWTH = 256)
GO
ALTER DATABASE tempdb MODIFY FILE (NAME = templog, FILENAME = 'G:\Logs\templog.ldf', SIZE = 2268, MAXSIZE = Unlimited, FILEGROWTH = 512)
```

**Step 1.** Open "**Microsoft SQL Server Management Studio 18**" and click on "**New Query**" from the toolbar. Copy / Paste my SQL query and make your changes before executing it.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_42.JPG)

**Step 2.** Right-click on the database "**tempdb**" and select "**Properties**". Click on the "**Files**" page and make sure that the owner is set to "**SA**". Verify that the Size, Autogrowth / Maxsize and Path is correct.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_43.JPG)

**Step 3.** Verify that the database and log file has been changed.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_44.JPG)

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_45.JPG)

### SQL Network Configuration

We can make a few changes to the SQL Server Network Configuration to ensure a proper SQL communication.

**Step 1.** Type "**SQL Server 2019**" in the search line next to the start button, and click "**SQL Server 2019 Configuration Manager**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_46.JPG)

**Step 2.** Expand the "**SQL Server Network Configuration**", right-click on "**Protocols for MSSQLSERVER**" and select "**Properties**". Ensure that "**Enabled**" is set to "**Yes**" and "**Listen All**" is set to "**No**"

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_47.JPG)

**Step 3.** Click on the "**IP Addresses**" tab and find the IP setting containing the IP address of your CM server and make sure "**Enabled**" is set to "**Yes**". Set "**Enabled**" to "**No**" for the remaining IP settings.

![Configuration Manager - SQL](../../../../.gitbook/assets/CM_SQL_48.JPG)

## WSUS SERVER ROLE

This blog post won't be covering the Software Update Point (**SUP)** installation, but I'll prepare the WSUS server role and database for an upcoming blog post covering this part.

**Step 1.** Open the "**Server Manager**" and click "**Add Roles and Features**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_49.JPG)

**Step 2.** Click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_50.JPG)

**Step 3.** Leave everything default and click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_51.JPG)

**Step 4.** Leave everything default and click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_52.JPG)

**Step 5.** Select "**Windows Server Update Services**". Leave everything default and click "**Add Features**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_53.JPG)

**Step 6.** Leave everything default and click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_54.JPG)

**Step 7.** Click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_55.JPG)

**Step 8.** Select "**WSUS Services**" and "**SQL Server Connectivity**" on the role services list. Click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_56.JPG)

**Step 9.** Navigate to the ConfigMgr drive (**E:\\**) and create a WSUS folder in the root.

Return to the "**Add Role and Features Wizard**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_57.JPG)

**Step 10.** Add the WSUS folder path and click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_58.JPG)

**Step 11.** Enter the fully qualified domain name (**FQDN**) of your SQL server and click "**Next**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_59.JPG)

**Step 12.** Check the "**Restart the destination server automatically if required**" box and click "**Install**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_60.JPG)

**Step 13.** Click "**Close**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_61.JPG)

**Step 14.** When the WSUS server role installation is done, we should see a yellow triangle with an exclamation mark in the "**Server Manager**", click on it and then click "**Launch Post-Installation tasks**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_62.JPG)

### SQL Database Configuration

The WSUS server role are now installed and we'll make a few changes to the WSUS database.

**Step 1.** Type "**Microsoft SQL Server**" in the search line next to the start button, and click "**Microsoft SQL Server Management Studio 18**"

![Configuration Manager - WSUS](<../../../../.gitbook/assets/CM_SQL_32 (1).JPG>)

**Step 2.** Right-click on the database "**SUSDB**" and select "**Properties**". Click on the "**Files**" page and change the owner to "**SA**". Change the "**SUSDB**" autogrowth to 512 MB and limit the "**SUSDB\_log**" to 10240 MB.

Click "**OK**" when done.

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_63.JPG)

### IIS Configuration

As the final step, we'll make a few important changes to the WSUS Application Pool in the Internet information Services (**IIS**) Manager.

{% hint style="info" %}
The computer that hosts a software update point requires the following configurations for IIS application pools.

* Increase the **WsusPool Queue Length** to **2000**.
* Increase the **WsusPool Private Memory limit** by four times, or set it to **0** (unlimited).

**Source**: [Microsoft Docs](https://docs.microsoft.com/en-us/configmgr/core/plan-design/configs/recommended-hardware#bkmk_RemoteSiteSystem)
{% endhint %}

**Step 1.** Type "**IIS**" in the search line next to the start button, and click "**Internet information Services (IIS) Manager**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_64.JPG)

**Step 2.** Navigate to the "**Application Pools**". Right-click on "**WsusPool**" and select "**Advanced Settings...**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_65.JPG)

**Step 3.** Change the "**Queue Length**" to 2000.

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_66.JPG)

**Step 4.** Change the "**Private Memory Limit (KB)**" to 0 and click "**OK**"

![Configuration Manager - WSUS](../../../../.gitbook/assets/CM_SQL_67.JPG)

This concludes the SQL installation and configuration. Go back to the main section by clicking on the link below or click "**Part 4 - Setting up Microsoft Endpoint Configuration Manager**" in the menu to the left.

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}
