---
title: Zarządzanie dziennikami generowanych przez system Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera opis danych zbieranych przez usługę ATA i kroki służące do wyłączania zbierania danych.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 17e5778543b9f08d3157ed91cb0a7a73ea268c0a
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="manage-system-generated-logs-note"></a>Zarządzanie dziennikami generowanych przez system > [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) w [sekcji GDPR witryny Microsoft 365 Enterprise zgodności] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Advanced Threat Analytics (ATA) zbiera anonimowe dane dziennika generowanych przez system dotyczące usługi ATA i przesyła dane za pośrednictwem połączenia HTTPS do serwerów firmy Microsoft.  Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA.

## <a name="data-collected"></a>Zbierane dane
Zebrane dane anonimowe zawiera następujące parametry:

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

- Adresy URL konsoli usługi ATA — adresów URL przy użyciu konsoli usługi ATA, są odwiedzane strony w konsoli usługi ATA.


### <a name="disable-data-collection"></a>Wyłączanie zbierania danych
Aby zatrzymać zbieranie i wysyłanie danych telemetrycznych do firmy Microsoft, wykonaj poniższe kroki:

1.  Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**.

2.  Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**.

## <a name="see-also"></a>Zobacz też
- [Rozwiązywanie problemów z usługą ATA przy użyciu dziennika zdarzeń](troubleshooting-ata-using-logs.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
