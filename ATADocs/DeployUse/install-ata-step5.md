---
# required metadata

title: Instalowanie usługi ATA — Krok 5 | Microsoft Advanced Threat Analytics
description: W kroku 5 procesu instalowania usługi ATA znajdują się informacje ułatwiające skonfigurowanie ustawień bramy usługi ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalowanie usługi ATA — Krok 5

>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)


## Krok 5. Konfigurowanie ustawień bramy usługi ATA
Po zainstalowaniu bramy usługi ATA wykonaj następujące kroki, aby skonfigurować ustawienia bramy usługi ATA.

1.  Na komputerze bramy usługi ATA w konsoli usługi ATA kliknij pozycję **Konfiguracja**, a następnie wybierz stronę **Bramy usługi ATA**.

2.  Wprowadź następujące informacje.



  - **Opis**: <br>Wprowadź opis bramy usługi ATA (opcjonalnie).
  - **Kontrolery domeny** (wymagane): <br>Dodatkowe informacje dotyczące listy kontrolerów znajdują się poniżej.<br>Wpisz pełną nazwę FQDN kontrolera domeny, a następnie kliknij znak plus, aby dodać go do listy. Na przykład **dc01.contoso.com**.<br /><br />![Obraz z przykładową nazwą FQDN](media/ATAGWDomainController.png)<br>Obiekty z pierwszego kontrolera domeny na liście zostaną zsynchronizowane za pomocą zapytań LDAP. W zależności od wielkości domeny może to trochę potrwać.<br>
  **Uwaga:** <br>Upewnij się, że pierwszy kontroler domeny **nie** jest tylko do odczytu. Kontrolery domeny tylko do odczytu powinny zostać dodane dopiero po zakończeniu początkowej synchronizacji.<br>


 - **Karty sieciowe przechwytywania** (wymagane):<br>Wybierz karty sieciowe połączone z przełącznikiem skonfigurowanym jako docelowy port dublowany służący do odbierania ruchu kontrolera domeny. Wybierz kartę sieciową przechwytywania.
    ![Obraz przedstawiający konfigurowanie ustawień bramy](media/ATA-Config-GW-Settings.jpg)

3.  Kliknij polecenie **Zapisz**..

    > [!NOTE]
    > Pierwsze uruchomienie bramy usługi ATA potrwa kilka minut. Jest to spowodowane tworzeniem pamięci podręcznej analizatorów przechwytywania ruchu sieciowego używanej przez bramę usługi ATA.

Poniższe informacje dotyczą serwerów wprowadzonych na liście **Kontrolery domeny**.

-   Pierwszy kontroler domeny na liście będzie używany przez bramę usługi ATA do synchronizowania obiektów w domenie za pomocą zapytań LDAP. W zależności od wielkości domeny może to trochę potrwać.

-   Wszystkie kontrolery domeny, których ruch jest monitorowany za pośrednictwem funkcji dublowania portów przez bramę usługi ATA, muszą znajdować się na liście **Kontrolery domeny**. Jeśli kontroler domeny nie znajduje się na liście **Kontrolery domeny**, wykrywanie podejrzanych działań może nie funkcjonować zgodnie z oczekiwaniami.

-   Upewnij się, że pierwszy kontroler domeny **nie** jest kontrolerem tylko do odczytu.

    Kontrolery domeny tylko do odczytu powinny zostać dodane dopiero po zakończeniu początkowej synchronizacji.

-   Co najmniej jeden kontroler domeny znajdujący się na liście musi być serwerem wykazu globalnego. Umożliwi to rozpoznawanie przez usługę ATA obiektów użytkowników i komputerów znajdujących się w innych domenach w lesie.

Zmiany konfiguracji zostaną zastosowane względem bramy usługi ATA podczas następnej zaplanowanej synchronizacji między bramą usługi ATA a centrum usługi ATA.

### Zweryfikuj instalację:
Aby zweryfikować, czy brama usługi ATA została pomyślnie wdrożona:

1.  Sprawdź, czy jest uruchomiona brama usługi Microsoft Advanced Threat Analytics. Po zapisaniu ustawień bramy usługi ATA może minąć kilka minut, zanim usługa zostanie uruchomiona.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik „Microsoft.Tri.Gateway-Errors.log” domyślnie znajdujący się w folderze „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs” i wyszukaj wpisy z ciągiem „transfer” lub „service start”.

3.  Sprawdź następujące liczniki wydajności bramy usługi Microsoft ATA:

    -   **Liczba komunikatów przechwytywanych przez odbiornik sieci na sekundę**: ten licznik służy do śledzenia liczby komunikatów przechwytywanych w ciągu sekundy przez usługę ATA. Ta wartość powinna wynosić od kilkuset do kilku tysięcy w zależności od liczby monitorowanych kontrolerów domeny i ich obciążenia. Wartości jednocyfrowe lub dwucyfrowe mogą oznaczać problem z konfiguracją funkcji dublowania portów.

    -   **Liczba transferów działań transferów jednostek na sekundę**: ta wartość powinna być zbliżona do kilkuset co kilka sekund.

4.  Jeśli jest to pierwsza zainstalowana brama usługi ATA, po kilku minutach zaloguj się do konsoli usługi ATA i otwórz okienko powiadomień, szybko przesuwając od prawej strony ekranu. Na pasku powiadomień po prawej stronie konsoli powinna zostać wyświetlona lista **Ostatnio poznane jednostki**.

5.  Aby zweryfikować, czy instalacja zakończyła się pomyślnie:

    W konsoli wyszukaj jakiś element na pasku wyszukiwania, na przykład użytkownika lub grupę w Twojej domenie.

    Otwórz Monitor wydajności. W drzewie Wydajność kliknij pozycję **Monitor wydajności**, a następnie kliknij ikonę znaku plus, aby **dodać licznik**. Rozwiń pozycję **Brama usługi Microsoft ATA**, przewiń w dół do pozycji **Liczba komunikatów przechwytywanych przez odbiornik sieci na sekundę** i dodaj ten licznik. Następnie upewnij się, że wykres jest aktywny.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)

## Zobacz też

- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


