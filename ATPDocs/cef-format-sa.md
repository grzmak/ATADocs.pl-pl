---
title: Dokumentacja dzienników w usłudze Azure ATP rozwiązania SIEM | Dokumentacja firmy Microsoft
description: Zawiera przykłady dzienników podejrzanych działań wysyłanych z usługi Azure ATP do rozwiązania SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 1d01f9cc5024404975b01445f9d379dea4d3d0a4
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783920"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-siem-log-reference"></a>Dokumentacja dziennika rozwiązania SIEM zaawansowanej ochrony przed zagrożeniami usługi Azure

Narzędzie Azure ATP może przekazywać zdarzenia alertów do rozwiązania SIEM monitorowania i podejrzanych działań. Zdarzenia podejrzanych działań są w formacie CEF. Ten artykuł dokumentacji zawiera przykłady dzienników podejrzanych działań wysyłanych do rozwiązania SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Przykład usługi Azure ATP podejrzane działania w formacie CEF
Następujące pola i ich wartości są przekazywane do rozwiązania SIEM:

-   start — czas rozpoczęcia alertu
-   suser — konto (zwykle jest to konto użytkownika), którego dotyczy alert
-   shost — maszyna źródłowa dla tego alertu
-   outcome — wynik przypadku Powodzenie/niepowodzenie działania wykonywane, którego dotyczy alert  
-   msg — opis alertu
-   CNT — dotyczy alertów mających liczbę wystąpień, które alert wystąpił (na przykład ataków siłowych zawierających liczbę odgadniętych haseł)
-   app — protokół używany w tym alercie
-   externalId — event ID Azure ATP zapisuje w dzienniku zdarzeń, który odpowiada temu alertowi
-   CS #label i cs # — są to ciągi klienta, umożliwiające w formacie CEF do użycia, cs #label to nazwa nowego pola, a cs # to wartość, na przykład: cs1Label = url cs1 =https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

W tym przykładzie pole cs1 jest polem zawierającym adres URL do alertu.

## <a name="sample-logs"></a>Przykładowe dzienniki

W poniższym przykładzie dzienników jest zgodny z RFC 5242, ale narzędzia Azure ATP obsługuje również RFC 3164.

Priorytety:

- 3 = niski
- 5=Medium
- 10 = wysoki

### <a name="bruteforce--ldap"></a>BruteForce — LDAP
2018-02-21 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 Centrum CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Ataku siłowego przy użyciu prostego powiązania LDAP | 5 | start = 2018-02-21T14:19:41.7422810Z app = Ldap suser Wofford Thurston shost = = KLIENT1 msg = ataku siłowego przy użyciu protokołu nastąpiła próba protokołu Ldap na Wofford Thurston (inżynier oprogramowania) z maszyny KLIENT1 (100 odgadnięcia prób). CNT = 100 externalId = 2004 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
2018-02-21 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 Centrum CEF 6076 BruteForceSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | BruteForceSecurityAlert | Podejrzane błędy uwierzytelniania | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = KLIENT1 msg = podejrzane błędy uwierzytelniania wskazujące na potencjalny atak siłowy zostały wykryte z maszyny KLIENT1. externalId = 2023 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Podwyższenie poziomu uprawnień
#### <a name="silver"></a>Srebrny
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + 00:00 Centrum CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Eskalacja uprawnień przy użyciu sfałszowanych danych autoryzacji | 10 | start = 2018-02 — 21T14:19:02.8595383Z aplikacji = Kerberos suser = KLIENT1 msg = Użytkownik1 podjęło próbę eskalacji uprawnień do host/domain1.test.local z maszyny KLIENT1 przy użyciu sfałszowanych danych autoryzacji. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Złoty
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + 00:00 Centrum CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Eskalacja uprawnień przy użyciu sfałszowanych danych autoryzacji | 10 | start = 2018-02 — 21T14:19:02.8595383Z aplikacji = Kerberos suser = KLIENT1 msg = Użytkownik1 eskalacji uprawnień wobec komputerów DC1 do host/domain1.test.local z maszyny KLIENT1 przy użyciu sfałszowanych danych autoryzacji nie udało się. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Sfałszowany bilet uwierzytelniania Golden Ticket
2018-02-21 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 Centrum CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | GoldenTicketSecurityAlert | Działanie bilet uwierzytelniania Golden Ticket protokołu Kerberos | 10 | start = 2018-02-21T14:19:03.2416152Z aplikacji Kerberos suser = Lanell Campos msg = = podejrzane użycie biletu Kerberos Lanell Campos (inżynier oprogramowania) firmy, wskazujące na potencjalny atak bilet uwierzytelniania Golden Ticket, zostało wykryte. externalId = 2022 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="kerberos-golden-ticket-nonexistent-account"></a>Nieistniejące konto bilet uwierzytelniania Golden Ticket protokołu Kerberos
07-01-2018 14:28:49 Auth.Error 192.168.0.100: 1 2018-07-01T11:28:35.546638 + 00:00 Centrum CEF 38768 ForgedPrincipalSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.39.0.0 | ForgedPrincipalSecurityAlert | Kerberos Golden Ticket - nieistniejące konto | 10 | start = 2018-07-01T09:48:31.2567987Z aplikacji = Kerberos msg=domain1.test.local\fake suser=domain1.test.local\fake, który nie istnieje w usłudze Active Directory, używane biletu protokołu Kerberos. --Ticket zostało wykryte z 2 komputerom dostęp do zasobów 3. Może to wskazywać na potencjalny atak bilet uwierzytelniania Golden Ticket. externalId = 2027 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4


