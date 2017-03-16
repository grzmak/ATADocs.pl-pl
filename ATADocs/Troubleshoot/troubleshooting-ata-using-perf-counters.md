---
title: "Rozwiązywanie problemów z usługą Advanced Threat Analytics przy użyciu liczników wydajności | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób rozwiązywania problemów z usługą ATA przy użyciu liczników wydajności."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5c4662cd2d83135227cf86e339d5e30f9713f022
ms.sourcegitcommit: 998e8aed5835b228e907aab78845723a02521741
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="troubleshooting-ata-using-the-performance-counters"></a>Rozwiązywanie problemów z usługą ATA przy użyciu liczników wydajności
Liczniki wydajności usługi ATA zapewniają wgląd w funkcjonowanie poszczególnych składników usługi ATA. Składniki usługi ATA przetwarzają dane sekwencyjnie, dlatego wystąpienie problemu może powodować reakcję łańcuchową prowadzącą do pominięcia części ruchu sieciowego. Aby rozwiązać problem, należy ustalić, który składnik go powoduje i usunąć jego przyczynę na początku sekwencji. Korzystając z danych liczników wydajności, można zrozumieć funkcjonowanie poszczególnych składników.
Aby uzyskać informacje na temat przepływu wewnętrznych składników usługi ATA, zobacz [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture).

**Proces składnika usługi ATA**:

1.  Gdy składnik osiągnie maksymalny rozmiar, uniemożliwia poprzedniemu składnikowi wysyłanie do niego kolejnych jednostek.

2.  Wtedy poprzedni składnik zacznie zwiększać **swój** rozmiar, aż zablokuje poprzedzający go składnik, uniemożliwiając wysyłanie kolejnych jednostek.

3.  Ten proces jest kontynuowany wstecz i prowadzi do składnika NetworkListener, który będzie pomijać ruch sieciowy, gdy nie będzie już mógł przesyłać dalej jednostek.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Pobieranie plików monitora wydajności w celu rozwiązywania problemów

Aby pobrać pliki monitora wydajności (BLG) z różnych składników ATA:
1.  Otwórz monitora wydajności.
2.  Zatrzymaj zestaw modułów zbierających dane o nazwie „Brama usługi Microsoft ATA” lub „Centrum usługi Microsoft ATA”.
3.  Przejdź do folderu zestawu modułów zbierających dane (domyślnie jest to „C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets” lub „C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs\DataCollectorSets”).
4.  Skopiuj plik BLG z najnowszą datą modyfikacji.
5.  Ponownie uruchom zestaw modułów zbierających dane o nazwie „Brama usługi Microsoft ATA” lub „Centrum usługi Microsoft ATA”.


## <a name="ata-gateway-performance-counters"></a>Liczniki wydajności bramy usługi ATA

W tej sekcji każde odwołanie do bramy usługi ATA odnosi się także do bramy ATA Lightweight Gateway.

Możesz obserwować stan wydajności bramy usługi ATA w czasie rzeczywistym, dodając liczniki wydajności bramy usługi ATA.
Aby to zrobić, należy otworzyć „Monitor wydajności” i dodać wszystkie liczniki dla bramy usługi ATA. Nazwa obiektu liczników wydajności to „Brama usługi Microsoft ATA”.

Oto lista głównych liczników bramy usługi ATA, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF Parsed Messages/Sec (Brama usługi Microsoft ATA\Liczba komunikatów PEF analizowanych przez składnik NetworkListener na sekundę)|Ilość ruchu sieciowego przetwarzanego przez bramę usługi ATA w ciągu sekundy.|Brak wartości progowej.|Ułatwia ustalenie ilości ruchu sieciowego analizowanego przez bramę usługi ATA.|
|NetworkListener PEF Dropped Events\Sec (Liczba zdarzeń PEF porzucanych przez składnik NetworkListener na sekundę)|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Gateway\NetworkListener ETW Dropped Events/Sec (Brama usługi Microsoft ATA\Liczba zdarzeń ETW porzucanych przez składnik NetworkListener na sekundę)|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Gateway\NetworkActivityTranslator Message Data # Block Size (Brama usługi Microsoft ATA\Rozmiar bloku liczby danych komunikatów składnika NetworkActivityTranslator)|Ilość ruchu sieciowego znajdującego się w kolejce w celu translacji na działania w sieci.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 100 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Gateway\EntityResolver Activity Block Size (Brama usługi Microsoft ATA\Rozmiar bloku działań składnika EntityResolver)|Liczba działań w sieci znajdujących się w kolejce w celu rozwiązania.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Gateway\EntitySender Entity Batch Block Size (Brama usługi Microsoft ATA\Rozmiar bloku partii jednostek EntitySender)|Liczba działań w sieci znajdujących się w kolejce w celu wysłania do centrum usługi ATA.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 1 000 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Gateway\EntitySender Batch Send Time (Brama usługi Microsoft ATA\Czas wysyłania partii EntitySender)|Ilość czasu, jaką zajęło wysłanie ostatniej partii.|W większości przypadków ta wartość powinna być mniejsza niż 1000 milisekund.|Sprawdź, czy nie wystąpiły problemy z siecią między bramą usługi ATA a centrum usługi ATA.|

