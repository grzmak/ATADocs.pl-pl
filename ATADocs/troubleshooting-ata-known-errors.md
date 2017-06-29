---
# required metadata

title: Troubleshooting the Advanced Threat Analytics error log | Microsoft Docs 
description: Describes how you can troubleshoot common errors in ATA 
keywords:
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/14/2017
ms.topic: article
ms.prod:
ms.service: advanced-threat-analytics
ms.technology:
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: arzinger

ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

*Applies to: Advanced Threat Analytics version 1.7*



# Troubleshooting the ATA error log

This section details possible errors in the deployments of ATA and the steps required for troubleshooting them.

## ATA Gateway errors

|Error|Description|Resolution|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: A local error occurred|The ATA Gateway failed to authenticate against the domain controller.|1. Confirm that the domain controller’s DNS record is configured properly in the DNS server. <br>2. Verify that the time of the ATA Gateway is synchronized with the time of the domain controller.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Failed to validate certificate chain|The ATA Gateway failed to validate the certificate of the ATA Center.|1. Verify that the Root CA certificate is installed in the trusted certificate authority certificate store on the ATA Gateway. <br>2. Validate that the certificate revocation list (CRL) is available and that certificate revocation validation can be performed.|
|Microsoft.Common.ExtendedException: Failed to parse time generated|The ATA Gateway failed to parse syslog messages that were forwarded from the SIEM.|Verify that the SIEM is configured to forward the messages in one of the formats that are supported by ATA.|
|System.ServiceModel.FaultException: An error occurred when verifying security for the message.|The ATA Gateway failed to authenticate against ATA Center.|Verify that the time of the ATA Gateway is synchronized with the time of the ATA Center.|
|System.ServiceModel.EndpointNotFoundException: Could not connect to net.tcp://center.ip.addr:443/IEntityReceiver|The ATA Gateway failed to establish connection to the ATA Center.|Ensure that the network settings are correct and that the network connection between the ATA Gateway and the ATA Center is active.|
|System.DirectoryServices.Protocols.LdapException: The LDAP server is unavailable.|The ATA Gateway failed to query the domain controller using the LDAP protocol.|1.Verify that the user account used by ATA to connect to the Active Directory domain has read access to all the objects in the Active Directory tree. <br>2.Make sure that the domain controller is not hardened to prevent LDAP queries from the user account used by ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Contract exception|The ATA Gateway failed to synchronize the configuration from the ATA Center.|Complete configuration of the ATA Gateway in the ATA Console.|
|System.Reflection.ReflectionTypeLoadException: Unable to load one or more of the requested types. Retrieve the LoaderExceptions property for more information.|Message Analyzer is installed on the ATA Gateway.| Uninstall Message Analyzer.|
|Error [Layout] System.OutOfMemoryException: Exception of type 'System.OutOfMemoryException' was thrown.|The ATA Gateway does not have enough memory.|Increase the amount of memory on the domain controller.|
|Fail to start live consumer  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: The PEFNDIS event provider is not ready|PEF (Message Analyzer) was not installed correctly.|If using Hyper-V, try to upgrade Hyper-V Integration services otherwise, contact support for a workaround.|
|Installation failed with error: 0x80070652|There are other pending installations on your computer.|Wait for the other installations to complete and, if necessary, restart the computer.|
|System.InvalidOperationException: Instance 'Microsoft.Tri.Gateway' does not exist in the specified Category.|PIDs was enabled for process names in the ATA Gateway|Use [KB281884](https://support.microsoft.com/en-us/kb/281884) to disable PIDs in process names|
|System.InvalidOperationException: Category does not exist.|Counters might be disabled in the registry|Use [KB2554336](https://support.microsoft.com/en-us/kb/2554336) to rebuild Performance Counters|
|System.ApplicationException: Unable to start ETW session MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|There is a host entry in the HOSTS file pointing to the machine's shortname|Remove the host entry from C:\Windows\System32\drivers\etc\HOSTS file or change it to an FQDN.|
|System.IO.IOException: Authentication failed because the remote party has closed the transport stream.|TLS 1.0 is disabled on the ATA Gatewau but .Net is set to use TLS 1.2|Use one of the following options: </br> Enable TLS 1.0 on the ATA Gateway </br>Enable TLS 1.2 on .Net by setting the registry keys to use the operating system defaults for LLS and TLS, as follows: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`|



## ATA Lightweight Gateway errors

**Error**: Dropped port mirror traffic alerts when using Lightweight Gateway on VMware

**Description**: If you are using DCs on VMware virtual machines, you might receive alerts about **Dropped port mirrored network traffic**. This might be due to a configuration mismatch in VMware. 
**Resolution**: To avoid these alerts, you can check that the following settings are set to 0 or Disabled:  TsoEnable, LargeSendOffload, IPv4, TSO Offload. Also, consider disabling IPv4 Giant TSO Offload. For more information consult your VMware documentation.


## ATA IIS errors (Not applicable for ATA v1.7 and above)
|Error|Description|Resolution|
|-------------|----------|---------|
|HTTP Error 500.19 – Internal Server Error|The IIS URL Rewrite module failed to install correctly.|Uninstall and reinstall the IIS URL Rewrite module.<br>[Download the IIS URL Rewrite module](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Deployment errors
|Error|Description|Resolution|
|-------------|----------|---------|
|.Net Framework 4.6.1 installation fails with error 0x800713ec|The pre-requisites for .Net Framework 4.6.1 are not installed on the server. |Before installing ATA, verify that the windows updates [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) and [KB2919355](https://support.microsoft.com/kb/2919355) are installed on the server.|

![ATA .NET installation error image](media/netinstallerror.png)


## See Also
- [ATA prerequisites](ata-prerequisites.md)
- [ATA capacity planning](ata-capacity-planning.md)
- [Configure event collection](configure-event-collection.md)
- [Configuring Windows event forwarding](configure-event-collection.md#configuring-windows-event-forwarding)
- [Check out the ATA forum!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
