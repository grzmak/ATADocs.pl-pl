---
# required metadata

title: Rozwiązywanie problemów z usługą ATA przy użyciu liczników wydajności | Microsoft Advanced Threat Analytics
description: W tym temacie opisano sposób rozwiązywania problemów z usługą ATA przy użyciu liczników wydajności.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rozwiązywanie problemów z usługą ATA przy użyciu liczników wydajności
Liczniki wydajności usługi ATA zapewniają wgląd w funkcjonowanie poszczególnych składników usługi ATA. Składniki usługi ATA przetwarzają dane sekwencyjnie, dlatego wystąpienie problemu powoduje reakcję łańcuchową prowadzącą do pominięcia ruchu sieciowego. Aby rozwiązać problem, należy ustalić, który składnik go powoduje i usunąć jego przyczynę na początku sekwencji.
    Aby uzyskać informacje na temat przepływu wewnętrznych składników usługi ATA, zobacz [Architektura usługi ATA](/advanced-threat-analytics/understand-explore/ata-architecture).

**Proces składnika usługi ATA**:

1.  Gdy składnik osiągnie maksymalny rozmiar, uniemożliwia poprzedniemu składnikowi wysyłanie do niego kolejnych jednostek.

2.  Wtedy poprzedni składnik zacznie zwiększać **swój** rozmiar, aż zablokuje poprzedzający go składnik, uniemożliwiając wysyłanie kolejnych jednostek.

3.  Ten proces jest kontynuowany i prowadzi do początkowego składnika NetworkListener, który będzie pomijać ruch sieciowy, gdy nie będzie już mógł przekazywać jednostek.

4. Korzystając z danych liczników wydajności, można zrozumieć funkcjonowanie poszczególnych składników.

## Liczniki wydajności bramy usługi ATA
Możesz obserwować stan wydajności bramy usługi ATA w czasie rzeczywistym, dodając liczniki wydajności bramy usługi ATA.
Aby to zrobić, należy otworzyć „Monitor wydajności” i dodać wszystkie liczniki dla bramy usługi ATA. Nazwa obiektu liczników wydajności to „Brama usługi Microsoft ATA”.

![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-performance-counters.png)

Oto lista głównych liczników bramy usługi ATA, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Liczba komunikatów analizatora przechwytywanych przez składnik NetworkListener na sekundę|Ilość ruchu sieciowego przetwarzanego przez bramę usługi ATA w ciągu sekundy.|Brak wartości progowej.|Ułatwia ustalenie ilości ruchu sieciowego analizowanego przez bramę usługi ATA.|
|Liczba pominiętych komunikatów przechwytywanych przez składnik NetworkListener na sekundę|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Liczba pominiętych buforów czasu rzeczywistego ETW przechwytywanych przez składnik NetworkListener na sekundę|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Liczba pominiętych buforów dziennika ETW przechwytywanych przez składnik NetworkListener na sekundę|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Liczba pominiętych zdarzeń ETW przechwytywanych przez składnik NetworkListener na sekundę|Ilość ruchu sieciowego pomijanego przez bramę usługi ATA w ciągu sekundy.|Ta wartość powinna zawsze wynosić zero (dopuszczalne jest krótkie zwiększenie tej wartości).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku n danych komunikatu NetworkActivityTranslator|Ilość ruchu sieciowego znajdującego się w kolejce w celu translacji na działania w sieci.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 100 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku działań EntityResolver|Liczba działań w sieci znajdujących się w kolejce w celu rozwiązania.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku partii jednostek EntitySender|Liczba działań w sieci znajdujących się w kolejce w celu wysłania do centrum usługi ATA.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 1 000 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Czas wysyłania partii EntitySender|Ilość czasu, jaką zajęło wysłanie ostatniej partii.|W większości przypadków ta wartość powinna być mniejsza niż 1000 milisekund.|Sprawdź, czy nie wystąpiły problemy z siecią między bramą usługi ATA a centrum usługi ATA.|

> [!NOTE]
> -   Wartości liczników czasu są podawane w milisekundach.
> -   Czasami wygodniej jest monitorować pełną listę liczników przy użyciu wykresu „Raport” (przykład: monitorowanie wszystkich liczników w czasie rzeczywistym).

## Liczniki wydajności centrum usługi ATA
Możesz obserwować stan wydajności centrum usługi ATA w czasie rzeczywistym, dodając liczniki wydajności centrum usługi ATA.

Aby to zrobić, należy otworzyć „Monitor wydajności” i dodać wszystkie liczniki dla centrum usługi ATA. Nazwa obiektu liczników wydajności to „Centrum usługi Microsoft ATA”.

![Dodawanie liczników wydajności centrum usługi ATA](media/ATA-Gateway-perf-counters.png)

