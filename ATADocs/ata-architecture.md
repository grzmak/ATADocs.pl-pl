---
title: Architektura usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Opis architektury usługi Microsoft Advanced Threat Analytics (ATA).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b620e5b6203d387de389cfb857c2dd6125239ed9
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010061"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*




# <a name="ata-architecture"></a>Architektura usługi ATA
Architektura usługi Advanced Threat Analytics została szczegółowo opisana na poniższym diagramie:

![Diagram topologii architektury usługi ATA](media/ATA-architecture-topology.jpg)

Usługa ATA monitoruje ruch sieciowy kontrolera domeny przy użyciu funkcji dublowania portów do bramy usługi ATA za pomocą przełączników fizycznych lub wirtualnych. W przypadku wdrożenia uproszczonej bramy usługi ATA bezpośrednio na kontrolerach domeny stosowanie dublowania portów nie jest konieczne. Ponadto usługa ATA może wykorzystywać zdarzenia systemu Windows (przekazywane bezpośrednio z kontrolerów domeny lub serwera SIEM) i analizować dane pod kątem ataków i zagrożeń.
W tej sekcji opisano przepływ sieci i przechwytywanie zdarzeń oraz podano bardziej szczegółowe informacje dotyczące funkcjonalności głównych składników usługi ATA: bramy usługi ATA, uproszczonej bramy usługi ATA (której główna funkcjonalność jest taka sama jak bramy usługi ATA) oraz centrum usługi ATA.


