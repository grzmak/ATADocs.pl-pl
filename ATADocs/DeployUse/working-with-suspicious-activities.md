---
title: "Praca z podejrzanymi działaniami | Microsoft ATA"
description: "Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez usługę ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 30fbeb0682bd4b253d7a6eb52b8b31e487b363cb


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Praca z podejrzanymi działaniami
W tym temacie przedstawiono podstawowe informacje dotyczące pracy z usługą Advanced Threat Analytics.

## Przeglądanie podejrzanych działań na osi czasu ataków
Po zalogowaniu się do konsoli usługi ATA jest automatycznie otwierana **Oś czasu podejrzanych działań**. Podejrzane działania są wymienione na liście w kolejności chronologicznej. Najnowsze podejrzane działania znajdują się u góry osi czasu.
Każde podejrzane działanie zawiera następujące informacje:

-   Odnośne jednostki, w tym użytkownicy, komputery, serwery, kontrolery domeny i zasoby.

-   Godziny i przedział czasu podejrzanych działań.

-   Poziom ważności podejrzanego działania: Wysoki, Średni lub Niski.

-   Stan: Otwarte, Rozwiązane lub Odrzucone.

-   Możliwość wykonania następujących akcji:

    -   Udostępnienie podejrzanego działania innym osobom w organizacji za pomocą wiadomości e-mail.

    -   Wyeksportowanie podejrzanego działania do pliku programu Excel.

    -   Dodanie uwagi do podejrzanego działania.

    -   Podanie danych wejściowych dotyczących podejrzanego działania.

-   Zawiera zalecenia dotyczące sposobu reagowania na podejrzane działanie.

> [!NOTE]
> -   Umieszczenie wskaźnika myszy na użytkowniku lub komputerze spowoduje wyświetlenie mini profilu zawierającego dodatkowe informacje o tej jednostce oraz liczbie podejrzanych działań, z którymi powiązana jest ta jednostka.
> -   Kliknięcie jednostki spowoduje przejście do profilu jednostki użytkownika lub komputera.

![Obraz osi czasu podejrzanych działań usługi ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtrowanie listy podejrzanych działań
Aby filtrować listę podejrzanych działań:

1.  W okienku **Filtruj według** po lewej stronie ekranu wybierz jedną z następujących pozycji: **Wszystkie**, **Otwarte**, **Rozwiązane** lub **Odrzucone**.

2.  Aby dokładniej przefiltrować listę, wybierz pozycję **Wysoki**, **Średni** lub **Niski**.

**Poziom ważności podejrzanego działania**

-   **Niski**

    Wskazuje podejrzane działania, które mogą prowadzić do ataków opracowanych dla złośliwych użytkowników lub oprogramowania w celu uzyskania dostępu do danych organizacji.

-   **Średni**

    Wskazuje podejrzane działania mogące stanowić dla określonych tożsamości zagrożenie poważnymi atakami, mogącymi skutkować kradzieżą tożsamości lub podwyższeniem poziomu uprawnień.

-   **Wysoki**

    Wskazuje podejrzane działania mogące prowadzić do kradzieży tożsamości, podwyższenia poziomu uprawnień lub innych ataków o dużym znaczeniu.

**Stan podejrzanego działania**

-   **Otwarte**

    Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Resolved**

    Służy do śledzenia podejrzanych działań, które zostały zidentyfikowane i zbadane, a następnie naprawione lub uniemożliwione.

    > [!NOTE]
    > Usługa ATA może ponownie otworzyć rozwiązane działanie w przypadku ponownego wykrycia tego samego działania w krótkim czasie.

-   **Odrzucone**

    Działania, które zostały ręcznie odrzucone. Jeśli usługa ATA wykryje podobne podejrzane działanie, zostanie utworzone nowe wykrycie.

## Podawanie danych wejściowych dotyczących podejrzanego działania
Aby usługa ATA mogła uczyć się sieci z udziałem użytkownika, w przypadku niektórych podejrzanych działań (rekonesans DNS, ataki typu Pass the Ticket, wyliczenie sesji SMB, nietypowe zachowanie i zdalne wykonywanie kodu) użytkownik jest proszony o podanie danych wejściowych umożliwiających ulepszenie wykrywania podejrzanych działań w przyszłości.

1.  Prośba o podanie danych wejściowych jest automatycznie otwierana dla podejrzanych działań z możliwością podania danych wejściowych. Użytkownik zostanie poproszony o udzielenie odpowiedzi na pytania dotyczące działań w sieci oraz tego, czy powinny zostać uznane za podejrzane. W poniższym przykładzie użytkownik jest pytany, czy uruchamianie narzędzi do skanowania jest dozwolone przy użyciu określonego komputera.

    ![Obraz przedstawiający podawanie danych wejściowych dotyczących podejrzanych działań w usłudze ATA](media/ATA-Input.JPG)

2.  W przypadku odmowy to działanie zostanie uznane za podejrzane, a za każdym razem, gdy usługa ATA napotka to działanie z tego komputera, zostanie wygenerowany alert.

3.  Jednak w przypadku zgody podejrzane działanie można odrzucić, a przyszłe działania tego typu z tego komputera mogą nie spowodować wygenerowania podejrzanego działania lub wygenerować działanie, które zostanie automatycznie odrzucone.

4.  Jeśli nie znasz odpowiedzi, możesz kliknąć przycisk **Anuluj**.

## Zmiana stanu podejrzanego działania
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących pozycji: **Otwarte**, **Rozwiązane** lub **Odrzucone**.

## Zobacz też
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Praca z ustawieniami wykrywania usługi ATA](working-with-detection-settings.md)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-configuration.md)



<!--HONumber=Aug16_HO5-->


