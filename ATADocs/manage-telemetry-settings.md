---
title: "Zarządzanie ustawieniami telemetrii usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Zawiera opis danych zbieranych przez usługę ATA i kroki służące do wyłączania zbierania danych."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a164179261dd5a50df973fab89be7ddce99f8c47
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="manage-telemetry-settings"></a>Zarządzanie ustawieniami telemetrii
Usługa Advanced Threat Analytics (ATA) zbiera anonimowe dane telemetryczne o usłudze ATA i przesyła jest za pośrednictwem połączenia HTTPS do serwerów firmy Microsoft.  Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA.

## <a name="data-collected"></a>Zbierane dane
Zbierane są następujące anonimowe dane:

-   Liczniki wydajności centrum usługi ATA i bramy usługi ATA

-   Identyfikator produktu licencjonowanych kopii usługi ATA

-   Data wdrożenia centrum usługi ATA

-   Liczba wdrożonych bram usługi ATA

-   Następujące anonimowe informacje dotyczące usługi Active Directory:

    -   Identyfikator domeny, której nazwa jest pierwsza w przypadku sortowania alfabetycznego

    -   Liczba kontrolerów domeny

    -   Liczba kontrolerów domeny monitorowanych przez usługę ATA za pośrednictwem funkcji dublowania portów

    -   Liczba witryn

    -   Liczba komputerów

    -   Liczba grup

    -   Liczba użytkowników

-   Podejrzane działania — następujące anonimowe dane są zbierane dla każdego podejrzanego działania:

    (nazwy komputerów, nazwy użytkowników i adresy IP **nie** są zbierane)

    -   Typ podejrzanego działania

    -   Identyfikator podejrzanego działania

    -   Stan

    -   Godzina rozpoczęcia i zakończenia

    -   Dostarczone dane wejściowe

- Problemy dotyczące kondycji — następujące dane poddane anonimizacji są gromadzone dla każdego problemu związanego z kondycją:

    (Nazwy komputerów, nazwy użytkowników i adresy IP nie są zbierane).

    -   Typ problemu dotyczącego kondycji

    -   Identyfikator problemu dotyczącego kondycji

    -   Stan

    -   Godzina rozpoczęcia i zakończenia

- Adresy URL konsoli ATA — adresy URL używane w konsoli ATA tj. odwiedzone strony w konsoli ATA.


### <a name="disable-data-collection"></a>Wyłączanie zbierania danych
Aby zatrzymać zbieranie i wysyłanie danych telemetrycznych do firmy Microsoft, wykonaj poniższe kroki:

1.  Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**.

2.  Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**.

## <a name="see-also"></a>Zobacz też
- [Rozwiązywanie problemów z usługą ATA przy użyciu dziennika zdarzeń](troubleshooting-ata-using-logs.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
