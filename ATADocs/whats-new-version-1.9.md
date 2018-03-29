---
title: Nowości w wersji 1.9 usługi ATA | Dokumentacja firmy Microsoft
description: Zawiera listę nowych w wersji 1.9 oraz znanych problemów usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: f4a0776d52a69ba519e5cfdd0befb6bbd39d73c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-ata-version-19"></a>Nowości w wersji 1.9 usługi ATA

Najnowszą wersję aktualizacji usługi ATA można [pobrać z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=56725), a pełną wersję można pobrać z centrum [Eval Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Te informacje o wersji zawierają informacje o aktualizacji, nowe funkcje, poprawki i znane problemy w tej wersji usługi Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nowe i zaktualizowane funkcje wykrywania

-  **Tworzenie usługi podejrzane**: osoby atakujące usiłują Uruchamianie podejrzanych usługi w sieci. Usługa ATA zgłasza alert teraz, gdy rozpozna, że Uruchamianie nowej usługi, który wydaje się podejrzane, na kontrolerze domeny. Wykrywanie jest na podstawie zdarzeń (nie ruchu sieciowego), aby uzyskać więcej informacji, zobacz [przewodnik podejrzanych działań](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nowe raporty pomagają w badaniach 

-   [ **Hasła widoczne w zwykłym tekstem** ](reports.md) pozwala wykryć kont poufnych i niepoufnych, wysyłania poświadczenia konta w postaci zwykłego tekstu. Dzięki temu można zbadać i ograniczyć użycie proste powiązanie LDAP w danym środowisku, poprawy poziom zabezpieczeń sieci. Ten raport zastępuje usługi i poufne konto zwykłym tekstem podejrzane działanie alertów.

- [ **Penetracji ścieżki ruchu do kont poufnych** ](reports.md) listy kont poufnych, które są dostępne za pośrednictwem ścieżki penetracji sieci. Dzięki temu można zmniejszyć tych ścieżek i ograniczać funkcjonalność sieci, aby ograniczyć ryzyko powierzchni ataku. Dzięki temu można zapobiec penetracja sieci, aby osoby atakujące nie można przenieść w sieci między użytkownikami i komputerami, dopóki ich trafień jackpot wirtualnego zabezpieczeń: poświadczeń konta administratora poufnych.

## <a name="improved-investigation"></a>Ulepszone badań

-  ATA 1.9 zawiera nowe i ulepszone [profilu jednostki](entity-profiles.md). Profilu jednostki udostępnia pulpit nawigacyjny przeznaczony do badania pełnej szczegółowo użytkownicy, zasoby, które były dostępne i historii. Profilu jednostki umożliwia także zidentyfikować poufnych użytkowników, którzy są dostępne za pośrednictwem ścieżki penetracji sieci. 

-   ATA 1.9 umożliwia [ręcznie tagu grup](tag-sensitive-accounts.md) lub kont poufnych w celu ułatwienia wykrycia. Ten znakowania skutki że wielu wykrywania usługi ATA, takich jak grupy poufnej modyfikacji wykrywania i ścieżka penetracja sieci, zależą od tego, które grupy i konta są traktowane jako poufne.

## <a name="performance-improvements"></a>Ulepszenia wydajności

- Infrastruktura Centrum usługi ATA została ulepszona pod kątem wydajności: zagregowany widok ruchu umożliwia optymalizacji potoku procesora CPU i pakietu, a następnie ponownie używa gniazda do kontrolerów domeny, aby zminimalizować sesji SSL do kontrolera domeny.



## <a name="additional-changes"></a>Dodatkowe zmiany

- Po zainstalowaniu nowej wersji usługi ATA [ **nowości** ](working-with-ata-console.md) ikona jest wyświetlana na pasku narzędzi, aby umożliwić wiesz, co zostało zmienione w najnowszej wersji. Umożliwia także możesz z łączem do wersji szczegółowy wykaz zmian.


## <a name="removed-and-deprecated-features"></a>Usunięte i przestarzałe funkcje

- **Broken zaufania podejrzanych działań** alert został usunięty.
- Usunięto haseł w podejrzane działania w postaci zwykłego tekstu. Został zastąpiony przez [ **widoczne hasła w postaci zwykłego tekstu raporcie**](reports.md).



## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.9 — Przewodnik migracji](ata-update-1.9-migration-guide.md)

