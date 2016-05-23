---
# required metadata

title: Wymagania wstępne usługi ATA | Microsoft Advanced Threat Analytics
description: Zawiera opis wymagań, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Wymagania wstępne usługi ATA
W tym artykule opisano wymagania, które należy spełnić w celu pomyślnego wdrożenia usługi ATA w środowisku.

Usługa ATA ma dwa składniki: bramę usługi ATA i centrum usługi ATA. Aby uzyskać więcej informacji o składnikach usługi ATA, zobacz [Architektura usługi ATA](/advanced-threat-analytics/understand-explore/ata-architecture)..

[Przed rozpoczęciem](#before-you-start): w tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.

[Centrum usługi ATA](#ata-center-requirements): ta sekcja zawiera informacje o wymaganiach centrum usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerze centrum usługi ATA.

[Brama usługi ATA](#ata-gateway-requirements): ta sekcja zawiera informacje o wymaganiach bramy usługi ATA dotyczących sprzętu i oprogramowania, a także ustawieniach, które należy skonfigurować na serwerach bramy usługi ATA.

[Konsola usługi ATA](#ata-console): ta sekcja zawiera informacje o wymaganiach dotyczących przeglądarek związanych z uruchamianiem konsoli usługi ATA.

![Diagram architektury usługi ATA](media/ATA-architecture-topology.jpg)

## Przed rozpoczęciem
W tej sekcji opisano informacje, które należy zebrać, oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi ATA.

-   **Kontrolery domeny** uruchomione w systemie Windows Server 2008 lub nowszym.

-   **Konto i hasło użytkownika** z dostępem do odczytu do **wszystkich obiektów** w domenach, które będą monitorowane.

    > [!NOTE]
    > Jeśli ustawiono niestandardowe listy kontroli dostępu w różnych jednostkach organizacyjnych w domenie, upewnij się, że wybrany użytkownik ma uprawnienia do odczytu do tych jednostek organizacyjnych.

    Opcjonalnie: użytkownik powinien mieć uprawnienia tylko do odczytu do kontenera usuniętych obiektów. Umożliwi to wykrywanie zbiorczego usuwania obiektów w domenie przez usługę ATA. Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz sekcję **Zmienianie uprawnień do kontenera usuniętych obiektów** w temacie [Wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcjonalnie: konto użytkownika, który nie ma żadnych działań w sieci. To konto zostanie skonfigurowane jako użytkownik usługi ATA wystawiony jako przynęta. Do skonfigurowania użytkownika wystawionego jako przynęta potrzebny jest identyfikator SID konta użytkownika, a nie nazwa użytkownika.

-   Opcjonalnie: oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny usługa ATA może dodatkowo ulepszyć wykrywanie ataków typu Pass-the-Hash przy użyciu zdarzenia 4776 systemu Windows. Może być ono odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.

-   Warto utworzyć listę wszystkich podsieci używanych w ramach sieci dla połączeń VPN i Wi-Fi, w których przypisania adresów IP między urządzeniami ulegają zmianie w bardzo krótkim czasie (liczonym w sekundach lub minutach).  Warto również zidentyfikować te podsieci o krótkim okresie dzierżawy, aby umożliwić zmniejszenie okresu istnienia pamięci podręcznej przez usługę ATA w celu dostosowania do szybkiego ponownego przypisywania adresów IP między urządzeniami. Aby uzyskać informacje na temat konfigurowania podsieci dzierżawy krótkoterminowej, zobacz [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-useinstall-ata).

## Wymagania centrum usługi ATA
Ta sekcja zawiera listę wymagań centrum usługi ATA.

Centrum usługi ATA obsługuje instalację na serwerze z systemem Windows Server 2012 R2. Uruchom usługę Windows Update i upewnij się, że wszystkie ważne aktualizacje zostały zainstalowane.
 Liczba monitorowanych kontrolerów domeny i obciążenie poszczególnych kontrolerów domeny decyduje o wymaganiach dotyczących sprzętu.

Instalacja centrum usługi ATA jako maszyny wirtualnej jest obsługiwana. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md)..

Jeśli centrum usługi ATA jest uruchamiane jako maszyna wirtualna, należy wyłączyć serwer przed utworzeniem nowego punktu kontrolnego w celu uniknięcia potencjalnego uszkodzenia bazy danych.

> [!NOTE]
> - Centrum usługi ATA można zainstalować na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
>
> - W celu wykonania analizy behawioralnej użytkowników centrum usługi ATA wymaga danych z co najmniej 21 dni.
>
> - Aby uzyskać więcej informacji o wymaganiach dotyczących sprzętu, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md)..


### Synchronizacja czasu
Różnica czasu ustawionego na serwerze centrum usługi ATA, serwerach bramy usługi ATA i kontrolerach domeny nie może być większa niż 5 minut.

### Ustawienia systemu BIOS
Baza danych usługi ATA wymaga **wyłączenia** obsługi niejednolitego dostępu do pamięci (NUMA) w systemie BIOS. Technologia NUMA może być nazwana w systemie przeplataniem węzłów. W tym przypadku należy **włączyć** przeplatanie węzłów. Aby uzyskać więcej informacji, zapoznaj się z dokumentacją systemu BIOS.

### Karty sieciowe
Wymagania:

-   Jedna karta sieciowa

-   Dwa adresy IP

Komunikacja między centrum usługi ATA i bramą usługi ATA jest szyfrowana przy użyciu protokołu SSL na porcie 443. Dodatkowo konsola usługi ATA działa w oparciu o usługi IIS i jest zabezpieczona przy użyciu protokołu SSL na porcie 443. Zalecane są **dwa adresy IP**. Centrum usługi ATA powiąże port 443 z pierwszym adresem IP, a usługi IIS powiążą port 443 z drugim adresem IP.

> [!NOTE]
> Możliwe jest użycie pojedynczego adresu IP z dwoma różnymi portami, ale zaleca się użycie dwóch adresów IP.

### Porty
W poniższej tabeli wymieniono niezbędne porty, które należy otworzyć, aby centrum usługi ATA działało poprawnie.

W tej tabeli adres IP 1 jest powiązany z centrum usługi ATA, a adres IP 2 jest powiązany z usługami IIS dla konsoli usługi ATA.

|Protokół|Transport|Port|Do/z|Kierunek|Adres IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (komunikacja usługi ATA)|TCP|443 lub inny skonfigurowany|Brama usługi ATA|Przychodzące|Adres IP 1|
|**HTTP**|TCP|80|Sieć firmowa|Przychodzące|Adres IP 2|
|**HTTPS**|TCP|443|Sieć firmowa i brama usługi ATA|Przychodzące|Adres IP 2|
|**SMTP** (opcjonalnie)|TCP|25|Serwer SMTP|Wychodzące|Adres IP 2|
|**SMTPS** (opcjonalnie)|TCP|465|Serwer SMTP|Wychodzące|Adres IP 2|
|**Syslog** (opcjonalnie)|TCP|514|Serwer Syslog|Wychodzące|Adres IP 2|

### Certyfikaty
Upewnij się, że bramy usługi ATA mają dostęp do punktu dystrybucji listy CRL. Jeśli bramy usługi ATA nie mają dostępu do Internetu, wykonaj [procedurę ręcznego importowania listy CRL](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx), zwracając szczególną uwagę na zainstalowanie wszystkich punktów dystrybucji listy CRL dla całego łańcucha.

Aby ułatwić instalację centrum usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu możesz zastąpić certyfikat z podpisem własnym certyfikatem z wewnętrznego urzędu certyfikacji, który będzie używany przez bramę usługi ATA.

> [!NOTE]
> Certyfikatów z podpisem własnym powinno się używać tylko w przypadku wdrożenia laboratoryjnego.

Centrum usługi ATA wymaga certyfikatów dla następujących usług:

-   Usługi Internet Information Services (IIS) — certyfikat serwera sieci Web

-   Centrum usługi ATA — certyfikat uwierzytelniania serwera

> [!NOTE]
> Jeśli dostęp do konsoli usługi ATA ma się odbywać z innych komputerów, upewnij się, że te komputery ufają certyfikatowi używanemu przez usługi IIS. W przeciwnym razie przed przejściem do strony logowania zostanie wyświetlona strona ostrzeżenia z informacją, że wystąpił problem z certyfikatem zabezpieczeń witryny sieci Web.

## Wymagania bramy usługi ATA
Brama usługi ATA obsługuje instalację na serwerze z systemem Windows Server 2012 R2.

Uruchom usługę Windows Update i upewnij się, że wszystkie **ważne** aktualizacje zostały zainstalowane.
Przed zainstalowaniem bramy usługi ATA potwierdź, że następująca aktualizacja została zainstalowana: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/)..

Możesz to sprawdzić, uruchamiając następujące polecenie cmdlet programu Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

> [!NOTE]
> -   Brama usługi ATA może zostać zainstalowana na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
> -   Brama usługi ATA nie może zostać zainstalowana w kontrolerze domeny.

Aby uzyskać informacje o używaniu maszyn wirtualnych z bramą usługi ATA, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md)..

> [!NOTE]
> Jeśli brama usługi ATA jest uruchamiana jako maszyna wirtualna, należy wyłączyć serwer przed utworzeniem nowego punktu kontrolnego w celu uniknięcia potencjalnego uszkodzenia bazy danych.

Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego do i z kontrolerów domeny.
Aby uzyskać więcej informacji, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md)..