### <a name="honey-token-activity"></a>Działania związane z kontem wystawionym jako przynęta
2018-02-21 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 Centrum CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Działanie wystawionego jako przynęta | 5 | start = 2018-02-21T14:20:26.6705617Z aplikacji Kerberos suser = wystawione jako przynęta msg = = następujące działania zostały wykonane przez konto wystawione jako przynęta: \r\nLogged w do komputera KLIENT2 przy użyciu komputera DC1. externalId = 2014 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Podejrzana replikacja usług katalogowych
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. wynik = sukces externalId = 2006 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Podejrzana replikacja żądania (potencjalny atak DcShadow)
2018-07-12 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989 + 00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.40.0.0 | DirectoryServicesRogueReplicationSecurityAlert | **Podejrzana replikacja żądania (potencjalny atak DcShadow)**| 10 | start = 2018-07-12T08:17:55.3816102Z **aplikacji = działanie replikacji** shost = KLIENT1 msg = CLIENT1, który nie jest prawidłową domenę Kontroler w domain1.test.local, wysyłane zmiany do obiektów katalogu na komputerze DC1. externalId = 2029 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515
### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Podwyższanie poziomu kontrolera domeny podejrzane (potencjalny atak DcShadow)
2018-07-12 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880 + 00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.40.0.0 | DirectoryServicesRoguePromotionSecurityAlert | **Podwyższania poziomu kontrolera domeny podejrzane (potencjalny atak DcShadow)**| 10 | start = 2018-07 — 12T08:17:55.4067092Z app = Ldap shost = KLIENT1 msg = KLIENT1, czyli komputer w domain1.test.local, zarejestrowany jako kontroler domeny na kontrolerze domeny DC1. externalId = 2028 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53

