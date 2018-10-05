---
title: Wymagania wstępne usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje wymagania dotyczące pomyślnego wdrożenia usługi Azure ATP w danym środowisku
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 127d7ad5717837c8723c71de167e04f2fdd7ddde
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783903"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="azure-atp-prerequisites"></a>Wymagania wstępne dotyczące usługi Azure ATP
W tym artykule opisano wymagania dotyczące pomyślnego wdrożenia usługi Azure ATP w danym środowisku.

>[!NOTE]
> Aby uzyskać informacje o planowaniu zasobów i pojemności, zobacz [Planowanie pojemności usługi Azure ATP](atp-capacity-planning.md).


Narzędzie Azure ATP składa się z narzędzia Azure ATP usługę w chmurze, która składa się z portalu usługi Azure ATP, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i/lub czujnik autonomiczny narzędzia Azure ATP. Aby uzyskać więcej informacji na temat poszczególnych składników usługi Azure ATP zobacz [architektury usługi Azure ATP](atp-architecture.md).

Każde wystąpienie usługi Azure ATP obsługuje wiele granica lasu usługi Active Directory i lasu funkcjonalności poziomu (FFL) systemu Windows 2003 lub nowszym. 

Ten przewodnik wymagań wstępnych jest podzielona na sekcje, aby upewnić się, że masz wszystko, czego potrzebujesz do pomyślnego wdrożenia usługi Azure ATP. 


