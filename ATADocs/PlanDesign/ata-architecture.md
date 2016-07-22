---
title: "Architektura usługi ATA | Microsoft Advanced Threat Analytics"
description: "Opis architektury usługi Microsoft Advanced Threat Analytics (ATA)."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 2d753060f30cbcc7d16959355b86d64fdaa2ecd8


---

# Architektura usługi ATA
Architektura usługi Advanced Threat Analytics została szczegółowo opisana na poniższym diagramie:

![Diagram topologii architektury usługi ATA](media/ATA-architecture-topology.jpg)

Usługa ATA monitoruje ruch sieciowy kontrolera domeny przy użyciu funkcji dublowania portów wobec bramy usługi ATA z wykorzystaniem przełączników fizycznych lub wirtualnych lub poprzez wdrożenie bramy ATA Lightweight Gateway bezpośrednio w kontrolerach domeny, co usuwa potrzebę zastosowania funkcji dublowania portów. Ponadto usługa ATA może wykorzystywać zdarzenia systemu Windows (przekazywane bezpośrednio z kontrolerów domeny lub serwera SIEM) i analizować dane pod kątem ataków i zagrożeń.
W tej części opisano przepływ sieci i przechwytywanie zdarzeń oraz zawarto bardziej szczegółowe informacje dotyczące funkcjonalności głównych komponentów usługi ATA: bramy usługi ATA, bramy ATA Lightweight Gateway (której główna funkcjonalność jest taka sama jak bramy usługi ATA) oraz centrum usługi ATA.


![Diagram przepływu ruchu usługi ATA](media/ATA-traffic-flow.jpg)

## Składniki usługi ATA
Usługa ATA zawiera następujące składniki:

-   **Centrum usługi ATA** <br>
Centrum usługi ATA odbiera dane z dowolnych wdrożonych bram usługi ATA i/lub bram ATA Lightweight Gateway.
-   **Brama usługi ATA**<br>
Brama usługi ATA jest instalowana na dedykowanym serwerze, który monitoruje ruch kontrolerów domeny za pomocą funkcji dublowania portów lub podsłuchu sieci.
-   **Brama ATA Lightweight Gateway**<br>
Brama ATA Lightweight Gateway jest instalowana bezpośrednio w kontrolerach domeny. Brama monitoruje ruch kontrolerów bezpośrednio, bez konieczności użycia serwera dedykowanego lub funkcji dublowania portów. Jest to alternatywa dla bramy usługi ATA.

Wdrożenie usługi ATA może zawierać jedno centrum usługi ATA połączone z wszystkimi bramami usługi ATA, wszystkimi bramami ATA Lightweight Gateway lub kombinacją bram usługi ATA i bram ATA Lightweight Gateway.


## Opcje wdrażania
Usługę ATA można wdrożyć przy użyciu następujących kombinacji bram:

-   **Zastosowanie wyłącznie bram usługi ATA** <br>
Jeśli wdrożenie usługi ATA zawiera wyłącznie bramy usługi ATA (bez bram ATA Lightweight Gateway), wszystkie kontrolery domeny muszą być skonfigurowane tak, aby umożliwiać dublowanie portów do bramy usługi ATA lub należy włączyć funkcję podsłuchu sieci.
-   **Zastosowanie wyłącznie bram ATA Lightweight Gateway**<br>
Jeśli wdrożenie usługi ATA zawiera tylko bramy ATA Lightweight Gateway, bramy ATA Lightweight Gateway zostają wdrożone w każdym kontrolerze domeny. Nie ma potrzeby zastosowania dodatkowych serwerów ani konfiguracji dublowania portów.
-   **Zastosowanie bram usługi ATA oraz bram ATA Lightweight Gateway**<br>
Jeśli wdrożenie usługi ATA zawiera zarówno bramy usługi ATA, jak i bramy ATA Lightweight Gateway, brama ATA Lightweight Gateway jest instalowana w niektórych kontrolerach domeny (np. wszystkich kontrolerach domeny w oddziałach), a inne kontrolery domeny są monitorowane przez bramy usługi ATA (np. większe kontrolery domeny w głównych centrach danych).

We wszystkich trzech scenariuszach wszystkie bramy wysyłają dane do centrum usługi ATA.




## Centrum usługi ATA
**Centrum usługi ATA** pełni następujące funkcje:

