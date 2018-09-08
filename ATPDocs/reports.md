---
title: Praca z raportami usługi Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można generować raporty z usługi Azure ATP w celu monitorowania sieci.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: eb1a29038d8afb47328970ff7179f0e1ff01614d
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165936"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-reports"></a>Raporty usługi Azure ATP

W sekcji raporty usługi Azure ATP w portalu obszaru roboczego umożliwia generowanie raportów, które udostępniają informacje o stanie systemu, zarówno w kondycję systemu, jak i raport o podejrzanych działaniach wykrytych w Twoim środowisku.


Aby uzyskać dostęp do strony raportów, kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/atp-report-icon.png).
Do raportów, które są dostępne, należą: 

- **Raport z podsumowaniem**: raport z podsumowaniem przedstawia pulpit nawigacyjny stanu systemu. Możesz wyświetlić trzy karty — jedną dla **Podsumowanie** programu co zostało wykryte w sieci, **otwierania podejrzanych działań** , zawiera listę podejrzanych działań, możesz należy się zająć, i **Otwórz kondycji problemy z** czy listy kondycji narzędzia Azure ATP problemów, które należy się zająć. Wyświetlane podejrzane działania są podzielone według typu, tak jak problemy z kondycją. 

- **Modyfikacja wrażliwych grup**: Ten raport zawiera listę za każdym razem, gdy zostanie podjęta modyfikacja wrażliwych grup (na przykład Administratorzy, lub ręcznie oznakowane kont lub grup). Jeśli używasz narzędzia Azure ATP autonomicznych czujniki, aby otrzymać pełny raport o wrażliwych grup, jest to konieczne upewnić się, że [zdarzenia są przekazywane z kontrolerów domeny do czujników autonomiczny](configure-event-forwarding.md). 

- **Hasła ujawnione w zwykłym tekście**: niektóre usługi protokół LDAP — zabezpieczanie wysyłają poświadczenia kont w postaci zwykłego tekstu. Można to zrobić nawet w przypadku kont poufnych. Osoby atakujące monitorujące ruch sieciowy może przechwytywać i korzystać z nich te poświadczenia do złośliwych celów. Ten raport przedstawia wszystkie komputery źródłowy i hasła kont, które narzędzia Azure ATP wykryte jako jest wysyłane w postaci zwykłego tekstu. 

- **Boczne ścieżki ruchu do wrażliwych kont**: Ten raport zawiera listę kont poufnych, które są udostępniane za pośrednictwem ścieżki ruchu poprzecznego. Aby uzyskać więcej informacji, zobacz [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md). Ten raport umożliwia zbieranie informacji o ścieżkach, które zostały utworzone w ciągu ostatnich 60 dni, w przeciwieństwie do informacji wyświetlanych w portalu obszaru roboczego, który reprezentuje tylko dwa dni.

Istnieją dwa sposoby generowania raportu: na żądanie albo zaplanowanie okresowego wysyłania raportu na adres e-mail.

Aby wygenerować raport na żądanie:

1. W pasku menu portalu usługi Azure ATP obszaru roboczego kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/atp-report-icon.png).

2. W obszarze typu wybranego raportu, ustaw **z** i **do** dat i kliknij przycisk **Pobierz**. 
 ![raporty](./media/reports.png)

Aby ustawić zaplanowany raport:
 
1. W **raporty** kliknij **Ustaw Zaplanowane raporty**, lub na stronie konfiguracji portalu obszaru roboczego usługi Azure ATP, w obszarze powiadomień i raportów, kliknij przycisk **Zaplanowane raporty**.

   ![Planowanie raportów](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Codzienne raporty są przeznaczone do wysłania wkrótce po północy czasu UTC.

2. Kliknij przycisk **harmonogram** obok typu wybranego raportu, aby ustawić częstotliwość i adres e-mail dostarczania raportów, a następnie kliknij znak plus obok adresów e-mail, aby je dodać, a następnie kliknij przycisk **Zapisz**.

   ![Planowanie częstotliwości raportów i wysyłania poczty e-mail](./media/sched-report1.png)


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)