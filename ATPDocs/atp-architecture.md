---
title: Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure | Dokumentacja firmy Microsoft
description: W tym artykule opisano architekturę z usługi Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c7fda04658dc70406fc7c0d543286e46da4cfa86
ms.sourcegitcommit: 56886d06abd25035ffc9885c69aca9b0ebf14abc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2018
ms.locfileid: "43039083"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-architecture"></a>Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure
Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure:

![Diagram topologii architektury usługi Azure ATP](media/atp-architecture-topology.png)

Narzędzie Azure ATP monitoruje ruch sieciowy kontrolera domeny przy użyciu funkcji dublowania portów do usługi Azure ATP czujnik autonomiczny, za pomocą przełączników fizycznych lub wirtualnych. W przypadku wdrożenia czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure bezpośrednio w kontrolerach domeny, usuwa potrzebę funkcji dublowania portów. Ponadto narzędzia Azure ATP można korzystać z wydarzenia Windows (przekazywane bezpośrednio z kontrolerów domeny lub z serwera SIEM) i analizować dane pod kątem ataków i zagrożeń. Narzędzie Azure ATP odbiera przeanalizowany ruch z czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i usługi Azure ATP czujnik autonomiczny. Następnie narzędzie Azure ATP Wykonuje profilowanie, uruchamia wykrywanie deterministyczne oraz uruchamia uczenie maszynowe i algorytmy behawioralne, aby uczyć się sieci, włącza wykrywanie anomalii i ostrzeganie o podejrzanych działaniach.

W tej sekcji opisano przepływ sieci i Przechwytywanie zdarzeń oraz zawarto bardziej szczegółowe informacje dotyczące funkcjonalności głównych składników zaawansowanej ochrony przed zagrożeniami: czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, usługi Azure ATP czujnik autonomiczny (który ma te same funkcje podstawowe jako czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, ale wymaga dodatkowy sprzęt, dublowanie konfiguracji portów i nie obsługuje wykrywania śledzenie zdarzeń dla Windows (ETW) na podstawie) i usługą w chmurze usługi Azure ATP. 

Zainstalowany bezpośrednio na kontrolerach domeny, czujnika zaawansowanej ochrony przed zagrożeniami uzyskuje dostęp do wymaganych dzienników zdarzeń bezpośrednio z poziomu kontrolera domeny. Po tych dzienników i ruchu sieciowym analizie za pomocą czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wysyła te przeanalizowane informacje do usługi Azure ATP (nie wszystkie dzienniki).

## <a name="azure-atp-components"></a>Składniki usługi Azure ATP
Narzędzie Azure ATP składa się z następujących składników:

-   **Portalu zarządzania obszarami roboczymi w usłudze Azure ATP** <br>
Portalu zarządzania obszarami roboczymi usługi Azure ATP pozwala na tworzenie i zarządzanie obszarem roboczym i umożliwia integrację z innymi usługami firmy Microsoft.

-   **Portalu obszaru roboczego usługi Azure ATP** <br>
Portalu obszaru roboczego usługi Azure ATP odbiera dane z czujników zaawansowanej ochrony przed zagrożeniami i czujniki autonomicznych. Monitoruje, zarządza i bada zagrożenia w danym środowisku.

-   **Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami**<br>
Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest instalowany bezpośrednio na kontrolerach domeny i monitoruje ruch kontrolerów bezpośrednio, bez konieczności użycia serwera dedykowanego lub funkcji dublowania portów. 

-   **Czujnik autonomiczny usługi Azure ATP**<br>
Narzędzia Azure ATP czujnik autonomiczny jest instalowany na dedykowanych serwerach, które monitoruje ruch kontrolerów domeny za pomocą funkcji dublowania portów lub PODSŁUCHU sieci. Jest to alternatywa, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, która wymaga dodatkowego sprzętu, funkcji dublowania portów i konfiguracji. Azure ATP autonomiczny czujników nie obsługują wykrywania śledzenie zdarzeń dla Windows (ETW) na podstawie objęte czujnika zaawansowanej ochrony przed zagrożeniami. 

