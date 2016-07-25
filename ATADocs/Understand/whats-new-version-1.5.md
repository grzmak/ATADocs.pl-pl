---
title: "Co nowego w wersji 1.5 usługi ATA | Microsoft ATA"
description: "Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.5 usługi ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 43e9d7af0eaa74abcb81ed9ade6b6a6fa452e6a4


---

# Co nowego w wersji 1.5 usługi ATA
Te informacje o wersji zawierają znane problemy w tej wersji usługi Advanced Threat Analytics.

## Co nowego w aktualizacji usługi ATA do wersji 1.5?
Aktualizacja usługi ATA do wersji 1.5 zapewnia następujące ulepszenia:

-   Szybsze wykrywanie

-   Rozszerzony algorytm automatycznego wykrywania dla urządzeń translacji adresów sieciowych

-   Rozszerzony proces rozpoznawania nazw dla urządzeń, które nie są dołączone do domeny

-   Obsługa migracji danych podczas aktualizacji produktów

-   Szybsza reakcja interfejsu użytkownika w przypadku podejrzanych działań związanych z tysiącami jednostek

-   Ulepszone automatyczne rozwiązywanie alertów monitorowania

-   Dodatkowe liczniki wydajności na potrzeby rozszerzonego monitorowania i rozwiązywania problemów

## Znane problemy
W tej wersji występują następujące znane problemy.

### Nowa instalacja bramy usługi ATA kończy się niepowodzeniem
Po zaktualizowaniu wdrożenia usługi ATA do wersji 1.5 podczas instalowania nowej bramy ATA występuje następujący błąd: Brama usługi Microsoft Advanced Threat Analytics nie jest zainstalowana

![Błąd bramy usługi ATA](media/ata-install-error.png)

<b>Obejście:</b> wyślij wiadomość e-mail na adres <ataeval@microsoft.com>, aby uzyskać instrukcje dotyczące obejścia.
### wdrażania
Folder określony w ustawieniach „Ścieżka danych bazy danych” i „Ścieżka dziennika bazy danych” musi być pusty (nie może zawierać plików ani podfolderów).
Jeśli folder nie jest pusty, wdrażanie nie będzie kontynuowane.

### Instalacja z pliku Zip
Podczas instalacji bramy usługi ATA należy wyodrębnić pliki z pliku zip do katalogu lokalnego i zainstalować ją z tej lokalizacji. Nie należy instalować bramy usługi ATA bezpośrednio z pliku zip, ponieważ instalacja zakończy się niepowodzeniem.

### Konfiguracja
Po ustawieniu konfiguracji bramy usługi ATA podczas pierwszego uruchomienia bramy usługi ATA jest wyświetlana etykieta „Nie zsynchronizowano” do momentu pełnego uruchomienia usługi, co może potrwać do 10 minut, gdy usługa jest uruchamiana po raz pierwszy.

### Oprogramowanie do przechwytywania ruchu sieciowego
Jedynym obsługiwanym oprogramowaniem do przechwytywania ruchu sieciowego, które można zainstalować na bramie usługi ATA, jest program [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Nie należy instalować programu Microsoft Message Analyzer ani żadnego innego oprogramowania do przechwytywania ruchu sieciowego. Zainstalowanie innego oprogramowania spowoduje nieprawidłowe działanie bramy usługi ATA.

### Aktualizacja na hoście wirtualizacji
Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji. Może to spowodować nieprawidłowe działanie funkcji dublowania portów.

## Zobacz też

[Aktualizacja usługi ATA do wersji 1.5 — przewodnik migracji](ata-update-1.5-migration-guide.md)

[Aktualizacja usługi ATA do wersji 1.6 — przewodnik migracji](ata-update-1.6-migration-guide.md)

[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


