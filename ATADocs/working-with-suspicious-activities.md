---
title: Praca z podejrzanymi działaniami w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez usługę ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1557dff19375a5751eb655205dabadd684c655ba
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133178"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="working-with-suspicious-activities"></a>Praca z podejrzanymi działaniami
W tym artykule opisano podstawowe informacje dotyczące korzystania z usługi Advanced Threat Analytics.

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

> [!NOTE]
> -   Umieszczenie wskaźnika myszy na użytkowniku lub komputerze spowoduje wyświetlenie mini profilu zawierającego dodatkowe informacje o tej jednostce oraz liczbie podejrzanych działań, z którymi powiązana jest ta jednostka.
> -   Po kliknięciu jednostki jego przejście do profilu jednostki użytkownika lub komputera.

![Obraz osi czasu podejrzanych działań usługi ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrowanie listy podejrzanych działań
Aby filtrować listę podejrzanych działań:

1.  W **filtrowanie według** w okienku po lewej stronie ekranu, wybierz jedną z następujących opcji: **wszystkich**, **Otwórz**, **zamknięte**, lub **Pominięte**.

2.  Aby dokładniej przefiltrować listę, wybierz pozycję **wysokiej**, **średni**, lub **niski**.

**Poziom ważności podejrzanego działania**

-   **Niski**

    Wskazuje podejrzane działania, które mogą prowadzić do ataków opracowanych dla złośliwych użytkowników lub oprogramowania w celu uzyskania dostępu do danych organizacji.

-   **Średni**

    Wskazuje podejrzane działania mogące stanowić dla określonych tożsamości zagrożenie poważnymi atakami, mogącymi skutkować kradzieżą tożsamości lub podwyższeniem poziomu uprawnień.

-   **Wysoki**

    Wskazuje podejrzane działania, które mogą prowadzić do kradzieży tożsamości, eskalacją uprawnień lub innymi atakami wywierającymi duży wpływ




## <a name="remediating-suspicious-activities"></a>Korygowanie podejrzanych działań
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących **Otwórz**, **pominięte**, **zamknięte**, lub **usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego podejrzanego działania, aby wyświetlić listę dostępnych akcji.

![Akcje usługi ATA dla podejrzanych działań](./media/sa-actions.png)

**Stan podejrzanego działania**

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: jest używane do śledzenia podejrzanych działań, które identyfikowane, zbadane i stałej uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim okresie czasu, usługa ATA może ponownie otworzyć zamkniętych działań.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że, jeśli istnieje podobny alert, usługa ATA nie otworzyć go ponownie. Ale jeśli alert zatrzymuje przez siedem dni, a następnie zostanie zauważony ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alert, jest on usuwany z systemu, z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład możesz ustawić usługę ATA do wykluczania określonej jednostki (użytkownika lub komputera) z ponownego wysyłania alertów dla określonego typu podejrzanych działań, takich jak konkretny administrator, który uruchamia zdalny kod, lub skaner zabezpieczeń, który wykonuje rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio do podejrzanego działania, gdy zostanie ono wykryte na osi czasu, możesz też przejść do strony konfiguracji, do pozycji **Wykluczenia**, i dla każdego podejrzanego działania możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku ataku typu Pass-the-Ticket). 
> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## <a name="related-videos"></a>Pokrewne wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Zobacz też
- [Podręcznik dotyczący podejrzanych działań usługi ATA](http://aka.ms/ataplaybook)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
