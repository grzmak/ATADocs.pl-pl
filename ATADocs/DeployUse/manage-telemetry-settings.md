---
# required metadata

title: Zarządzanie ustawieniami telemetrii | Microsoft Advanced Threat Analytics
description: Zawiera opis danych zbieranych przez usługę ATA i kroki służące do wyłączania zbierania danych.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Zarządzanie ustawieniami telemetrii
Usługa Advanced Threat Analytics (ATA) zbiera anonimowe dane telemetryczne o usłudze ATA i przesyła jest za pośrednictwem połączenia HTTPS do serwerów firmy Microsoft.  Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA.

## Zbierane dane
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

### Wyłączanie zbierania danych
Aby zatrzymać zbieranie i wysyłanie danych telemetrycznych do firmy Microsoft, wykonaj poniższe kroki:

1.  Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**.

2.  Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**.

## Zobacz też
- [Co nowego w wersji 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


