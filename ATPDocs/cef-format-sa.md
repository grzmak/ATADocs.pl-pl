---
title: "Azure odwołanie dziennika ATP SIEM | Dokumentacja firmy Microsoft"
description: "Udostępnia przykłady podejrzanych działań dzienniki wysyłane z Azure ATP do rozwiązania SIEM."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 5d466014d96edb2deecf0c5d7b937d9e576a57b0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Odwołanie do dziennika Azure ATP SIEM

Azure ATP może przekazywać podejrzane działania i monitorowanie zdarzeń alertów do rozwiązania SIEM. Zdarzenia podejrzanych działań są w formacie CEF. Ten artykuł dokumentacji zawiera przykłady dzienników podejrzanych działań wysyłanych do rozwiązania SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Przykładowe Azure ATP podejrzane działania w formacie CEF
Następujące pola i ich wartości są przekazywane do rozwiązania SIEM:

-   start — czas rozpoczęcia alertu
-   suser — konto (zwykle jest to konto użytkownika), którego dotyczy alert
-   shost — maszyna źródłowa dla tego alertu
-   outcome — wynik (powodzenie/niepowodzenie) wykonywanego działania, którego dotyczy alert  
-   msg — opis alertu
-   CNT — dla alertów, które mają liczbę razy, które generują alerty wystąpił (na przykład siłowych z odpowiednią ilością odgadnięcia hasła)
-   app — protokół używany w tym alercie
-   externalId — zdarzenie ATP Azure identyfikator zapisuje w dzienniku zdarzeń, który odpowiada ten alert
-   cs#label i cs# — są to ciągi klienta dozwolone w formacie CEF; cs#label to nazwa nowego pola, a cs# to wartość, na przykład: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

W tym przykładzie pole cs1 jest polem zawierającym adres URL do alertu.

## <a name="sample-logs"></a>Przykładowe dzienniki

W poniższym przykładzie dzienniki wykonania RFC 5242, ale Azure ATP obsługuje również RFC 3164.

Priorytety:

- 3 = niski
- 5=Medium
- 10 = wysoki

