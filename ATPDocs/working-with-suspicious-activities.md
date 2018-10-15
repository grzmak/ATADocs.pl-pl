---
title: Praca z alertami zabezpieczeń w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W tym artykule opisano jak przeglądać alerty zabezpieczeń wydane przez usługi Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59bc8cdb995b1f7473efb7c0e601aca50a9ccafe
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315833"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="working-with-security-alerts"></a>Praca z alertami zabezpieczeń
W tym artykule opisano podstawowe informacje dotyczące korzystania z usługi Azure Advanced Threat Protection.

## Przeglądanie alertów zabezpieczeń na osi czasu ataków <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Po zalogowaniu się do portalu usługi Azure ATP, nastąpi automatyczne przekierowanie do Otwórz **oś czasu alerty zabezpieczeń**. Alerty zabezpieczeń są wymienione w kolejności chronologicznej z najnowszych alert u góry osi czasu.
Każdy alert zabezpieczeń zawiera następujące informacje:

-   Odnośne jednostki, w tym użytkownicy, komputery, serwery, kontrolery domeny i zasoby.

-   Godziny i przedział czasu podejrzanych działań, które inicjowane alertu zabezpieczeń.

-   Ważność alertu: wysoki, średni lub niski.

-   Stan: Otwarte, Zamknięte lub Pominięte.

-   Możliwość wykonania następujących akcji:

    -   Alert zabezpieczeń można udostępniać innym osobom w organizacji za pośrednictwem poczty e-mail.

    -   Alert zabezpieczeń Eksportuj do programu Excel.

> [!NOTE]
> -   Po umieszczeniu wskaźnika myszy komputera lub użytkownika, spowoduje wyświetlenie mini profilu jednostki zostanie wyświetlony zawiera dodatkowe informacje na temat jednostki oraz liczbę alertów zabezpieczeń, połączone z jednostki.
> -   Po kliknięciu jednostki jego przejście do profilu jednostki użytkownika lub komputera.

![Obraz osi czasu alerty zabezpieczeń usługi Azure ATP](media/atp-sa-timeline.png)

## Wykrycia (wersja zapoznawcza)<a name="preview-detections"></a>

Zespół badań narzędzia Azure ATP stale pracuje nad Implementowanie wykrywanie nowych zagrożeń dla nowo odnalezionych ataków. Ponieważ usługi Azure ATP to usługa w chmurze, wykrywanie nowych zagrożeń są wydawane szybko umożliwiające klientom usługi Azure ATP korzystać z nowych wykryć tak szybko, jak to możliwe.

Wykrywane odmiany są oznaczane za pomocą wskaźnika (wersja zapoznawcza), aby zidentyfikować wykrywanie nowych zagrożeń i wiedzieć, czy jesteś nowym użytkownikiem produktu. Jeśli wyłączysz wykrycia (wersja zapoznawcza) one nie będą wyświetlane w konsoli usługi Azure ATP — nie osi czasu lub profile jednostek — i nie będzie można otworzyć nowe alerty.

![sieć vpn wykrywania (wersja zapoznawcza)](./media/preview-detection-vpn.png) 

Domyślnie wykrycia (wersja zapoznawcza) są włączone w narzędzia Azure ATP. 

Aby wyłączyć wykrywanie (wersja zapoznawcza):

1. W konsoli usługi Azure ATP kliknij przypominającą koło zębate.
2. W menu po lewej stronie w obszarze (wersja zapoznawcza), kliknij przycisk **wykrywania**.
3. Za pomocą suwaka, aby włączyć funkcje wykrywania w wersji zapoznawczej, włączać i wyłączać.
 
![Wykrycia (wersja zapoznawcza)](./media/preview-detections.png) 


## <a name="filter-security-alerts-list"></a>Filtrowanie listy alertów zabezpieczeń
Aby filtrować listę alertów zabezpieczeń:

1.  W **filtrowanie według** w okienku po lewej stronie ekranu, wybierz jedną z następujących opcji: **wszystkich**, **Otwórz**, **zamknięte**, lub **Pominięte**.

2.  Aby dokładniej przefiltrować listę, wybierz pozycję **wysokiej**, **średni**, lub **niski**.

**Poziom ważności podejrzanego działania**

-   **Niski**

    Wskazuje działania, które mogą prowadzić do ataków opracowanych dla złośliwych użytkowników lub oprogramowania w celu uzyskania dostępu do danych organizacji.

-   **Średni**

    Wskazuje działania, które może stanowić dla określonych tożsamości zagrożenie poważnymi atakami, mogącymi skutkować kradzieżą tożsamości lub podwyższeniem poziomu uprawnień

-   **Wysoki**

    Wskazuje działania, które mogą prowadzić do kradzieży tożsamości, eskalacją uprawnień lub innymi atakami wywierającymi duży wpływ


## <a name="managing-security-alerts"></a>Zarządzanie alertami zabezpieczeń
Stan alertu zabezpieczeń można zmienić, klikając bieżący stan alertu zabezpieczeń i wybierając jedną z następujących **Otwórz**, **pominięte**, **zamknięte**, lub **Usunięte**.
Aby to zrobić, kliknij przycisk z wielokropkiem w prawym górnym rogu określonego alertu, aby wyświetlić listę dostępnych akcji.

![Usługa Azure ATP akcje w przypadku alertów zabezpieczeń](./media/atp-sa-actions.png)

**Stan alertu zabezpieczeń**

-   **Otwórz**: wszystkie nowe alerty zabezpieczeń są wyświetlane na tej liście.

-   **Zamknij**: jest używane do śledzenia alerty zabezpieczeń, które są identyfikowane, zbadane i stałej uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim czasie, narzędzia Azure ATP może ponownie otworzyć zamkniętego alertu.

-   **Pomiń**: pomijanie aalert oznacza, że chcesz go zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Oznacza to, że, jeśli istnieje podobny alert usługi Azure ATP nie otworzyć go ponownie. Ale jeśli alert zatrzymuje przez siedem dni, a następnie zostanie zauważony ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alert, jest on usuwany z systemu, z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie alerty zabezpieczeń tego samego typu.

- **Wyklucz**: Możliwość wykluczania jednostki z wywoływania większej liczby alertów określonego typu. Na przykład można ustawić narzędzia Azure ATP do wykluczania określonej jednostki (użytkownika lub komputera) z ponownego wysyłania alertów dla określonego typu działań, takich jak konkretny administrator, który uruchamia zdalny kod lub skaner zabezpieczeń, który wykonuje Rekonesans DNS. Oprócz możliwości dodawania wykluczeń bezpośrednio na alert zabezpieczeń, gdy zostanie ono wykryte na osi czasu, możesz również przejść do strony konfiguracji, aby **wykluczenia**i dla każdego alertu zabezpieczeń, możesz ręcznie dodawać i usuwać wykluczone jednostki lub podsieci (na przykład w przypadku Pass--Ticket). 

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi Azure ATP.


## <a name="see-also"></a>Zobacz też

- [Praca z portalem usługi Azure ATP](workspace-portal.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)