## <a name="deployment-options"></a>Opcje wdrażania
Można wdrożyć narzędzia Azure ATP przy użyciu następujących kombinacji czujniki:

-   **Przy użyciu tylko usługi Azure ATP czujników**<br>
Wdrożenie usługi Azure ATP może zawierać tylko usługi Azure ATP czujniki: narzędzia Azure ATP czujników są wdrażane bezpośrednio na każdym kontrolerze domeny i żadne dodatkowe serwery lub konfigurację funkcji dublowania portów jest konieczne.

-   **Przy użyciu tylko czujników autonomiczne narzędzia Azure ATP** <br>
Wdrożenie usługi Azure ATP może zawierać tylko usługi Azure ATP autonomiczny czujników, bez żadnych czujników narzędzia Azure ATP: wszystkie kontrolery domeny należy skonfigurować, aby umożliwić dublowanie portów do usługi Azure ATP czujnik autonomiczny lub podsłuchu sieci musi znajdować się w miejscu.

-   **Przy użyciu zarówno usługi Azure ATP czujniki, jak i czujniki autonomiczne narzędzia Azure ATP**<br>
Wdrożenia usługi Azure ATP obejmuje zarówno usługi Azure ATP czujniki, jak i czujniki autonomiczne narzędzia Azure ATP. Czujniki narzędzia Azure ATP są instalowane na niektórych kontrolerach domeny (na przykład, wszystkie kontrolery domeny w oddziałach). W tym samym czasie inne kontrolery domeny są monitorowane przy użyciu narzędzia Azure ATP autonomiczny czujników (na przykład większe kontrolery domeny w głównych centrach danych. 


### <a name="azure-atp-management-portal"></a>Portal zarządzania systemu Azure ATP

W portalu zarządzania usługi Azure ATP pozwala na:

-   Tworzenie i zarządzanie obszarem roboczym usługi Azure ATP

-   Integracja z innymi usługami zabezpieczeń firmy Microsoft

> [!NOTE]
> - Narzędzie Azure ATP aktualnie obsługuje tworzenie tylko jeden obszar roboczy. Po usunięciu obszaru roboczego można się z pomocą techniczną, aby uaktywnić go ponownie. Może mieć maksymalnie trzy obszary robocze z usuniętych. Zwiększenie liczby obszarów roboczych zapisane, usunięte, skontaktuj się z działem pomocy technicznej usługi Azure ATP.
> - Jeśli nie czujnik jest zainstalowany w obszarze roboczym w ciągu 60 dni, może zostać usunięty obszar roboczy i musisz utworzyć go ponownie.



### <a name="azure-atp-workspace-portal"></a>Portalu obszaru roboczego usługi Azure ATP

Obszar roboczy usługi Azure ATP umożliwia zarządzanie następujące funkcje usługi Azure ATP:

-   Narzędzia Azure ATP czujnik autonomiczny czujnik ustawienia konfiguracji i zarządzanie

-   Wyświetlanie danych odebranych z czujników autonomiczne narzędzia Azure ATP i czujniki narzędzia Azure ATP 

-   Monitor wykryto podejrzane działania na podstawie algorytmów uczenia maszynowego behawioralnej do wykrywania nietypowych zachowań i algorytmy deterministyczne w celu wykrywania zaawansowanych ataków opartych na łańcuchu kończenia ataków

-   Opcjonalnie: portalu zarządzania obszarami roboczymi można skonfigurować do wysyłania wiadomości e-mail i zdarzeń po wykryciu podejrzanego działania lub zdarzenia dotyczące kondycji.


|||
|-|-|
|Portal zarządzania systemu Azure ATP|Zarządza obszaru roboczego usługi Azure ATP.|
|Portalu obszaru roboczego usługi Azure ATP|Obszar roboczy usługi Azure ATP służy do konfigurowania usługi Azure ATP i monitorowania podejrzanych działań wykrytych przez narzędzia Azure ATP w sieci. Obszar roboczy usługi Azure ATP jest niezależna od czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i jest uruchamiany nawet wtedy, gdy usługa czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure została zatrzymana. |
|Detektory|Detektory używają algorytmów uczenia maszynowego i reguł deterministycznych do znajdowania podejrzanych działań i nietypowego zachowania użytkowników w sieci.|


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami i czujnik autonomiczny narzędzia Azure ATP

**Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure** i **czujnik autonomiczny narzędzia Azure ATP** mają te same funkcje podstawowe:

-   Przechwytują i analizują ruch sieciowy kontrolera domeny. Jest to ruch lokalny kontrolera domeny usługi Azure ATP czujniki i ruch po dublowaniu portów dla usługi Azure ATP autonomiczny czujników. 

-   Odbieranie zdarzeń Windows, bezpośrednio z kontrolerów domeny (dla zaawansowanej ochrony przed zagrożeniami, czujniki) lub z serwerów SIEM lub Syslog (dla zaawansowanej ochrony przed zagrożeniami czujników autonomiczne)

-   Odbieranie informacji o kontach usługi RADIUS z dostawcę sieci VPN

-   Pobierają dane o użytkownikach i komputerach z domeny usługi Active Directory

-   Przeprowadzają rozpoznawanie jednostek sieci (użytkowników, grup i komputerów)

-   Transferują odpowiednie dane do usługi w chmurze usługi Azure ATP

-   Monitorowanie jednego kontrolera domeny do czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure lub monitorują wiele kontrolerów domeny z jednym czujnik autonomiczny narzędzia Azure ATP.

Domyślnie narzędzia Azure ATP obsługuje maksymalnie 100 czujników. Jeśli chcesz zainstalować więcej się z pomocą techniczną usługi Azure ATP.

Czujnik autonomiczny narzędzia Azure ATP odbiera ruch sieciowy i zdarzenia Windows z sieci użytkownika i przetwarza je za pomocą następujących głównych składników:

|||
|-|-|
|Odbiornik sieci|Odbiornik sieci przechwytuje ruch sieciowy i analizuje ruch. Jest to zadanie silnie obciążające procesor CPU, więc jest szczególnie ważne sprawdzić [wymagania wstępne dotyczące usługi Azure ATP](atp-prerequisites.md) podczas planowania usługi Azure ATP czujnik lub czujnik autonomiczny narzędzia Azure ATP.|
|Odbiornik zdarzeń|Odbiornik zdarzeń przechwytuje i analizuje zdarzenia Windows przekazywanych z serwera SIEM w sieci.|
|Czytnik dziennika zdarzeń systemu Windows|Czytnik dziennika zdarzeń Windows odczytuje i analizuje zdarzenia Windows przekazane do dziennika zdarzeń Windows czujnik autonomiczny narzędzia Azure ATP z kontrolerów domeny.|
|Translator aktywności sieciowej | Translacji przeanalizowanego ruchu na logiczną reprezentację ruchu używaną przez usługi Azure ATP (NetworkActivity).
|Mechanizm rozpoznawania jednostek|Mechanizm rozpoznawania jednostek pobiera przeanalizowane dane (ruch sieciowy i zdarzenia), a następnie przetwarza je za pomocą usługi Active Directory w celu znalezienia informacji o kontach i tożsamościach. Informacje te są następnie dopasowywane do adresów IP znalezionych w przeanalizowanych danych. Mechanizm rozpoznawania jednostek w sposób wydajny sprawdza nagłówki pakietów, aby umożliwić analizę pakietów uwierzytelniania pod kątem nazw maszyn, właściwości i tożsamości. Mechanizm rozpoznawania jednostek łączy przeanalizowane pakiety uwierzytelniania z danymi znajdującymi się w rzeczywistym pakiecie.|
|Nadawca jednostek|Nadawca jednostek wysyła przeanalizowane i dopasowane dane do usługi w chmurze usługi Azure ATP.|

## <a name="azure-atp-sensor-features"></a>Funkcje platformy Azure czujnika zaawansowanej ochrony przed zagrożeniami

Następujące funkcje działają inaczej w zależności od tego, czy korzystasz z czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure lub czujnik autonomiczny narzędzia Azure ATP.

-   Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure odczytuje zdarzenia lokalnie — bez konieczności zakupu i utrzymywania dodatkowego sprzętu ani konfigurowania przekazywania zdarzeń wymagane czujników autonomiczny zaawansowanej ochrony przed zagrożeniami. Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure obsługuje również zdarzeń wątku dla Windows (ETW) zawiera informacje dziennika dla wielu wykrywania. ETW oparte odmiany to między innymi podejrzane żądania replikacji i podejrzane podwyższania poziomu kontrolera domeny, oba są potencjalnymi atakami DCShadow i nie są obsługiwane przez czujniki autonomiczny zaawansowanej ochrony przed zagrożeniami.  

-   **Kandydat synchronizatora domeny**<br>
Kandydat Synchronizatora domeny jest odpowiedzialna za aktywne synchronizowanie wszystkich jednostek z określonej domeny usługi Active Directory (podobnie do mechanizmu używanego przez kontrolery domeny w przypadku replikacji). Jeden czujnik jest wybierany losowo, z listy kandydatów, która będzie służyć jako Synchronizator domeny. <br><br>
Jeśli synchronizator będzie w trybie offline przez ponad 30 minut, zamiast niego zostanie wybrany inny kandydat. Jeśli żadnego Synchronizatora domeny jest dostępny dla określonej domeny, narzędzia Azure ATP jest mogła aktywnie synchronizować jednostek i ich zmian, jednak narzędzia Azure ATP pobiera nowe jednostki po ich wykryciu w monitorowanym ruchu. 
<br>Jeśli żadnego Synchronizatora domeny jest dostępny i wyszukiwać jednostkę, które nie mają cały ruch odnoszących się do niego, są wyświetlane żadne wyniki wyszukiwania.<br><br>
Domyślnie wszystkie czujniki autonomiczne narzędzia Azure ATP są kandydatami Synchronizatora.<br><br>
Usługa Azure ATP czujników nie są domyślnymi kandydatami Synchronizatora.


-   **Ograniczenia zasobów**<br>
Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zawiera składnik monitorowania, który ocenia dostępne moc obliczeniową i pamięć na kontrolerze domeny, na którym jest uruchomiony. Proces monitorowania jest wykonywana co 10 sekund i dynamicznie aktualizuje przydział użycia procesora CPU i pamięci na temat procesu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, aby upewnić się, w dowolnym danym momencie w czasie kontroler domeny ma co najmniej 15% wolnej mocy obliczeniowej i zasobów pamięci.<br><br>
Niezależnie od tego, co się dzieje w kontrolerze domeny, proces ten zawsze zwalnia zasoby, aby upewnić się, że podstawowa funkcjonalność kontrolera domeny nie zostanie zaburzona.<br><br>
Jeśli powoduje to, że czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure brakować zasobów, tylko część ruchu będzie monitorowana, a alert monitorowania "Opuszczono ruch po dublowaniu portów sieciowych" pojawia się na stronie kondycji.

W poniższej tabeli zawarto przykład kontrolera domeny z wystarczającą ilością zasobów obliczeniowych, która umożliwia zastosowanie większego limitu przydziału niż obecnie wymagany, dzięki czemu cały ruch jest monitorowany:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami (Microsoft.Tri.sensor.exe)|Różne (inne procesy) |Przydziału usługi Azure czujnika zaawansowanej ochrony przed zagrożeniami|Czujnik odrzuca ruch?|
|30%|20%|10%|45%|Nie|

Jeśli usługi Active Directory potrzebuje więcej mocy obliczeniowej, przydział wymagany przez czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest ograniczona. W poniższym przykładzie czujnik narzędzia Azure ATP potrzebuje więcej zasobów niż jej przydzielone i pomija część ruchu (monitoruje tylko część ruchu):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami (Microsoft.Tri.sensor.exe)|Różne (inne procesy) |Przydziału usługi Azure czujnika zaawansowanej ochrony przed zagrożeniami|Czujnik odrzuca ruch?|
|60%|15%|10%|15%|Tak|


## <a name="your-network-components"></a>Składniki Twojej sieci
Sprawdź, czy następujące składniki są skonfigurowane, aby pracować z narzędzia Azure ATP.

### <a name="port-mirroring"></a>Dublowanie portów
Jeśli używasz narzędzia Azure ATP autonomiczny czujników, portu dublowania zestaw się jest wymagany dla kontrolerów domeny, które są monitorowane. Czujnik autonomiczny narzędzia Azure ATP należy ustawić jako miejsce docelowe, za pomocą przełączników fizycznych lub wirtualnych. Innym rozwiązaniem jest użycie funkcji podsłuchu sieci. Narzędzie Azure ATP działa, gdy niektóre, ale nie wszystkie kontrolery domeny są monitorowane, ale w przypadku wykrycia są mniej skuteczne.

Funkcja dublowania portów dubluje wszystkie ruchu sieciowego kontrolera domeny do usługi Azure ATP czujnik autonomiczny, tylko niewielką część tego ruchu jest następnie wysyłane, skompresowany, do usługi Azure ATP usługi w chmurze do analizy.

Kontrolery domeny i czujniki autonomiczne narzędzia Azure ATP, może być fizyczne lub wirtualne. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).