### <a name="bruteforce--ldap"></a>BruteForce — LDAP
2018-02-21 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + ï CENTER CEF 6076 LdapBruteForceSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Ataków siłowych przy użyciu prostego powiązania LDAP | 5 | start = 2018-02-aplikacji 21T14:19:41.7422810Z = Ldap suser Wofford Thurston shost = = KLIENT1 msg = ataków siłowych za pomocą podjęto protokołu Ldap na Wofford Thurston (inżynier oprogramowania) z komputera CLIENT1 (100 wynik prób). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
2018-02-21 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + ï CENTER CEF 6076 BruteForceSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | BruteForceSecurityAlert | Niepowodzenia uwierzytelniania podejrzane | 5 | start = 2018-02-21T14:19:03.3831122Z aplikacji Kerberos shost = = KLIENT1 msg = błędy uwierzytelniania podejrzane wskazujący potencjalnych ataków siłowych wykryto z komputera KLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Podwyższenie poziomu uprawnień
#### <a name="silver"></a>Srebrny
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + ï CENTER CEF 6076 ForgedPacSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Przy użyciu eskalacji uprawnień sfałszowane danych autoryzacji | 10 | start = 2018-02-21T14:19:02.8595383Z aplikacji = Kerberos suser = msg Użytkownik1 = Użytkownik1 próbował podwyższania poziomu uprawnień, aby host/domain1.test.local z komputera CLIENT1 przy użyciu danych autoryzacji sfałszowanego. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Złoty
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + ï CENTER CEF 6076 ForgedPacSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Przy użyciu eskalacji uprawnień sfałszowane danych autoryzacji | 10 | start = 2018-02-21T14:19:02.8595383Z aplikacji = Kerberos suser = msg Użytkownik1 = nie można eskalować uprawnienia na komputerze DC1 do host/domain1.test.local z komputera CLIENT1 przy użyciu danych autoryzacji sfałszowanego Użytkownik1. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Sfałszowany bilet uwierzytelniania Golden Ticket
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="honey-token-activity"></a>Działania związane z kontem wystawionym jako przynęta
2018-02-21 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + ï CENTER CEF 6076 HoneytokenActivitySecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Działanie wystawionego jako przynęta | 5 | start = 2018-02-21T14:20:26.6705617Z aplikacji = suser protokołu Kerberos = msg wystawione jako przynęta = następujące działania były wykonywane przez wystawione jako przynęta: \r\nLogged w do komputera KLIENT2 za pośrednictwem DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Podejrzana replikacja usług katalogowych
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych
02-21-2018  16:22:08    Auth.Error  192.168.0.220   1 2018-02-21T14:21:54.080266+00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-02-21T14:19:41.8382786Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Ataki typu Over-Pass-the-Hash
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + ï CENTER CEF 6076 EncryptionDowngradeSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Działanie obniżenia poziomu szyfrowania | 5 | start = 2018-02-aplikacji 21T14:19:41.8737870Z = komunikaty protokołu Kerberos = metodę szyfrowania pola Encrypted_Timestamp AS_REQ obniżono wiadomości z komputera CLIENT1, na podstawie zachowania uprzednio zapamiętane. Przyczyną może być kradzież poświadczeń przy użyciu ataku typu Over-Pass-the-Hash z maszyny KLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Ataki typu Pass-the-Hash
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://test-syslog.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Wyliczanie kont
2018-02-21 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + ï CENTER CEF 6076 AccountEnumerationSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekonesans przy użyciu wyliczania kont | 5 | start = 2018-02-21T14:19:02.6045416Z aplikacji Kerberos shost = = KLIENT1 suser = LMaldonado msg = konto podejrzane działanie wyliczenie przy użyciu protokołu Kerberos, pochodzących z komputera CLIENT1 zaobserwowano i pomyślnie odgadnąć Lamon Maldonado (inżynier oprogramowania). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>Rekonesans DNS
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + ï CENTER CEF 6076 DnsReconnaissanceSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekonesans przy użyciu systemu DNS | 5 | start = 2018-02 — 21T14:19:41.9417776Z aplikacji Dns shost = = KLIENT1 żądania = demo requestMethod zapytania = Przyczyna Axfr = brak błędu wynik = Powodzenie msg = podejrzane DNS zaobserwowano działania pochodzące z komputera KLIENT1 (który nie jest serwerem DNS). Kwerenda ma dla zapytania pokaz (typ Axfr). Odpowiedź jest brak błędu. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>Wyliczanie sesji SMB
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + ï CENTER CEF 6076 EnumerateSessionsSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekonesans przy użyciu wyliczenie sesji SMB | 5 | start = 2018-02-21T14:19:03.2071170Z app SrvSvc shost = = KLIENT1 msg = sesji SMB pomyślnie przeprowadzono próby wyliczenia Użytkownik1 z komputera CLIENT1 przed DC1, udostępnianie Eugene Wpięć (Użytkownik2 komputer) . externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>SAM-R — wyliczenie
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + ï CENTER CEF 6076 SamrReconnaissanceSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekonesans przy użyciu wyliczania katalogu usług | 5 | start = 2018-02-21T14:19:41.9912772Z aplikacji Samr shost = = KLIENT1 suser = Użytkownik1 wynik = Powodzenie msg = następujące usługi katalogowe wyliczenia przy użyciu protokołu SAMR została użyta przed DC1 z Wyliczenie CLIENT1:\r\nSuccessful wszystkich grup w domain1.test.local za pomocą konta user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Zdalne wykonywanie kodu
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + ï CENTER CEF 6076 RemoteExecutionSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Wykryto próbę wykonania zdalnego | 5 | start = 2018-02-21T14:19:41.9912772Z aplikacji Wmi shost = = KLIENT1 suser = Użytkownik1 wynik = Powodzenie msg = następujące zdalne wykonywanie prób zostały wykonane na komputerze DC1 z CLIENT1:\r\nSuccessful zdalne wykonywanie kodu WMI co najmniej jeden metody za pomocą konta user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Wytrych
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + ï CENTER CEF 6076 EncryptionDowngradeSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Działanie obniżenia poziomu szyfrowania | 5 | start = 2018-02-aplikacji 21T14:19:41.8737870Z = komunikaty protokołu Kerberos = metodę szyfrowania pola ETYPE_INFO2 KRB_ERR obniżono wiadomości z komputera CLIENT1, na podstawie zachowania uprzednio zapamiętane. Może to być wynikiem Skeleton Key na komputerze DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + ï CENTER CEF 6076 AbnormalProtocolSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Implementacja nietypowego protokołu | 5 | start = 2018-02-21T14:19:03.1981155Z aplikacji Ntlm shost = = wynik KLIENT2 = Powodzenie msg = zostały prób uwierzytelnienia od komputera KLIENT2 przed DC1 przy użyciu implementacja nietypowego protokołu. Przyczyną może być użycie złośliwych narzędzi służących na przykład do wykonywania ataków typu Pass-the-Hash lub ataków siłowych. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Tworzenie złośliwe usługi
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Ataki typu Pass-the-Ticket

2018-02-21 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + ï CENTER CEF 6076 PassTheTicketSecurityAlert 00:00 "¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | PassTheTicketSecurityAlert | Kradzieży tożsamości za pomocą ataku Pass--Ticket | 10 | start = 2018-02-21T15:02:22.2577465Z aplikacji = Kerberos suser = msg Eugene Wpięć = Kerberos Eugene Wpięć (inżynier oprogramowania) na kradzieży z komputera administratora do komputera Victom i umożliwiają dostęp do krbtgt/domena1 biletów. TEST. LOKALNE. externalId=2017 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)