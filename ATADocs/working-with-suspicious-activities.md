---
title: "Praca z podejrzanymi działaniami w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez usługę ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/15/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 634341bf4ca15e077e3fd6424dd9fa8b8d74c301
ms.sourcegitcommit: 55f7ac32bcd4ac8edb8b8b3b47993bf96b9acce2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2018
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="working-with-suspicious-activities"></a>Praca z podejrzanymi działaniami
W tym artykule opisano podstawy sposób pracy z Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Przeglądanie podejrzanych działań na osi czasu ataków
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

> [!NOTE]
> -   Umieszczenie wskaźnika myszy na użytkowniku lub komputerze spowoduje wyświetlenie mini profilu zawierającego dodatkowe informacje o tej jednostce oraz liczbie podejrzanych działań, z którymi powiązana jest ta jednostka.
> -   Po kliknięciu jednostki go przejście do profilu jednostki użytkownika lub komputera.

![Obraz osi czasu podejrzanych działań usługi ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrowanie listy podejrzanych działań
Aby filtrować listę podejrzanych działań:

1.  W **Filtruj według** w okienku po lewej stronie ekranu wybierz jedną z następujących opcji: **wszystkie**, **Otwórz**, **zamknięte**, lub **Pomijane**.

2.  Aby dokładniej przefiltrować listę, wybierz **wysokiej**, **średni**, lub **małej**.

**Poziom ważności podejrzanego działania**

-   **Niski**

    Wskazuje podejrzane działania, które mogą prowadzić do ataków opracowanych dla złośliwych użytkowników lub oprogramowania w celu uzyskania dostępu do danych organizacji.

-   **Średni**

    Wskazuje podejrzane działania mogące stanowić dla określonych tożsamości zagrożenie poważnymi atakami, mogącymi skutkować kradzieżą tożsamości lub podwyższeniem poziomu uprawnień.

-   **Wysoki**

    Wskazuje podejrzane działania, które mogą prowadzić do kradzieży tożsamości, podwyższenia poziomu uprawnień lub inne ataki poważnych




## <a name="remediating-suspicious-activities"></a>Korygowanie podejrzanych działań
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących **Otwórz**, **Suppressed**, **zamknięte**, lub **usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego podejrzanego działania, aby wyświetlić listę dostępnych akcji.

![Akcje usługi ATA dla podejrzanych działań](./media/sa-actions.png)

**Stan podejrzanego działania**

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: służy do śledzenia podejrzanych działań, które zidentyfikowane, zbadane i naprawione lub uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim czasie, usługa ATA może ponownie otworzyć zamkniętego działania.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że w przypadku podobnych alertów usługi ATA nie otwórz go ponownie. Jednak jeśli alert zatrzymuje na siedem dni, a następnie pojawia się ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alertu, zostaje usunięte z systemu z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład możesz ustawić usługę ATA do wykluczania określonej jednostki (użytkownika lub komputera) z ponownego wysyłania alertów dla określonego typu podejrzanych działań, takich jak konkretny administrator, który uruchamia zdalny kod, lub skaner zabezpieczeń, który wykonuje rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio do podejrzanego działania, gdy zostanie ono wykryte na osi czasu, możesz też przejść do strony konfiguracji, do pozycji **Wykluczenia**, i dla każdego podejrzanego działania możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku ataku typu Pass-the-Ticket). 
> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## <a name="related-videos"></a>Powiązane pliki wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Zobacz też
- [Podręcznika dotyczącego podejrzanych działań usługi ATA](http://aka.ms/ataplaybook)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