### Ustawienia zasilania
Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** bramy usługi ATA na wartość **Wysoka wydajność**..

### Synchronizacja czasu
Różnica czasu ustawionego na serwerze centrum usługi ATA i serwerze bramy usługi ATA nie może być większa niż 5 minut.

Dodatkowo różnica czasu ustawionego w bramie usługi ATA i kontrolerach domeny, z którymi ta brama nawiązuje połączenie, nie może być większa niż 5 minut.

### Karty sieciowe
Brama usługi ATA wymaga co najmniej jednej karty administracyjnej i co najmniej jednej karty sieciowej przechwytywania:

-   **Karta administracyjna** — będzie używana do komunikacji w sieci firmowej. Tę kartę należy skonfigurować w następujący sposób:

    -   Statyczny adres IP obejmujący bramę domyślną

    -   Preferowane i alternatywne serwery DNS

    -   W polu **Sufiks DNS dla tego połączenia** należy podać nazwę DNS każdej monitorowanej domeny.

        ![Konfigurowanie sufiksu DNS w zaawansowanych ustawieniach protokołu TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Jeśli brama usługi ATA jest elementem członkowskim domeny, te ustawienia zostaną skonfigurowane automatycznie.

-   **Karta przechwytywania** — będzie używana do przechwytywania ruchu do i z kontrolerów domeny.

    > [!IMPORTANT]
    > -   Skonfiguruj funkcję dublowania portów dla karty przechwytywania jako miejsce docelowe ruchu sieciowego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md). Zwykle w celu skonfigurowania funkcji dublowania portów konieczna jest współpraca z zespołem ds. sieci lub wirtualizacji.
    > -   Skonfiguruj statyczny adres IP bez obsługi routingu dla danego środowiska bez bramy domyślnej i bez adresów serwerów DNS. Na przykład 1.1.1.1/32. Dzięki temu karta sieciowa przechwytywania może przechwytywać maksymalną ilość ruchu, a karta administracyjna będzie używana do wysyłania i odbierania wymaganego ruchu sieciowego.

