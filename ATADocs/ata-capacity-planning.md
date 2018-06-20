---
title: Planowanie wdrożenia usługi Advanced Threat Analytics| Dokumentacja firmy Microsoft
description: Ułatwia zaplanowanie wdrożenia i określenie, ile serwerów usługi ATA będzie potrzebnych do obsługi sieci
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: ''
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e58fe62fc655fed8f17ae800dda20e022e198a26
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010027"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="ata-capacity-planning"></a>Planowanie pojemności usługi ATA
Ten artykuł ułatwia określenie, ile serwerów usługi ATA są niezbędne do monitorowania sieci. Pomaga ustalić ile bram usługi ATA i/lub bram ATA Lightweight Gateway można potrzeby oraz jaka pojemność serwera dla Centrum usługi ATA i bram usługi ATA.

> [!NOTE] 
> Centrum usługi ATA można wdrożyć na dowolnym dostawcy IaaS, jeśli są spełnione wymagania dotyczące wydajności opisane w tym artykule.

## <a name="using-the-sizing-tool"></a>Korzystanie z narzędzia do określania rozmiaru
Zalecaną i najprostszą metodą ustalenia pojemności na potrzeby wdrożenia usługi ATA jest użycie [narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool). Uruchom narzędzie do określania rozmiaru usługi ATA i określ wymaganą pojemność usługi ATA za pomocą następujących pól wyników w pliku programu Excel:

- Procesor i pamięć centrum usługi ATA: dopasuj wartość pola **Zajęte pakiety/s** w pliku wyników tabeli centrum usługi ATA do wartości pola **PAKIETY/S** w [tabeli centrum usługi ATA](#ata-center-sizing).

- Magazyn centrum usługi ATA: dopasuj wartość pola **Średnia liczba pakietów/s** w pliku wyników tabeli centrum usługi ATA do wartości pola **PAKIETY/S** w [tabeli centrum usługi ATA](#ata-center-sizing).
- Brama usługi ATA: dopasuj wartość pola **Zajęte pakiety/s** w tabeli bramy usługi ATA w pliku wyników do wartości pola **PAKIETY/S** w [tabeli bramy usługi ATA](#ata-gateway-sizing) lub [tabeli uproszczonej bramy usługi ATA](#ata-lightweight-gateway-sizing) w zależności od [wybranego typu bramy](#choosing-the-right-gateway-type-for-your-deployment).


![Przykładowe narzędzie do planowania pojemności](media/capacity tool.png)


> [!NOTE]
> Ponieważ różnych środowiskach zależą i ma wiele cech ruchu sieci specjalnych i nieoczekiwany po początkowym wdrożeniu usługi ATA i uruchom narzędzie ustalania rozmiaru, może być konieczne dostosowanie i dostrojenia wdrożenia pojemności.


Jeśli z jakiegoś powodu nie możesz użyć narzędzia do określania rozmiaru usługi ATA, zbierz ręcznie informacje licznika liczby pakietów na sekundę ze wszystkich kontrolerów domeny z okresu 24 godzin i z krótkim interwałem zbierania (około 5 sekund). Następnie dla każdego kontrolera domeny musisz obliczyć średnią wartość dzienną i średnią z okresu o największym obciążeniu (15 minut).
Poniższe sekcje zawierają instrukcje dotyczące zbierania informacji licznika pakietów na sekundę z jednego kontrolera domeny.


> [!NOTE]
> Ponieważ różnych środowiskach zależą i ma wiele cech ruchu sieci specjalnych i nieoczekiwany po początkowym wdrożeniu usługi ATA i uruchom narzędzie ustalania rozmiaru, może być konieczne dostosowanie i dostrojenia wdrożenia pojemności.


### <a name="ata-center-sizing"></a>Ustalanie rozmiaru centrum usługi ATA
W celu wykonania analizy behawioralnej użytkowników zaleca się, aby centrum usługi ATA dysponowało danymi z co najmniej 30 dni.
 

|Pakiety na sekundę ze wszystkich kontrolerów domeny|Procesor CPU (rdzenie&#42;)|Pamięć (GB)|Przestrzeń dyskowa bazy danych dziennie (GB)|Przestrzeń dyskowa bazy danych miesięcznie (GB)|Operacje we/wy na sekundę&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1000|2|32|0,3|9|30 (100)
|40,000|4|48|12|360|500 (750)
|200 000|8|64|60|1800|1000 (1500)
|400 000|12|96|120|3,600|2000 (2500)
|750 000|24|112|225|6750|2500 (3000)
|1 000 000|40|128|300|9000|4,000 (5,000)

&#42;Dotyczy rdzeni fizycznych, a nie rdzeni hiperwątkowych.

&#42;&#42;Wartości średnie (wartości szczytowe)
> [!NOTE]
> -   Centrum usługi ATA może obsługiwać maksymalnie 1 mln pakietów na sekundę ze wszystkich monitorowanych kontrolerów domeny łącznie. W niektórych środowiskach tego samego Centrum usługi ATA może obsługiwać ruch ogólnej, jest większa niż 1M. Skontaktuj się z nami pod adresem askcesec@microsoft.com, aby uzyskać pomoc w przypadku pracy w takich środowiskach.
> -   Jeśli wolne miejsce osiągnie wartość co najmniej 20% lub 200 GB, dane z najstarszej kolekcji jest usunięte. Alert zostanie zarejestrowany, jeśli nie jest możliwe zmniejszenie pomyślnie zbierania danych na tym poziomie.  Usługi ATA będą nadal działać dopóki próg 5% lub 50 GB wolnego miejsca.  W tym momencie usługi ATA zostanie zatrzymane, wypełnianie bazy danych, a dodatkowe alertu zostaną wystawione.
> - Centrum usługi ATA można wdrożyć na dowolnym dostawcy IaaS, jeśli są spełnione wymagania dotyczące wydajności opisane w tym artykule.
> -   Opóźnienie magazynu dla działań odczytu i zapisu powinno być niższe niż 10 ms.
> -   Stosunek między działaniami odczytu i zapisu to około 1:3 poniżej 100 000 pakietów na sekundę i 1:6 powyżej 100 000 pakietów na sekundę.
> -   W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.
> -   Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** centrum usługi ATA na wartość **Wysoka wydajność**.<br>
> -   Podczas pracy na serwerze fizycznym baza danych usługi ATA wymaga **wyłączenia** obsługi niejednolitego dostępu do pamięci (NUMA) w systemie BIOS. Technologia NUMA może być nazywana w Twoim systemie przeplataniem węzłów. W tym przypadku należy **włączyć** przeplatanie węzłów, aby wyłączyć technologię NUMA. Aby uzyskać więcej informacji zobacz dokumentację systemu BIOS. Nie jest to istotne w przypadku uruchomienia centrum usługi ATA na serwerze wirtualnym.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Wybieranie odpowiedniego typu bramy dla danego wdrożenia
We wdrożeniu ATA obsługiwane są dowolne kombinacje typów bramy ATA:

- Tylko bramy usługi ATA
- Tylko uproszczone bramy usługi ATA
- Kombinacja obu bram

Podczas wybierania typu wdrożenia bramy należy uwzględnić następujące korzyści:

|Typ bramy|Korzyści|Koszt|Topologia wdrożenia|Użycie kontrolera domeny|
|----|----|----|----|-----|
|Brama usługi ATA|Wdrożenie poza pasmem utrudnia osobom atakującym odkrycie usługi ATA|Wyższe|Instalacja obok kontrolera domeny (poza pasmem)|Obsługuje maksymalnie 50 000 pakietów na sekundę|
|Uproszczona brama usługi ATA|Nie wymaga dedykowanego serwera i konfiguracji dublowania portów|Niższe|Instalacja na kontrolerze domeny|Obsługuje maksymalnie 10 000 pakietów na sekundę|

Poniżej przedstawiono przykładowe scenariusze, w których kontrolery domeny powinny być objęte przez uproszczoną bramę usługi ATA:


- Oddziały

- Wirtualne kontrolery domeny wdrożone w chmurze (IaaS)


Poniżej przedstawiono przykładowe scenariusze, w których kontrolery domeny powinny być objęte przez bramę usługi ATA:


- Główne centra danych (z kontrolerami domeny obsługującymi ponad 10 000 pakietów na sekundę)


### <a name="ata-lightweight-gateway-sizing"></a>Ustalanie rozmiaru uproszczonej bramy usługi ATA

Uproszczona brama usługi ATA może obsługiwać monitorowanie jednego kontrolera domeny w oparciu o ilość ruchu sieciowego generowanego przez kontroler domeny. 


|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1000|2|6|
|5000|6|16|
    |10 000|10|24|

&#42;Łączna liczba pakietów na sekundę w kontrolerze domeny monitorowanym przez daną uproszczoną bramę usługi ATA.

&#42;&#42;Łączna liczba zainstalowanych w kontrolerze domeny rdzeni innych niż hiperwątkowe.<br>Chociaż hiperwątkowość jest dopuszczalna w przypadku użycia uproszczonych bram usługi ATA, podczas planowania pojemności należy policzyć faktyczną liczbę rdzeni, a nie rdzeni hiperwątkowych.

&#42;&#42;&#42;Łączna ilość pamięci zainstalowanej w kontrolerze domeny.

> [!NOTE]   
> -   Jeśli kontroler domeny nie ma zasobów wymaganych przez uproszczoną bramę usługi ATA, nie będzie to miało wpływu na wydajność kontrolera domeny, ale uproszczona brama usługi ATA może nie działać zgodnie z oczekiwaniami.
> -   W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.
> -   Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** uproszczonej bramy usługi ATA na wartość **Wysoka wydajność**.
> -   Wymagane jest co najmniej 5 GB miejsca i 10 GB jest zalecane miejsce wymagane do plików binarnych usługi ATA, w tym [dzienniki usługi ATA](troubleshooting-ata-using-logs.md), i [dzienników wydajności](troubleshooting-ata-using-perf-counters.md).


### <a name="ata-gateway-sizing"></a>Ustalanie rozmiaru bramy usługi ATA

Podczas podejmowania decyzji o liczbie bram usługi ATA, które mają zostać wdrożone, należy wziąć pod uwagę następujące zagadnienia.

-   **Lasy i domeny usługi Active Directory**<br>
    Usługa ATA może monitorować ruch z wielu domen pochodzących z jednego lasu usługi Active Directory. Monitorowanie wielu lasów usługi Active Directory wymaga oddzielnych wdrożeń usługi ATA. Nie należy konfigurować pojedynczego wdrożenia usługi ATA do monitorowania ruchu sieciowego z kontrolerów domeny znajdujących się w różnych lasach.

-   **Dublowanie portów**<br>
Zagadnienia związane z dublowaniem portów mogą wymagać wdrożenia wielu bram usługi ATA dla centrum danych lub oddziału.

-   **Wydajność**<br>
    Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego monitorowanych kontrolerów domeny. 
<br>



|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)|
|---------------------------|-------------------------|---------------|
|1000|1|6|
|5,000|2|10|
|10 000|3|12|
|20,000|6|24|
|50 000|16|48|
&#42;Średnia łączna liczba pakietów na sekundę ze wszystkich kontrolerów domeny monitorowanych przez daną bramę usługi ATA w najbardziej zajętej godzinie dnia.

&#42;Łączny ruch objęty funkcją dublowania portów kontrolera domeny nie może przekraczać wydajności karty sieciowej przechwytywania w bramie usługi ATA.

&#42;&#42;Hiperwątkowość musi być wyłączona.

> [!NOTE] 
> -   Pamięć dynamiczna nie jest obsługiwana.
> -   Aby uzyskać optymalną wydajność, ustaw pozycję **Opcja zasilania** bramy usługi ATA na wartość **Wysoka wydajność**.
> -   Wymagane jest co najmniej 5 GB miejsca i 10 GB jest zalecane miejsce wymagane do plików binarnych usługi ATA, w tym [dzienniki usługi ATA](troubleshooting-ata-using-logs.md), i [dzienników wydajności](troubleshooting-ata-using-perf-counters.md).



## <a name="related-videos"></a>Powiązane pliki wideo
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Architektura usługi ATA](ata-architecture.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