![Diagram przepływu ruchu usługi ATA](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>Składniki usługi ATA
Usługa ATA składa się z następujących składników:

-   **Centrum usługi ATA** <br>
Centrum usługi ATA odbiera dane z dowolnych wdrożonych bram usługi ATA i/lub uproszczonych bram usługi ATA.
-   **Brama usługi ATA**<br>
Brama usługi ATA jest instalowana na dedykowanym serwerze, który monitoruje ruch kontrolerów domeny za pomocą funkcji dublowania portów lub podsłuchu sieci.
-   **Uproszczona brama usługi ATA**<br>
Uproszczona brama usługi ATA jest instalowana bezpośrednio w kontrolerach domeny. Brama monitoruje ruch kontrolerów bezpośrednio, bez konieczności użycia serwera dedykowanego lub funkcji dublowania portów. Jest to alternatywa dla bramy usługi ATA.

Wdrożenie usługi ATA może składać się z jednego centrum usługi ATA połączonego ze wszystkimi bramami usługi ATA, wszystkimi uproszczonymi bramami usługi ATA lub kombinacją bram usługi ATA i uproszczonych bram usługi ATA.


## <a name="deployment-options"></a>Opcje wdrażania
Usługę ATA można wdrożyć przy użyciu następujących kombinacji bram:

-   **Zastosowanie wyłącznie bram usługi ATA** <br>
Wdrożenie usługi ATA może składać się wyłącznie z bram usługi ATA (bez uproszczonych bram usługi ATA). Wszystkie kontrolery domeny muszą być skonfigurowane tak, aby umożliwić dublowanie portów do bramy usługi ATA, lub należy zastosować urządzenia do podsłuchu sieci.
-   **Zastosowanie wyłącznie uproszczonych bram usługi ATA**<br>
Wdrożenie usługi ATA może składać się tylko z uproszczonych bram usługi ATA. Uproszczone bramy usługi ATA wdraża się na każdym kontrolerze domeny. Nie ma potrzeby stosowania dodatkowych serwerów ani konfigurowania dublowania portów.
-   **Zastosowanie bram usługi ATA oraz uproszczonych bram usługi ATA**<br>
Wdrożenie usługi ATA obejmuje zarówno bramy usługi ATA, jak i uproszczone bramy usługi ATA. Uproszczone bramy usługi ATA są instalowane na niektórych kontrolerach domeny (na przykład na wszystkich kontrolerach domeny w oddziałach). W tym samym czasie inne kontrolery domeny są monitorowane przez bramy usługi ATA (np. większe kontrolery domeny w głównych centrach danych).

We wszystkich tych scenariuszach wszystkie bramy wysyłają dane do centrum usługi ATA.




## <a name="ata-center"></a>Centrum usługi ATA
**Centrum usługi ATA** pełni następujące funkcje:

-   Zarządza ustawieniami konfiguracji bram usługi ATA i uproszczonych bram usługi ATA

-   Odbiera dane z bram usługi ATA i uproszczonych bram usługi ATA 

-   Wykrywa podejrzane działania

-   Uruchamia algorytmy behawioralne usługi ATA związane z funkcją uczenia maszynowego w celu wykrywania nietypowych zachowań

-   Uruchamia rozmaite algorytmy deterministyczne w celu wykrywania zaawansowanych ataków opartych na łańcuchu kończenia ataków

-   Uruchamia konsolę usługi ATA

-   Opcjonalnie: centrum usługi ATA można skonfigurować do wysyłania wiadomości e-mail i zdarzeń po wykryciu podejrzanego działania

Centrum usługi ATA odbiera przeanalizowany ruch z bramy usługi ATA i uproszczonej bramy usługi ATA. Następnie wykonuje profilowanie, uruchamia wykrywanie deterministyczne oraz uruchamia uczenie maszynowe i algorytmy behawioralne, aby uzyskać więcej informacji dotyczących sieci, włącza wykrywanie anomalii i ostrzega o podejrzanych działaniach.

|||
|-|-|
|Odbiornik jednostek|Odbiera partie jednostek ze wszystkich bram usługi ATA i uproszczonych bram usługi ATA.|
|Procesor aktywności sieciowej|Przetwarza wszystkie działania w sieci w ramach każdej otrzymanej partii. Dotyczy to na przykład dopasowywania między różnymi krokami protokołu Kerberos wykonywanymi z potencjalnie różnych komputerów|
|Profiler jednostek|Profiluje wszystkie unikatowe jednostki na podstawie ruchu i zdarzeń. Na przykład usługa ATA aktualizuje listę zalogowanych komputerów dla każdego profilu użytkownika.|
|Baza danych centrum|Zarządza procesem zapisu działań w sieci i zdarzeń do bazy danych. |
|Baza danych|Usługa ATA korzysta z bazy danych MongoDB do przechowywania wszystkich danych w systemie:<br /><br />— działania w sieci<br />— działania związane ze zdarzeniami<br />— unikatowe jednostki<br />— podejrzane działania<br />— konfiguracja usługi ATA|
|Detektory|Detektory używają algorytmów uczenia maszynowego i reguł deterministycznych do znajdowania podejrzanych działań i nietypowego zachowania użytkowników w sieci.|
|Konsola usługi ATA|Konsola usługi ATA służy do konfigurowania usługi ATA i monitorowania podejrzanych działań wykrytych przez usługę ATA w sieci użytkownika. Konsola usługi ATA jest niezależna od centrum usługi ATA i będzie działać nawet wtedy, gdy centrum usługi ATA zostanie zatrzymane, pod warunkiem, że będzie mogła komunikować się z bazą danych.|
Podczas podejmowania decyzji o liczbie centrów usługi ATA, które mają zostać wdrożone w sieci, należy wziąć pod uwagę następujące kryteria:

-   Jedno centrum usługi ATA może monitorować pojedynczy las usługi Active Directory. Jeśli masz wiele lasów usługi Active Directory, na każdy las usługi Active Directory potrzebujesz co najmniej jednego centrum usługi ATA.

-    W dużych wdrożeniach usługi Active Directory pojedyncze Centrum usługi ATA może nie być w stanie obsłużyć całego ruchu wszystkich kontrolerów domeny. W takim przypadku należy użyć wielu centrów usługi ATA. Liczba centrów usługi ATA powinna zostać ustalona zgodnie z informacjami znajdującymi się w sekcji [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>Brama usługi ATA i uproszczona brama usługi ATA

### <a name="gateway-core-functionality"></a>Podstawowe funkcje bramy
**Brama usługi ATA** oraz **uproszczona brama usługi ATA** mają te same funkcje podstawowe:

-   Przechwytują i analizują ruch sieciowy kontrolera domeny. Jest to ruch pochodzący ze zdublowanych portów w przypadku bram usługi ATA i ruch lokalny kontrolera domeny w przypadku uproszczonych bram usługi ATA. 

-   Odbierają zdarzenia systemu Windows z serwera SIEM, serwera Syslog lub kontrolerów domeny przy użyciu funkcji przekazywania zdarzeń systemu Windows

-   Pobierają dane o użytkownikach i komputerach z domeny usługi Active Directory

-   Przeprowadzają rozpoznawanie jednostek sieci (użytkowników, grup i komputerów)

-   Transferują odpowiednie dane do centrum usługi ATA

-   Monitorują wiele kontrolerów domeny w jednej bramie usługi ATA lub monitorują pojedynczy kontroler domeny w przypadku uproszczonej bramy usługi ATA.

Brama usługi ATA odbiera ruch sieciowy i zdarzenia systemu Windows z sieci użytkownika i przetwarza je za pomocą następujących głównych składników:

|||
|-|-|
|Odbiornik sieci|Odbiornik sieci przechwytuje ruch sieciowy i analizuje go. Jest to zadanie silnie obciążające procesor CPU, więc zapoznanie się z sekcją [Wymagania wstępne usługi ATA](ata-prerequisites.md) jest szczególnie ważne podczas planowania bramy usługi ATA lub uproszczonej bramy usługi ATA.|
|Odbiornik zdarzeń|Odbiornik zdarzeń przechwytuje i analizuje zdarzenia systemu Windows przekazywane z serwera SIEM w sieci.|
|Czytnik dziennika zdarzeń systemu Windows|Czytnik dziennika zdarzeń systemu Windows odczytuje i analizuje zdarzenia systemu Windows przekazane do dziennika zdarzeń systemu Windows bramy usługi ATA z kontrolerów domeny.|
|Translator aktywności sieciowej | Służy do przeprowadzania translacji przeanalizowanego ruchu na logiczną reprezentację ruchu używaną przez usługę ATA (NetworkActivity).
|Mechanizm rozpoznawania jednostek|Mechanizm rozpoznawania jednostek pobiera przeanalizowane dane (ruch sieciowy i zdarzenia), a następnie przetwarza je za pomocą usługi Active Directory w celu znalezienia informacji o kontach i tożsamościach. Informacje te są następnie dopasowywane do adresów IP znalezionych w przeanalizowanych danych. Mechanizm rozpoznawania jednostek w sposób wydajny sprawdza nagłówki pakietów, aby umożliwić analizę pakietów uwierzytelniania pod kątem nazw maszyn, właściwości i tożsamości. Mechanizm rozpoznawania jednostek łączy przeanalizowane pakiety uwierzytelniania z danymi znajdującymi się w rzeczywistym pakiecie.|
|Nadawca jednostek|Nadawca jednostek wysyła przeanalizowane i dopasowane dane do centrum usługi ATA.|

## <a name="ata-lightweight-gateway-features"></a>Funkcje uproszczonej bramy usługi ATA

Następujące funkcje działają inaczej w zależności od tego, czy jest uruchomiona brama usługi ATA, czy uproszczona brama usługi ATA.

-   Uproszczona brama usługi ATA może odczytywać zdarzenia lokalnie — bez potrzeby konfigurowania przekazywania zdarzeń.

-   **Kandydat synchronizatora domeny**<br>
Brama synchronizatora domeny jest odpowiedzialna za aktywne synchronizowanie wszystkich jednostek z konkretnej domeny usługi Active Directory (podobnie do mechanizmu używanego przez kontrolery domeny w przypadku replikacji). Z listy kandydatów wybierana jest losowo jedna brama, która będzie służyć jako synchronizator domeny. <br><br>
Jeśli synchronizator będzie w trybie offline przez ponad 30 minut, zamiast niego zostanie wybrany inny kandydat. Nie jest dostępny dla określonej domeny Synchronizatora domeny, usługa ATA jest mogła aktywnie synchronizować jednostek i ich zmian, jednak usługa ATA będzie reagować i odbierać nowe jednostki po ich wykryciu w monitorowanym ruchu. 
<br>Jeśli nie ma dostępnego Synchronizatora domeny, a następnie wyszukaj jednostki, która nie ma żadnych ruch związany z jej, nie wyszukiwania są wyświetlane wyniki.<br><br>
Domyślnie wszystkie bramy usługi ATA są kandydatami synchronizatora.<br><br>
Ponieważ wszystkie uproszczone bramy usługi ATA są najprawdopodobniej wdrażane w oddziałach i małych kontrolerach domeny, nie są domyślnymi kandydatami synchronizatora.


-   **Ograniczenia zasobów**<br>
Brama ATA Lightweight Gateway zawiera składnik monitorowania, które ocenia dostępne moc obliczeniową i pamięć na kontrolerze domeny, na którym jest uruchomiony. Proces monitorowania jest wykonywany co 10 sekund i dynamicznie aktualizuje przydział użycia procesora CPU i pamięci w procesie uproszczonej bramy usługi ATA, aby upewnić się, że w każdym momencie kontroler domeny ma co najmniej 15% wolnej mocy obliczeniowej i zasobów pamięci.<br><br>
Niezależnie od tego, co się dzieje w kontrolerze domeny, proces ten zawsze zwalnia zasoby, aby upewnić się, że podstawowa funkcjonalność kontrolera domeny nie zostanie zaburzona.<br><br>
Powoduje to bramy ATA Lightweight Gateway brakować zasobów, tylko część ruchu będzie monitorowana, a alert monitorowania "Opuszczono ruch sieciowy dublowaniu portów" pojawia się na stronie kondycji.

W poniższej tabeli zawarto przykład kontrolera domeny z wystarczającą ilością zasobów obliczeniowych, która umożliwia zastosowanie większego limitu przydziału niż obecnie wymagany, dzięki czemu cały ruch jest monitorowany:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Uproszczona brama usługi ATA (Microsoft.Tri.Gateway.exe)|Różne (inne procesy) |Przydział uproszczonej bramy usługi ATA|Brama pomija|
|30%|20%|10%|45%|Nie|

Jeśli usługa Active Directory potrzebuje więcej mocy obliczeniowej, przydział wymagany przez uproszczoną bramę usługi ATA zostanie zmniejszony. W poniższym przykładzie uproszczona brama usługi ATA potrzebuje więcej zasobów niż zostało jej przydzielone i pomija część ruchu (monitoruje tylko część ruchu):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Uproszczona brama usługi ATA (Microsoft.Tri.Gateway.exe)|Różne (inne procesy) |Przydział uproszczonej bramy usługi ATA|Brama pomija|
|60%|15%|10%|15%|Tak|


## <a name="your-network-components"></a>Składniki Twojej sieci
Aby pracować z usługą ATA, upewnij się sprawdzić, czy następujące składniki są skonfigurowane.

### <a name="port-mirroring"></a>Dublowanie portów
Jeśli używasz bram usługi ATA, należy skonfigurować dublowanie portów dla kontrolerów domeny, które są monitorowane oraz ustawić bramę usługi ATA jako miejsce docelowe za pomocą przełączników fizycznych lub wirtualnych. Innym rozwiązaniem jest użycie funkcji podsłuchu sieci. Usługa ATA działa, jeśli niektóre, ale nie wszystkie kontrolery domeny są monitorowane, ale wykryć są mniej skuteczne.

Choć funkcja dublowania portów dubluje całość ruchu sieciowego kontrolera domeny do bramy usługi ATA, tylko niewielką część tego ruchu jest następnie wysyłana, kompresji do Centrum usługi ATA do analizy.

Kontrolery domeny i bramy usługi ATA mogą być fizyczne lub wirtualne. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).


### <a name="events"></a>Zdarzenia
Aby poprawić wykrywanie przez usługę ATA ataków typu Pass-the-Hash, ataków siłowych, modyfikacji wrażliwych grup i ataków na przynęty, usługa ATA potrzebuje następujących zdarzeń systemu Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Uproszczona brama usługi ATA może odczytywać je automatycznie. W przypadku gdy nie jest ona wdrożona, zdarzenia mogą być przekazywane do bramy usługi ATA na jeden z dwóch sposobów: przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń rozwiązania SIEM lub przez [skonfigurowanie przekazywania zdarzeń systemu Windows](#configuring-windows-event-forwarding).

-   Konfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM <br>Skonfiguruj system SIEM do przekazywania określonych zdarzeń systemu Windows do usługi ATA. Usługa ATA obsługuje wielu dostawców systemów SIEM. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zbierania zdarzeń](configure-event-collection.md).

-   Konfigurowanie funkcji przekazywania zdarzeń systemu Windows<br>Innym sposobem na odbieranie zdarzeń usługi ATA jest skonfigurowanie kontrolerów domeny do przekazywania zdarzeń systemu Windows 4776, 4732, 4733, 4728, 4729, 4756 i 4757 do bramy usługi ATA. Jest to szczególnie przydatne wtedy, gdy nie jest używany system SIEM lub system SIEM nie jest aktualnie obsługiwany przez usługę ATA. Aby uzyskać więcej informacji na temat funkcji przekazywania zdarzeń systemu Windows w usłudze ATA, zobacz [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding). Dotyczy to tylko fizycznych bram usługi ATA — nie do bramy ATA Lightweight Gateway.

## <a name="related-videos"></a>Powiązane pliki wideo
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

