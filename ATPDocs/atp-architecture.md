---
title: Architektura Advanced Threat Protection Azure | Dokumentacja firmy Microsoft
description: Opis architektury z Azure Advanced Threat Analytics (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 435e5141c8abda338c1115004d1876ff5b7736a4
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="azure-atp-architecture"></a>Architektura ATP Azure
Architektura Azure Advanced Threat Protection została szczegółowo opisana na tym diagramie:

![Diagram topologii architektury usługi Azure ATP](media/atp-architecture-topology.png)

Azure ATP monitorowanie ruchu sieciowego kontrolera domeny przy użyciu funkcji dublowania portów Sensor autonomiczny Azure ATP za pomocą przełączników fizycznych lub wirtualnych. Jeśli wdrożono czujnik Azure ATP bezpośrednio na kontrolerach domeny, usuwa wymaganie dublowania portów. Ponadto Azure ATP może wykorzystywać zdarzenia systemu Windows (przekazywane bezpośrednio z kontrolerów domeny lub z serwera SIEM) i analizować dane pod kątem ataków i zagrożeń. Azure ATP odbiera przeanalizowany ruch z czujnika autonomiczny Azure ATP i czujnik Azure ATP. Następnie wykonuje profilowanie, uruchamia wykrywanie deterministyczne oraz uruchamia uczenie maszynowe i algorytmy behawioralne, aby uzyskać więcej informacji dotyczących sieci, włącza wykrywanie anomalii i ostrzega o podejrzanych działaniach.

W tej sekcji opisano przepływ sieci i Przechwytywanie zdarzeń oraz zawarto bardziej szczegółowe informacje dotyczące funkcjonalności głównych komponentów ATP: czujnik autonomiczny Azure ATP, Azure ATP czujnik (który ma te same funkcje podstawowe jako czujnik autonomiczny Azure ATP), i usługa w chmurze Azure ATP. 

## <a name="azure-atp-components"></a>Składniki platformy Azure ATP
Azure ATP składa się z następujących składników:

-   **Portal zarządzania obszaru roboczego w usłudze Azure ATP** <br>
Portal zarządzania Azure ATP obszaru roboczego służy do tworzenia obszarów roboczych i umożliwia integrację z innymi usługami firmy Microsoft.

> [!NOTE]
> Tylko czujników z jednego lasu usługi Active Directory mogą łączyć się jednego obszaru roboczego.

-   **Portal Azure obszaru roboczego ATP** <br>
Portalu Azure ATP obszaru roboczego odbiera dane z ATP czujników i czujników autonomicznych. Monitoruje, zarządza i sprawdza zagrożenia w danym środowisku.

-   **Azure czujnik ATP**<br>
Czujnik Azure ATP jest instalowana bezpośrednio w kontrolerach domeny i monitoruje ruch bezpośrednio, bez konieczności użycia serwera dedykowanego lub funkcji dublowania portów. 

-   **Azure czujnik autonomiczny ATP**<br>
Czujnik autonomiczny Azure ATP jest zainstalowana na dedykowanym serwerze, który monitoruje ruch kontrolerów domeny za pomocą funkcji dublowania portów lub podsłuchu sieci. Jest to alternatywa czujnika Azure ATP.

## <a name="deployment-options"></a>Opcje wdrażania
Można wdrożyć przy użyciu następujących kombinacji czujników ATP Azure:

-   **Przy użyciu tylko Azure ATP czujników**<br>
Wdrożenia Azure ATP może zawierać tylko czujników Azure ATP: czujniki ATP Azure są wdrażane na każdym kontrolerze domeny i żadne dodatkowe serwery lub konfiguracją funkcji dublowania portów jest konieczne.

-   **Przy użyciu tylko czujników autonomiczny Azure ATP** <br>
Wdrożenie Azure ATP może zawierać tylko Azure ATP autonomiczny czujników, bez żadnych czujników Azure ATP: wszystkie kontrolery domeny należy skonfigurować, aby włączyć dublowanie portów Sensor autonomiczny Azure ATP lub podsłuchu sieci należy spełnić.

-   **Używając Azure ATP autonomiczny czujników i czujników Azure ATP**<br>
Wdrożenie Azure ATP zawiera Azure ATP autonomiczny czujników i czujników Azure ATP. Czujniki Azure ATP są zainstalowane na niektórych kontrolerach domeny (na przykład wszystkich kontrolerów domeny w oddziałach). W tym samym czasie inne kontrolery domeny są monitorowane przez czujniki autonomiczny Azure ATP (np. większe kontrolery domeny w głównych centrach danych).


### <a name="azure-atp-workspace-management-portal"></a>Portal zarządzania obszaru roboczego w usłudze Azure ATP

Portal zarządzania Azure ATP obszaru roboczego umożliwia:

-   Tworzenie i zarządzanie nimi Azure ATP obszary robocze

-   Integracja z innymi usługami zabezpieczeń firmy Microsoft

Ustaw obszar roboczy głównego jako **głównej**. Tylko jeden obszar roboczy, może być ustawiony jako podstawowy. Ustawienia obszaru roboczego jako podstawowy integracji efekty — tylko zintegrować Azure ATP z Windows Defender ATP obszaru roboczego podstawowego. Można zmienić, które obszaru roboczego jest podstawowym później, ale aby zrobić, należy usunąć wszystkie integracji został już ustawiony dla podstawowym obszarem roboczym.

> [!NOTE]
> Azure ATP obecnie obsługuje tworzenie dwóch obszarów roboczych. Zalecane jest tworzenie podstawowym obszarem roboczym dla środowiska produkcyjnego i dodatkowe obszar roboczy jako środowisko tymczasowe.
> Po usunięciu obszaru roboczego można się z pomocą techniczną, aby uaktywnić go ponownie. Można mieć maksymalnie trzy obszary robocze usunięte. Aby zwiększyć liczbę zapisanych, usunięto obszary robocze, skontaktuj się z obsługą Azure ATP.


### <a name="azure-atp-workspace-portal"></a>Portal Azure obszaru roboczego ATP

Obszar roboczy Azure ATP umożliwia zarządzanie Azure ATP następujące funkcje:

-   Zarządzanie Azure ATP czujników i autonomicznych czujnik ustawieniami konfiguracji

-   Widok danych otrzymywanych z czujników autonomiczny Azure ATP i czujników Azure ATP 

-   Monitor wykryto podejrzane działania na podstawie algorytmów uczenia maszynowego behawioralnej do wykrywania nietypowe zachowanie i algorytmy deterministyczne w celu wykrywania zaawansowanych ataków opartych na łańcuchu kończenia ataków

-   Opcjonalnie: portal zarządzania obszaru roboczego można skonfigurować do wysyłania wiadomości e-mail i zdarzeń po wykryciu podejrzanych działań lub zdarzenia kondycji.


|||
|-|-|
|Odbiornik jednostek|Odbiera partie jednostek ze wszystkich Azure ATP czujników i czujników autonomiczny Azure ATP.|
|Procesor aktywności sieciowej|Przetwarza wszystkie działania w sieci w ramach każdej otrzymanej partii. Dotyczy to na przykład dopasowywania między różnymi krokami protokołu Kerberos wykonywanymi z potencjalnie różnych komputerów|
|Profiler jednostek|Profiluje wszystkie unikatowe jednostki na podstawie ruchu i zdarzeń. Na przykład Azure ATP aktualizuje listę zalogowanych komputerów dla każdego profilu użytkownika.|
|Portal zarządzania obszaru roboczego w usłudze Azure ATP|Zarządza obszarami roboczymi Azure ATP.|
|Portal Azure obszaru roboczego ATP|Obszar roboczy Azure ATP służy do konfigurowania Azure ATP i monitorowania podejrzanych działań wykrytych przez Azure ATP w sieci. Obszar roboczy Azure ATP nie jest zależna od czujnik Azure ATP i jest uruchamiany nawet wtedy, gdy czujnik Azure ATP usługa została zatrzymana. |
|Detektory|Detektory używają algorytmów uczenia maszynowego i reguł deterministycznych do znajdowania podejrzanych działań i nietypowego zachowania użytkowników w sieci.|

Podczas podejmowania decyzji o liczbie Azure ATP obszarów roboczych wdrażania w sieci, należy wziąć pod uwagę następujące kryteria:

-   Jeden obszar roboczy Azure ATP można monitorować pojedynczy las usługi Active Directory. Jeśli masz więcej niż jednym lesie usługi Active Directory, należy co najmniej jednej usługi w chmurze Azure ATP dla każdego lasu usługi Active Directory.


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Czujnik ATP Azure i czujnik autonomiczny Azure ATP

**Czujnik Azure ATP** i **czujnik autonomiczny Azure ATP** mają te same funkcje podstawowe:

-   Przechwytują i analizują ruch sieciowy kontrolera domeny. Jest to ruch po dublowaniu portów dla czujników autonomiczny Azure ATP lub ruch lokalny kontrolera domeny w czujniki Azure ATP. 

-   Odbierają zdarzenia systemu Windows bezpośrednio z kontrolerów domeny (dla czujników ATP) lub z rozwiązania SIEM lub Syslog serwerów (na potrzeby ATP czujników autonomiczne)

-  Otrzymywanie informacji ewidencjonowania aktywności usługi RADIUS przez dostawcę sieci VPN

-   Pobierają dane o użytkownikach i komputerach z domeny usługi Active Directory

-   Przeprowadzają rozpoznawanie jednostek sieci (użytkowników, grup i komputerów)

-   Transferują odpowiednie dane do usługi w chmurze Azure ATP

-   Monitorowanie wielu kontrolerów domeny, które z czujnika jednej autonomicznej Azure ATP lub monitorują pojedynczy kontroler domeny dla czujnika Azure ATP.

Domyślnie Azure ATP obsługuje maksymalnie 100 czujników. Jeśli chcesz zainstalować więcej, skontaktuj się z obsługą Azure ATP.

Czujnik autonomiczny Azure ATP odbiera ruch sieciowy i zdarzenia systemu Windows z sieci i przetwarza je za pomocą następujących głównych składników:

|||
|-|-|
|Odbiornik sieci|Odbiornik sieci przechwytywania ruchu sieciowego i analizuje dane. Jest to zadanie silnie obciążające procesor CPU, więc jest szczególnie ważne sprawdzić [wymagania wstępne ATP Azure](atp-prerequisites.md) podczas planowania z czujnika Azure ATP lub czujnik autonomiczny Azure ATP.|
|Odbiornik zdarzeń|Odbiornik zdarzeń powoduje przechwycenie i analizowania zdarzeń systemu Windows przekazywanych z serwera SIEM w sieci.|
|Czytnik dziennika zdarzeń systemu Windows|Czytnik dziennika zdarzeń systemu Windows odczytuje i analizuje zdarzenia systemu Windows przekazywanych do dziennika zdarzeń systemu Windows Azure ATP czujnik autonomicznej z kontrolerów domeny.|
|Translator aktywności sieciowej | Translacji przeanalizowanego ruchu na logiczną reprezentację ruchu używaną przez ATP Azure (NetworkActivity).
|Mechanizm rozpoznawania jednostek|Mechanizm rozpoznawania jednostek pobiera przeanalizowane dane (ruch sieciowy i zdarzenia), a następnie przetwarza je za pomocą usługi Active Directory w celu znalezienia informacji o kontach i tożsamościach. Informacje te są następnie dopasowywane do adresów IP znalezionych w przeanalizowanych danych. Mechanizm rozpoznawania jednostek w sposób wydajny sprawdza nagłówki pakietów, aby umożliwić analizę pakietów uwierzytelniania pod kątem nazw maszyn, właściwości i tożsamości. Mechanizm rozpoznawania jednostek łączy przeanalizowane pakiety uwierzytelniania z danymi znajdującymi się w rzeczywistym pakiecie.|
|Nadawca jednostek|Nadawca jednostek wysyła przeanalizowanych i dopasowanych danych do usługi w chmurze Azure ATP.|

## <a name="azure-atp-sensor-features"></a>Funkcje platformy Azure czujnik ATP

Następujące funkcje działają inaczej w zależności od tego, czy są uruchomione czujnika autonomiczny Azure ATP lub czujnik Azure ATP.

-   Czujnik Azure ATP mogą odczytywać zdarzenia lokalnie, bez konieczności konfigurowania funkcji przekazywania zdarzeń.

-   **Kandydat synchronizatora domeny**<br>
Kandydat Synchronizatora domeny jest odpowiedzialna za aktywne synchronizowanie wszystkich jednostek z konkretnej domeny usługi Active Directory (podobnie do mechanizmu używanego przez kontrolery domeny dla replikacji). Jeden czujnik jest wybierany losowo, z listy kandydatów, służyć jako Synchronizator domeny. <br><br>
Jeśli synchronizator będzie w trybie offline przez ponad 30 minut, zamiast niego zostanie wybrany inny kandydat. Jeśli nie jest dostępny dla określonej domeny Synchronizatora domeny, Azure ATP jest mogła aktywnie synchronizować jednostek i ich zmian jednak Azure ATP pobiera nowe jednostki po ich wykryciu w monitorowanym ruchu. 
<br>Jeśli nie ma dostępnego Synchronizatora domeny, a następnie wyszukaj jednostki, która nie ma żadnych ruch związany z jej, nie wyszukiwania są wyświetlane wyniki.<br><br>
Domyślnie wszystkie czujników autonomiczny Azure ATP są kandydatami Synchronizatora.<br><br>
Azure czujników ATP nie są domyślnymi kandydatami Synchronizatora.


-   **Ograniczenia zasobów**<br>
Czujnik Azure ATP zawiera składnik monitorowania, które ocenia dostępne moc obliczeniową i pamięć na kontrolerze domeny, na którym jest uruchomiony. Proces monitorowania jest wykonywana co 10 sekund i dynamicznie aktualizuje przydział użycia procesora CPU i pamięci dla procesu czujnik Azure ATP, aby upewnić się na dowolnym etapie w czasie, kontroler domeny ma co najmniej 15% wolnej mocy obliczeniowej i zasobów pamięci.<br><br>
Niezależnie od tego, co się dzieje w kontrolerze domeny, proces ten zawsze zwalnia zasoby, aby upewnić się, że podstawowa funkcjonalność kontrolera domeny nie zostanie zaburzona.<br><br>
Jeśli spowoduje czujnik Azure ATP brakować zasobów, tylko część ruchu będzie monitorowana, a alert monitorowania "Opuszczono ruch sieciowy dublowaniu portów" są wyświetlane na stronie kondycji.

W poniższej tabeli zawarto przykład kontrolera domeny z wystarczającą ilością zasobów obliczeniowych, która umożliwia zastosowanie większego limitu przydziału niż obecnie wymagany, dzięki czemu cały ruch jest monitorowany:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Czujnik ATP Azure (Microsoft.Tri.sensor.exe)|Różne (inne procesy) |Azure przydziału czujnik ATP|Czujnik odrzuca ruch?|
|30%|20%|10%|45%|Nie|

Jeśli usługi Active Directory potrzebuje więcej mocy obliczeniowej, przydział wymagany przez czujnik Azure ATP zostanie zmniejszona. W poniższym przykładzie czujnik ATP Azure potrzebuje więcej zasobów niż jej przydzielone i pomija część ruchu (monitoruje tylko część ruchu):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Usługa Active Directory (Lsass.exe)|Czujnik ATP Azure (Microsoft.Tri.sensor.exe)|Różne (inne procesy) |Azure przydziału czujnik ATP|Czujnik odrzuca ruch?|
|60%|15%|10%|15%|Tak|


## <a name="your-network-components"></a>Składniki Twojej sieci
Aby pracować z Azure ATP, upewnij się sprawdzić, czy następujące składniki są skonfigurowane.

### <a name="port-mirroring"></a>Dublowanie portów
Jeśli używasz czujników autonomiczny Azure ATP należy skonfigurować port dublowania dla kontrolerów domeny, które są monitorowane oraz ustawić czujnik autonomiczny Azure ATP jako miejsca docelowego, za pomocą przełączników fizycznych lub wirtualnych. Innym rozwiązaniem jest użycie funkcji podsłuchu sieci. Azure ATP działa, jeśli niektóre, ale nie wszystkie kontrolery domeny są monitorowane, ale wykryć są mniej skuteczne.

Funkcja dublowania portów dubluje wszystkich ruchu sieciowego kontrolera domeny czujnika autonomiczny Azure ATP, tylko niewielką część tego ruchu jest następnie wysyłane, skompresowany, aby Azure ATP usługa w chmurze dla analizy.

Kontrolery domeny i czujników autonomiczny Azure ATP może być fizyczne lub wirtualne. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).