### <a name="events"></a>Zdarzenia
Aby zwiększyć pokrycie wykrywania usługi Azure ATP Pass--Hash, podejrzane błędy uwierzytelniania, modyfikacji wrażliwych grup, tworzenie podejrzanego usług i wystawione jako przynęta token typy działań ataku, potrzeb zaawansowanej ochrony przed zagrożeniami w usłudze Azure do analizy dzienników z następujących czynności Zdarzenia Windows: 4776,4732,4733,4728,4729,4756,4757 i 7045. Te zdarzenia są odczytywane automatycznie przez czujniki narzędzia Azure ATP z poprawną Zaawansowane ustawienia zasad inspekcji. W sytuacjach, wdrożonym narzędzia Azure ATP autonomiczny czujników dzienniki zdarzeń mogą być przekazywane do czujnik autonomiczny w jeden z dwóch sposobów; Konfigurowanie usługi Azure ATP czujnik autonomiczny do nasłuchiwania zdarzeń SIEM lub przez [konfigurowania przekazywania zdarzeń Windows](configure-event-forwarding.md). 

> [!NOTE]
> - Przesyłanie do autonomicznego czujników zdarzeń Windows nie obsługuje funkcji ETW (Event Tracing for Windows). ETW oparte odmiany to między innymi żądanie podejrzana Replikacja i podwyższania poziomu kontrolera domeny podejrzane, są potencjalnymi atakami DCShadow.  