> [!NOTE]
> -   Wartości liczników czasu są podawane w milisekundach.
> -   Czasami wygodniej jest monitorować pełną listę liczników przy użyciu wykresu „Raport” (przykład: monitorowanie wszystkich liczników w czasie rzeczywistym).

## <a name="ata-lightweight-gateway-performance-counters"></a>Liczniki wydajności bramy ATA Lightweight Gateway
Liczniki wydajności mogą służyć do zarządzania przydziałem w bramie Lightweight Gateway w celu zapewnienia, że usługa ATA nie wyczerpuje zbyt wielu zasobów z kontrolerów domeny, na których jest zainstalowana.
W celu mierzenia ograniczeń zasobów, które usługa ATA wymusza w bramie Lightweight Gateway, dodaj następujące liczniki:

Aby to zrobić, należy otworzyć „Monitor wydajności” i dodać wszystkie liczniki dla bramy ATA Lightweight Gateway. Nazwy obiektów liczników wydajności to: „Microsoft ATA Gateway” i „Microsoft ATA Gateway Updater”.


|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max % (Aktualizator bramy usługi Microsoft ATA\maksymalny czas procesora CPU składnika GatewayUpdaterResourceManager w %)|Maksymalna ilość czasu procesora (w procentach) do wykorzystania przez proces bramy Lightweight Gateway. |Brak wartości progowej. | Jest to ograniczenie, które chroni zasoby kontrolera domeny przed zużyciem przez bramę ATA Lightweight Gateway. Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size (Aktualizator bramy usługi Microsoft ATA\maksymalny rozmiar przydziału pamięci składnika GatewayUpdaterResourceManager)|Maksymalna ilość przydzielonej pamięci (w bajtach), którą może wykorzystać proces bramy Lightweight Gateway.|Brak wartości progowej. | Jest to ograniczenie, które chroni zasoby kontrolera domeny przed zużyciem przez bramę ATA Lightweight Gateway. Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size (Aktualizator bramy usługi Microsoft ATA\limit rozmiaru zestawu roboczego składnika GatewayUpdaterResourceManager)|Maksymalna ilość pamięci fizycznej (w bajtach), którą może wykorzystać proces bramy Lightweight Gateway.|Brak wartości progowej. | Jest to ograniczenie, które chroni zasoby kontrolera domeny przed zużyciem przez bramę ATA Lightweight Gateway. Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.|



Aby zobaczyć rzeczywiste zużycie, sprawdź następujące liczniki:



|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Proces(Microsoft.TRI.Gateway)\%Czas procesora|Maksymalna ilość czasu procesora (w procentach), którą faktycznie zużywa proces bramy Lightweight Gateway. |Brak wartości progowej. | Należy porównać wyniki tego licznika do limitu odczytanego z licznika GatewayUpdaterResourceManager CPU Time Max % (maksymalny czas procesora CPU składnika GatewayUpdaterResourceManager w %). Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.|
|Proces(Microsoft.Tri.Gateway)\Bajty prywatne|Maksymalna ilość przydzielonej pamięci (w bajtach), którą może wykorzystać proces bramy Lightweight Gateway.|Brak wartości progowej. | Należy porównać wyniki tego licznika z limitem odczytanym z licznika GatewayUpdaterResourceManager Commit Memory Max Size (maksymalny rozmiar przydziału pamięci składnika GatewayUpdaterResourceManager). Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.| 
|Proces(Microsoft.Tri.Gateway)\Zestaw roboczy|Maksymalna ilość pamięci fizycznej (w bajtach), którą faktycznie zużywa proces bramy Lightweight Gateway.|Brak wartości progowej. |Należy porównać wyniki tego licznika z limitem odczytanym z licznika GatewayUpdaterResourceManager Working Set Limit Size (limit rozmiaru zestawu roboczego składnika GatewayUpdaterResourceManager). Jeśli widzisz, że proces często osiąga maksymalny limit w przedziale czasu (proces osiąga limit, a następnie zaczyna pomijać ruch), oznacza to, należy dodać więcej zasobów do serwera z działającym kontrolerem domeny.|

