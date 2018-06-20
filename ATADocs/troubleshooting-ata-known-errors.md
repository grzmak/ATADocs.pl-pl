---
title: Rozwiązywanie znanych problemów z usługą ATA | Microsoft Docs
description: W tym artykule opisano, jak można rozwiązać znane problemy dotyczące usługi Advanced Threat Analytics
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: a7172447de5b4d4088da2d8d687a7bec47a01551
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010486"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="troubleshooting-ata-known-issues"></a>Rozwiązywanie znanych problemów z usługą ATA

W tej sekcji szczegółowo opisano możliwe błędy we wdrożeniach usługi ATA oraz czynności, jakie należy wykonać w celu ich usunięcia.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Błędy bramy i uproszczonej bramy usługi ATA

> [!div class="mx-tableFixed"]
|Error|Opis|Rozwiązanie|
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
|System.InvalidOperationException: Wystąpienie „Microsoft.Tri.Gateway” nie istnieje w określonej kategorii.|Identyfikatory PID zostały włączone dla nazw procesów w bramie usługi ATA|Użyj aktualizacji [KB281884](https://support.microsoft.com/kb/281884), aby wyłączyć identyfikatory PID w nazwach procesów|
|System.InvalidOperationException: Kategoria nie istnieje.|Liczniki mogą być wyłączone w rejestrze|Użyj aktualizacji [KB2554336](https://support.microsoft.com/kb/2554336) , aby odbudować liczniki wydajności|
|System.ApplicationException: Nie można uruchomić sesji ETW o identyfikatorze MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|W pliku HOSTS znajduje się wpis hosta wskazujący skróconą nazwę komputera|Usuń wpis hosta z pliku C:\Windows\System32\drivers\etc\HOSTS lub zmień jego treść na nazwę FQDN.|
|System.IO.IOException: Uwierzytelnianie nie powiodło się, ponieważ strona zdalna zamknęła strumień transportowy.|Protokołu TLS 1.0 na bramie usługi ATA jest wyłączona, ale .net jest skonfigurowany do używania protokołu TLS 1.2|Skorzystaj z jednej z następujących opcji: </br> Włącz szyfrowanie TLS 1.0 na bramie ATA </br>Włącz protokół TLS 1.2 na platformie .net, ustawiając klucze rejestru, aby użyć wartości domyślnych systemu operacyjnego dla protokołu SSL i TLS, w następujący sposób: </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|System.TypeLoadException: Nie można załadować typu „Microsoft.Opn.Runtime.Values.BinaryValueBufferManager” z zestawu „Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35”|Brama usługi ATA nie mogła załadować wymaganych plików analizowania.|Sprawdź, czy program Microsoft Message Analyzer jest aktualnie zainstalowany. Instalacja programu Message Analyzer z bramą/uproszczoną bramą usługi ATA nie jest obsługiwana. Odinstaluj program Message Analyzer i uruchom ponownie usługę bramy.|
|System.Net.WebException: Serwer zdalny zwrócił błąd: (407) Wymagane uwierzytelnianie serwera proxy|Komunikacja bramy usługi ATA z Centrum usługi ATA jest zakłócana przez serwer proxy.|Wyłącz serwer proxy na maszynie bramy usługi ATA. <br></br>Pamiętaj, że ustawienia serwera proxy mogą być określane oddzielnie dla każdego konta.|
|System.IO.DirectoryNotFoundException: System nie może odnaleźć określonej ścieżki. (Wyjątek od HRESULT: 0x80070003)|Co najmniej jedna usługa potrzebna do działania usługi ATA nie została uruchomiona.|Uruchom następujące usługi: <br></br>Dzienniki wydajności i alerty (PLA), Harmonogram zadań (Schedule).|
|System.Net.WebException: Serwer zdalny zwrócił błąd: (403) zabroniony|Brama usługi ATA lub bramy Lightweight może zostało zabronione od ustanawiania połączenia HTTP, ponieważ Centrum usługi ATA nie jest zaufany.|Dodaj nazwę NetBIOS i FQDN Centrum usługi ATA do listy zaufanych witryn sieci Web i wyczyść pamięć podręczną w Eksploratorze Interne (lub nazwę Centrum usługi ATA, jak określono w konfiguracji, jeśli skonfigurowanego jest inna niż nazwa NetBIOS/FQDN).|
|System.Net.Http.HttpRequestException: PostAsync failed [requestTypeName=StopNetEventSessionRequest]|Brama usługi ATA lub bramy ATA Lightweight Gateway nie może zatrzymać i uruchomić sesję funkcji ETW, która gromadzi ruchu sieciowego z powodu problemu z usługi WMI|Postępuj zgodnie z instrukcjami [WMI: ponowne tworzenie repozytorium WMI](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) Aby rozwiązać problem WMI|
|System.Net.Sockets.SocketException: Podjęto próbę dostępu do gniazda w sposób zabroniony przez jego uprawnień dostępu|Inna aplikacja używa portu 514 w bramie usługi ATA|Użyj `netstat -o` do ustalenia, które procesy wykorzystują tego portu.|
 
## <a name="deployment-errors"></a>Błędy wdrażania
> [!div class="mx-tableFixed"]
|Error|Opis|Rozwiązanie|
|-------------|----------|---------|
|Instalacja platformy .Net Framework 4.6.1 nie powiodła się z powodu błędu 0x800713ec|Na serwerze nie są zainstalowane wymagania wstępne platformy .Net Framework 4.6.1. |Przed zainstalowaniem usługi ATA sprawdź, czy na serwerze są zainstalowane aktualizacje systemu Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) i [KB2919355](https://support.microsoft.com/kb/2919355).|
|System.Threading.Tasks.TaskCanceledException: Zadanie zostało anulowane|Upłynął limit czasu procesu wdrażania, ponieważ nie może on uzyskać dostępu do centrum usługi ATA.|1.    Sprawdź łączność sieciową z centrum usługi ATA, przechodząc do niego przy użyciu jego adresu IP. <br></br>2.    Sprawdź konfigurację serwera proxy lub zapory.|
|System.Net.Http.HttpRequestException: Wystąpił błąd podczas wysyłania żądania. ---> System.Net.WebException: Serwer zdalny zwrócił błąd: (407) Wymagane jest uwierzytelnianie serwera proxy.|Upłynął limit czasu procesu wdrażania, ponieważ nie mógł on uzyskać dostępu do centrum usługi ATA ze względu na błędną konfigurację serwera proxy.|Wyłącz konfigurację serwera proxy przed przystąpieniem do wdrożenia, a następnie ponownie włącz konfigurację serwera proxy. Możesz też skonfigurować wyjątek na serwerze proxy.|
|System.Net.Sockets.SocketException: Istniejące połączenie zostało zamknięte przez hosta zdalnego||Skorzystaj z jednej z następujących opcji: </br>Włącz szyfrowanie TLS 1.0 na bramie ATA </br>Włącz protokół TLS 1.2 na platformie .net, ustawiając klucze rejestru, aby użyć wartości domyślnych systemu operacyjnego dla protokołu SSL i TLS, w następujący sposób:</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|Błąd [\[] DeploymentModel [\]] uwierzytelniania zarządzania nie powiodło się [\[] CurrentlyLoggedOnUser =<domain>\<nazwa użytkownika > Stan = wyjątek FailedAuthentication = [\]]|Proces wdrażania bramy usługi ATA lub bramy ATA Lightweight Gateway nie można pomyślnie uwierzytelnić Centrum usługi ATA|Otwórz przeglądarkę z komputera, na którym nie powiodło się proces wdrażania i zobacz, jeśli można nawiązać połączenia z konsolą usługi ATA. </br>Jeśli nie, Uruchom Rozwiązywanie problemów, aby zobaczyć, dlaczego przeglądarka nie może uwierzytelnić Centrum usługi ATA. </br>Czynności do wykonania: </br>Konfiguracja serwera proxy</br>Problemy z sieci</br>Ustawienia zasad grupy dla uwierzytelniania na tej maszynie, która różni się od centrum usługi ATA.|





## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Problemy z bramą i uproszczoną bramą usługi ATA

> [!div class="mx-tableFixed"]
|Problem|Opis|Rozwiązanie|
|-------------|----------|---------|
|Brak odebranego ruchu z kontrolera domeny, ale pojawiają się alerty monitorowania|    Brak odebranego ruchu z kontrolera domeny za pomocą funkcji dublowania portów przez bramę usługi ATA|Na karcie sieciowej przechwytywania bramy usługi ATA wyłącz następujące funkcje w obszarze **Ustawienia zaawansowane**:<br></br>Łączenie segmentów odbieranych pakietów (IPv4)<br></br>Łączenie segmentów odbieranych pakietów (IPv6)|
|Ten alert monitorowania jest wyświetlany: **ruch w sieci nie jest analizowana**|Jeśli bramy usługi ATA lub bramy Lightweight na maszynach wirtualnych VMware, zostanie zgłoszony alert monitorowania. Dzieje się z powodu niezgodności konfiguracji w środowisku programu VMware.|Ustaw następujące ustawienia **0** lub **wyłączone** w konfiguracji maszyny wirtualnej karty Sieciowej: TsoEnable, LargeSendOffload, odciążania TSO, bardzo duże odciążania TSO|Protokołu TLS 1.0 na bramie usługi ATA jest wyłączona, ale .net jest skonfigurowany do używania protokołu TLS 1.2|




## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
