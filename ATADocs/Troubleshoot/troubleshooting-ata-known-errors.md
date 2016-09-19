---
title: "Rozwiązywanie problemów z dziennikiem błędów usługi ATA | Microsoft ATA"
description: "W tym artykule opisano, jak można rozwiązywać typowe błędy w usłudze ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 15c1a0d7ae213876c0e3a955eaeea8887281b4e6
ms.openlocfilehash: b073a1b969f8841c9bbe540722349a5ef70340d4


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Rozwiązywanie problemów z dziennika błędów usługi ATA
W tej sekcji szczegółowo opisano możliwe błędy we wdrożeniach usługi ATA oraz czynności, jakie należy wykonać w celu ich usunięcia.
## Błędy bramy usługi ATA
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


## Błędy ATA IIS (nie dotyczy usług ATA w wersji 1.7 ani nowszych)
|Błąd|Opis|Rozwiązanie|
|-------------|----------|---------|
|Błąd HTTP 500.19 — wewnętrzny błąd serwera|Nie można poprawnie zainstalować modułu Ponowne zapisywanie adresów URL IIS.|Odinstaluj i zainstaluj ponownie moduł Ponowne zapisywanie adresów URL IIS.<br>[Pobierz moduł Ponowne zapisywanie adresów URL IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Błędy wdrażania
|Błąd|Opis|Rozwiązanie|
|-------------|----------|---------|
|Instalacja platformy .Net Framework 4.6.1 nie powiodła się z powodu błędu 0x800713ec|Na serwerze nie są zainstalowane wymagania wstępne platformy .Net Framework 4.6.1. |Przed zainstalowaniem usługi ATA sprawdź, czy na serwerze są zainstalowane aktualizacje systemu Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) i [KB2919355](https://support.microsoft.com/kb/2919355).|

![Ilustracja błędu instalacji platformy .NET dla usługi ATA](media/netinstallerror.png)


## Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