-   Zarządza ustawieniami konfiguracji bram usługi ATA i bram ATA Lightweight Gateway

-   Odbiera dane z bram usługi ATA i bram ATA Lightweight Gateway 

-   Wykrywa podejrzane działania

-   Uruchamia algorytmy behawioralne usługi ATA związane z funkcją uczenia maszynowego w celu wykrywania nietypowych zachowań

-   Uruchamia rozmaite algorytmy deterministyczne w celu wykrywania zaawansowanych ataków opartych na łańcuchu kończenia ataków

-   Uruchamia konsolę usługi ATA

-   Opcjonalnie: centrum usługi ATA można skonfigurować do wysyłania wiadomości e-mail i zdarzeń po wykryciu podejrzanego działania

Centrum usługi ATA odbiera przeanalizowany ruch z bramy usługi ATA i bramy ATA Lightweight Gateway, wykonuje profilowanie, uruchamia wykrywanie deterministyczne oraz uruchamia uczenie maszynowe i algorytmy behawioralne, aby uzyskać więcej informacji dotyczących sieci użytkownika. Umożliwia to wykrywanie anomalii i ostrzeganie o podejrzanych działaniach.

|||
|-|-|
|Odbiornik jednostek|Odbiera partie jednostek ze wszystkich bram usługi ATA i bram ATA Lightweight Gateway.|
|Procesor aktywności sieciowej|Przetwarza wszystkie działania w sieci w ramach każdej otrzymanej partii. Dotyczy to na przykład dopasowywania między różnymi krokami protokołu Kerberos wykonywanymi z potencjalnie różnych komputerów|
|Profiler jednostek|Profiluje wszystkie unikatowe jednostki na podstawie ruchu i zdarzeń. Na przykład w ten sposób usługa ATA aktualizuje listę zalogowanych komputerów dla każdego profilu użytkownika.|
|Baza danych centrum|Zarządza procesem zapisu działań w sieci i zdarzeń do bazy danych. |
|Baza danych|Usługa ATA korzysta z bazy danych MongoDB do przechowywania wszystkich danych w systemie:<br /><br />— działania w sieci<br />— działania związane ze zdarzeniami<br />— unikatowe jednostki<br />— podejrzane działania<br />— konfiguracja usługi ATA|
|Detektory|Detektory używają algorytmów uczenia maszynowego i reguł deterministycznych do znajdowania podejrzanych działań i nietypowego zachowania użytkowników w sieci.|
|Konsola usługi ATA|Konsola usługi ATA służy do konfigurowania usługi ATA i monitorowania podejrzanych działań wykrytych przez usługę ATA w sieci użytkownika. Konsola usługi ATA jest niezależna od centrum usługi ATA i będzie działać nawet wtedy, gdy centrum usługi ATA zostanie zatrzymane, pod warunkiem, że będzie mogła komunikować się z bazą danych.|
Podczas podejmowania decyzji o liczbie centrów usługi ATA, które mają zostać wdrożone w ramach sieci, należy wziąć pod uwagę następujące informacje:

-   Jedno centrum usługi ATA może monitorować pojedynczy las usługi Active Directory. Jeśli masz więcej niż jeden las usługi Active Directory, na każdy las usługi Active Directory będzie musiało przypadać co najmniej jedno centrum usługi ATA.

