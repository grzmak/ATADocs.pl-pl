---
title: "Praca z podejrzanymi działaniami w Azure Advanced Threat Protection | Dokumentacja firmy Microsoft"
description: "Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a5e7598e94e1d6d4b09c827770e062be9fefd1c4
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="working-with-suspicious-activities"></a>Praca z podejrzanymi działaniami
W tym artykule opisano podstawy sposób pracy z Azure Advanced Threat Protection.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Przeglądanie podejrzanych działań na osi czasu ataków
Po zalogowaniu się do portalu Azure ATP obszaru roboczego, jest automatycznie otwierana do otwarcia **oś czasu podejrzanych działań**. Podejrzane działania są wymienione na liście w kolejności chronologicznej. Najnowsze podejrzane działania znajdują się u góry osi czasu.
Każde podejrzane działanie zawiera następujące informacje:

-   Odnośne jednostki, w tym użytkownicy, komputery, serwery, kontrolery domeny i zasoby.

-   Godziny i przedział czasu podejrzanych działań.

-   Poziom ważności podejrzanego działania: Wysoki, Średni lub Niski.

-   Stan: Otwarte, Zamknięte lub Pominięte.

-   Możliwość wykonania następujących akcji:

    -   Udostępnienie podejrzanego działania innym osobom w organizacji za pomocą wiadomości e-mail.

    -   Wyeksportowanie podejrzanego działania do pliku programu Excel.

> [!NOTE]
> -   Umieszczenie wskaźnika myszy na użytkowniku lub komputerze spowoduje wyświetlenie mini profilu zawierającego dodatkowe informacje o tej jednostce oraz liczbie podejrzanych działań, z którymi powiązana jest ta jednostka.
> -   Po kliknięciu jednostki go przejście do profilu jednostki użytkownika lub komputera.

![Obraz osi czasu podejrzanych działań w usłudze Azure ATP](media/atp-sa-timeline.png)

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




## <a name="managing-suspicious-activities"></a>Zarządzanie podejrzanych działań
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących **Otwórz**, **Suppressed**, **zamknięte**, lub **usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego podejrzanego działania, aby wyświetlić listę dostępnych akcji.

![Azure ATP akcje dotyczące podejrzanych działań](./media/atp-sa-actions.png)

**Stan podejrzanego działania**

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: służy do śledzenia podejrzanych działań, które zidentyfikowane, zbadane i naprawione lub uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim czasie, Azure ATP może ponownie otworzyć zamkniętego działania.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że w przypadku podobnych alertów ATP Azure nie otwórz go ponownie. Jednak jeśli alert zatrzymuje na siedem dni, a następnie pojawia się ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alertu, zostaje usunięte z systemu z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład można ustawić ATP Azure, aby wykluczyć określone jednostki (użytkownik lub komputer) z ponownie alerty dla określonego typu podejrzanych działań, takich jak określonego administratora, który uruchamia kod zdalnego lub skanera zabezpieczeń, który wykonuje Rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio do podejrzanego działania, gdy zostanie ono wykryte na osi czasu, możesz też przejść do strony konfiguracji, do pozycji **Wykluczenia**, i dla każdego podejrzanego działania możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku ataku typu Pass-the-Ticket). 

> [!NOTE]
> Strony konfiguracji może zostać zmodyfikowany tylko przez administratorów Azure ATP.


## <a name="see-also"></a>Zobacz też

- [Praca z portalu Azure ATP obszaru roboczego](workspace-portal.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)