### <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych
2018-02-21 16:22:08 Auth.Error 192.168.0.220 1 2018-02-21T14:21:54.080266 + 00:00 Centrum CEF 6076 RetrieveDataProtectionBackupKeyS ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | RetrieveDataProtectionBackupKeySecurityAlert | Złośliwe żądanie informacji prywatnych ochrony danych | 10 | start = 2018-02 — 21T14:19:41.8382786Z app = LsaRpc shost = KLIENT1 msg = Użytkownik1 wykonywane 1 pomyślnych prób z maszyny KLIENT1 do pobrania klucza kopii zapasowej domeny DPAPI z komputera DC1. externalId = 2020 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Ataki typu Over-Pass-the-Hash
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 Centrum CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Działanie obniżenia poziomu szyfrowania | 5 | start = 2018-02-21T14:19:41.8737870Z aplikacji = Kerberos msg = metodę szyfrowania pola encrypted_timestamp. Data: AS_REQ obniżono wiadomości z maszyny KLIENT1, na podstawie zachowania uprzednio zapamiętane. Przyczyną może być kradzież poświadczeń przy użyciu ataku typu Over-Pass-the-Hash z maszyny KLIENT1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Ataki typu Pass-the-Hash
2018-02-21 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 Centrum CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | PassTheHashSecurityAlert | Kradzież tożsamości za pomocą ataku typu Pass--Hash | 10 | start = 2018-02-21T15:02:22.2577465Z aplikacji Kerberos suser = Eugene Jenkins msg = = Eugene Jenkins wyznaczania wartości skrótu (inżynier oprogramowania) firmy został skradziony z jednego z komputerów, zalogowano się wcześniej przez Eugene narzędzia Jenkins (oprogramowanie Inżynier) i użyty z komputera KLIENT1. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Wyliczanie kont
2018-02-21 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 Centrum CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekonesans przy użyciu wyliczania kont | 5 | start = 2018-02-21T14:19:02.6045416Z aplikacji = Kerberos shost = KLIENT1 suser = LMaldonado msg = konto podejrzane działanie wyliczenia przy użyciu protokołu Kerberos, pochodzące z maszyny KLIENT1, zostało zaobserwowane i pomyślnie odgadnięcia Lamon Maldonado (inżynier oprogramowania). externalId = 2003 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>Rekonesans DNS
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + 00:00 Centrum CEF 6076 DnsReconnaissanceSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekonesans przy użyciu systemu DNS | 5 | start = 2018-02-21T14:19:41.9417776Z aplikacji = Dns shost = KLIENT1 żądanie pokaz zapytania requestMethod = = Axfr Przyczyna = outcome brak błędu = Success msg = podejrzane DNS zaobserwowano działanie pochodzące z maszyny KLIENT1 (która nie jest serwerem DNS). Zapytanie dotyczyło pokaz zapytania (typ Axfr). Odpowiedź była brak błędu. externalId = 2007 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>Wyliczanie sesji SMB
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 Centrum CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekonesans przy użyciu wyliczania sesji SMB | 5 | start = 2018-02-21T14:19:03.2071170Z app = SrvSvc shost = KLIENT1 msg = sesji SMB pomyślnie wykonano próby wyliczenia przy użyciu konta użytkownik1 z maszyny KLIENT1 względem kontrolera domeny KD1, udostępnianie Eugene narzędzia Jenkins (Użytkownik2 komputer) . externalId = 2012 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>Wyliczenie SAM-R
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 Centrum CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekonesans przy użyciu wyliczania usług katalogowych | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = KLIENT1 suser = Użytkownik1 outcome = Success msg = podjęto próby wyliczenia przy użyciu protokołu SAMR względem kontrolera domeny KD1 z następującymi usługami katalogu CLIENT1:\r\nSuccessful wyliczenie wszystkich grup w domain1.test.local przy użyciu konta użytkownik1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Zdalne wykonywanie kodu
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 Centrum CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Wykryto próbę zdalnego wykonania | 5 | start = 2018-02-aplikacji 21T14:19:41.9912772Z Wmi shost = = KLIENT1 suser = Użytkownik1 outcome = Success msg = następujące zdalne wykonywanie kodu wykonano próby na kontrolerze domeny DC1 z CLIENT1:\r\nSuccessful zdalne wykonanie metod WMI co najmniej jeden metody przy użyciu konta użytkownik1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Wytrych
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 Centrum CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Działanie obniżenia poziomu szyfrowania | 5 | start = 2018-02-21T14:19:41.8737870Z aplikacji = Kerberos msg = metodę szyfrowania pola ETYPE_INFO2 KRB_ERR obniżono wiadomości z maszyny KLIENT1, na podstawie zachowania uprzednio zapamiętane. Może to być wynik umieszczenia klucza uniwersalnego na kontrolerze domeny DC1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 Centrum CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Nietypowa implementacja protokołu | 5 | start = 2018-02 — 21T14:19:03.1981155Z aplikacji = Ntlm shost = KLIENT2 outcome = Success msg = Brak, zostały próby uwierzytelnienia z komputera KLIENT2 względem kontrolera domeny KD1 przy użyciu nietypowej implementacji protokołu. Przyczyną może być użycie złośliwych narzędzi służących na przykład do wykonywania ataków typu Pass-the-Hash lub ataków siłowych. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1 =https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Tworzenie usługi złośliwy
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 Centrum CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Podejrzanie utworzenie usługi | 5 | start = 2018-02-aplikacji 21T14:19:41.7897808Z ServiceInstalledEvent shost = = KLIENT1 msg = MaliciousService Użytkownik1 utworzone, aby można było wykonać potencjalnie szkodliwe polecenia na komputerze KLIENT1. externalId = 2026 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Ataki typu Pass-the-Ticket
2018-02-21 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 Centrum CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.22.4228.22540 | PassTheTicketSecurityAlert | Kradzież tożsamości za pomocą ataku typu Pass--Ticket | 10 | start = 2018-02-21T15:02:22.2577465Z aplikacji Kerberos suser = Eugene Jenkins msg = = Kerberos Eugene narzędzia Jenkins (inżynier oprogramowania) firmy biletów zostały skradzione z Admin-PC do Victim-PC i umożliwiają dostęp do domeny krbtgt/1. TEST. LOKALNE. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd

### <a name="suspicious-vpn-connection"></a>Połączenie sieci VPN podejrzanych
07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834 + 00:00 AbnormalVpnSecurityAlert DC1 CEF 2520 ï» ¿0 | Firmy Microsoft | Narzędzie Azure ATP | 2.39.0.0 | AbnormalVpnSecurityAlert | Podejrzane połączenia sieci VPN | 5 | start = 2018-06-30T15:34:05.3887333Z aplikacji VpnConnection suser = = KLIENT1 msg = Użytkownik1 nawiązanie połączenia sieci VPN na komputerach z 3 z 3 lokalizacji.     externalId = 2025 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)