Oto lista głównych liczników centrum usługi ATA, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Rozmiar bloku partii jednostek EntityReceiver|Liczba partii jednostek umieszczonych w kolejce przez centrum usługi ATA.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 100).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener.  Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku działań w sieci NetworkActivityProcessor|Liczba działań w sieci znajdujących się w kolejce w celu przetworzenia.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku działań w sieci EntityProfiler|Liczba działań w sieci znajdujących się w kolejce w celu profilowania.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 10 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Rozmiar bloku &#42; CenterDatabaseClient|Liczba działań w sieci określonego typu znajdujących się w kolejce w celu zapisania w bazie danych.|Ta wartość powinna być mniejsza niż wartość maksymalna – 1 (domyślna wartość maksymalna: 50 000).|Sprawdź, czy jakikolwiek składnik osiągnął maksymalny rozmiar i blokuje poprzednie składniki, aż do składnika NetworkListener. Zobacz **Proces składnika usługi ATA** powyżej.<br /><br />Sprawdź, czy nie wystąpił problem z procesorem CPU lub pamięcią.|
|Czas wykrywania DetectionEngine|Łączny czas trwania ostatniego pełnego cyklu wykrywania deterministycznego.|Ta wartość powinna być mniejsza niż 900 000 (15 minut).|Sprawdź, czy nie wystąpił problem z procesorem CPU, pamięcią lub magazynem.|

> [!NOTE]
> -   Wartości liczników czasu są podawane w milisekundach.
> -   Czasami wygodniej jest monitorować pełną listę liczników przy użyciu wykresu Raport (przykład: monitorowanie wszystkich liczników w czasie rzeczywistym).

## Liczniki systemu operacyjnego
Oto lista głównych liczników systemu operacyjnego, na które należy zwrócić uwagę:

|Licznik|Opis|Próg|Rozwiązywanie problemów|
|-----------|---------------|-------------|-------------------|
|Procesor(_Total)\Czas procesora (%)|Procent czasu, który upłynął, przeznaczony przez procesor na wykonywanie wątku czynnego.|Przeciętnie mniej niż 80%.|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\Czas procesora (%)” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|System\Przełączenia kontekstu/s|Łączna szybkość przełączania wątków we wszystkich procesorach.|Mniej niż 5000&#42; rdzeni (fizycznych).|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\Czas procesora (%)” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|System\Długość kolejki procesora|Liczba wątków gotowych do wykonania i oczekujących na zaplanowanie.|Mniej niż 5&#42; rdzeni (fizycznych).|Sprawdź, czy istnieje proces zużywający znacznie większą ilość czasu procesora niż powinien.<br /><br />Dodaj więcej procesorów.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.<br /><br />Licznik „Procesor(_Total)\Czas procesora (%)” może być mniej dokładny w przypadku serwerów wirtualnych, na których bardziej dokładne pomiary braku mocy procesora umożliwia licznik „System\Długość kolejki procesora”.|
|Pamięć\Dostępna pamięć (MB)|Ilość pamięci fizycznej (RAM) dostępnej do przydzielenia.|Ta wartość powinna być większa niż 512.|Sprawdź, czy istnieje proces zużywający znacznie większą ilość pamięci fizycznej niż powinien.<br /><br />Zwiększ ilość pamięci fizycznej.<br /><br />Zmniejsz ilość ruchu sieciowego przypadającą na serwer.|
|Dysk logiczny(&#42;)\Średnia wartość operacji dysku na sek./odczyt|Średnie opóźnienie odczytu danych z dysku (należy wybrać dysk bazy danych jako wystąpienie).|Ta wartość powinna być mniejsza niż 10 milisekund.|Sprawdź, czy istnieje określony proces wykorzystujący dysk bazy danych znacznie intensywniej niż powinien.<br /><br />Skonsultuj się z zespołem/dostawcą magazynu, aby ustalić, czy dany dysk może obsługiwać bieżące obciążenie przy opóźnieniu mniejszym niż 10 ms. Bieżące obciążenie można ustalić przy użyciu liczników wykorzystania dysku.|
|Dysk logiczny(&#42;)\Średni czas dysku na sek./zapis|Średnie opóźnienie zapisu danych na dysku (należy wybrać dysk bazy danych jako wystąpienie).|Ta wartość powinna być mniejsza niż 10 milisekund.|Sprawdź, czy istnieje określony proces wykorzystujący dysk bazy danych znacznie intensywniej niż powinien.<br /><br />Skonsultuj się z zespołem/dostawcą magazynu, aby ustalić, czy dany dysk może obsługiwać bieżące obciążenie przy opóźnieniu mniejszym niż 10 ms. Bieżące obciążenie można ustalić przy użyciu liczników wykorzystania dysku.|
|\Dysk logiczny(&#42;)\Odczyty dysku/s|Szybkość wykonywania operacji odczytu z dysku.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny(&#42;)\Bajty odczytu dysku/s|Liczba bajtów odczytywanych z dysku w ciągu sekundy.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny(&#42;)\Zapisy dysku/s|Szybkość wykonywania operacji zapisu na dysku.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|
|\Dysk logiczny(&#42;)\Bajty zapisu dysku/s|Liczba bajtów zapisywanych na dysku w ciągu sekundy.|Brak wartości progowej.|Liczniki wykorzystania dysku zapewniają szczegółowe informacje podczas rozwiązywania problemów z opóźnieniem magazynu.|


<!--HONumber=Apr16_HO4-->


