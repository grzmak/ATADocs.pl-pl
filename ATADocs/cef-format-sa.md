---
title: "Dokumentacja dzienników rozwiązania SIEM usługi ATA | Microsoft Docs"
description: "Zawiera przykłady dzienników podejrzanych działań wysłanych z usługi ATA do rozwiązania SIEM."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/21/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: ca460647fbed07820e8d19083d5aca19a05bc0a8
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="ata-siem-log-reference"></a>Dokumentacja dziennika rozwiązania SIEM usługi ATA

Usługa ATA może przekazywać zdarzenia alertów monitorowania i podejrzanych działań do rozwiązania SIEM. Zdarzenia podejrzanych działań są w formacie CEF. Ten artykuł dokumentacji zawiera przykłady dzienników podejrzanych działań wysyłanych do rozwiązania SIEM.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Przykłady podejrzanych działań usługi ATA w formacie CEF
Następujące pola i ich wartości są przekazywane do rozwiązania SIEM:

-   start — czas rozpoczęcia alertu
-   suser — konto (zwykle jest to konto użytkownika), którego dotyczy alert
-   shost — maszyna źródłowa dla tego alertu
-   outcome — wynik (powodzenie/niepowodzenie) wykonywanego działania, którego dotyczy alert  
-   msg — opis alertu
-   cnt — dotyczy alertów mających liczbę wystąpień alertu (na przykład ataków siłowych zawierających liczbę odgadniętych haseł)
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
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Podejrzane niepowodzenia uwierzytelniania|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=KLIENT1 msg=Wykryto podejrzane niepowodzenia uwierzytelniania wskazujące potencjalny atak siłowy pochodzące z maszyny KLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Podwyższenie poziomu uprawnień
#### <a name="silver"></a>Srebrny
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych uwierzytelniania|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=Użytkownik1 msg=Użytkownik1 podjął próbę podwyższenia poziomu uprawnień do maszyny HOST/klient1 z maszyny KLIENT2 przy użyciu sfałszowanych danych uwierzytelniania. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Złoty
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Podwyższenie uprawnień przy użyciu sfałszowanych danych uwierzytelniania|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=Użytkownik1 msg=Użytkownik1 podjął próbę podwyższenia uprawnień na kontrolerze domeny KD4 z komputera KLIENT1 przy użyciu sfałszowanych danych uwierzytelniania. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Sfałszowany bilet uwierzytelniania Golden Ticket
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Działanie obniżenia poziomu szyfrowania|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=Poziom metody szyfrowania pola TGT komunikatu TGS_REQ z maszyny KLIENT1 został obniżony w porównaniu do wcześniej zapamiętanego zachowania. Przyczyną może być użycie sfałszowanego biletu uwierzytelniania Golden Ticket na maszynie KLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Działania związane z kontem wystawionym jako przynęta
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Działanie związane z kontem wystawionym jako przynęta|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=Usługa privtriservice wykonała następujące działania:\r\nUwierzytelnienie z kontrolera domeny KD1 przy użyciu protokołu NTLM względem zasobów firmy za pośrednictwem kontrolera domeny KD1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Podejrzana replikacja usług katalogowych
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Złośliwa replikacja usług katalogowych|10|start=2017-05-03T11:00:13.6560919Z suser=użytkownik1 shost=KLIENT1 outcome=Failure msg=Podjęto próby wysłania złośliwych żądań replikacji przy użyciu konta użytkownik1 z maszyny KLIENT1 względem kontrolera domeny KD1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Złośliwe żądanie informacji prywatnych z zakresu ochrony danych|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=KLIENT1 suser= outcome=Success msg=Nieznany użytkownik wykonał 4 pomyślne próby pobrania klucza zapasowego domeny interfejsu DPAPI z kontrolera domeny KD1 przy użyciu maszyny KLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Usunięcie dużej liczby obiektów
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Usunięcie dużej liczby obiektów|5|start=2017-05-14T11:33:32.0000000Z msg=W krótkim czasie z domeny domena1.test.local usunięto 496 obiektów (9,75% łącznej liczby obiektów w usłudze AD). cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Ataki typu Over-Pass-the-Hash
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Działanie obniżenia poziomu szyfrowania|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=Poziom metody szyfrowania pola Encrypted_Timestamp komunikatu AS_REQ z maszyny KLIENT1 został obniżony w porównaniu do wcześniej zapamiętanego zachowania. Przyczyną może być kradzież poświadczeń przy użyciu ataku typu Over-Pass-the-Hash z maszyny KLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Ataki typu Pass-the-Hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Kradzież tożsamości przy użyciu ataku typu Pass-the-Hash|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=użytkownik2 msg=Skrót użytkownika użytkownik2 został ukradziony z jednego z komputerów, na których użytkownik użytkownik2 był wcześniej zalogowany, i użyty z poziomu maszyny KLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Wyliczanie kont
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Rekonesans przy użyciu wyliczania kont|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=KLIENT3 msg=Wykryto podejrzane działanie związane z wyliczaniem kont przy użyciu protokołu Kerberos pochodzące z maszyny KLIENT3. Osoba atakująca wykonała łącznie 72 próby odgadnięcia nazw kont, z czego 2 próby odgadnięcia były zgodne z istniejącymi nazwami kont w usłudze Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>Rekonesans DNS
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekonesans przy użyciu systemu DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=KLIENT1 msg=Zaobserwowano podejrzane działanie związane z systemem DNS pochodzące z maszyny KLIENT1 (która nie jest serwerem DNS) względem kontrolera domeny KD1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekonesans przy użyciu systemu DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=KLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Zaobserwowano podejrzane działanie związane z systemem DNS pochodzące z maszyny KLIENT1 (która nie jest serwerem DNS). Zapytanie dotyczyło domeny contoso.com (typ Axfr). Odpowiedź: NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>Wyliczanie sesji SMB
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Rekonesans przy użyciu wyliczania sesji SMB|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=KLIENT1 msg=Wykonano pomyślne próby wyliczania sesji SMB z maszyny KLIENT1 względem kontrolera domeny KD1, co spowodowało uwidocznienie użytkownika użytkownik1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>Wyliczenie SAMR
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Rekonesans przy użyciu wyliczania usług katalogowych|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=KLIENT1 suser=użytkownik1 outcome=Success msg=Wykonano następujące próby wyliczenia przy użyciu protokołu SAMR względem kontrolera domeny KD1 z maszyny KLIENT1:\r\nPomyślne wyliczenie wszystkich grup w domenie domena1.test.local przez użytkownika użytkownik1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Zdalne wykonywanie kodu
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Wykryto próbę zdalnego wykonania kodu|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=KLIENT1 suser=Administrator outcome=Success msg=Wykonano następujące próby zdalnego wykonania kodu na kontrolerze domeny KD1 pochodzące z maszyny KLIENT1:\r\nPomyślne zdalne utworzenie usługi PSEXESVC przez użytkownika Administrator. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Wytrych
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Działanie obniżenia poziomu szyfrowania|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=Poziom metody szyfrowania pola ETYPE_INFO2 komunikatu KRB_ERR z maszyny KLIENT2 został obniżony w porównaniu do wcześniej zapamiętanego zachowania. Przyczyną może być instalacja złośliwego oprogramowania Skeleton Key na kontrolerze domeny KD3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Nietypowa implementacja protokołu|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=KLIENT1 suser=Administrator outcome=Success msg=Administrator został pomyślnie uwierzytelniony z maszyny KLIENT1 względem kontrolera domeny KD1 przy użyciu nietypowej implementacji protokołu. Przyczyną może być użycie złośliwych narzędzi służących na przykład do wykonywania ataków typu Pass-the-Hash lub ataków siłowych. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="sensitive-account-credentials-exposed"></a>Ujawnienie poufnych poświadczeń konta
May  3 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Ujawniono poufne poświadczenia konta|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=KLIENT1 suser=Administrator msg=Poświadczenia użytkownika Administrator zostały ujawnione w postaci zwykłego tekstu przy użyciu prostego powiązania LDAP z maszyny KLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### <a name="services-exposing-account-credentials"></a>Usługi ujawniające poświadczenia kont
May  3 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Usługi ujawniające poświadczenia kont|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=Usługi uruchomione na maszynie daf::220 (daf::220) ujawniają poświadczenia kont w postaci zwykłego teksu przy użyciu prostego powiązania LDAP. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### <a name="pass-the-ticket"></a>Ataki typu Pass-the-Ticket
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Kradzież tożsamości za pomocą ataku typu Pass-the-Ticket|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=KLIENT1 suser=Administrator request=krbtgt/DOMENA1.TEST.LOCAL msg=Bilety protokołu Kerberos użytkownika Administrator zostały ukradzione z maszyny KLIENT2 przez maszynę KLIENT1 i użyte do uzyskania dostępu do domeny krbtgt/DOMENA1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=KLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
