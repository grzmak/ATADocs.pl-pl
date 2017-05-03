---
title: "Rozwiązywanie problemów z dziennika błędów usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można rozwiązywać typowe błędy w usłudze ATA"
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
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0c72b14a042e473c0cd59811db63ecafc4ec02d4
ms.sourcegitcommit: f18c0841d85e54eca940c8cbf226938b3c2bc80f
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>Rozwiązywanie problemów z dziennika błędów usługi ATA

W tej sekcji szczegółowo opisano możliwe błędy we wdrożeniach usługi ATA oraz czynności, jakie należy wykonać w celu ich usunięcia.

## <a name="ata-gateway-errors"></a>Błędy bramy usługi ATA

|Błąd|Opis|Rozwiązanie|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Wystąpił błąd lokalny|Nie można uwierzytelnić bramy usługi ATA na kontrolerze domeny.|1. Upewnij się, że rekord DNS kontrolera domeny jest prawidłowo skonfigurowany na serwerze DNS. <br>2. Sprawdź, czy czas bramy usługi ATA jest zsynchronizowany z czasem kontrolera domeny.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Nie można zweryfikować łańcucha certyfikatów|Brama usługi ATA nie może zweryfikować certyfikatu centrum usługi ATA.|1. Sprawdź, czy w magazynie certyfikatów zaufanego urzędu certyfikacji w bramie ATA jest zainstalowany certyfikat głównego urzędu certyfikacji. <br>2. Sprawdź, czy jest dostępna lista odwołań certyfikatów (CRL) i czy można zweryfikować poprawność odwołania certyfikatu.|
|Microsoft.Common.ExtendedException: Nie można przeanalizować godziny wygenerowania|Brama ATA nie może przeanalizować komunikatów usługi Syslog, które zostały przesłane z systemu SIEM.|Sprawdź, czy w systemie SIEM skonfigurowano przesyłanie komunikatów w jednym z formatów obsługiwanych przez usługę ATA.|
|System.ServiceModel.FaultException: Wystąpił błąd podczas sprawdzania zabezpieczeń komunikatu.|Nie można uwierzytelnić bramy usługi ATA w centrum usługi ATA.|Sprawdź, czy czas bramy usługi ATA jest zsynchronizowany z czasem centrum usługi ATA.|
|System.ServiceModel.EndpointNotFoundException: Nie można połączyć z net.tcp://center.ip.addr: 443/IEntityReceiver|Brama usługi ATA nie może nawiązać połączenia z centrum usługi ATA.|Upewnij się, że ustawienia sieci są poprawne i że połączenie sieciowe między bramą usługi ATA a centrum usługi ATA jest aktywne.|
|System.DirectoryServices.Protocols.LdapException: Serwer LDAP jest niedostępny.|Brama usługi ATA nie może wysłać zapytania do kontrolera domeny przy użyciu protokołu LDAP.|1. Sprawdź, czy konto użytkownika używane przez usługę ATA do łączenia się z domeną usługi Active Directory ma dostęp z możliwością odczytu do wszystkich obiektów w drzewie usługi Active Directory. <br>2. Upewnij się, że kontroler domeny nie pracuje w trybie uniemożliwiającym wysyłanie zapytań LDAP z konta użytkownika używanego przez usługę ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Wyjątek umowy|Brama usługi ATA nie może zsynchronizować konfiguracji z centrum usługi ATA.|Dokończ konfigurację bramy usługi ATA w konsoli usługi ATA.|
|System.Reflection.ReflectionTypeLoadException: Nie można załadować co najmniej jednego z żądanych typów. Pobierz właściwość LoaderExceptions, aby uzyskać więcej informacji.|W bramie ATA jest zainstalowany analizator komunikatów.| Odinstaluj analizatora komunikatów.|
|Błąd [Układ] System.OutOfMemoryException: Zgłoszono wyjątek typu „System.OutOfMemoryException”.|Brama usługi ATA ma za mało pamięci.|Zwiększ ilość pamięci na kontrolerze domeny.|
|Nie można uruchomić klienta na żywo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Dostawca zdarzeń PEFNDIS nie jest gotowy|PEF (analizator komunikatów) nie został poprawnie zainstalowany.|Jeśli korzystasz z funkcji Hyper-V, spróbuj uaktualnić usługi integracji funkcji Hyper-V. W przeciwnym razie skontaktuj się z pomocą techniczną, aby uzyskać obejście tego problemu.|
|Instalacja nie powiodła się z powodu błędu: 0x80070652|Na komputerze znajdują się inne instalacje oczekujące.|Zaczekaj na dokończenie innych instalacji i w razie potrzeby uruchom ponownie komputer.|
|System.InvalidOperationException: Wystąpienie „Microsoft.Tri.Gateway” nie istnieje w określonej kategorii.|Identyfikatory PID zostały włączone dla nazw procesów w bramie usługi ATA|Użyj aktualizacji [KB281884](https://support.microsoft.com/en-us/kb/281884), aby wyłączyć identyfikatory PID w nazwach procesów|
|System.InvalidOperationException: Kategoria nie istnieje.|Liczniki mogą być wyłączone w rejestrze|Użyj aktualizacji [KB2554336](https://support.microsoft.com/en-us/kb/2554336) , aby odbudować liczniki wydajności|
|System.ApplicationException: Nie można uruchomić sesji ETW o identyfikatorze MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|W pliku HOSTS znajduje się wpis hosta wskazujący skróconą nazwę komputera|Usuń wpis hosta z pliku C:\Windows\System32\drivers\etc\HOSTS lub zmień jego treść na nazwę FQDN.|
|System.IO.IOException: Uwierzytelnianie nie powiodło się, ponieważ strona zdalna zamknęła strumień transportowy.|Szyfrowanie TLS 1.0 jest wyłączone na bramie ATA Gateway, ale platforma .Net jest skonfigurowane do korzystania z szyfrowania TLS 1.2|Skorzystaj z jednej z następujących opcji: </br> Włącz szyfrowanie TLS 1.0 na bramie ATA </br>Włącz szyfrowanie TLS 1.2 na platformie .Net, konfigurując klucze rejestru w taki sposób, aby były używane domyślne ustawienia systemu operacyjnego dotyczące szyfrowania LLS i TLS: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"`|



## <a name="ata-lightweight-gateway-errors"></a>Błędy bramy ATA Lightweight Gateway

**Błąd**: alerty dotyczące porzuconego ruchu sieciowego na zdublowanym porcie podczas korzystania z lekkiej bramy w programie VMware

**Opis**: jeśli używasz kontrolerów domeny na maszynach wirtualnych programu VMware, możesz odbierać alerty dotyczące **porzuconego ruchu sieciowego na zdublowanym porcie**. Może być to spowodowane niezgodnością konfiguracji w programie VMware. 
**Rozwiązanie**: aby zapobiegać tym alertom, można sprawdzić, czy następujące ustawienia są ustawione na 0 lub wyłączone: TsoEnable (Włączanie TSO), LargeSendOffload (Odciążanie dużego wysyłania), IPv4, TSO Offload (Odciążanie TSO). Należy również rozważyć wyłączenie ustawienia IPv4 Giant TSO Offload (Bardzo duże odciążanie TSO IPv4). Aby uzyskać więcej informacji, zapoznaj się z dokumentacją programu VMware.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>Błędy ATA IIS (nie dotyczy usług ATA w wersji 1.7 ani nowszych)
|Błąd|Opis|Rozwiązanie|
|-------------|----------|---------|
|Błąd HTTP 500.19 — wewnętrzny błąd serwera|Nie można poprawnie zainstalować modułu Ponowne zapisywanie adresów URL IIS.|Odinstaluj i zainstaluj ponownie moduł Ponowne zapisywanie adresów URL IIS.<br>[Pobierz moduł Ponowne zapisywanie adresów URL IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>Błędy wdrażania
|Błąd|Opis|Rozwiązanie|
|-------------|----------|---------|
|Instalacja platformy .Net Framework 4.6.1 nie powiodła się z powodu błędu 0x800713ec|Na serwerze nie są zainstalowane wymagania wstępne platformy .Net Framework 4.6.1. |Przed zainstalowaniem usługi ATA sprawdź, czy na serwerze są zainstalowane aktualizacje systemu Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) i [KB2919355](https://support.microsoft.com/kb/2919355).|

![Ilustracja błędu instalacji platformy .NET dla usługi ATA](media/netinstallerror.png)


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
