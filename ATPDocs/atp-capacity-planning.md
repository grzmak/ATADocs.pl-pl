---
title: Planowanie wdrożenia usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Ułatwia zaplanowanie wdrożenia i zdecydować, ile serwerów usługi Azure ATP będzie potrzebnych do obsługi sieci
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.prod: ''
ms.assetid: da0ee438-35f8-4097-b3a1-1354ad59eb32
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9f2b8f31f88c14f67c8a03b748ac3d2fb6179a62
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783461"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="azure-atp-capacity-planning"></a>Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami
W tym artykule zawarto informacje ułatwiające określenie, ile narzędzia Azure ATP czujniki i czujniki autonomicznego należy.

## <a name="using-the-sizing-tool"></a>Korzystanie z narzędzia do określania rozmiaru
Zalecaną i najprostszą metodą ustalenia pojemności na potrzeby wdrożenia usługi Azure ATP jest użycie [narzędzie zmiany rozmiaru do usługi Azure ATP](http://aka.ms/aatpsizingtool). Uruchom narzędzie Azure ATP rozmiaru i z wyników pliku programu Excel, należy użyć następujących pól do określenia pamięci i procesora CPU używanej przez czujnik:

> [!NOTE] 
> Narzędzia do określania rozmiaru ma dwa arkusze — jeden dla usługi ATA i jeden dla usługi Azure ATP. Upewnij się, że używasz poprawne arkusza.

- Azure czujnika zaawansowanej ochrony przed zagrożeniami: dopasowanie **zajęte pakiety/s** pola w tabeli czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, w pliku wyników do **pakietów na SEKUNDĘ** pole [tabeli czujnik autonomiczny narzędzia Azure ATP](#azure-atp-sensor-sizing)lub [tabeli czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure](#azure-atp-standalone-sensor-sizing), w zależności od [wybranego typu czujnika](#choosing-the-right-sensor-type-for-your-deployment).


![Przykładowe narzędzie do planowania pojemności](media/capacity-tool.png)


Jeśli z jakiegoś powodu nie można użyć narzędzia platformy Azure do określania rozmiaru zaawansowanej ochrony przed zagrożeniami, Zbierz ręcznie informacje licznika pakietów na sekundę ze wszystkich kontrolerów domeny przez 24 godziny z krótkim interwałem zbierania (około 5 sekund). Następnie dla każdego kontrolera domeny musisz obliczyć średnią wartość dzienną i średnią z okresu o największym obciążeniu (15 minut).
Poniższe sekcje zawierają instrukcje dotyczące zbierania informacji licznika pakietów na sekundę z jednego kontrolera domeny.

## Wybieranie typu czujnika odpowiednie dla danego wdrożenia<a name="choosing-the-right-sensor-type-for-your-deployment"></a>
We wdrożeniu usługi Azure ATP dowolnej kombinacji typów czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest obsługiwane:

- Tylko usługi Azure ATP czujników
- Tylko czujników autonomiczne narzędzia Azure ATP
- Kombinacja obu bram

Podczas wybierania typu wdrożenia czujnika, należy wziąć pod uwagę następujące korzyści:

|Typ czujnika|Korzyści|Koszt|Topologia wdrożenia|Użycie kontrolera domeny|
|----|----|----|----|-----|
|Czujnik autonomiczny usługi Azure ATP|Poza wdrożenie poza pasmem utrudnia osobom atakującym odkrycie usługi Azure ATP jest obecny|Wyższe|Instalacja obok kontrolera domeny (poza pasmem)|Obsługuje maksymalnie 100 000 pakietów na sekundę|
|Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami|Nie wymaga dedykowanego serwera i konfiguracji dublowania portów|Niższe|Instalacja na kontrolerze domeny|Obsługuje maksymalnie 100 000 pakietów na sekundę|

Podejmując decyzję o ile czujników autonomiczne narzędzia Azure ATP do wdrożenia, należy wziąć pod uwagę następujące kwestie.

-   **Lasy i domeny usługi Active Directory**<br>
    Narzędzie Azure ATP można monitorować ruch z wielu domen w obrębie wielu lasów usługi Active Directory dla każdego obszaru roboczego, który tworzysz. 

-   **Dublowanie portów**<br>
    Specyfika funkcji dublowania portów mogą wymagać można wdrażać wiele czujników autonomiczne narzędzia Azure ATP na witrynę Centrum lub gałęzi danych.

-   **Wydajność**<br>
    Czujnik autonomiczny narzędzia Azure ATP może obsługiwać monitorowanie wielu kontrolerów domeny, w zależności od ilości ruchu sieciowego monitorowanych kontrolerów domeny. 


## Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami i rozmiaru czujnik autonomiczny <a name="sizing"></a>

Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure może obsługiwać monitorowanie jednego kontrolera domeny na podstawie ilości ruchu sieciowego, generowanych przez kontroler domeny. Poniższa tabela jest szacowana, końcowe kwotę, która analizuje czujnika zależy od ilości ruchu sieciowego i dystrybucja ruchu. 
> [!NOTE]
> Ma następującą pojemność procesora CPU i pamięci odnosi się do użycia własnej czujnik — nie pojemności kontrolera domeny.

|Pakiety na sekundę *|Procesor CPU (rdzenie)|Pamięć (GB)|
|----|----|-----|
|0 – 1 k|0.25|2.50|
|1k-5k|0.75|6.00|
|5k-10k|1.00|6.50|
|10k-20k|2.00|9,00|
|20k-50k|3.50|9,50|
|50k-75k |3.50|9,50|
|75k-100k|3.50 |9,50|

> [!NOTE]
> - Łączna liczba rdzeni, które będą używane przez usługi czujnika.<br>Zalecane jest, aby nie pracować rdzeni hiperwątkowych.
> - Całkowita ilość pamięci, który będzie używany przez usługi czujnika.
> -   Jeśli kontroler domeny nie ma zasobów wymaganych przez czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, nie dotyczy wydajności kontrolera domeny, ale czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure może nie działać zgodnie z oczekiwaniami.
> -   W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.
> -   Aby uzyskać optymalną wydajność, ustaw **opcji zasilania** czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure do **o wysokiej wydajności**.
> -   Wymagana jest co najmniej 2 rdzeni i 6 GB miejsca, a zalecane 10 GB, co obejmuje miejsce wymagane dla usługi Azure ATP pliki binarne i dzienniki.


## <a name="domain-controller-traffic-estimation"></a>Szacowanie ruchu kontrolera domeny

Istnieją różne narzędzia, za pomocą których można określić średnią liczbę pakietów na sekundę kontrolerów domeny. Jeśli nie masz żadnych narzędzi do określenia tej wartości, możesz użyć Monitora wydajności do zebrania wymaganych informacji.

Aby określić liczbę pakietów na sekundę, wykonaj następujące kroki na każdym kontrolerze domeny:

1.  Otwórz Monitor wydajności.

    ![Obraz przedstawiający Monitor wydajności](media/atp-traffic-estimation-1.png)

2.  Rozwiń węzeł **Zestawy modułów zbierających dane**.

    ![Obraz przedstawiający zestawy modułów zbierających dane](media/atp-traffic-estimation-2.png)

3.  Kliknij prawym przyciskiem myszy pozycję **Zdefiniowany przez użytkownika**, a następnie wybierz pozycję **Nowy** &gt; **Zestaw modułów zbierających dane**.

    ![Obraz przedstawiający nowy zestaw modułów zbierających dane](media/atp-traffic-estimation-3.png)

4.  Wprowadź nazwę dla zestawu modułów zbierających dane, a następnie wybierz pozycję **Utwórz ręcznie (zaawansowane)**.

5.  W obszarze **Jakiego typu dane chcesz uwzględnić?** wybierz pozycje **Utwórz dzienniki danych i Licznik wydajności**.

    ![Obraz przedstawiający typ danych nowego zestawu modułów zbierających dane](media/atp-traffic-estimation-5.png)

6.  W obszarze **Które liczniki wydajności chcesz rejestrować?** kliknij przycisk **Dodaj**.

7.  Rozwiń węzeł **Karta sieciowa**, wybierz pozycję **Pakiety/s**, a następnie wybierz odpowiednie wystąpienie. Jeśli nie masz pewności, możesz wybrać pozycję **&lt;Wszystkie wystąpienia&gt;**, kliknąć przycisk **Dodaj**, a następnie kliknąć przycisk **OK**.

    > [!NOTE]
    > Aby wykonać tę operację w wierszu polecenia, uruchom polecenie `ipconfig /all` w celu wyświetlenia nazwy karty i konfiguracji.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/atp-traffic-estimation-7.png)

8.  Zmiana **interwał próbkowania** do **pięć sekund**.

9. Ustaw lokalizację, w której mają być zapisywane dane.

10. W obszarze **utworzyć zestaw modułów zbierających dane**, wybierz opcję **Uruchom ten zestaw modułów zbierających dane teraz**i kliknij przycisk **Zakończ**.

    Powinien zostać wyświetlony utworzony zestaw modułów zbierających dane z zielonym trójkątem wskazującym, że zestaw działa.

11. Po 24 godzinach zatrzymaj zestaw modułów zbierających dane, klikając go prawym przyciskiem myszy, a następnie wybierając polecenie **Zatrzymaj**.

    ![Obraz przedstawiający zatrzymywanie działania zestawu modułów zbierających dane](media/atp-traffic-estimation-12.png)

12. W Eksploratorze plików przejdź do folderu, w którym zapisano plik blg, a następnie kliknij go dwukrotnie w celu otworzenia w Monitorze wydajności.

13. Wybierz licznik Pakiety/s i zapisz wartość średnią oraz maksymalną.

    ![Obraz przedstawiający licznik Pakiety/s](media/atp-traffic-estimation-14.png)



## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Architektura Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-architecture.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
