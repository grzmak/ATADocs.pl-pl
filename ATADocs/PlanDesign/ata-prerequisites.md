---
title: "Wymagania wstępne usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Zawiera opis wymagań, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/30/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 270a16feada7db5462c5232f023c0bab9ef23c7e
ms.sourcegitcommit: cb2a4df6805d41bf030d3439ef87281fc6acc98f
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="ata-prerequisites"></a>Wymagania wstępne usługi ATA
W tym artykule opisano wymagania, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku.

>[!NOTE]
> Aby uzyskać więcej informacji o planowaniu zasobów i pojemności, zobacz temat [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


Usługa ATA składa się z centrum usługi ATA, bramy usługi ATA i/lub bramy ATA Lightweight Gateway. Aby uzyskać więcej informacji o składnikach usługi ATA, zobacz [Architektura usługi ATA](ata-architecture.md).

System ATA działa na granicy lasu usługi Active Directory i obsługuje poziom funkcjonalności lasu (FFL) systemu Windows 2003 lub nowszego.


[Przed rozpoczęciem](#before-you-start): w tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.

[Centrum usługi ATA](#ata-center-requirements): ta sekcja zawiera informacje o wymaganiach centrum usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerze centrum usługi ATA.

[Brama usługi ATA](#ata-gateway-requirements): ta sekcja zawiera informacje o wymaganiach bramy usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerach bramy usługi ATA.

[Brama ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): w tej sekcji przedstawiono wymagania sprzętowe i programowe bramy ATA Lightweight Gateway.

[Konsola usługi ATA](#ata-console): ta sekcja zawiera informacje o wymaganiach dotyczących przeglądarek związanych z uruchamianiem konsoli usługi ATA.

![Diagram architektury usługi ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Przed rozpoczęciem
W tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.


-   Konto i hasło użytkownika z dostępem do odczytu do wszystkich obiektów w domenach, które będą monitorowane.

    > [!NOTE]
    > Jeśli ustawiono niestandardowe listy kontroli dostępu w różnych jednostkach organizacyjnych w domenie, upewnij się, że wybrany użytkownik ma uprawnienia do odczytu do tych jednostek organizacyjnych.

-   Upewnij się, że analizator komunikatów i program WireShark nie są zainstalowane w bramie usługi ATA.
-    Zalecane: użytkownik powinien mieć uprawnienia dostępu tylko do odczytu do kontenera usuniętych obiektów. Umożliwi to wykrywanie zbiorczego usuwania obiektów w domenie przez usługę ATA. Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz sekcję **Zmienianie uprawnień do kontenera usuniętych obiektów** w temacie [Wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcjonalnie: konto użytkownika, który nie ma żadnych działań w sieci. To konto zostanie skonfigurowane jako użytkownik usługi ATA wystawiony jako przynęta. Do skonfigurowania użytkownika wystawionego jako przynęta potrzebny jest identyfikator SID konta użytkownika, a nie nazwa użytkownika. Aby uzyskać więcej informacji, zobacz [Praca z ustawieniami wykrywania usługi ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings).

-   Opcjonalnie: oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny usługa ATA może dodatkowo ulepszyć wykrywanie ataków typu Pass-the-Hash przy użyciu zdarzenia 4776 systemu Windows. Może być ono odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.


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
Podczas pracy na serwerze fizycznym baza danych usługi ATA wymaga **wyłączenia** obsługi niejednolitego dostępu do pamięci (NUMA) w systemie BIOS. Technologia NUMA może być nazwana w systemie przeplataniem węzłów. W tym przypadku należy **włączyć** przeplatanie węzłów, aby wyłączyć technologię NUMA. Aby uzyskać więcej informacji, zapoznaj się z dokumentacją systemu BIOS. Należy zauważyć, że nie jest to istotne w przypadku uruchomienia centrum usługi ATA na serwerze wirtualnym.<br>
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** centrum usługi ATA na wartość **Wysoka wydajność**.<br>
Liczba monitorowanych kontrolerów domeny i obciążenie poszczególnych kontrolerów domeny decyduje o wymaganych specyfikacjach serwera. Aby uzyskać więcej szczegółów, zobacz temat [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Synchronizacja czasu
Różnica czasu ustawionego na serwerze centrum usługi ATA, serwerach bramy usługi ATA i kontrolerach domeny nie może być większa niż 5 minut.


### <a name="network-adapters"></a>Karty sieciowe
Musisz mieć następujące elementy:
-   Co najmniej jedna karta sieciowa (w przypadku korzystania z serwera fizycznego w środowisku sieci VLAN zaleca się używanie dwóch kart sieciowych)

-   Dwa adresy IP (zalecane, ale niewymagane)

Komunikacja między centrum usługi ATA i bramą usługi ATA jest szyfrowana przy użyciu protokołu SSL na porcie 443. Ponadto konsola usługi ATA również używa protokołu SSL na porcie 443. Zalecane są **dwa adresy IP**. Centrum usługi ATA powiąże port 443 z pierwszym adresem IP, a konsola usługi ATA powiąże port 443 z drugim adresem IP.

> [!NOTE]
> Możliwe jest użycie pojedynczego adresu IP z dwoma różnymi portami, ale zaleca się użycie dwóch adresów IP.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty, które należy otworzyć, aby centrum usługi ATA działało poprawnie.

W tej tabeli adres IP 1 jest powiązany z centrum usługi ATA, a adres IP 2 jest powiązany z konsolą usługi ATA:

|Protokół|Transport|Port|Do/z|Kierunek|Adres IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (komunikacja usługi ATA)|TCP|443 lub inny skonfigurowany|Brama usługi ATA|Przychodzące|Adres IP 1|
|**HTTP**|TCP|80|Sieć firmowa|Przychodzące|Adres IP 2|
|**HTTPS**|TCP|443|Sieć firmowa i brama usługi ATA|Przychodzące|Adres IP 2|
|**SMTP** (opcjonalnie)|TCP|25|Serwer SMTP|Wychodzące|Adres IP 2|
|**SMTPS** (opcjonalnie)|TCP|465|Serwer SMTP|Wychodzące|Adres IP 2|
|**Syslog** (opcjonalnie)|TCP|514|Serwer Syslog|Wychodzące|Adres IP 2|

### <a name="certificates"></a>Certyfikaty
Upewnij się, że centrum usługi ATA ma dostęp do punktu dystrybucji listy CRL. Jeśli bramy usługi ATA nie mają dostępu do Internetu, wykonaj [procedurę ręcznego importowania listy CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), zwracając szczególną uwagę na zainstalowanie wszystkich punktów dystrybucji listy CRL dla całego łańcucha.

Aby ułatwić instalację usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu możesz zastąpić certyfikat z podpisem własnym certyfikatem z wewnętrznego urzędu certyfikacji, który będzie używany przez bramę usługi ATA.<br>
> [!NOTE]
> Typem dostawcy certyfikatu musi być Dostawca usług kryptograficznych (CSP).


> Korzystanie z automatycznego odnawiania certyfikatów nie jest obsługiwane.


> [!NOTE]
> Jeśli dostęp do konsoli usługi ATA ma być uzyskiwany z innych komputerów, upewnij się, że te komputery ufają certyfikatowi używanemu przez centrum usługi ATA. W przeciwnym razie przed przejściem do strony logowania zostanie wyświetlona strona ostrzeżenia z informacją, że wystąpił problem z certyfikatem zabezpieczeń witryny internetowej.

## <a name="ata-gateway-requirements"></a>Wymagania bramy usługi ATA
Ta sekcja zawiera listę wymagań bramy usługi ATA.
### <a name="general"></a>Ogólne
Brama usługi ATA obsługuje instalację na serwerze z systemem Windows Server 2012 R2 lub Windows Server 2016 (w tym Server Core).
Brama usługi ATA może zostać zainstalowana na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
Brama usługi ATA może służyć do monitorowania kontrolerów domeny z poziomem funkcjonalności domeny systemu Windows 2003 lub nowszego.

Przed zainstalowaniem bramy usługi ATA w systemie Windows 2012 R2 upewnij się, że została zainstalowana następująca aktualizacja: [KB2919355](https://support.microsoft.com/kb/2919355/).

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`.


Aby uzyskać informacje o używaniu maszyn wirtualnych z bramą usługi ATA, zobacz [Konfigurowanie funkcji dublowania portów](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

> [!NOTE]
> Minimalne miejsce wymagane to 5 GB, a zalecane to 10 GB. Obejmuje to miejsce wymagane dla plików binarnych ATA, [dzienników ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) i [dzienników wydajności](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters).

### <a name="server-specifications"></a>Specyfikacje serwera
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** bramy usługi ATA na wartość **Wysoka wydajność**.<br>
Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego do i z kontrolerów domeny.

>[!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach bramy usługi ATA dotyczących sprzętu, zobacz artykuł [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu
Różnica czasu ustawionego na serwerze centrum usługi ATA, serwerach bramy usługi ATA i kontrolerach domeny nie może być większa niż 5 minut.

### <a name="network-adapters"></a>Karty sieciowe
Brama usługi ATA wymaga co najmniej jednej karty administracyjnej i co najmniej jednej karty sieciowej przechwytywania:

-   **Karta administracyjna** — będzie używana do komunikacji w sieci firmowej. Tę kartę należy skonfigurować w następujący sposób:

    -   Statyczny adres IP obejmujący bramę domyślną

    -   Preferowane i alternatywne serwery DNS

    -   W polu **Sufiks DNS dla tego połączenia** należy podać nazwę DNS każdej monitorowanej domeny.

        ![Konfigurowanie sufiksu DNS w zaawansowanych ustawieniach protokołu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Jeśli brama usługi ATA jest elementem członkowskim domeny, te ustawienia mogą zostać skonfigurowane automatycznie.

-   **Karta przechwytywania** — będzie używana do przechwytywania ruchu do i z kontrolerów domeny.

    > [!IMPORTANT]
    > -   Skonfiguruj funkcję dublowania portów dla karty przechwytywania jako miejsce docelowe ruchu sieciowego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](/advanced-threat-analytics/deploy-use/configure-port-mirroring). Zwykle w celu skonfigurowania funkcji dublowania portów konieczna jest współpraca z zespołem ds. sieci lub wirtualizacji.
    > -   Skonfiguruj statyczny adres IP bez obsługi routingu dla danego środowiska bez bramy domyślnej i bez adresów serwerów DNS. Na przykład 1.1.1.1/32. Dzięki temu karta sieciowa przechwytywania może przechwytywać maksymalną ilość ruchu, a karta administracyjna będzie używana do wysyłania i odbierania wymaganego ruchu sieciowego.

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

### <a name="certificates"></a>Certyfikaty
Upewnij się, że centrum usługi ATA ma dostęp do punktu dystrybucji listy CRL. Jeśli bramy usługi ATA nie mają dostępu do Internetu, wykonaj procedurę ręcznego importowania listy CRL, zwracając szczególną uwagę na zainstalowanie wszystkich punktów dystrybucji listy CRL dla całego łańcucha.<br>
Aby ułatwić instalację usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu możesz zastąpić certyfikat z podpisem własnym certyfikatem z wewnętrznego urzędu certyfikacji, który będzie używany przez bramę usługi ATA.

> [!NOTE]
> Typem dostawcy certyfikatu musi być Dostawca usług kryptograficznych (CSP).<br>

W magazynie Komputer bramy usługi ATA w ramach magazynu Komputer lokalny musi być zainstalowany certyfikat obsługujący **uwierzytelnianie serwera**. Ten certyfikat musi być zaufany przez centrum usługi ATA.

## <a name="ata-lightweight-gateway-requirements"></a>Wymagania dotyczące bramy ATA Lightweight Gateway
Ta sekcja zawiera listę wymagań bramy ATA Lightweight Gateway.
### <a name="general"></a>Ogólne
Brama ATA Lightweight Gateway obsługuje instalację na kontrolerze domeny z systemami Windows Server 2008 R2 z dodatkiem SP1 (bez instalacji Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (z instalacją Core, ale nie Nano).

Kontroler domeny może być kontrolerem domeny tylko do odczytu (RODC).

Przed zainstalowaniem bramy ATA Lightweight Gateway na kontrolerze domeny z systemem Windows Server 2012 R2 upewnij się, że zainstalowano następującą aktualizację: [KB2919355](https://support.microsoft.com/kb/2919355/).

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`

W przypadku instalacji systemu Windows Server 2012 R2 Server Core musisz również zainstalować następującą aktualizację:  [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb3000850]`


Podczas instalacji instalowany jest program .Net Framework 4.6.1, który może spowodować ponowny rozruch kontrolera domeny.


> [!NOTE]
> Minimalne miejsce wymagane to 5 GB, a zalecane to 10 GB. Obejmuje to miejsce wymagane dla plików binarnych ATA, [dzienników ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs.md) i [dzienników wydajności](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Specyfikacje serwera

Brama ATA Lightweight Gateway wymaga co najmniej 2 rdzeni i 6 GB pamięci RAM zainstalowanych na kontrolerze domeny.
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** bramy ATA Lightweight Gateway na wartość **Wysoka wydajność**.
Bramę ATA Lightweight Gateway można wdrożyć na kontrolerach domeny o różnych obciążeniach i rozmiarach, w zależności od ilości ruchu sieciowego w kontrolerach domeny oraz ilości zasobów zainstalowanych w danym kontrolerze domeny.

>[!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach bramy ATA Lightweight Gateway dotyczących sprzętu, zobacz artykuł [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu
Różnica czasu ustawionego na serwerze centrum usługi ATA, serwerach bramy ATA Lightweight Gateway i kontrolerach domeny nie może być większa niż 5 minut.
### <a name="network-adapters"></a>Karty sieciowe
Brama ATA Lightweight Gateway monitoruje lokalny ruch na wszystkich kartach sieciowych kontrolera domeny. <br>
Po przeprowadzeniu wdrożenia możesz użyć konsoli usługi ATA, jeśli chcesz określić, które karty sieciowe są monitorowane.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty wymagane przez bramę ATA Lightweight Gateway:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Wychodzące|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Wychodzące|
|Protokół SSL|TCP|443 lub skonfigurowany dla usługi centrum|Centrum usługi ATA:<br /><br />— adres IP usługi centrum<br />— adres IP konsoli|Wychodzące|
|Syslog (opcjonalnie)|UDP|514|Serwer SIEM|Przychodzące|

> [!NOTE]
> W ramach procesu rozpoznawania wykonywanego przez bramę ATA Lightweight Gateway następujące porty muszą być otwarte dla danych przychodzących z bram ATA Lightweight Gateway na urządzeniach w sieci.
>
> -   NTLM za pośrednictwem wywołania RPC
> -   NetBIOS

### <a name="certificates"></a>Certyfikaty
Upewnij się, że centrum usługi ATA ma dostęp do punktu dystrybucji listy CRL. Jeśli bramy ATA Lightweight Gateway nie mają dostępu do Internetu, wykonaj procedurę ręcznego importowania listy CRL, zwracając szczególną uwagę na zainstalowanie wszystkich punktów dystrybucji listy CRL dla całego łańcucha.
Aby ułatwić instalację usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu możesz zastąpić certyfikat z podpisem własnym certyfikatem z wewnętrznego urzędu certyfikacji, który będzie używany przez bramę ATA Lightweight Gateway.
> [!NOTE]
> Typem dostawcy certyfikatu musi być Dostawca usług kryptograficznych (CSP).

W magazynie Komputer bramy ATA Lightweight Gateway w ramach magazynu Komputer lokalny musi być zainstalowany certyfikat obsługujący uwierzytelnianie serwera. Ten certyfikat musi być zaufany przez centrum usługi ATA.

## <a name="ata-console"></a>Konsola usługi ATA
Dostęp do konsoli usługi ATA odbywa się za pośrednictwem przeglądarki. Obsługiwane są następujące z nich:

-   Internet Explorer 10 i nowsze

-   Microsoft Edge

-   Google Chrome 40 i nowsze

-   Minimalna rozdzielczość ekranu w poziomie: 1700 pikseli

## <a name="see-also"></a>Zobacz też

- [Architektura usługi ATA](ata-architecture.md)
- [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


