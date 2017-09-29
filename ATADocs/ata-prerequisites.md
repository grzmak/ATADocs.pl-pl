---
title: "Wymagania wstępne usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Zawiera opis wymagań, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/24/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b681a6a27189d2e1aec3f7f9913b97f9e7717911
ms.sourcegitcommit: 47b2b9ebaadff79c087d14f86462d3d8102cc551
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="ata-prerequisites"></a>Wymagania wstępne usługi ATA
W tym artykule opisano wymagania, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku.

>[!NOTE]
> Aby uzyskać więcej informacji o planowaniu zasobów i pojemności, zobacz temat [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


Usługa ATA składa się z Centrum usługi ATA, bramy usługi ATA i/lub bramy ATA Lightweight Gateway. Aby uzyskać więcej informacji o składnikach usługi ATA, zobacz [Architektura usługi ATA](ata-architecture.md).

System ATA działa na granicy lasu usługi Active Directory i obsługuje poziom funkcjonalności lasu (FFL) systemu Windows 2003 lub nowszego.


[Przed rozpoczęciem](#before-you-start): w tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.

[Centrum usługi ATA](#ata-center-requirements): ta sekcja zawiera informacje o wymaganiach centrum usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerze centrum usługi ATA.

[Brama usługi ATA](#ata-gateway-requirements): ta sekcja zawiera informacje o wymaganiach bramy usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerach bramy usługi ATA.

[Uproszczona brama usługi ATA](#ata-lightweight-gateway-requirements): w tej sekcji przedstawiono wymagania sprzętowe i programowe uproszczonej bramy usługi ATA.

[Konsola usługi ATA](#ata-console): ta sekcja zawiera informacje o wymaganiach dotyczących przeglądarek związanych z uruchamianiem konsoli usługi ATA.

![Diagram architektury usługi ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Przed rozpoczęciem
W tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.


-   Konto użytkownika i hasło z dostępem do odczytu do wszystkich obiektów w monitorowanej domeny.

    > [!NOTE]
    > Jeśli ustawiono niestandardowe listy kontroli dostępu w różnych jednostkach organizacyjnych w domenie, upewnij się, że wybrany użytkownik ma uprawnienia do odczytu do tych jednostek organizacyjnych.

-   Nie należy instalować programu Microsoft Message Analyzer na bramie usługi ATA lub bramy Lightweight. Sterownik Analizatora komunikatów powoduje konflikt ze sterownikami bramy usługi ATA i uproszczonej bramy usługi ATA. Jeśli uruchomiono program Wireshark na bramie usługi ATA, to należy ponownie uruchomić bramę usługi Microsoft Advanced Threat Analytics po zatrzymaniu przechwytywania za pomocą programu Wireshark. Jeśli nie, brama zatrzymuje przechwytywanie ruchu. Należy pamiętać, że uruchomienie programu Wireshark na uproszczonej bramie usługi ATA nie zakłóca pracy uproszczonej bramy usługi ATA.

-    Zalecane: Użytkownik powinien mieć uprawnienia tylko do odczytu kontenera usuniętych obiektów. Umożliwia to wykrywanie zbiorczego usuwania obiektów w domenie przez usługę ATA. Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz **Zmienianie uprawnień do kontenera usuniętych obiektów** sekcji [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) tematu.

-   Opcjonalnie: konto użytkownika, który nie ma żadnych działań w sieci. To konto jest skonfigurowana jako użytkownika wystawionego jako przynęta usługi ATA. Do skonfigurowania użytkownika wystawionego jako przynęta, potrzebny jest identyfikator SID konta użytkownika, a nie nazwa użytkownika. Aby uzyskać więcej informacji, zobacz [Praca z ustawieniami wykrywania usługi ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings) tematu.

-   Opcjonalnie: Oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny, ATA umożliwia zdarzeń systemu Windows 4776, 4732, 4733, 4728, 4729, 4756 i 4757 zwiększyć ataków typu Pass--Hash, ataki Siłowe, modyfikację poufnych grup i Związane wystawionym jako przynęta wykryć tokenów. Można je odbierać z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.


## <a name="ata-center-requirements"></a>Wymagania centrum usługi ATA
Ta sekcja zawiera listę wymagań centrum usługi ATA.
### <a name="general"></a>Ogólne
Centrum usługi ATA obsługuje instalację na serwerze z systemem Windows Server 2012 R2 lub Windows Server 2016. Centrum usługi ATA można zainstalować na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.

Przed zainstalowaniem centrum usługi ATA w systemie Windows 2012 R2 upewnij się, że została zainstalowana następująca aktualizacja: [KB2919355](https://support.microsoft.com/kb/2919355/).

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

Instalacja centrum usługi ATA jako maszyny wirtualnej jest obsługiwana. 

>[!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

Jeśli centrum usługi ATA jest uruchamiane jako maszyna wirtualna, należy wyłączyć serwer przed utworzeniem nowego punktu kontrolnego w celu uniknięcia potencjalnego uszkodzenia bazy danych.
### <a name="server-specifications"></a>Specyfikacje serwera
Podczas pracy na serwerze fizycznym baza danych usługi ATA wymaga **wyłączenia** obsługi niejednolitego dostępu do pamięci (NUMA) w systemie BIOS. System może odwoływać się do architektury NUMA przeplataniem węzłów, w którym to przypadku należy **włączyć** Przeplatanie, aby wyłączyć technologię NUMA. Aby uzyskać więcej informacji zobacz dokumentację systemu BIOS. Nie jest to istotne w przypadku uruchomienia centrum usługi ATA na serwerze wirtualnym.<br>
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** centrum usługi ATA na wartość **Wysoka wydajność**.<br>
Liczba monitorowanych kontrolerów domeny i obciążenie poszczególnych kontrolerów domeny decyduje specyfikacje serwera. Aby uzyskać więcej informacji, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Synchronizacja czasu
Serwerze Centrum usługi ATA, serwerach bramy usługi ATA i kontrolerach domeny musi mieć czasu synchronizowane w ciągu pięciu minut od siebie.


### <a name="network-adapters"></a>Karty sieciowe
Musisz mieć następujące:
-   Co najmniej jedna karta sieciowa (w przypadku korzystania z serwera fizycznego w środowisku sieci VLAN zaleca się używanie dwóch kart sieciowych)

-   Adres IP do komunikacji między centrum usługi ATA i bramy usługi ATA, która jest szyfrowana przy użyciu protokołu SSL na porcie 443. (Usługa ATA jest powiązany z wszystkie adresy IP Centrum usługi ATA ma się na porcie 443).

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty, które należy otworzyć, aby centrum usługi ATA działało poprawnie.

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|**SSL** (komunikacja usługi ATA)|TCP|443 lub inny skonfigurowany|Brama usługi ATA|Przychodzące|
|**HTTP** (opcjonalnie)|TCP|80|Sieć firmowa|Przychodzące|
|**HTTPS**|TCP|443|Sieć firmowa i brama usługi ATA|Przychodzące|
|**SMTP** (opcjonalnie)|TCP|25|Serwer SMTP|Wychodzące|
|**SMTPS** (opcjonalnie)|TCP|465|Serwer SMTP|Wychodzące|
|**Syslog** (opcjonalnie)|TCP|514|Serwer Syslog|Wychodzące|
|**LDAP**|TCP i UDP|389|Kontrolery domeny|Wychodzące|
|**LDAPS** (opcjonalnie)|TCP|636|Kontrolery domeny|Wychodzące|
|**DNS**|TCP i UDP|53|Serwery DNS|Wychodzące|
|**Kerberos** (opcjonalnie, jeśli przyłączono do domeny)|TCP i UDP|88|Kontrolery domeny|Wychodzące|
|**Netlogon** (opcjonalnie, jeśli przyłączono do domeny)|TCP i UDP|445|Kontrolery domeny|Wychodzące|
|**Czas systemu Windows** (opcjonalne, jeśli przyłączonych do domeny)|UDP|123|Kontrolery domeny|Wychodzące|

> [!NOTE]
> LDAP jest wymagane do przetestowania poświadczenia do użycia między bram usługi ATA i kontrolerach domeny. Uruchomienie testu jest wykonywane z Centrum usługi ATA do kontrolera domeny, aby sprawdzić poprawność tych poświadczeń, po których bramy usługi ATA używa protokołu LDAP jako część procesu zwykłej rozdzielczości.

### <a name="certificates"></a>Certyfikaty

Aby ułatwić instalację usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu własnym certyfikatem z wewnętrznego urzędu certyfikacji, który ma być używany przez Centrum usługi ATA należy zastąpić podpisem.


Upewnij się, że Centrum usługi ATA i bramy usługi ATA mają dostęp do punktu dystrybucji z listy CRL. Jeśli nie ma dostępu do Internetu, wykonaj [procedurę ręcznego importowania listy CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), zwracając szczególną uwagę, aby zainstalować wszystkie dystrybucji listy CRL punktów dla całego łańcucha.

Certyfikat musi mieć:
-   Klucz prywatny
-   Typ dostawcy, dostawca usług kryptograficznych (CSP) lub dostawcy magazynu kluczy (KSP)
-   Publiczny klucz o długości 2048 bitów
-   Wartość dla KeyEncipherment i ServerAuthentication flagi użycia

Na przykład można użyć standardowego **serwera sieci Web** lub **komputera** szablonów.

> [!WARNING]
> - Proces odnowienie istniejącego certyfikatu nie jest obsługiwane. Jedynym sposobem, aby odnowić certyfikat jest tworzony nowy certyfikat i konfigurowania usługi ATA przy użyciu nowego certyfikatu.


> [!NOTE]
> - Jeśli ma dostęp do konsoli usługi ATA z innych komputerów, upewnij się, że te komputery ufają certyfikatowi używanemu przez Centrum usługi ATA w przeciwnym razie otrzymasz strona z ostrzeżeniem że występuje problem z certyfikatem zabezpieczeń witryny sieci Web przed przejściem do strony logowania.
> - Począwszy od wersji 1.8 usługi ATA bramy usługi ATA i bram Lightweight zarządzanym własne certyfikaty i wymagają interakcji ze strony administratora do zarządzania nimi.

## <a name="ata-gateway-requirements"></a>Wymagania bramy usługi ATA
Ta sekcja zawiera listę wymagań bramy usługi ATA.
### <a name="general"></a>Ogólne
Brama usługi ATA obsługuje instalację na serwerze z systemem Windows Server 2012 R2 lub Windows Server 2016 (w tym Server Core).
Brama usługi ATA może zostać zainstalowana na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
Brama usługi ATA może służyć do monitorowania kontrolerów domeny z poziomem funkcjonalności domeny systemu Windows 2003 lub nowszego.

Przed zainstalowaniem bramy usługi ATA w systemie Windows 2012 R2 upewnij się, że została zainstalowana następująca aktualizacja: [KB2919355](https://support.microsoft.com/kb/2919355/).

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`.


Aby uzyskać informacje o używaniu maszyn wirtualnych z bramą usługi ATA, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).

> [!NOTE]
> Minimalne miejsce wymagane to 5 GB, a zalecane to 10 GB. Dotyczy to również miejsce wymagane do plików binarnych usługi ATA, [dzienniki usługi ATA i [dzienników wydajności](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specyfikacje serwera
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** bramy usługi ATA na wartość **Wysoka wydajność**.<br>
Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego do i z kontrolerów domeny.

>[!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach sprzętowych bramy usługi ATA, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu
Serwerze Centrum usługi ATA, serwerach bramy usługi ATA i kontrolerach domeny musi mieć czasu synchronizowane w ciągu pięciu minut od siebie.

### <a name="network-adapters"></a>Karty sieciowe
Brama usługi ATA wymaga co najmniej jednej karty administracyjnej i co najmniej jednej karty sieciowej przechwytywania:

-   **Karta sieciowa zarządzania** — używane do komunikacji w sieci firmowej. Ta karta powinna skonfigurowana z następującymi ustawieniami:

    -   Statyczny adres IP obejmujący bramę domyślną

    -   Preferowane i alternatywne serwery DNS

    -   W polu **Sufiks DNS dla tego połączenia** należy podać nazwę DNS każdej monitorowanej domeny.

        ![Konfigurowanie sufiksu DNS w zaawansowanych ustawieniach protokołu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Jeśli brama usługi ATA jest elementem członkowskim domeny, te ustawienia mogą zostać skonfigurowane automatycznie.

-   **Karta przechwytywania** — będzie używana do przechwytywania ruchu do i z kontrolerów domeny.

    > [!IMPORTANT]
    > -   Skonfiguruj funkcję dublowania portów dla karty przechwytywania jako miejsce docelowe ruchu sieciowego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md). Zazwyczaj należy współpracować z zespołem sieci lub wirtualizacji w celu skonfigurowania funkcji dublowania portów.
    > -   Skonfiguruj statyczny adres IP bez obsługi routingu dla danego środowiska bez bramy domyślnej i bez adresów serwerów DNS. Na przykład 1.1.1.1/32. Dzięki temu, że karta sieciowa przechwytywania może przechwytywać maksymalną ilość ruchu sieciowego i że administracyjnej karty sieciowej jest używany do wysyłania i odbierania wymaganego ruchu sieciowego.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty, których skonfigurowanie na karcie administracyjnej jest wymagane przez bramę usługi ATA:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP i UDP|389|Kontrolery domeny|Wychodzące|
|Bezpieczny protokół LDAP (LDAPS)|TCP|636|Kontrolery domeny|Wychodzące|
|LDAP do wykazu globalnego|TCP|3268|Kontrolery domeny|Wychodzące|
|LDAPS do wykazu globalnego|TCP|3269|Kontrolery domeny|Wychodzące|
|Kerberos|TCP i UDP|88|Kontrolery domeny|Wychodzące|
|Netlogon|TCP i UDP|445|Kontrolery domeny|Wychodzące|
|Czas systemu Windows|UDP|123|Kontrolery domeny|Wychodzące|
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Wychodzące|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Wychodzące|
|Protokół SSL|TCP|443 lub skonfigurowany dla usługi centrum|Centrum usługi ATA:<br /><br />— adres IP usługi centrum<br />— adres IP konsoli|Wychodzące|
|Syslog (opcjonalnie)|UDP|514|Serwer SIEM|Przychodzące|

> [!NOTE]
> W ramach procesu rozpoznawania wykonywanego przez bramę usługi ATA następujące porty muszą być otwarte dla danych przychodzących z bram usługi ATA na urządzeniach w sieci.
>
> -   NTLM przez RPC (port TCP 135)
> -   NetBIOS (port UDP 137)

## <a name="ata-lightweight-gateway-requirements"></a>Wymagania dotyczące uproszczonej bramy usługi ATA
Ta sekcja zawiera listę wymagań uproszczonej bramy usługi ATA.
### <a name="general"></a>Ogólne
Uproszczona brama usługi ATA obsługuje instalację na kontrolerze domeny z systemami Windows Server 2008 R2 z dodatkiem SP1 (bez instalacji Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (z instalacją Core, ale nie Nano).

Kontroler domeny może być kontrolerem domeny tylko do odczytu (RODC).

Przed zainstalowaniem uproszczonej bramy usługi ATA na kontrolerze domeny z systemem Windows Server 2012 R2 upewnij się, że zainstalowano następującą aktualizację: [KB2919355](https://support.microsoft.com/kb/2919355/).

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`

W przypadku instalacji systemu Windows Server 2012 R2 Server Core musisz również zainstalować następującą aktualizację: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb3000850]`


Podczas instalacji instalowany jest program .Net Framework 4.6.1, który może spowodować ponowny rozruch kontrolera domeny.


> [!NOTE]
> Minimalne miejsce wymagane to 5 GB, a zalecane to 10 GB. Dotyczy to również miejsce wymagane do plików binarnych usługi ATA, [dzienniki usługi ATA i [dzienników wydajności](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specyfikacje serwera

Brama ATA Lightweight Gateway wymaga co najmniej dwa rdzenie i 6 GB pamięci RAM zainstalowanych na kontrolerze domeny.
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** uproszczonej bramy usługi ATA na wartość **Wysoka wydajność**.
Uproszczoną bramę usługi ATA można wdrożyć na kontrolerach domeny o różnych obciążeniach i rozmiarach, w zależności od ilości ruchu sieciowego w kontrolerach domeny oraz ilości zasobów zainstalowanych w danym kontrolerze domeny.

>[!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach sprzętowych bramy ATA Lightweight Gateway, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu
Serwerze Centrum usługi ATA, serwerów bramy ATA Lightweight Gateway i kontrolerach domeny musi mieć czasu synchronizowane w ciągu pięciu minut od siebie.
### <a name="network-adapters"></a>Karty sieciowe
Uproszczona brama usługi ATA monitoruje lokalny ruch na wszystkich kartach sieciowych kontrolera domeny. <br>
Po przeprowadzeniu wdrożenia możesz użyć konsoli usługi ATA, jeśli chcesz określić, które karty sieciowe są monitorowane.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty wymagane przez uproszczoną bramę usługi ATA:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Wychodzące|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Wychodzące|
|Protokół SSL|TCP|443 lub skonfigurowany dla usługi centrum|Centrum usługi ATA:<br /><br />— adres IP usługi centrum<br />— adres IP konsoli|Wychodzące|
|Syslog (opcjonalnie)|UDP|514|Serwer SIEM|Przychodzące|

> [!NOTE]
> W ramach procesu rozpoznawania wykonywanego przez uproszczoną bramę usługi ATA następujące porty muszą być otwarte dla danych przychodzących z uproszczonych bram usługi ATA na urządzeniach w sieci.
>
> -   NTLM za pośrednictwem wywołania RPC
> -   NetBIOS

## <a name="ata-console"></a>Konsola usługi ATA
Dostęp do konsoli usługi ATA jest za pośrednictwem przeglądarki, pomocniczych przeglądarki oraz ustawienia:

-   Internet Explorer 10 i nowsze

-   Microsoft Edge

-   Google Chrome 40 i nowsze

-   Minimalna rozdzielczość ekranu w poziomie: 1700 pikseli

## <a name="related-videos"></a>Powiązane pliki wideo
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Architektura usługi ATA](ata-architecture.md)
- [Instalowanie usługi ATA](install-ata-step1.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