-    W bardzo dużych wdrożeniach usługi Active Directory pojedyncze centrum usługi ATA może nie być w stanie obsłużyć całego ruchu wszystkich kontrolerów domeny. W takim przypadku wymaga się użycia wielu centrów usługi ATA. Liczba centrów usługi ATA powinna zostać ustalona zgodnie z informacjami znajdującymi się w sekcji [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

## Brama usługi ATA i brama ATA Lightweight Gateway

### Podstawowe funkcje bramy
**Brama usługi ATA** oraz **brama ATA Lightweight Gateway** mają te same funkcje podstawowe:

-   Przechwytują i sprawdzają ruch sieciowy kontrolera domeny (ruch po dublowaniu portów w przypadku bramy usługi ATA lub ruch lokalny kontrolera domeny w przypadku bramy ATA Lightweight Gateway) 

-   Odbierają zdarzenia systemu Windows z serwera SIEM, serwera Syslog lub kontrolerów domeny przy użyciu funkcji przekazywania zdarzeń systemu Windows

-   Pobierają dane o użytkownikach i komputerach z domeny usługi Active Directory

-   Przeprowadzają rozpoznawanie jednostek sieci (użytkowników, grup i komputerów)

-   Transferują odpowiednie dane do centrum usługi ATA

-   Monitorują wiele kontrolerów domeny w jednej bramie usługi ATA lub monitorują pojedynczy kontroler domeny w przypadku bramy ATA Lightweight Gateway.

Brama usługi ATA odbiera ruch sieciowy i zdarzenia systemu Windows z sieci użytkownika i przetwarza je za pomocą następujących głównych składników:

|||
|-|-|
|Odbiornik sieci|Odbiornik sieci jest odpowiedzialny za przechwytywanie ruchu sieciowego i jego analizowanie. Jest to zadanie silnie obciążające procesor CPU, więc zapoznanie się z sekcją [Wymagania wstępne usługi ATA](ata-prerequisites.md) jest szczególnie ważne podczas planowania bramy usługi ATA lub bramy ATA Lightweight Gateway.|
|Odbiornik zdarzeń|Odbiornik zdarzeń jest odpowiedzialny za przechwytywanie i analizowanie zdarzeń systemu Windows przekazywanych z serwera SIEM w sieci użytkownika.|
|Czytnik dziennika zdarzeń systemu Windows|Czytnik dziennika zdarzeń systemu Windows jest odpowiedzialny za odczytywanie i analizowanie zdarzeń systemu Windows przekazanych do dziennika zdarzeń systemu Windows bramy usługi ATA z kontrolerów domeny.|
|Translator aktywności sieciowej | Służy do przeprowadzania translacji przeanalizowanego ruchu na logiczną reprezentację ruchu używaną przez usługę ATA (NetworkActivity).
|Mechanizm rozpoznawania jednostek|Mechanizm rozpoznawania jednostek pobiera przeanalizowane dane (ruch sieciowy i zdarzenia), a następnie przetwarza je za pomocą usługi Active Directory w celu znalezienia informacji o kontach i tożsamościach. Informacje te są następnie dopasowywane do adresów IP znalezionych w przeanalizowanych danych. Mechanizm rozpoznawania jednostek w sposób wydajny sprawdza nagłówki pakietów, aby umożliwić analizę pakietów uwierzytelniania pod kątem nazw maszyn, właściwości i tożsamości. Mechanizm rozpoznawania jednostek łączy przeanalizowane pakiety uwierzytelniania z danymi znajdującymi się w rzeczywistym pakiecie.|
|Nadawca jednostek|Nadawca jednostek jest odpowiedzialny za wysyłanie przeanalizowanych i dopasowanych danych do centrum usługi ATA.|

## Funkcje bramy ATA Lightweight Gateway

Następujące funkcje działają inaczej w zależności od tego, czy jest uruchomiona brama usługi ATA, czy brama ATA Lightweight Gateway.

-   **Kandydat synchronizatora domeny**<br>
Brama synchronizatora domeny jest odpowiedzialna za aktywne synchronizowanie wszystkich jednostek z konkretnej domeny usługi Active Directory (podobnie do mechanizmu używanego przez kontrolery domeny w przypadku replikacji). Z listy kandydatów wybierana jest losowo jedna brama, która będzie służyć jako synchronizator domeny. <br><br>
Jeśli synchronizator będzie w trybie offline przez ponad 30 minut, zamiast niego zostanie wybrany inny kandydat. Jeśli dla danej domeny nie ma dostępnego synchronizatora domeny, usługa ATA nie będzie mogła aktywnie synchronizować jednostek i ich zmian. Niemniej usługa ATA będzie reagować i odbierać nowe jednostki po ich wykryciu w monitorowanym ruchu. 
<br>Jeśli nie ma dostępnego synchronizatora domeny, a użytkownik będzie wyszukiwać jednostkę, z którą nie jest powiązany żaden ruch sieciowy, nie zostaną wyświetlone żadne wyniki.<br><br>
Domyślnie wszystkie bramy usługi ATA są kandydatami synchronizatora.<br><br>
Ponieważ wszystkie bramy ATA Lightweight Gateway są najprawdopodobniej wdrażane w oddziałach i małych kontrolerach domeny, nie są domyślnymi kandydatami synchronizatora.


-   **Ograniczenia zasobów**<br>
Brama ATA Lightweight Gateway zawiera składnik monitorowania, który ocenia dostępną moc obliczeniową i pamięć kontrolera domeny, na którym jest uruchomiony. Proces monitorowania jest wykonywany co 10 sekund i dynamicznie aktualizuje przydział użycia procesora CPU i pamięci w procesie bramy ATA Lightweight Gateway, aby upewnić się, że w każdym momencie kontroler domeny ma co najmniej 15% wolnej mocy obliczeniowej i zasobów pamięci.<br><br>
Niezależnie od tego, co się dzieje w kontrolerze domeny, proces ten zawsze zwalnia zasoby, aby upewnić się, że podstawowa funkcjonalność kontrolera domeny nie zostanie zaburzona.<br><br>
Jeśli spowoduje to zużycie wszystkich zasobów bramy ATA Lightweight Gateway, tylko część ruchu będzie monitorowana, a na stronie kondycji pojawi się alert monitorowania „Opuszczono ruch sieciowy po dublowaniu portów”.

W poniższej tabeli zawarto przykład kontrolera domeny z wystarczającą ilością zasobów obliczeniowych, która umożliwia zastosowanie większego limitu przydziału niż obecnie wymagany, dzięki czemu cały ruch jest monitorowany:

||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Brama ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Różne (inne procesy) |Przydział bramy ATA Lightweight Gateway|Brama pomija|
|30%|20%|10%|45%|Nie|

Jeśli usługa Active Directory potrzebuje więcej mocy obliczeniowej, przydział wymagany przez bramę ATA Lightweight Gateway zostanie zmniejszony. W poniższym przykładzie brama ATA Lightweight Gateway potrzebuje więcej zasobów niż zostało jej przydzielone i pomija część ruchu (monitoruje tylko część ruchu):

||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Brama ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Różne (inne procesy) |Przydział bramy ATA Lightweight Gateway|Brama pomija|
|60%|15%|10%|15%|Tak|



## Składniki Twojej sieci
Aby móc pracować z usługą ATA, należy spełnić następujące wymagania:

### Dublowanie portów
Jeśli używasz bram usługi ATA, musisz skonfigurować dublowanie portów dla kontrolerów domeny, które będą monitorowane, oraz ustawić bramę usługi ATA jako miejsce docelowe za pomocą przełączników fizycznych lub wirtualnych. Innym rozwiązaniem jest użycie funkcji podsłuchu sieci. Usługa ATA będzie działać, jeśli tylko część kontrolerów domeny jest monitorowana, ale wykrywanie będzie mniej skuteczne.

Choć funkcja dublowania portów dubluje całość ruchu sieciowego kontrolera domeny do bramy usługi ATA, tylko niewielka część tego ruchu jest następnie wysyłana po kompresji do centrum usługi ATA w celu analizy.

Kontrolery domeny i bramy usługi ATA mogą być fizyczne lub wirtualne. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](/advanced-threat-analytics/deploy-use/configure-port-mirroring).


### Zdarzenia
Aby poprawić wykrywanie przez usługę ATA ataków typu Pass-the-Hash, ataków siłowych i ataków z wykorzystaniem przynęty, usługa ATA wymaga dziennika zdarzeń systemu Windows o identyfikatorze 4776. Może on być przekazywany do bramy usługi ATA na jeden z dwóch sposobów: przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM lub przy użyciu funkcji przekazywania zdarzeń systemu Windows.

-   Konfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM <br>Skonfiguruj system SIEM do przekazywania określonych zdarzeń systemu Windows do usługi ATA. Usługa ATA obsługuje wielu dostawców systemów SIEM. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection).

-   Konfigurowanie funkcji przekazywania zdarzeń systemu Windows<br>Innym sposobem na odbieranie zdarzeń przez usługę ATA jest skonfigurowanie kontrolerów domeny do przekazywania dziennika zdarzeń 4776 systemu Windows do bramy usługi ATA. Jest to szczególnie przydatne wtedy, gdy nie jest używany system SIEM lub system SIEM nie jest aktualnie obsługiwany przez usługę ATA. Aby uzyskać więcej informacji na temat funkcji przekazywania zdarzeń systemu Windows w usłudze ATA, zobacz [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO4-->