### <a name="events"></a>Zdarzenia
Aby poprawić wykrywanie Azure ATP ataków typu Pass--Hash, ataki Siłowe, modyfikację poufnych grup, tworzenie usług podejrzane, modyfikacje przynęty, Azure ATP wymaga następujących zdarzeń systemu Windows: 4776, 4732 4733, 4728, 4729, 4756, 4757 i 7045. Można albo je odczytać automatycznie przez czujnik Azure ATP lub w przypadku, gdy czujnik Azure ATP nie została wdrożona, go mogą być przekazywane do czujnik autonomiczny Azure ATP w jeden z dwóch sposobów, konfigurując czujnik autonomiczny Azure ATP do nasłuchiwania zdarzeń SIEM lub przez [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md).

-   Konfigurowanie czujnik autonomiczny Azure ATP do nasłuchiwania zdarzeń SIEM <br>Skonfiguruj system SIEM do przekazywania określonych zdarzeń systemu Windows do ATP. Azure ATP obsługuje wielu dostawców systemów SIEM. Aby uzyskać więcej informacji, zobacz [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md).

-   Konfigurowanie funkcji przekazywania zdarzeń systemu Windows<br>Innym sposobem na odbieranie zdarzeń Azure ATP jest skonfigurowanie kontrolerów domeny do przekazywania zdarzeń systemu Windows 4776, 4732 4733, 4728, 4729, 4756, 4757 i 7045 Twojego Sensor autonomiczny Azure ATP. Jest to szczególnie przydatne, jeśli nie jest używany system SIEM lub system SIEM nie jest obsługiwana przez ATP. Aby uzyskać więcej informacji na temat systemu Windows w ATP funkcji przekazywania zdarzeń, zobacz [Windows Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md). Dotyczy to tylko fizyczne czujników autonomiczny Azure ATP - nie z czujnika Azure ATP.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/trisizingtool)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md)

- - [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