### Porty
W poniższej tabeli wymieniono niezbędne porty, których skonfigurowanie na karcie administracyjnej jest wymagane przez bramę usługi ATA.

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
|Protokół SSL|TCP|443 lub skonfigurowany dla usługi centrum|Centrum usługi ATA:<br /><br />— adres IP usługi centrum<br />— adres IP usług IIS|Wychodzące|
|Syslog (opcjonalnie)|UDP|514|Serwer SIEM|Przychodzące|

> [!NOTE]
> W ramach procesu rozpoznawania wykonywanego przez bramę usługi ATA następujące porty muszą być otwarte dla danych przychodzących z bram usługi ATA na urządzeniach w sieci.
>
> -   NTLM za pośrednictwem wywołania RPC
> -   NetBIOS

### Certyfikaty
Aby ułatwić instalację centrum usługi ATA, podczas instalacji możesz zainstalować certyfikaty z podpisem własnym. Po wdrożeniu możesz zastąpić certyfikat z podpisem własnym certyfikatem z wewnętrznego urzędu certyfikacji, który będzie używany przez bramę usługi ATA.

> [!NOTE]
> Certyfikatów z podpisem własnym powinno się używać tylko w przypadku wdrożenia laboratoryjnego.

W magazynie Komputer bramy usługi ATA w ramach magazynu Komputer lokalny musi być zainstalowany certyfikat obsługujący **uwierzytelnianie serwera**. Ten certyfikat musi być zaufany przez centrum usługi ATA.

## Konsola usługi ATA
Dostęp do konsoli usługi ATA odbywa się za pośrednictwem przeglądarki. Obsługiwane są następujące z nich:

-   Internet Explorer 10 i nowsze

-   Google Chrome 40 i nowsze

-   Minimalna rozdzielczość ekranu w poziomie: 1700 pikseli

## Zobacz też
- [Architektura usługi ATA](/advanced-threat-analytics/understand-explore/ata-architecture)
- [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-useinstall-ata)
- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->


