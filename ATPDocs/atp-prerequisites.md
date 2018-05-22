---
title: Wymagania wstępne platformy Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje wymagania dotyczące pomyślnego wdrożenia Azure ATP w danym środowisku
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1fc2b3656701ee5db54a4f918ab617a2ad487780
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="azure-atp-prerequisites"></a>Wymagania wstępne Azure ATP
W tym artykule opisano wymagania dotyczące pomyślnego wdrożenia Azure ATP w danym środowisku.

>[!NOTE]
> Aby uzyskać informacje o planowaniu zasobów i pojemności, zobacz [planowania pojemności Azure ATP](atp-capacity-planning.md).


Azure ATP składa się z usługi w chmurze Azure ATP, która składa się z obszaru roboczego portalu zarządzania i portalu obszaru roboczego, czujnik autonomiczny Azure ATP i/lub czujnik Azure ATP. Aby uzyskać więcej informacji o składnikach Azure ATP, zobacz [architektura Azure ATP](atp-architecture.md).

Każdy obszar roboczy Azure ATP obsługuje granica lasu usługi Active Directory oraz lasu funkcjonalności poziom (FFL) systemu Windows 2003 lub nowszym. W przypadku wdrożeń z wieloma lasami oddzielne roboczym Azure ATP jest wymagany dla każdego lasu.


