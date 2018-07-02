---
title: Praca z podejrzanymi działaniami w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opis sposobu przeglądania podejrzanych działań zidentyfikowanych przez narzędzia Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7caae52ff7402fdc8cb18ce1a01bba469c2d649b
ms.sourcegitcommit: f61616a8269d27a8fcde6ecf070a00e2c56481ac
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2018
ms.locfileid: "35259212"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="working-with-suspicious-activities"></a>Praca z podejrzanymi działaniami
W tym artykule opisano podstawowe informacje dotyczące korzystania z usługi Azure Advanced Threat Protection.

## Przeglądanie podejrzanych działań na osi czasu ataków <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Po zalogowaniu się do portalu usługi Azure ATP obszar roboczy, użytkownik jest automatycznie otwierana Otwórz **oś czasu podejrzanych działań**. Podejrzane działania są wymienione na liście w kolejności chronologicznej. Najnowsze podejrzane działania znajdują się u góry osi czasu.
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

![Obraz osi czasu podejrzanych działań w usłudze Azure ATP](media/atp-sa-timeline.png)

## Wykrycia (wersja zapoznawcza)<a name="preview-detections"></a>

Zespół badań narzędzia Azure ATP stale pracuje nad Implementowanie wykrywanie nowych zagrożeń dla nowo odnalezionych ataków. Ponieważ usługi Azure ATP to usługa w chmurze, jest możliwość zwolnienia te nowe funkcje wykrywania szybko, aby włączyć narzędzia Azure ATP klientów do korzystania z rozwiązaniami do wykrywania nowych tak szybko, jak to możliwe.

Wykrywane odmiany są oznaczane za pomocą wskaźnika (wersja zapoznawcza), aby zidentyfikować wykrywanie nowych zagrożeń i wiedzieć, czy jesteś nowym użytkownikiem produktu. Jeśli wyłączysz wykrycia (wersja zapoznawcza) one nie będą wyświetlane w konsoli usługi Azure ATP — nie osi czasu lub profile jednostek — i nie będzie można otworzyć nowe alerty.

![sieć vpn wykrywania (wersja zapoznawcza)](./media/preview-detection-vpn.png) 

Domyślnie wykrycia (wersja zapoznawcza) są włączone w narzędzia Azure ATP. 

Aby wyłączyć wykrywanie (wersja zapoznawcza):

1. W konsoli usługi Azure ATP kliknij przypominającą koło zębate.
2. W menu po lewej stronie w obszarze (wersja zapoznawcza), kliknij przycisk **wykrywania**.
3. Za pomocą suwaka, aby włączyć funkcje wykrywania w wersji zapoznawczej, włączać i wyłączać.
 
![wykrycia (wersja zapoznawcza)](./media/preview-detections.png) 


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




## <a name="managing-suspicious-activities"></a>Zarządzanie podejrzanymi działaniami
Stan podejrzanego działania można zmienić, klikając bieżący stan podejrzanego działania i wybierając jedną z następujących **Otwórz**, **pominięte**, **zamknięte**, lub **usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego podejrzanego działania, aby wyświetlić listę dostępnych akcji.

![Usługa Azure ATP akcje w przypadku podejrzanych działań](./media/atp-sa-actions.png)

**Stan podejrzanego działania**

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: jest używane do śledzenia podejrzanych działań, które identyfikowane, zbadane i stałej uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim czasie, narzędzia Azure ATP może ponownie otworzyć zamkniętych działań.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że, jeśli istnieje podobny alert usługi Azure ATP nie otworzyć go ponownie. Ale jeśli alert zatrzymuje przez siedem dni, a następnie zostanie zauważony ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alert, jest on usuwany z systemu, z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład można ustawić narzędzia Azure ATP do wykluczania określonej jednostki (użytkownika lub komputera) z ponownego wysyłania alertów dla określonego typu podejrzanych działań, takich jak konkretny administrator, który uruchamia zdalny kod lub skaner zabezpieczeń, który wykonuje Rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio do podejrzanego działania, gdy zostanie ono wykryte na osi czasu, możesz też przejść do strony konfiguracji, do pozycji **Wykluczenia**, i dla każdego podejrzanego działania możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku ataku typu Pass-the-Ticket). 

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi Azure ATP.


## <a name="see-also"></a>Zobacz też

- [Praca z portalem obszarów roboczych Zaawansowanej ochrony przed zagrożeniami na platformie Azure](workspace-portal.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)