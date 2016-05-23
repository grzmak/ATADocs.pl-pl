---
# required metadata

title: Planowanie pojemności usługi ATA | Microsoft Advanced Threat Analytics
description: Ułatwia określenie, ile serwerów usługi ATA będzie potrzebnych do obsługi sieci
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planowanie pojemności usługi ATA
Informacje zawarte w tym temacie ułatwiają określenie, ile serwerów usługi ATA będzie potrzebnych do obsługi sieci.

## Ustalanie rozmiaru centrum usługi ATA
W celu wykonania analizy behawioralnej użytkowników zaleca się, aby centrum usługi ATA dysponowało danymi z co najmniej 30 dni. Wymagana ilość miejsca na dysku dla bazy danych usługi ATA na każdy kontroler domeny jest zdefiniowana poniżej. Jeśli istnieje wiele kontrolerów domeny, zsumuj ilość miejsca na dysku wymaganego przez każdy kontroler domeny, aby obliczyć łączną ilość miejsca wymaganego dla bazy danych usługi ATA.

|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)|Przestrzeń dyskowa systemu operacyjnego (GB)|Przestrzeń dyskowa bazy danych dziennie (GB)|Przestrzeń dyskowa bazy danych miesięcznie (GB)|Operacje we/wy na sekundę&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1000|4|48|200|1.5|45|30 (100)
|10 000|4|48|200|15|450|200 (300)
|40 000|8|64|200|60|1800|500 (1000)
|100 000|12|96|200|150|4500|1000 (1500)
|200 000|16|128|200|300|9000|2000 (2500)
&#42;Łączna dzienna średnia liczba pakietów na sekundę ze wszystkich kontrolerów domeny monitorowanych przez wszystkie bramy usługi ATA.

&#42;&#42;Dotyczy rdzeni fizycznych, a nie rdzeni hiperwątkowych.

&#42;&#42;&#42;Wartość średnia (szczytowa)
> [!NOTE]
> -   Centrum usługi ATA może obsługiwać maksymalnie 200 000 ramek na sekundę zagregowanych ze wszystkich monitorowanych kontrolerów domeny.
> -   W przypadku dużych wdrożeń (od około 100 000 pakietów na sekundę) wymagane jest umieszczenie dziennika bazy danych na innym dysku niż baza danych.
> -   Podane wielkości przestrzeni dyskowej to wartości netto. Zawsze należy uwzględnić przyszły wzrost oraz zapewnić co najmniej 20% wolnego miejsca na dysku, na którym znajduje się baza danych.
> -   Jeśli wolne miejsce osiągnie wartość minimalną (20% lub 100 GB), zostaną usunięte najstarsze dane z okresu 24 godzin. Ta operacja będzie powtarzana, dopóki nie pozostaną dane tylko z dwóch dni bądź jedynie 5% lub 50 GB wolnego miejsca. W takim przypadku zbieranie danych przestanie działać.
> -  Opóźnienie magazynu dla działań odczytu i zapisu powinno być niższe niż 10 ms.
> -  Stosunek między działaniami odczytu i zapisu to około 1:3 poniżej 100 000 pakietów na sekundę i 1:6 powyżej 100 000 pakietów na sekundę.

## Ustalanie rozmiaru bramy usługi ATA
Brama usługi ATA może obsługiwać monitorowanie wielu kontrolerów domeny w zależności od natężenia ruchu sieciowego monitorowanych kontrolerów domeny.

|Pakiety na sekundę&#42;|Procesor CPU (rdzenie&#42;&#42;)|Pamięć (GB)|Przestrzeń dyskowa systemu operacyjnego (GB)|
|---------------------------|-------------------------|---------------|-------------------|
|10 000|4|12|80|
|20 000|8|24|100|
|40 000|16|64|200|
&#42;Łączna liczba pakietów na sekundę ze wszystkich kontrolerów domeny monitorowanych przez daną bramę usługi ATA.

&#42;Łączny ruch objęty funkcją dublowania portów kontrolera domeny nie może przekraczać wydajności karty sieciowej przechwytywania w bramie usługi ATA.

&#42;&#42;Hiperwątkowość musi być wyłączona.

## Szacowanie ruchu kontrolera domeny
Istnieją różne narzędzia, za pomocą których można określić średnią liczbę pakietów na sekundę kontrolerów domeny. Jeśli nie masz żadnych narzędzi do określenia tej wartości, możesz użyć Monitora wydajności do zebrania wymaganych informacji.

Aby określić liczbę pakietów na sekundę, wykonaj następujące czynności na każdym kontrolerze domeny:

1.  Otwórz Monitor wydajności.

    ![Obraz przedstawiający Monitor wydajności](media/ATA-traffic-estimation-1.png)

2.  Rozwiń węzeł **Zestawy modułów zbierających dane**..

    ![Obraz przedstawiający zestawy modułów zbierających dane](media/ATA-traffic-estimation-2.png)

3.  Kliknij prawym przyciskiem myszy pozycję **Zdefiniowany przez użytkownika**, a następnie wybierz pozycję **Nowy** &gt; **Zestaw modułów zbierających dane**..

    ![Obraz przedstawiający nowy zestaw modułów zbierających dane](media/ATA-traffic-estimation-3.png)

4.  Wprowadź nazwę dla zestawu modułów zbierających dane, a następnie wybierz pozycję **Utwórz ręcznie (zaawansowane)**..

5.  W obszarze **Jakiego typu dane chcesz uwzględnić?** wybierz pozycję **Utwórz dzienniki danych i Licznik wydajności**..

    ![Obraz przedstawiający typ danych nowego zestawu modułów zbierających dane](media/ATA-traffic-estimation-5.png)

6.  W obszarze **Które liczniki wydajności chcesz rejestrować?** kliknij przycisk **Dodaj**..

7.  Rozwiń węzeł **Karta sieciowa**, wybierz pozycję **Pakiety/s**, a następnie wybierz odpowiednie wystąpienie. Jeśli nie masz pewności, możesz wybrać pozycję **&lt;Wszystkie wystąpienia&gt;**, kliknąć przycisk **Dodaj**, a następnie kliknąć przycisk **OK**..

    > [!NOTE]
    > W tym celu w wierszu polecenia uruchom polecenie `ipconfig /all`, aby wyświetlić nazwę karty i konfigurację.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-traffic-estimation-7.png)

8.  Zmień wartość pozycji **Interwał próbkowania** na **1 sekundę**..

9. Ustaw lokalizację, w której mają być zapisywane dane.

10. W obszarze **Czy utworzyć zestaw modułów zbierających dane?** wybierz polecenie **Uruchom teraz ten zestaw modułów zbierających dane**, a następnie kliknij przycisk **Zakończ**..

    Powinien zostać wyświetlony właśnie utworzony zestaw modułów zbierających dane z zielonym trójkątem wskazującym, że zestaw działa.

11. Po 24 godzinach zatrzymaj zestaw modułów zbierających dane, klikając go prawym przyciskiem myszy, a następnie wybierając polecenie **Zatrzymaj**.

    ![Obraz przedstawiający zatrzymywanie działania zestawu modułów zbierających dane](media/ATA-traffic-estimation-12.png)

12. W Eksploratorze plików przejdź do folderu, w którym zapisano plik blg, a następnie kliknij go dwukrotnie w celu otworzenia w Monitorze wydajności.

13. Wybierz licznik Pakiety/s i zapisz wartość średnią oraz maksymalną.

    ![Obraz przedstawiający licznik Pakiety/s](media/ATA-traffic-estimation-14.png)

## Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Architektura usługi ATA](/advanced-threat-analytics/understand-explore/ata-architecture)
- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->


