---
title: "Dokumentacja dzienników rozwiązania SIEM usługi ATA | Microsoft Docs"
description: "Zawiera przykłady dzienników podejrzanych działań wysłanych z usługi ATA do rozwiązania SIEM."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7c6eaba8f80dcc7a8fc767f2bb8168221fbc7207
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*


# <a name="ata-siem-log-reference"></a>Dokumentacja dziennika rozwiązania SIEM usługi ATA

Usługa ATA może przekazywać zdarzenia alertów monitorowania i podejrzanych działań do rozwiązania SIEM. Zdarzenia podejrzanych działań są w formacie CEF. Ten artykuł dokumentacji zawiera przykłady dzienników podejrzanych działań wysyłanych do rozwiązania SIEM.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Przykłady podejrzanych działań usługi ATA w formacie CEF
Następujące pola i ich wartości są przekazywane do rozwiązania SIEM:

-   start — czas rozpoczęcia alertu
-   suser — konto (zwykle jest to konto użytkownika), którego dotyczy alert
-   shost — maszyna źródłowa dla tego alertu
-   outcome — wynik (powodzenie/niepowodzenie) wykonywanego działania, którego dotyczy alert  
-   msg — opis alertu
-   CNT — dla alertów, które mają liczbę razy, które generują alerty wystąpił (na przykład siłowych z odpowiednią ilością odgadnięcia hasła)
-   app — protokół używany w tym alercie
-   externalId — identyfikator zdarzenia zapisywany przez usługę ATA w dzienniku zdarzeń, który odpowiada temu alertowi
-   cs#label i cs# — są to ciągi klienta dozwolone w formacie CEF; cs#label to nazwa nowego pola, a cs# to wartość, na przykład: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

W tym przykładzie pole cs1 jest polem zawierającym adres URL do alertu.

## <a name="sample-logs"></a>Przykładowe dzienniki

Priorytety: 3=Niski 5=Średni 10=Wysoki

