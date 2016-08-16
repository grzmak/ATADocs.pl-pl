---
title: "Planowanie wdrożenia usługi ATA | Microsoft ATA"
description: "Ułatwia zaplanowanie wdrożenia i określenie, ile serwerów usługi ATA będzie potrzebnych do obsługi sieci"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: 
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: e0174ecac39b2a8cd469ed698853c447a85e4251


---

# Planowanie pojemności usługi ATA
Ten temat ułatwia określenie, ile serwerów usługi ATA będzie potrzebnych do monitorowania sieci, ile będzie potrzebnych bram usługi ATA i/lub bram ATA Lightweight Gateway oraz jaka pojemność serwera będzie wymagana dla centrum usługi ATA i bram usługi ATA.

##Korzystanie z narzędzia do określania rozmiaru
Zalecaną i najprostszą metodą ustalenia pojemności na potrzeby wdrożenia usługi ATA jest użycie [narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool). Uruchom narzędzie do określania rozmiaru usługi ATA i określ wymaganą pojemność usługi ATA za pomocą następujących pól wyników w pliku programu Excel:

- Procesor CPU i pamięć centrum usługi ATA: dopasuj wartość pola **Zajęte pakiety/s** w tabeli centrum usługi ATA w pliku wyników do wartości pola **PAKIETY/S** w [tabeli centrum usługi ATA](#ata-center-sizing).

- Magazyn centrum usługi ATA: dopasuj wartość pola **Średnia liczba pakietów/s** w tabeli centrum usługi ATA w pliku wyników do wartości pola **PAKIETY/S** w [tabeli centrum usługi ATA](#ata-center-sizing).
- Brama usługi ATA: dopasuj wartość pola **Zajęte pakiety/s** w tabeli bramy usługi ATA w pliku wyników do wartości pola **PAKIETY/S** w [tabeli bramy usługi ATA](#ata-gateway-sizing) lub [tabeli ATA Lightweight Gateway](#ata-lightweight-gateway-sizing) w zależności od [wybranego typu bramy](#choosing-the-right-gateway-type-for-your-deployment).


![Przykładowe narzędzie do planowania pojemności](media/capacity tool.png)



Jeśli z jakiegoś powodu nie możesz użyć narzędzia do określania rozmiaru usługi ATA, musisz ręcznie zebrać informacje licznika pakietów na sekundę ze wszystkich kontrolerów domeny z okresu 24 godzin z bardzo krótkim interwałem zbierania (około 5 sekund). Następnie dla każdego kontrolera domeny musisz obliczyć średnią wartość dzienną i średnią z okresu o największym obciążeniu (15 minut).
Poniższe sekcje zawierają instrukcje dotyczące zbierania informacji licznika pakietów na sekundę z jednego kontrolera domeny.



### Ustalanie rozmiaru centrum usługi ATA
W celu wykonania analizy behawioralnej użytkowników zaleca się, aby centrum usługi ATA dysponowało danymi z co najmniej 30 dni. Wymagana ilość miejsca na dysku dla bazy danych usługi ATA na każdy kontroler domeny jest zdefiniowana poniżej. Jeśli istnieje wiele kontrolerów domeny, zsumuj ilość miejsca na dysku wymaganego przez każdy kontroler domeny, aby obliczyć łączną ilość miejsca wymaganego dla bazy danych usługi ATA.
> [!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)|Przestrzeń dyskowa bazy danych dziennie (GB)|Przestrzeń dyskowa bazy danych miesięcznie (GB)|Operacje we/wy na sekundę&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1000|2|32|0,3|9|30 (100)
|10 000|4|48|3|90|200 (300)
|40 000|8|64|12|360|500 (1000)
|100 000|12|96|30|900|1000 (1500)
|400 000|40|128|120|1800|2000 (2500)
&#42;Łączna dzienna średnia liczba pakietów na sekundę ze wszystkich kontrolerów domeny monitorowanych przez wszystkie bramy usługi ATA.

&#42;&#42;Dotyczy rdzeni fizycznych, a nie rdzeni hiperwątkowych.

&#42;&#42;&#42;Wartość średnia (szczytowa)
> [!NOTE]
> -   Centrum usługi ATA może obsługiwać maksymalnie 400 000 ramek na sekundę zagregowanych ze wszystkich monitorowanych kontrolerów domeny.
> -   Podane wielkości przestrzeni dyskowej to wartości netto. Zawsze należy uwzględnić przyszły wzrost oraz zapewnić co najmniej 20% wolnego miejsca na dysku, na którym znajduje się baza danych.
> -   Jeśli wolne miejsce osiągnie wartość minimalną (20% lub 100 GB), zostaną usunięte dane z najstarszej kolekcji. Ta operacja będzie powtarzana, dopóki nie pozostaną dane tylko z dwóch dni bądź jedynie 5% lub 50 GB wolnego miejsca. W takim przypadku zbieranie danych przestanie działać.
> -  Opóźnienie magazynu dla działań odczytu i zapisu powinno być niższe niż 10 ms.
> -  Stosunek między działaniami odczytu i zapisu to około 1:3 poniżej 100 000 pakietów na sekundę i 1:6 powyżej 100 000 pakietów na sekundę.

## Wybieranie odpowiedniego typu bramy dla danego wdrożenia
We wdrożeniu ATA obsługiwane są dowolne kombinacje typów bramy ATA:

- Wyłącznie bramy usługi ATA
- Wyłącznie bramy ATA Lightweight Gateway
- Kombinacja obu bram

Podczas wybierania typu wdrożenia bramy należy uwzględnić następujące kwestie:

|Typ bramy|Korzyści|Koszt|Topologia wdrożenia|Użycie kontrolera domeny|
|----|----|----|----|-----|
|Brama usługi ATA|Wdrożenie poza pasmem utrudnia osobom atakującym odkrycie usługi ATA|Wyższe|Instalacja obok kontrolera domeny (poza pasmem)|Obsługuje maksymalnie 50 000 pakietów na sekundę|
|Brama ATA Lightweight Gateway|Nie wymaga dedykowanego serwera i konfiguracji dublowania portów|Niższe|Instalacja na kontrolerze domeny|Obsługuje maksymalnie 10 000 pakietów na sekundę|

Poniżej przedstawiono przykładowe scenariusze, w których kontrolery domeny powinny być objęte przez bramę ATA Lightweight Gateway:


- Oddziały

- Wirtualne kontrolery domeny wdrożone w chmurze (IaaS)


Poniżej przedstawiono przykładowe scenariusze, w których kontrolery domeny powinny być objęte przez bramę usługi ATA:


- Główne centra danych (z kontrolerami domeny obsługującymi ponad 10 000 pakietów na sekundę)


### Ustalanie rozmiaru bramy ATA Lightweight Gateway

Brama ATA Lightweight Gateway może obsługiwać monitorowanie jednego kontrolera domeny w oparciu o ilość ruchu sieciowego generowanego przez kontroler domeny. 
> [!NOTE] 
> W przypadku uruchamiania jako pamięci dynamicznej maszyny wirtualnej lub innej pamięci funkcja przydziału balonowego nie jest obsługiwana.

|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1000|2|6|
|5000|6|16|
    |10 000|10|24|

&#42;Łączna liczba pakietów na sekundę w kontrolerze domeny monitorowanym przez daną bramę ATA Lightweight Gateway.

&#42;&#42;Łączna liczba zainstalowanych w kontrolerze domeny rdzeni innych niż hiperwątkowe.<br>Chociaż hiperwątkowość jest dopuszczalna w przypadku użycia bram ATA Lightweight Gateway, podczas planowania pojemności należy policzyć faktyczną liczbę rdzeni, a nie rdzeni hiperwątkowych.

&#42;&#42;&#42;Łączna ilość pamięci zainstalowanej w kontrolerze domeny.
> [!NOTE]   
> Jeśli kontroler domeny nie ma niezbędnej ilości zasobów wymaganych przez bramę ATA Lightweight Gateway, nie będzie to miało wpływu na wydajność kontrolera domeny, ale brama ATA Lightweight Gateway może nie działać zgodnie z oczekiwaniami.


### Ustalanie rozmiaru bramy usługi ATA

Podczas podejmowania decyzji o liczbie bram usługi ATA, które mają zostać wdrożone, należy wziąć pod uwagę następujące informacje.

-   **Lasy i domeny usługi Active Directory**<br>
    Usługa ATA może monitorować ruch z wielu domen pochodzących z jednego lasu usługi Active Directory. Monitorowanie wielu lasów usługi Active Directory wymaga oddzielnych wdrożeń usługi ATA. Pojedyncze wdrożenie usługi ATA nie powinno być konfigurowane do monitorowania ruchu sieciowego z kontrolerów domeny znajdujących się w różnych lasach.

-   **Dublowanie portów**<br>
Zagadnienia związane z dublowaniem portów mogą wymagać wdrożenia wielu bram usługi ATA dla centrum danych lub oddziału.

-   **Pojemność**<br>
    Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego monitorowanych kontrolerów domeny. 
<br>

> [!NOTE] 
> Pamięć dynamiczna nie jest obsługiwana.

|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)|
|---------------------------|-------------------------|---------------|
|1000|1|6|
|5000|2|10|
|10 000|3|12|
|20 000|6|24|
|50 000|16|48|
&#42;Średnia łączna liczba pakietów na sekundę ze wszystkich kontrolerów domeny monitorowanych przez daną bramę usługi ATA w najbardziej zajętej godzinie dnia.

&#42;Łączny ruch objęty funkcją dublowania portów kontrolera domeny nie może przekraczać wydajności karty sieciowej przechwytywania w bramie usługi ATA.

&#42;&#42;Hiperwątkowość musi być wyłączona.



## Szacowanie ruchu kontrolera domeny
Istnieją różne narzędzia, za pomocą których można określić średnią liczbę pakietów na sekundę kontrolerów domeny. Jeśli nie masz żadnych narzędzi do określenia tej wartości, możesz użyć Monitora wydajności do zebrania wymaganych informacji.

Aby określić liczbę pakietów na sekundę, wykonaj następujące czynności na każdym kontrolerze domeny:

1.  Otwórz Monitor wydajności.

    ![Obraz przedstawiający Monitor wydajności](media/ATA-traffic-estimation-1.png)

2.  Rozwiń węzeł **Zestawy modułów zbierających dane**.

    ![Obraz przedstawiający zestawy modułów zbierających dane](media/ATA-traffic-estimation-2.png)

3.  Kliknij prawym przyciskiem myszy pozycję **Zdefiniowany przez użytkownika**, a następnie wybierz pozycję **Nowy** &gt; **Zestaw modułów zbierających dane**.

    ![Obraz przedstawiający nowy zestaw modułów zbierających dane](media/ATA-traffic-estimation-3.png)

4.  Wprowadź nazwę dla zestawu modułów zbierających dane, a następnie wybierz pozycję **Utwórz ręcznie (zaawansowane)**.

5.  W obszarze **Jakiego typu dane chcesz uwzględnić?** wybierz pozycję **Utwórz dzienniki danych i Licznik wydajności**.

    ![Obraz przedstawiający typ danych nowego zestawu modułów zbierających dane](media/ATA-traffic-estimation-5.png)

6.  W obszarze **Które liczniki wydajności chcesz rejestrować?** kliknij przycisk **Dodaj**.

7.  Rozwiń węzeł **Karta sieciowa**, wybierz pozycję **Pakiety/s**, a następnie wybierz odpowiednie wystąpienie. Jeśli nie masz pewności, możesz wybrać pozycję **&lt;Wszystkie wystąpienia&gt;**, kliknąć przycisk **Dodaj**, a następnie kliknąć przycisk **OK**.

    > [!NOTE]
    > W tym celu w wierszu polecenia uruchom polecenie `ipconfig /all`, aby wyświetlić nazwę karty i konfigurację.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-traffic-estimation-7.png)

8.  Zmień wartość pozycji **Interwał próbkowania** na **1 sekundę**.

9. Ustaw lokalizację, w której mają być zapisywane dane.

10. W obszarze **Czy utworzyć zestaw modułów zbierających dane?** wybierz polecenie **Uruchom teraz ten zestaw modułów zbierających dane**, a następnie kliknij przycisk **Zakończ**.

    Powinien zostać wyświetlony właśnie utworzony zestaw modułów zbierających dane z zielonym trójkątem wskazującym, że zestaw działa.

11. Po 24 godzinach zatrzymaj zestaw modułów zbierających dane, klikając go prawym przyciskiem myszy, a następnie wybierając polecenie **Zatrzymaj**.

    ![Obraz przedstawiający zatrzymywanie działania zestawu modułów zbierających dane](media/ATA-traffic-estimation-12.png)

12. W Eksploratorze plików przejdź do folderu, w którym zapisano plik blg, a następnie kliknij go dwukrotnie w celu otworzenia w Monitorze wydajności.

13. Wybierz licznik Pakiety/s i zapisz wartość średnią oraz maksymalną.

    ![Obraz przedstawiający licznik Pakiety/s](media/ATA-traffic-estimation-14.png)

## Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Architektura usługi ATA](ata-architecture.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