[Przed rozpoczęciem](#before-you-start): Wyświetla informacje, aby zebrać i konta i jednostki sieciowe, konieczne będzie istnieć przed rozpoczęciem instalacji.

[Witryna Azure portal zaawansowanej ochrony przed zagrożeniami](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): wymagania dotyczące przeglądarki portal opisano narzędzia Azure ATP.

[Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami](#azure-atp-lightweight-sensor-requirements): Wyświetla listę narzędzia Azure ATP czujnik, wymagania sprzętowe i programowe.

[Czujnik autonomiczny usługi Azure ATP](#azure-atp-sensor-requirements): sprzętu czujnik autonomiczny zawiera narzędzia Azure ATP, wymagania dotyczące oprogramowania, a także ustawieniach, należy skonfigurować na serwerach czujnik autonomiczny narzędzia Azure ATP.

## <a name="before-you-start"></a>Przed rozpoczęciem
W tej sekcji opisano informacje, które należy zebrać oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji usługi Azure ATP.

- Sprawdź, czy zamierzasz zainstalować narzędzia Azure ATP czujników na kontrolerach domeny mają łączność z Internetem do usługi Azure ATP w chmurze. Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure obsługuje użycia serwera proxy. Aby uzyskać więcej informacji na temat konfiguracji serwera proxy, zobacz [konfigurowania serwera proxy dla usługi Azure ATP](configure-proxy.md).  

-   **Lokalnych** AD konto i hasło użytkownika z dostępem do odczytu do wszystkich obiektów w monitorowanej domeny.

    > [!NOTE]
    > Jeśli ustawiono niestandardowe listy kontroli dostępu w różnych jednostkach organizacyjnych w domenie, upewnij się, że wybrany użytkownik ma uprawnienia do odczytu do tych jednostek organizacyjnych.

-   Po uruchomieniu programu Wireshark na czujnik autonomiczny narzędzia Azure ATP, konieczne będzie ponowne uruchomienie usługi czujnika zaawansowanej ochrony przed zagrożeniami dla platformy Azure, po zatrzymaniu przechwytywania programu Wireshark. W przeciwnym razie czujnika zatrzymuje przechwytywanie ruchu.

- Jeśli spróbujesz zainstalować czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure na maszynie skonfigurowane z kartą zespołu kart interfejsu Sieciowego, wystąpi błąd instalacji. Jeśli chcesz zainstalować czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure na komputerze, który został skonfigurowany z zespołu kart interfejsu Sieciowego, zobacz [czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure problem tworzenia zespołu kart interfejsu Sieciowego](troubleshooting-atp-known-issues.md#nic-teaming).

-    Zalecane: Użytkownik powinien mieć uprawnienia tylko do odczytu kontenera usuniętych obiektów. Dzięki temu usługi Azure ATP to wykrywanie zbiorczego usuwania obiektów w domenie. Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz **Zmienianie uprawnień do kontenera usuniętych obiektów** sekcji [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) artykułu.

-   Opcjonalnie: konto użytkownika, który nie ma żadnych działań w sieci. To konto jest skonfigurowane jako użytkownika wystawionego jako przynęta Azure ATP. Aby uzyskać więcej informacji, zobacz [Konfigurowanie wykluczeń i użytkownika wystawionego jako przynęta](install-atp-step7.md).

-   Opcjonalnie: Wdrażając czujnik autonomiczny, należy go przekazywać Windows zdarzeń 4776, 4732, 4733, 4728, 4729, 4756, 4757 i 7045 zure zaawansowanej ochrony przed zagrożeniami w celu dodatkowego zwiększenia Azure ATP Pass--Hash, ataków siłowych, modyfikacji wrażliwych grup, tokeny wystawione jako przynęta wykrywanie i tworzenie złośliwe usługi. Azure czujnika zaawansowanej ochrony przed zagrożeniami, które automatycznie otrzymuje tych zdarzeń. W przypadku narzędzia Azure ATP czujnik autonomiczny te zdarzenia mogą być odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają narzędzia Azure ATP z dodatkowymi informacjami, która nie jest dostępna za pośrednictwem ruchu sieciowego kontrolera domeny.

## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Wymagania platformy Azure ATP obszar roboczy zarządzania portalu i w obszarze roboczym portalu
Dostęp do portalu usługi Azure ATP obszaru roboczego i portalu zarządzania obszarami roboczymi usługi Azure ATP jest za pośrednictwem przeglądarki, obsługuje następujące przeglądarki i ustawienia:
-   Microsoft Edge
-   Internet Explorer 10 i nowsze
-   Google Chrome 4.0 i nowsze wersje
-   Minimalna rozdzielczość ekranu w poziomie: 1700 pikseli
-   Serwera proxy i zapory jest otwarty — do komunikowania się z usługą w chmurze usługi Azure ATP *. atp.azure.com portu 443, musi być otwarty w zapory/serwera proxy.

 ![Diagram architektury usługi Azure ATP](media/ATP-architecture-topology.png)


> [!NOTE]
> Domyślnie narzędzia Azure ATP obsługuje maksymalnie 100 czujników. Jeśli chcesz zainstalować więcej się z pomocą techniczną usługi Azure ATP.

## <a name="azure-atp-sensor-requirements"></a>Wymagania platformy Azure czujnika zaawansowanej ochrony przed zagrożeniami
W tej sekcji przedstawiono wymagania dotyczące czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.
### <a name="general"></a>Ogólne
Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure obsługuje instalację na kontrolerze domeny z systemem Windows Server 2008 R2 z dodatkiem SP1 (bez instalacji Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (w tym Core, ale nie Nano).

Kontroler domeny może być kontrolerem domeny tylko do odczytu (RODC).

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, należy otworzyć port 443 w zapór i serwerów proxy do *. atp.azure.com.

Podczas instalacji programu .net Framework 4.7 jest zainstalowany i może być konieczne jest ponowne uruchomienie kontrolera domeny, jeśli ponowne uruchomienie jest już w toku.


> [!NOTE]
> Wymagany jest co najmniej 5 GB miejsca na dysku, a zalecane to 10 GB. Obejmuje to miejsce wymagane dla usługi Azure ATP pliki binarne, dzienniki usługi Azure ATP i wydajności dzienniki.

### <a name="server-specifications"></a>Specyfikacje serwera

Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wymaga co najmniej dwa rdzenie i 6 GB pamięci RAM zainstalowanych na kontrolerze domeny.
Aby uzyskać optymalną wydajność, ustaw **opcji zasilania** czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure do **o wysokiej wydajności**.
Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure można wdrożyć na kontrolerach domeny o różnych obciążeniach i rozmiarach, w zależności od ilości ruchu sieciowego do i z kontrolerów domeny oraz ilości zasobów zainstalowanych na tym kontrolerze domeny.

>[!NOTE] 
> Podczas uruchamiania, jako maszynę wirtualną, pamięć dynamiczna lub innych funkcji ballooning pamięci nie jest obsługiwane.

Aby uzyskać więcej informacji na temat wymagań sprzętowych czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, zobacz [Planowanie pojemności usługi Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu

Serwery i kontrolery domeny, na których jest zainstalowany czujnik musi mieć różnica czasu ustawionego pięciu minut od siebie nawzajem.

### <a name="network-adapters"></a>Karty sieciowe

Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure monitoruje lokalny ruch na wszystkich kartach sieciowych kontrolera domeny. <br>
Po wdrożeniu można użyć portalu obszaru roboczego usługi Azure ATP, jeśli chcesz zmodyfikować, które karty sieciowe są monitorowane.

Czujnik nie jest obsługiwana w domenie, kontrolerów z systemem Windows 2008 R2 z Broadcom kart sieciowych jest włączona.

### <a name="ports"></a>Porty
Poniższej tabeli wymieniono niezbędne porty, których wymaga czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|**Porty Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Usługa w chmurze Azure ATP|Wychodzące|
|**Wewnętrznych portów**|||||
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|Netlogon (SAM-R protokół SMB, CIFS)|TCP/UDP|445|Wszystkie urządzenia w sieci|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Oba|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Oba|
|Syslog (opcjonalnie)|TCP/UDP|514, w zależności od konfiguracji|Serwer SIEM|Przychodzące|
|USŁUGI RADIUS|UDP|1813|USŁUGI RADIUS|Przychodzące|
|Protokół TLS w celu portu RDP|TCP|3389|Wszystkie urządzenia w sieci|Oba|

> [!NOTE]
> - Przy użyciu konta użytkownika usługi katalogu, czujnika zapytania punktów końcowych w organizacji dla administratorów lokalnych przy użyciu SAM-R (logowanie do sieci), aby można było tworzyć [wykres ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md). Aby uzyskać więcej informacji, zobacz [SAM-R skonfigurować wymagane uprawnienia](install-atp-step8-samr.md).
> - Następujące porty muszą być otwarte dla ruchu przychodzącego na urządzeniach w sieci z czujników autonomiczne narzędzia Azure ATP:
>   -   NTLM przez RPC (Port TCP 135) do celów rozpoznawania
>   -   NetBIOS (UDP port 137) do celów rozpoznawania
>   -   Protokół RDP (TCP port 3389), tylko pierwszy pakiet *powitania klienta*, do celów rozpoznawania<br> Należy zauważyć, że uwierzytelnianie nie jest wykonywane na wszystkich portach.

## <a name="azure-atp-standalone-sensor-requirements"></a>Wymagania dotyczące usługi Azure ATP autonomiczny czujnika
W tej sekcji przedstawiono wymagania dotyczące usługi Azure ATP czujnik autonomiczny.
### <a name="general"></a>Ogólne
Czujnik autonomiczny narzędzia Azure ATP obsługuje instalację na serwerze z systemem Windows Server 2012 R2 lub Windows Server 2016 (w tym server core).
Czujnik autonomiczny narzędzia Azure ATP można zainstalować na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
Czujnik autonomiczny narzędzia Azure ATP może służyć do monitorowania kontrolerów domeny z domeny funkcjonalności poziomu systemu Windows 2003 lub nowszym.

Dla Twojej czujnik autonomiczny do komunikowania się z usługą w chmurze, portu 443 w zapór i serwerów proxy do *. atp.azure.com musi być otwarty.


Aby uzyskać informacje o używaniu maszyn wirtualnych za pomocą narzędzia Azure ATP czujnik autonomiczny, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).

> [!NOTE]
> Wymagany jest co najmniej 5 GB miejsca na dysku, a zalecane to 10 GB. Obejmuje to miejsce wymagane dla usługi Azure ATP pliki binarne, dzienniki usługi Azure ATP i wydajności dzienniki.

### <a name="server-specifications"></a>Specyfikacje serwera
Aby uzyskać optymalną wydajność, ustaw **opcji zasilania** czujnika autonomicznego narzędzia Azure ATP do **o wysokiej wydajności**.<br>
Czujnik autonomiczny narzędzia Azure ATP może obsługiwać monitorowanie wielu kontrolerów domeny, w zależności od ilości ruchu sieciowego do i z kontrolerów domeny.

>[!NOTE] 
> Podczas uruchamiania, jako maszynę wirtualną, pamięć dynamiczna lub innych funkcji ballooning pamięci nie jest obsługiwane.

Aby uzyskać więcej informacji na temat wymagań sprzętowych czujnika autonomicznego narzędzia Azure ATP zobacz [Planowanie pojemności usługi Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu

Serwery i kontrolery domeny, na których jest zainstalowany czujnik musi mieć różnica czasu ustawionego pięciu minut od siebie nawzajem.


### <a name="network-adapters"></a>Karty sieciowe
Czujnik autonomiczny narzędzia Azure ATP wymaga co najmniej jednej karty administracyjnej i co najmniej jednej karty sieciowej przechwytywania:

-   **Karta sieciowa zarządzania** — używany do komunikacji w sieci firmowej. Czujnika będą używać tej karty, aby wysłać zapytanie do kontrolera domeny jest ochrona i rozpoznawania do konta komputera. <br>Tę kartę należy skonfigurować następujące ustawienia:

    -   Statyczny adres IP obejmujący bramę domyślną

    -   Preferowane i alternatywne serwery DNS

    -   W polu **Sufiks DNS dla tego połączenia** należy podać nazwę DNS każdej monitorowanej domeny.

        ![Konfigurowanie sufiksu DNS w zaawansowanych ustawieniach protokołu TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > W przypadku narzędzia Azure ATP czujnik autonomiczny jest elementem członkowskim domeny, mogą zostać skonfigurowane automatycznie.

-   **Karta przechwytywania** — używane do przechwytywania ruchu do i z kontrolerów domeny.

    > [!IMPORTANT]
    > -   Skonfiguruj funkcję dublowania portów dla karty przechwytywania jako miejsce docelowe ruchu sieciowego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md). Zazwyczaj potrzebne do pracy z zespołem sieci lub wirtualizacji, aby skonfigurować funkcję dublowania portów.
    > -   Konfigurowanie statycznego adresu IP bez obsługi routingu (przy użyciu /32 maska) dla danego środowiska bez bramy czujnik domyślnej i bez adresów serwerów DNS. Na przykład 10.10.0.10/32. Gwarantuje to, że karta sieciowa przechwytywania może przechwytywać maksymalną ilość ruchu i że administracyjna karta sieciowa jest używana do wysyłania i odbierania wymaganego ruchu sieciowego.

### <a name="ports"></a>Porty
Poniższej tabeli wymieniono niezbędne porty, których wymaga usługi Azure ATP czujnik autonomiczny skonfigurowaną na tej karcie zarządzania:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|**Porty Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Usługa w chmurze Azure ATP|Wychodzące|
|**Wewnętrznych portów**|||||
|LDAP|TCP i UDP|389|Kontrolery domeny|Wychodzące|
|Bezpieczny protokół LDAP (LDAPS)|TCP|636|Kontrolery domeny|Wychodzące|
|LDAP do wykazu globalnego|TCP|3268|Kontrolery domeny|Wychodzące|
|LDAPS do wykazu globalnego|TCP|3269|Kontrolery domeny|Wychodzące|
|Kerberos|TCP i UDP|88|Kontrolery domeny|Wychodzące|
|Netlogon (SAM-R protokół SMB, CIFS)|TCP i UDP|445|Wszystkie urządzenia w sieci|Wychodzące|
|Czas systemu Windows|UDP|123|Kontrolery domeny|Wychodzące|
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Oba|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Oba|
|Syslog (opcjonalnie)|TCP/UDP|514, w zależności od konfiguracji|Serwer SIEM|Przychodzące|
|USŁUGI RADIUS|UDP|1813|USŁUGI RADIUS|Przychodzące|
|Protokołu TLS dla protokołu RDP|TCP|3389|Wszystkie urządzenia w sieci|Oba|

> [!NOTE]
> - Przy użyciu konta użytkownika usługi katalogu, czujnika zapytania punktów końcowych w organizacji dla administratorów lokalnych przy użyciu SAM-R (logowanie do sieci), aby można było tworzyć [wykres ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md). Aby uzyskać więcej informacji, zobacz [SAM-R skonfigurować wymagane uprawnienia](install-atp-step8-samr.md).
> - Następujące porty muszą być otwarte dla ruchu przychodzącego na urządzeniach w sieci z czujników autonomiczne narzędzia Azure ATP:
>   -   NTLM przez RPC (Port TCP 135) do celów rozpoznawania
>   -   NetBIOS (UDP port 137) do celów rozpoznawania
>   -   Protokół RDP (TCP port 3389), tylko pierwszy pakiet *powitania klienta*, do celów rozpoznawania<br> Należy zauważyć, że uwierzytelnianie nie jest wykonywane na wszystkich portach.



## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-architecture.md)
- [Zainstaluj narzędzie Azure ATP](install-atp-step1.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)