## <a name="ata-center-performance-counters"></a>Liczniki wydajności centrum usługi ATA
Możesz obserwować stan wydajności centrum usługi ATA w czasie rzeczywistym, dodając liczniki wydajności centrum usługi ATA.

Aby to zrobić, należy otworzyć „Monitor wydajności” i dodać wszystkie liczniki dla centrum usługi ATA. Nazwa obiektu liczników wydajności to „Centrum usługi Microsoft ATA”.

Oto lista głównych liczników centrum usługi ATA, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver Entity Batch Block Size (Centrum usługi Microsoft ATA\rozmiar bloku partii jednostek składnika EntityReceiver)|Liczba partii jednostek umieszczonych w kolejce przez centrum usługi ATA.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener.  Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size (Centrum usługi Microsoft ATA\rozmiar bloku działań sieciowych składnika NetworkActivityProcessor)|Liczba działań w sieci znajdujących się w kolejce w celu przetworzenia.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 50 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Center\EntityProfiler Network Activity Block Size (Centrum usługi Microsoft ATA\rozmiar bloku działań sieciowych składnika EntityProfiler)|Liczba działań w sieci znajdujących się w kolejce w celu profilowania.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Microsoft ATA Center\Database &#42; Block Size (Centrum usługi Microsoft ATA\rozmiar bloku składnika Database&#42;)|Liczba działań w sieci określonego typu znajdujących się w kolejce w celu zapisania w bazie danych.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 50 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|


> [!NOTE]
> -   Wartości liczników czasu są podawane w milisekundach.
> -   Czasami wygodniej jest monitorować pełną listę liczników przy użyciu wykresu Raport (przykład: monitorowanie wszystkich liczników w czasie rzeczywistym).

## <a name="operating-system-counters"></a>Liczniki systemu operacyjnego
Oto lista głównych liczników systemu operacyjnego, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Procesor(_Total)\% Czas procesora|Procent czasu, który upłynął, przeznaczony przez procesor na wykonywanie wątku czynnego.|Przeciętnie mniej niż 80%.|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\% Czas procesora” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|System\Przełączenia kontekstu/s|Łączna szybkość przełączania wątków we wszystkich procesorach.|Mniej niż 5000&#42; rdzeni (fizycznych).|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\% Czas procesora” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|System\Długość kolejki procesora|Liczba wątków gotowych do wykonania i oczekujących na zaplanowanie.|Mniej niż 5&#42; rdzeni (fizycznych).|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\% Czas procesora” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|Pamięć\Dostępna pamięć (MB)|Ilość pamięci fizycznej (RAM) dostępnej do przydzielenia.|Ta wartość powinna być większa niż 512.|Sprawdź, czy istnieje proces zużywający znacznie większą ilość pamięci fizycznej niż powinien.<br /><br />Zwiększ ilość pamięci fizycznej.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.|
|Dysk logiczny(&#42;)\Średnia czas dysku w s/Odczyt|Średnie opóźnienie odczytu danych z dysku (należy wybrać dysk bazy danych jako wystąpienie).|Ta wartość powinna być mniejsza niż 10 milisekund.|Sprawdź, czy istnieje określony proces wykorzystujący dysk bazy danych znacznie intensywniej niż powinien.<br /><br />Skonsultuj się z zespołem/dostawcą magazynu, aby ustalić, czy dany dysk może obsługiwać bieżące obciążenie przy opóźnieniu mniejszym niż 10 ms. Bieżące obciążenie można ustalić przy użyciu liczników wykorzystania dysku.|
|Dysk logiczny(&#42;)\Średnia czas dysku w s/Zapis|Średnie opóźnienie zapisu danych na dysku (należy wybrać dysk bazy danych jako wystąpienie).|Ta wartość powinna być mniejsza niż 10 milisekund.|Sprawdź, czy istnieje określony proces wykorzystujący dysk bazy danych znacznie intensywniej niż powinien.<br /><br />Skonsultuj się z zespołem/dostawcą magazynu, aby ustalić, czy dany dysk może obsługiwać bieżące obciążenie przy opóźnieniu mniejszym niż 10 ms. Bieżące obciążenie można ustalić przy użyciu liczników wykorzystania dysku.|
|\Dysk logiczny(&#42;)\Odczyty dysku/s|Szybkość wykonywania operacji odczytu z dysku.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny(&#42;)\Bajty odczytu dysku/s|Liczba bajtów odczytywanych z dysku w ciągu sekundy.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny&#42;\Zapisy dysku/s|Szybkość wykonywania operacji zapisu na dysku.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny(&#42;)\Bajty zapisu dysku/s|Liczba bajtów zapisywanych na dysku w ciągu sekundy.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