### <a name="bruteforce--ldap"></a>BruteForce — LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     May  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Atak siłowy przy użyciu prostego powiązania protokołu LDAP|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=KLIENT1 msg=Podjęto próbę ataku siłowego przy użyciu protokołu LDAP na konto użytkownika Darris Woods (inżynier oprogramowania) z maszyny KLIENT1 (76 prób odgadnięcia). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Atak siłowy przy użyciu prostego powiązania protokołu LDAP|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=KLIENT1 msg=Podjęto próbę ataku siłowego przy użyciu protokołu LDAP na konto użytkownika Dino Hopkins (inżynier oprogramowania) z maszyny KLIENT1 (3 próby odgadnięcia). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Atak siłowy przy użyciu prostego powiązania protokołu LDAP|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=KLIENT1 msg=Podjęto zakończoną pomyślnie próbę ataku siłowego przy użyciu protokołu LDAP na konto użytkownika Dino Hopkins (inżynier oprogramowania) z maszyny KLIENT1 (77 prób odgadnięcia). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
2017-05-14 13:27:05 Auth.Warning 192.168.0.220 1 2017-05-ï» ¿CEF:0 | Microsoft | USŁUGI ATA | 1.8.6455.41882 | BruteForceSuspiciousActivity | Niepowodzenia uwierzytelniania podejrzane | 5 | start = 2017-05-14T10:27:04.3904739Z aplikacji Kerberos shost = = KLIENT1 msg = błędy uwierzytelniania podejrzane wskazujący potencjalnych ataków siłowych wykryto z komputera KLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Podwyższenie poziomu uprawnień
#### <a name="silver"></a>Srebrny
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1 attempted to escalate privileges to HOST/client1 from CLIENT2 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Złoty
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1 attempted to escalate privileges against DC4 from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Sfałszowany bilet uwierzytelniania Golden Ticket
2017-05-14 15:57:10 Auth.Warning 192.168.0.220 1 2017-05-14T12:57:10.392730 + ï Centrum usługi ATA 4732 EncryptionDowngradeSuspiciousAct 00:00 "¿CEF:0 | Microsoft | USŁUGI ATA | 1.8.6455.41882 | EncryptionDowngradeSuspiciousActivity | Działanie obniżenia poziomu szyfrowania | 5 | start = 2017-05-14T12:55:08.6913033Z aplikacji = komunikaty protokołu Kerberos = metodę szyfrowania pola biletu TGT TGS_REQ obniżono wiadomości z komputera CLIENT1, na podstawie zachowania uprzednio zapamiętane. Przyczyną może być użycie sfałszowanego biletu uwierzytelniania Golden Ticket na maszynie KLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Działania związane z kontem wystawionym jako przynęta
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=The following activities were performed by privtriservice:\r\nAuthenticated from DC1 using NTLM against corporate resources via DC1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Podejrzana replikacja usług katalogowych
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Złośliwa replikacja usług katalogowych|10|start=2017-05-03T11:00:13.6560919Z suser=użytkownik1 shost=KLIENT1 outcome=Failure msg=Podjęto próby wysłania złośliwych żądań replikacji przy użyciu konta użytkownik1 z maszyny KLIENT1 względem kontrolera domeny KD1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Złośliwe żądanie informacji prywatnych z zakresu ochrony danych|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=KLIENT1 suser= outcome=Success msg=Nieznany użytkownik wykonał 4 pomyślne próby pobrania klucza zapasowego domeny interfejsu DPAPI z kontrolera domeny KD1 przy użyciu maszyny KLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Usunięcie dużej liczby obiektów
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Massive object deletion|5|start=2017-05-14T11:33:32.0000000Z msg=496 objects (9.75% of total AD objects) were deleted over a period of no time from domain domain1.test.local. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Ataki typu Over-Pass-the-Hash
2017-05-14 12:07:46 Auth.Warning 192.168.0.220 1 2017-05-14T09:07:46.652319 + ï EncryptionDowngradeSuspiciousAct Centrum usługi ATA 1116 00:00 "¿CEF:0 | Microsoft | USŁUGI ATA | 1.8.6455.41882 | EncryptionDowngradeSuspiciousActivity | Działanie obniżenia poziomu szyfrowania | 5 | start = 2017-05-14T09:07:44.9933773Z aplikacji = komunikaty protokołu Kerberos = metodę szyfrowania pola Encrypted_Timestamp AS_REQ obniżono wiadomości z komputera CLIENT1, na podstawie zachowania uprzednio zapamiętane. Przyczyną może być kradzież poświadczeń przy użyciu ataku typu Over-Pass-the-Hash z maszyny KLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Ataki typu Pass-the-Hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Identity theft using Pass-the-Hash attack|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=user2's hash was stolen from one of the computers previously logged into by user2 and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Wyliczanie kont
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Reconnaissance using account enumeration|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=Suspicious account enumeration activity using Kerberos protocol, originating from CLIENT3, was detected. Osoba atakująca wykonała łącznie 72 próby odgadnięcia nazw kont, z czego 2 próby odgadnięcia były zgodne z istniejącymi nazwami kont w usłudze Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>Rekonesans DNS
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekonesans przy użyciu systemu DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=KLIENT1 msg=Zaobserwowano podejrzane działanie związane z systemem DNS pochodzące z maszyny KLIENT1 (która nie jest serwerem DNS) względem kontrolera domeny KD1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekonesans przy użyciu systemu DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=KLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Zaobserwowano podejrzane działanie związane z systemem DNS pochodzące z maszyny KLIENT1 (która nie jest serwerem DNS). Zapytanie dotyczyło domeny contoso.com (typ Axfr). Odpowiedź: NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>Wyliczanie sesji SMB
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Rekonesans przy użyciu wyliczania sesji SMB|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=KLIENT1 msg=Wykonano pomyślne próby wyliczania sesji SMB z maszyny KLIENT1 względem kontrolera domeny KD1, co spowodowało uwidocznienie użytkownika użytkownik1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>Wyliczenie SAMR
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Rekonesans przy użyciu wyliczania usług katalogowych|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=KLIENT1 suser=użytkownik1 outcome=Success msg=Wykonano następujące próby wyliczenia przy użyciu protokołu SAMR względem kontrolera domeny KD1 z maszyny KLIENT1:\r\nPomyślne wyliczenie wszystkich grup w domenie domena1.test.local przez użytkownika użytkownik1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Zdalne wykonywanie kodu
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Wykryto próbę zdalnego wykonania kodu|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=KLIENT1 suser=Administrator outcome=Success msg=Wykonano następujące próby zdalnego wykonania kodu na kontrolerze domeny KD1 pochodzące z maszyny KLIENT1:\r\nPomyślne zdalne utworzenie usługi PSEXESVC przez użytkownika Administrator. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Wytrych
2017-05-14 12:13:12 Auth.Warning 192.168.0.220 1 2017-05-14T09:13:12.102468 + ï EncryptionDowngradeSuspiciousAct Centrum usługi ATA 1116 00:00 "¿CEF:0 | Microsoft | USŁUGI ATA | 1.8.6455.41882 | EncryptionDowngradeSuspiciousActivity | Działanie obniżenia poziomu szyfrowania | 5 | start = 2017-05-14T09:13:03.3509467Z aplikacji = komunikaty protokołu Kerberos = metodę szyfrowania pola ETYPE_INFO2 KRB_ERR obniżono komunikat z komputera KLIENT2, na podstawie zachowania uprzednio zapamiętane. Przyczyną może być instalacja złośliwego oprogramowania Skeleton Key na kontrolerze domeny KD3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Nietypowa implementacja protokołu|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=KLIENT1 suser=Administrator outcome=Success msg=Administrator został pomyślnie uwierzytelniony z maszyny KLIENT1 względem kontrolera domeny KD1 przy użyciu nietypowej implementacji protokołu. Przyczyną może być użycie złośliwych narzędzi służących na przykład do wykonywania ataków typu Pass-the-Hash lub ataków siłowych. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="pass-the-ticket"></a>Ataki typu Pass-the-Ticket
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Kradzież tożsamości za pomocą ataku typu Pass-the-Ticket|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=KLIENT1 suser=Administrator request=krbtgt/DOMENA1.TEST.LOCAL msg=Bilety protokołu Kerberos użytkownika Administrator zostały ukradzione z maszyny KLIENT2 przez maszynę KLIENT1 i użyte do uzyskania dostępu do domeny krbtgt/DOMENA1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=KLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

### <a name="monitoring-alert"></a>Alert monitorowania
2018-01-30T10:42:09.102595+00:00 CENTER ATA 4932 CenterDatabaseDisconnectedMonito ï»¿CEF:0|Microsoft|ATA|1.8.6765.50002|CenterDatabaseDisconnectedMonitoringAlert|CenterDatabaseDisconnectedMonitoringAlert|10|externalId=1005 cs1Label=url cs1=https://center/monitoring msg=The database that is used by the Center, CENTER, is down. Został ostatniego kontaktu z 1/30/2018 10:39:39 AM UTC.

> [!NOTE]
> Wszystkie alerty monitorowania są wysyłane przy użyciu tego samego szablonu jako powyżej.



## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
