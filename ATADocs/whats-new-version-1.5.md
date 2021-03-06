---
title: Co nowego w wersji 1.5 usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.5 usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 800d5d0ebf7eb044982c35e1f348b6c2faf14b07
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133246"
---
# <a name="whats-new-in-ata-version-15"></a>Co nowego w wersji 1.5 usługi ATA
Te informacje o wersji zawierają znane problemy w tej wersji usługi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Co nowego w aktualizacji usługi ATA do wersji 1.5?
Aktualizacja usługi ATA do wersji 1.5 zapewnia następujące ulepszenia:

-   Szybsze wykrywanie

-   Rozszerzony algorytm automatycznego wykrywania dla urządzeń translacji adresów sieciowych

-   Rozszerzony proces rozpoznawania nazw dla urządzeń, które nie są dołączone do domeny

-   Obsługa migracji danych podczas aktualizacji produktów

-   Szybsza reakcja interfejsu użytkownika w przypadku podejrzanych działań związanych z tysiącami jednostek

-   Ulepszone automatyczne rozwiązywanie alertów monitorowania

-   Dodatkowe liczniki wydajności na potrzeby rozszerzonego monitorowania i rozwiązywania problemów

## <a name="known-issues"></a>Znane problemy
W tej wersji występują następujące znane problemy.

### <a name="new-ata-gateway-installation-fails"></a>Nowa instalacja bramy usługi ATA kończy się niepowodzeniem
Po zaktualizowaniu wdrożenia usługi ATA do wersji 1.5 podczas instalowania nowej bramy ATA występuje następujący błąd: Brama usługi Microsoft Advanced Threat Analytics nie jest zainstalowana

![Błąd bramy usługi ATA](media/ata-install-error.png)

<b>Obejście:</b> Wyślij wiadomość e-mail do <ataeval@microsoft.com> Aby uzyskać instrukcje dotyczące obejścia.
### <a name="deployment"></a>wdrażania
Folder określony w ustawieniach „Ścieżka danych bazy danych” i „Ścieżka dziennika bazy danych” musi być pusty (nie może zawierać plików ani podfolderów).
Jeśli nie jest pusty, wdrażanie postępu.

### <a name="installation-from-zip-file"></a>Instalacja z pliku Zip
Podczas instalacji bramy usługi ATA należy wyodrębnić pliki z pliku zip do katalogu lokalnego i zainstalować ją z tej lokalizacji. Nie należy instalować bramy usługi ATA bezpośrednio z poziomu w pliku zip lub instalacja zakończy się niepowodzeniem.

### <a name="configuration"></a>Konfiguracja
Po ustawieniu konfiguracji bramy usługi ATA podczas pierwszego uruchomienia bramy usługi ATA jest wyświetlana etykieta „Nie zsynchronizowano” do momentu pełnego uruchomienia usługi, co może potrwać do 10 minut, gdy usługa jest uruchamiana po raz pierwszy.

### <a name="network-capture-software"></a>Oprogramowanie do przechwytywania ruchu sieciowego
Jedynym obsługiwanym oprogramowaniem do przechwytywania ruchu sieciowego, które można zainstalować na bramie usługi ATA, jest program [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Nie należy instalować programu Microsoft Message Analyzer ani żadnego innego oprogramowania do przechwytywania ruchu sieciowego. Zainstalowanie innego oprogramowania spowoduje nieprawidłowe działanie bramy usługi ATA.

### <a name="kb-on-virtualization-host"></a>Aktualizacja na hoście wirtualizacji
Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji. Może to spowodować nieprawidłowe działanie funkcji dublowania portów.

## <a name="see-also"></a>Zobacz też

[Aktualizacja usługi ATA do wersji 1.5 — przewodnik migracji](ata-update-1.5-migration-guide.md)

[Aktualizacja usługi ATA do wersji 1.6 — przewodnik migracji](ata-update-1.6-migration-guide.md)

[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
