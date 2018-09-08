---
title: Co nowego w wersji 1.9 usługi ATA | Dokumentacja firmy Microsoft
description: Lista nowości w wersji 1.9 oraz znanych problemów w usłudze ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: ddb93c2776dbb6e076314051068c4ca3544db756
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166616"
---
# <a name="whats-new-in-ata-version-19"></a>Co nowego w usłudze ATA w wersji 1.9

Najnowszą wersję aktualizacji usługi ATA można [pobrać z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=56725), a pełną wersję można pobrać z centrum [Eval Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Te informacje o wersji zawierają informacje o aktualizacji, nowe funkcje, poprawki błędów i znanych problemów występujących w tej wersji usługi Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nowe i zaktualizowane funkcje wykrywania

-  **Podejrzanie utworzenie usługi**: osoby atakujące usiłują podwyższyć do uruchomienia podejrzanych usługi w sieci. Usługa ATA zgłasza teraz alert, gdy zidentyfikuje ono ktoś uruchamia nową usługę, który wydaje się podejrzane, na kontrolerze domeny. Wykrywanie bazuje na zdarzeniach (nie ruchu w sieci), aby uzyskać więcej informacji, zobacz [Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nowe raporty pomagają w badaniach 

-   [ **Hasła ujawnione w zwykłym tekście** ](reports.md) pozwala wykrywać, gdy kont poufnych i niepoufnych, wysyłają poświadczenia kont w postaci zwykłego tekstu. Dzięki temu można zbadać i wyeliminować użycie prostego powiązania LDAP w danym środowisku, zwiększanie poziomu zabezpieczeń sieci. Ten raport zastępuje usługę i alertów podejrzanych działań jako zwykły tekst kont poufnych.

- [ **Boczne ścieżki ruchu do wrażliwych kont** ](reports.md) zawiera listę kont poufnych, które są udostępniane za pośrednictwem ścieżki ruchu poprzecznego. Dzięki temu można zmniejszyć tych ścieżek i ochrony sieci, aby zminimalizować ryzyko powierzchni ataku. Pozwala to zapobiegać penetracji sieci, dzięki czemu osoby atakujące nie można przenieść w sieci między użytkownicy i komputery, do momentu ich trafień Pula nagród zabezpieczeń wirtualnego: poświadczenia konta administratora poufnych.

## <a name="improved-investigation"></a>Ulepszone badania

-  1.9 usługi ATA zawiera nowe i ulepszone [profilu jednostki](entity-profiles.md). Profilu jednostki udostępnia pulpit nawigacyjny zaprojektowany do zbadania szczegółowym omówieniu użytkownicy, zasoby, które są dostępne i ich historii. Profilu jednostki umożliwia również zidentyfikować wrażliwych użytkowników, którzy są dostępne za pośrednictwem ścieżki ruchu poprzecznego. 

-   ATA 1.9 umożliwia [ręcznie oznaczyć grup](tag-sensitive-accounts.md) lub kont jako poufne, aby ulepszyć wykrywanie. Ten znakowania skutki, że wiele mechanizmy wykrywania usługi ATA, np. wykrywania modyfikacji wrażliwych grup i ścieżki ruchu poprzecznego zależą od tego, które grupy i konta są traktowane jako poufne.

## <a name="performance-improvements"></a>Ulepszenia wydajności

- Zwiększono wydajność infrastruktury Centrum usługi ATA: zagregowany widok ruchu włącza optymalizację potoku procesora CPU i pakietów, a następnie ponownie używa gniazda na kontrolerach domeny, aby zminimalizować sesji SSL do kontrolera domeny.



## <a name="additional-changes"></a>Dodatkowe zmiany

- Po zainstalowaniu nowej wersji usługi ATA [ **What's new** ](working-with-ata-console.md) pojawi się ikona na pasku narzędzi, aby umożliwić wiesz, co zostało zmienione w najnowszej wersji. Umożliwia także możesz z linkiem do dziennika zmian szczegółowe wersji.


## <a name="removed-and-deprecated-features"></a>Usunięte i przestarzałe funkcje

- **Broken zaufania podejrzanych działań** alert został usunięty.
- Hasła ujawnione w podejrzane działania w postaci zwykłego tekstu, został usunięty. Została zastąpiona [ **hasła ujawnione w postaci zwykłego tekstu raporcie**](reports.md).



## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.9 — Przewodnik migracji](ata-update-1.9-migration-guide.md)

