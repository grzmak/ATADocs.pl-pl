---
title: What's new in Azure ATP | Dokumentacja firmy Microsoft
description: "Opisuje najnowsze wersje Azure ATP i zawiera informacje o nowościach w każdej wersji."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/18/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6b3c9ddd1873b3139009a44e9c1f7a85ea3b6901
ms.sourcegitcommit: adfa7a3a3918518b6b14b94d3c0a9f899142196a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/19/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>What's new in Azure ATP 

## <a name="azure-atp-release-225"></a>Azure wersji ATP 2,25

Wydane 18 marca 2018

- Uwierzytelnianie wieloskładnikowe (MFA) jest teraz obsługiwana w Azure ATP. Dzierżawcy przy użyciu usługi MFA można wprowadzić teraz w portalu Azure ATP.
- Azure ATP ma teraz [ **stan systemu** ](https://health.atp.azure.com/) stronę, aby uzyskać informacje na portalu zarządzania obszaru roboczego jest w górę, jak i aktywnych, jeśli występują problemy z wykryć i czujnika jest możliwość wysyłania ruch w chmurze. Dostęp można uzyskać **stan systemu** na pasku menu Azure ATP.


## <a name="azure-atp-release-224"></a>Azure ATP wersji 2,24

Wydana 11 marca 2018

**Wykryć nowe i zaktualizowane**
  - Tworzenie usługi podejrzane — osoby atakujące usiłują do uruchamiania usług podejrzane w sieci. Azure ATP teraz zgłasza alert, gdy określa, że ktoś na określonym komputerze działa nowej usługi, który wydaje się podejrzane. Wykrywanie jest oparta na zdarzenia (nie ruch sieciowy) i na każdym kontrolerze domeny w sieci, która jest funkcji przekazywania zdarzeń 7045 Azure ATP została wykryta. Aby uzyskać więcej informacji, zobacz [przewodnik podejrzanych działań](suspicious-activity-guide.md).

**Ulepszone badań**
  - Azure ATP obejmuje wzbogaconego [profilu jednostki](entity-profiles.md). Profilu jednostki zapewnia platformy, które jest przeznaczone do badania szczegółowo działań użytkownika obejmuje zasoby, które były dostępne, komputery, które są zalogowani i wiele innych. Profilu jednostki również udostępnia dane katalogu i umożliwia identyfikację potencjalnych ścieżek penetracja sieci do lub z jednostki, dzięki któremu można dowiedzieć się więcej o potencjalnych naruszeń w Twojej organizacji.

  - ATP umożliwia ręczne tag jednostki jako *poufnych* w celu zwiększenia wykryć i monitorowania. Znakowanie tej wpływa na wiele wykryć Azure ATP, takich jak grupy poufnej modyfikacji wykrywania i [ścieżki penetracja sieci](use-case-lateral-movement-path.md), które zależą od obiektów, które są traktowane jako poufne.

**Nowe raporty badać**
  - [Widoczne hasła w postaci zwykłego tekstu raporcie](reports.md) pozwala wykryć usługi wysyłania poświadczenia konta są wysyłane w postaci zwykłego tekstu. Dzięki temu można zbadać usług i zwiększyć poziom zabezpieczeń sieci. Ten raport zastępuje alerty podejrzane działanie jako zwykły tekst.
  - [Penetracji przepływu ścieżki do raportu kont poufnych](reports.md) listy kont poufnych, które są dostępne za pośrednictwem ścieżki penetracji sieci. Dzięki temu można zmniejszyć tych ścieżek i ograniczać funkcjonalność sieci, aby ograniczyć ryzyko powierzchni ataku. Dzięki temu można zapobiec penetracja sieci, aby osoby atakujące nie można przenieść w sieci między użytkownikami i komputerami, dopóki ich trafień jackpot wirtualnego zabezpieczeń: poświadczeń konta administratora poufnych.

- Można teraz łatwo zapewniają dostęp do dokumentacji z łącza w ramach alertu o podejrzanym działaniu do wyświetlenia [dochodzenia czynności, które można wykonać](suspicious-activity-guide.md). 

**Ulepszenia wydajności**
 -  Infrastruktura czujnik Azure ATP została ulepszona pod kątem wydajności: zagregowany widok ruchu umożliwia optymalizacji potoku procesora CPU i pakietu, a następnie ponownie używa gniazda do kontrolerów domeny, aby zminimalizować sesji SSL do kontrolera domeny.

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)