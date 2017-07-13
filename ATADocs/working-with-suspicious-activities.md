---
title: "Praca z podejrzanymi działaniami w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez usługę ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1ff15a323f461cf8436e1ff7e15738a49bf3973c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Praca z podejrzanymi działaniami
<a id="working-with-suspicious-activities" class="xliff"></a>
W tym temacie przedstawiono podstawowe informacje dotyczące pracy z usługą Advanced Threat Analytics.

## Przeglądanie podejrzanych działań na osi czasu ataków
<a id="review-suspicious-activities-on-the-attack-time-line" class="xliff"></a>
Po zalogowaniu się do konsoli usługi ATA jest automatycznie otwierana **Oś czasu podejrzanych działań**. Podejrzane działania są wymienione na liście w kolejności chronologicznej. Najnowsze podejrzane działania znajdują się u góry osi czasu.
Każde podejrzane działanie zawiera następujące informacje:

-   Odnośne jednostki, w tym użytkownicy, komputery, serwery, kontrolery domeny i zasoby.

-   Godziny i przedział czasu podejrzanych działań.

-   Poziom ważności podejrzanego działania: Wysoki, Średni lub Niski.

-   Stan: Otwarte, Zamknięte lub Pominięte.

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
<a id="filter-suspicious-activities-list" class="xliff"></a>
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




## Korygowanie podejrzanych działań
<a id="remediating-suspicious-activities" class="xliff"></a>
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących pozycji: **Otwarte**, **Pominięte**, **Zamknięte** lub **Usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego podejrzanego działania, aby wyświetlić listę dostępnych akcji.

![Akcje usługi ATA dla podejrzanych działań](./media/sa-actions.png)

**Stan podejrzanego działania**

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: Służy do śledzenia podejrzanych działań, które zostały zidentyfikowane i zbadane, a następnie naprawione lub uniemożliwione.

    > [!NOTE]
    > Usługa ATA może ponownie otworzyć rozwiązane działanie w przypadku ponownego wykrycia tego samego działania w krótkim czasie.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że jeśli istnieje podobny alert, usługa ATA nie otworzy go ponownie. Jeśli jednak alertu nie będzie przez 7 dni, a następnie pojawi się on ponownie, znów go zobaczysz.

- **Usuń**: Jeśli usuniesz alert, zostanie on usunięty z systemu, z bazy danych i NIE BĘDZIE można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład możesz ustawić usługę ATA do wykluczania określonej jednostki (użytkownika lub komputera) z ponownego wysyłania alertów dla określonego typu podejrzanych działań, takich jak konkretny administrator, który uruchamia zdalny kod, lub skaner zabezpieczeń, który wykonuje rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio do podejrzanego działania, gdy zostanie ono wykryte na osi czasu, możesz też przejść do strony konfiguracji, do pozycji **Wykluczenia**, i dla każdego podejrzanego działania możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku ataku typu Pass-the-Ticket). 
> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## Zobacz też
<a id="see-also" class="xliff"></a>
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Praca z ustawieniami wykrywania usługi ATA](working-with-detection-settings.md)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