[Przed rozpoczęciem](#before-you-start): Ta sekcja zawiera informacje, które należy zebrać i konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji Azure ATP.

[Portal zarządzania obszaru roboczego w usłudze Azure ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): w tej sekcji opisano wymagania dotyczące przeglądarki portalu zarządzania obszaru roboczego.

[Portal Azure obszaru roboczego ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): w tej sekcji opisano wymagania dotyczące przeglądarki do uruchomienia portalu Azure ATP obszaru roboczego.

[Azure czujnik autonomiczny ATP](#azure-atp-sensor-requirements): w tej sekcji przedstawiono Azure ATP autonomiczny czujnika sprzętu, wymagania dotyczące oprogramowania, a także ustawienia należy skonfigurować na serwerach czujnik autonomiczny Azure ATP.

[Azure czujnik ATP](#azure-atp-lightweight-sensor-requirements): Ta sekcja zawiera Azure ATP czujnika, wymagania sprzętowe i programowe.

![Diagram architektury usługi Azure ATP](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
W tej sekcji opisano informacje, które należy zebrać oraz konta i jednostki sieciowe, które powinny istnieć przed rozpoczęciem instalacji Azure ATP.


-   **Lokalnymi** AD konto i hasło użytkownika z dostępem do odczytu do wszystkich obiektów w monitorowanej domeny.

    > [!NOTE]
    > Jeśli ustawiono niestandardowe listy kontroli dostępu w różnych jednostkach organizacyjnych w domenie, upewnij się, że wybrany użytkownik ma uprawnienia do odczytu do tych jednostek organizacyjnych.

-   Po uruchomieniu programu Wireshark na czujnik autonomiczny Azure ATP konieczne będzie ponowne uruchomienie czujnik Azure Advanced Threat Protection Service, po zatrzymaniu przechwytywania programu Wireshark. W przeciwnym razie czujnika zatrzymuje przechwytywanie ruchu.

- Jeśli spróbujesz zainstalować czujnik ATP na komputerze, który został skonfigurowany z kartą zespołu kart interfejsu sieciowego, zostanie wyświetlony błąd instalacji. Jeśli chcesz zainstalować czujnik ATP na komputerze, który został skonfigurowany z zespołu kart interfejsu sieciowego, zobacz [czujnik Azure ATP problem tworzenia zespołu kart interfejsu Sieciowego](troubleshooting-atp-known-issues.md#nic-teaming).

-    Zalecane: Użytkownik powinien mieć uprawnienia tylko do odczytu kontenera usuniętych obiektów. Dzięki temu ATP Azure to wykrywanie zbiorczego usuwania obiektów w domenie. Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz **Zmienianie uprawnień do kontenera usuniętych obiektów** sekcji [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) artykułu.

-   Opcjonalnie: konto użytkownika, który nie ma żadnych działań w sieci. To konto jest skonfigurowana jako użytkownika wystawionego jako przynęta Azure ATP. Aby uzyskać więcej informacji, zobacz [Skonfiguruj wykluczenia i użytkownika wystawionego jako przynęta](install-atp-step7.md).

-   Opcjonalnie: Wdrażając czujnik autonomiczny, konieczne jest do przekazywania zdarzeń systemu Windows 4776, 4732 4733, 4728, 4729, 4756, 4757 i 7045 do ATP dodatkowo ulepszyć Azure ATP Pass--Hash, ataki Siłowe, modyfikację wrażliwych wykryć przynęty i tworzenia złośliwe usługi. W czujnik Azure ATP te zdarzenia są odbierane automatycznie. W czujnika autonomiczny Azure ATP zdarzenia te mogą być odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają Azure ATP z dodatkowymi informacjami, który nie jest dostępny za pośrednictwem ruchu sieciowego kontrolera domeny.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>ATP obszaru roboczego management portal i obszar roboczy portalu wymagania dotyczące usługi Azure
Dostęp do portalu Azure ATP obszaru roboczego i portalu zarządzania Azure ATP obszaru roboczego jest za pośrednictwem przeglądarki. obsługiwane są poniższe przeglądarki i ustawienia:
-   Microsoft Edge
-   Internet Explorer 10 i nowsze
-   Google Chrome 4.0 i nowsze
-   Minimalna rozdzielczość ekranu w poziomie: 1700 pikseli
-   Zaporą/serwera proxy Otwórz — do komunikowania się z usługą w chmurze Azure ATP, musi mieć Otwórz: *. atp.azure.com portu 443 w zaporą/serwera proxy. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Wymagania dotyczące usługi Azure ATP autonomiczny czujnik
Ta sekcja zawiera wymagania dotyczące czujnik autonomiczny Azure ATP.
### <a name="general"></a>Ogólne
Czujnik autonomiczny Azure ATP obsługuje instalację na serwerze z systemem Windows Server 2012 R2 lub Windows Server 2016 (Dołącz server core).
Czujnik autonomiczny Azure ATP można zainstalować na serwerze, który jest elementem członkowskim domeny lub grupy roboczej.
Czujnik autonomiczny Azure ATP może służyć do monitorowania kontrolerów domeny z domeny funkcjonalności poziomu z systemem Windows 2003 lub nowszym.

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, należy otworzyć port 443 w zapory i serwery proxy do *. atp.azure.com.


Aby uzyskać informacje o używaniu maszyn wirtualnych z czujnika autonomiczny Azure ATP, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).

> [!NOTE]
> Wymagane jest co najmniej 5 GB miejsca na dysku i 10 GB jest zalecane. Dotyczy to również miejsce wymagane do plików binarnych Azure ATP, Azure ATP dzienniki i wydajności dzienników.

### <a name="server-specifications"></a>Specyfikacje serwera
Aby uzyskać optymalną wydajność, ustaw **opcja zasilania** czujnika autonomiczny Azure ATP do **wysokiej wydajności**.<br>
Czujnik autonomiczny Azure ATP może obsługiwać monitorowanie wielu kontrolerów domeny, w zależności od ilości ruchu sieciowego do i z kontrolerów domeny.

>[!NOTE] 
> W przypadku uruchamiania jako maszynę wirtualną, pamięć dynamiczna lub innych funkcji przydziałem balonowym pamięci nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach sprzętowych czujnik autonomiczny Azure ATP, zobacz [planowania pojemności Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu

Serwery kontrolerów domeny, na których zainstalowano czujnika czasu i może być synchronizowane w ciągu pięciu minut od siebie.


### <a name="network-adapters"></a>Karty sieciowe
Czujnik autonomiczny Azure ATP wymaga co najmniej jednej karty administracyjnej i co najmniej jednej karty sieciowej przechwytywania:

-   **Karta sieciowa zarządzania** — używane do komunikacji w sieci firmowej. Czujnik użyje tej karty do badania kontroler domeny jest ochrona i rozpoznawania do konta komputera. <br>Ta karta powinna skonfigurowana z następującymi ustawieniami:

    -   Statyczny adres IP obejmujący bramę domyślną

    -   Preferowane i alternatywne serwery DNS

    -   W polu **Sufiks DNS dla tego połączenia** należy podać nazwę DNS każdej monitorowanej domeny.

        ![Konfigurowanie sufiksu DNS w zaawansowanych ustawieniach protokołu TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Jeśli czujnik autonomiczny Azure ATP jest elementem członkowskim domeny, może być skonfigurowany automatycznie.

-   **Karta przechwytywania** — używana do przechwytywania ruchu do i z kontrolerów domeny.

    > [!IMPORTANT]
    > -   Skonfiguruj funkcję dublowania portów dla karty przechwytywania jako miejsce docelowe ruchu sieciowego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md). Zazwyczaj należy współpracować z zespołem sieci lub wirtualizacji w celu skonfigurowania funkcji dublowania portów.
    > -   Skonfiguruj statyczny adres IP bez obsługi routingu dla danego środowiska, które z czujnika nie domyślne i bez adresów serwerów DNS. Na przykład 1.1.1.1/32. Dzięki temu, że karta sieciowa przechwytywania może przechwytywać maksymalną ilość ruchu sieciowego i że administracyjnej karty sieciowej jest używany do wysyłania i odbierania wymaganego ruchu sieciowego.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty, których wymaga czujnik autonomiczny Azure ATP skonfigurowany na karcie zarządzania:

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
|Netlogon (SMB, CIFS, SAM-R)|TCP i UDP|445|Wszystkie urządzenia w sieci|Wychodzące|
|Czas systemu Windows|UDP|123|Kontrolery domeny|Wychodzące|
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Wychodzące|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Wychodzące|
|Syslog (opcjonalnie)|TCP/UDP|514, w zależności od konfiguracji|Serwer SIEM|Przychodzące|
|RADIUS|UDDP|1813|RADIUS|Przychodzące|
|RDP|TCP|3389|Wszystkie urządzenia w sieci|Wychodzące|

> [!NOTE]
> - Przy użyciu konta użytkownika usługi katalogu, wysyła zapytanie czujnika punktów końcowych w organizacji dla administratorów lokalnych przy użyciu SAM-R (logowania do sieci), aby można było skompilować [wykres ścieżki penetracja sieci](use-case-lateral-movement-path.md). Aby uzyskać więcej informacji, zobacz [SAM-R skonfigurować wymagane uprawnienia](install-atp-step8-samr.md).
> - Następujące porty muszą być otwarte dla ruchu przychodzącego na urządzeniach w sieci z czujników autonomiczny Azure ATP:
>   -   NTLM za pośrednictwem wywołania RPC (Port TCP 135) do celów rozpoznawania
>   -   NetBIOS (UDP port 137) dla celów rozpoznawania
>   -   RDP (TCP port 3389), tylko pierwszy pakiet *powitania klienta*, do celów rozpoznawania<br> Należy pamiętać, że uwierzytelnianie nie jest wykonywane na żadnym z portów.

## <a name="azure-atp-sensor-requirements"></a>Azure wymagania czujnik ATP
W tej sekcji wymieniono wymagania dotyczące czujnik Azure ATP.
### <a name="general"></a>Ogólne
Czujnik Azure ATP obsługuje instalację na kontrolerze domeny z systemem Windows Server 2008 R2 SP1 (nie w tym Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (w tym Core, ale nie Nano).

Kontroler domeny może być kontrolerem domeny tylko do odczytu (RODC).

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, należy otworzyć port 443 w zapory i serwery proxy do *. atp.azure.com.

Podczas instalacji programu .net Framework 4.7 jest zainstalowany i może wymagać ponowny rozruch kontrolera domeny, jeśli już oczekuje na ponowne uruchomienie.


> [!NOTE]
> Wymagane jest co najmniej 5 GB miejsca na dysku i 10 GB jest zalecane. Dotyczy to również miejsce wymagane do plików binarnych Azure ATP, Azure ATP dzienniki i wydajności dzienników.

### <a name="server-specifications"></a>Specyfikacje serwera

Czujnik Azure ATP wymaga co najmniej dwa rdzenie i 6 GB pamięci RAM zainstalowanych na kontrolerze domeny.
Aby uzyskać optymalną wydajność, ustaw **opcja zasilania** czujnika Azure ATP do **wysokiej wydajności**.
Czujnik Azure ATP można wdrożyć na kontrolerach domeny o różnych obciążeniach i rozmiarach, w zależności od ilości ruchu sieciowego do i z kontrolerów domeny oraz ilości zasobów zainstalowanych na tym kontrolerze domeny.

>[!NOTE] 
> W przypadku uruchamiania jako maszynę wirtualną, pamięć dynamiczna lub innych funkcji przydziałem balonowym pamięci nie jest obsługiwana.

Aby uzyskać więcej informacji o wymaganiach sprzętowych czujnik Azure ATP, zobacz [planowania pojemności Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronizacja czasu

Serwery kontrolerów domeny, na których zainstalowano czujnika czasu i może być synchronizowane w ciągu pięciu minut od siebie.

### <a name="network-adapters"></a>Karty sieciowe

Czujnik Azure ATP monitoruje lokalny ruch na wszystkie karty sieciowe z kontrolerem domeny. <br>
Po wdrożeniu można użyć portalu Azure ATP obszaru roboczego, jeśli chcesz zmodyfikować, które karty sieciowe są monitorowane.

Czujnik nie jest obsługiwana w domenie kontrolery z systemem Windows 2008 R2 z tworzeniem zespołu kart sieciowych Broadcom włączona.

### <a name="ports"></a>Porty
W poniższej tabeli wymieniono niezbędne porty, których wymaga czujnik Azure ATP:

|Protokół|Transport|Port|Do/z|Kierunek|
|------------|-------------|--------|-----------|-------------|
|**Porty Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Usługa w chmurze Azure ATP|Wychodzące|
|**Wewnętrznych portów**|||||
|systemem DNS,|TCP i UDP|53|Serwery DNS|Wychodzące|
|NTLM za pośrednictwem wywołania RPC|TCP|135|Wszystkie urządzenia w sieci|Wychodzące|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Wszystkie urządzenia w sieci|Wychodzące|
|NetBIOS|UDP|137|Wszystkie urządzenia w sieci|Wychodzące|
|Syslog (opcjonalnie)|TCP/UDP|514, w zależności od konfiguracji|Serwer SIEM|Przychodzące|
|RADIUS|UDDP|1813|RADIUS|Przychodzące|
|Protokół TLS w celu portem RDP|TCP|3389|Wszystkie urządzenia w sieci|Wychodzące|

> [!NOTE]
> - Przy użyciu konta użytkownika usługi katalogu, wysyła zapytanie czujnika punktów końcowych w organizacji dla administratorów lokalnych przy użyciu SAM-R (logowania do sieci), aby można było skompilować [wykres ścieżki penetracja sieci](use-case-lateral-movement-path.md). Aby uzyskać więcej informacji, zobacz [SAM-R skonfigurować wymagane uprawnienia](install-atp-step8-samr.md).
> - Następujące porty muszą być otwarte dla ruchu przychodzącego na urządzeniach w sieci z czujników autonomiczny Azure ATP:
>   -   NTLM za pośrednictwem wywołania RPC (Port TCP 135) do celów rozpoznawania
>   -   NetBIOS (UDP port 137) dla celów rozpoznawania
>   -   RDP (TCP port 3389), tylko pierwszy pakiet *powitania klienta*, do celów rozpoznawania<br> Należy pamiętać, że uwierzytelnianie nie jest wykonywane na żadnym z portów.




## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-architecture.md)
- [Zainstaluj ATP](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)

