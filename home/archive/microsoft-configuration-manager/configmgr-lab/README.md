---
description: 04-12-2020 5:39 PM
---

# ConfigMgr: Building a Basic LAB Environment

## BEFORE YOU BEGIN

{% hint style="warning" %}
**Disclaimer**: All information and content in these blog posts is provided without any warranty whatsoever. The entire risk of using this information or executing the provided content remains with you. Under no circumstances should Microsoft, its author, or anyone else involved in the creation of these blog posts be held liable for any damage or data loss.
{% endhint %}

## INTRODUCTION

In this series of blog posts I will walk you through a complete installation of a basic Microsoft Endpoint Configuration Manager LAB environment built on a Intel NUC 8i7BEH device.

It will be some relatively detailed step by step guides, which will include the following:

**Part 1** - [Installing Windows 10 (1909) on the Host](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-1)

_A review of the hardware specification and a walk-through of the Windows 10 (1909) installation, where I will demonstrate how to create disk partition by using a small script._

**Part 2** - [The Host and Hyper-V Configuration](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-2)

_Setting up the Hyper-V role and creating a NAT Virtual Switch by using PowerShell so that we can keep the LAB environment separate from the rest of the network, but still provide internet access to the VMs._

**Part 3** - [Setting up the Domain Controller](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-3)

_A walk-through of the Windows Server 2019 installation and we I will be setting up the Active Directory, DHCP, and DNS._

**Part 4** - [Setting up Microsoft Endpoint Configuration Manager](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-4)

_A walk-through of the basic installation of Microsoft Endpoint Configuration Manager including the SQL, Distribution Point and Management Point configuration._

**Part 5** - [Setting up Discovery Methods and Boundaries](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-5)

_Setting up discovery methods for users, systems etc. and configure boundaries and boundary groups._

**Part 6** - [Setting up Software Update Point](https://www.osdsune.com/home/blog/2020/configmgr-lab/part-6)

_Setting up the site system role for Software Update Point and I will give you a walk-through of the maintenance configuration for SQL and WSUS._

If you have any questions regarding these topics, feel free to reach out to me. I am most active on [Twitter](https://www.twitter.com/SuneThomsenDK)!

Let's get started, click "**Next**" below.