-   Konfigurowanie usługi Azure ATP czujnik autonomiczny do nasłuchiwania zdarzeń SIEM <br>Skonfiguruj system SIEM do przekazywania określonych zdarzeń Windows do zaawansowanej ochrony przed zagrożeniami. Narzędzie Azure ATP obsługuje wielu dostawców systemów SIEM. Aby uzyskać więcej informacji, zobacz [konfigurowania przekazywania zdarzeń Windows](configure-event-forwarding.md).

-   Konfigurowanie funkcji przekazywania zdarzeń systemu Windows<br>Innym sposobem na odbieranie zdarzeń usługi Azure ATP jest skonfigurowanie kontrolerów domeny do przekazywania Windows zdarzeń 4776, 4732, 4733, 4728, 4729, 4756, 4757 i 7045 do usługi Azure ATP czujnik autonomiczny. Jest to szczególnie przydatne, jeśli nie ma rozwiązania SIEM lub system SIEM nie jest obecnie obsługiwane przez zaawansowanej ochrony przed zagrożeniami. Aby uzyskać więcej informacji na temat Windows w usłudze ATP funkcji przekazywania zdarzeń, zobacz [Windows konfigurowania przekazywania zdarzeń](configure-event-forwarding.md). Dotyczy to tylko fizycznych czujników autonomiczne narzędzia Azure ATP — nie z czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/trisizingtool)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md)

- - [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
