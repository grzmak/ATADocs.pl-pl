---
title: Usługa Azure policy danych osobowych zaawansowanej ochrony przed zagrożeniami | Dokumentacja firmy Microsoft
description: Zawiera łącza do informacji o tym, jak usunąć informacje prywatne, jak i dane osobiste z narzędzia Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: d64cc0d40acc31e2187305c38a625924a91db06b
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/26/2018
ms.locfileid: "36948935"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="azure-atp-data-security-and-privacy"></a>Bezpieczeństwo danych w usłudze Azure ATP i ochrona prywatności

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Wyszukiwanie i zidentyfikować dane osobowe 

W usłudze Azure Advanced Threat Protection można wyświetlić identyfikowalne dane osobowe [portalem obszarów roboczych](workspace-portal.md) przy użyciu [paska wyszukiwania](workspace-portal.md#search-bar). 

Możesz wyszukać konkretnego użytkownika lub komputera, a kliknięcie jednostki spowoduje wyświetlenie użytkownika lub komputera [stronę profilu](entity-profiles.md). Profil, który zapewnia kompleksowe szczegóły jednostki z usługi Active Directory, w tym powiązane z daną jednostką a jego historię aktywności w sieci.

Azure ATP dane osobowe są zbierane z usługi Active Directory przy użyciu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i przechowywane w wewnętrznej bazy danych.

## <a name="update-personal-data"></a>Zaktualizuj dane osobowe 

Ponieważ dane osobowe użytkownika usługi Azure ATP jest tworzony na podstawie obiektu użytkownika w usłudze Active Directory w organizacji, wszelkie zmiany wprowadzone do profilu użytkownika w usłudze AD zostaną odzwierciedlone w usłudze Azure ATP.


## <a name="delete-personal-data"></a>Usunięcie danych osobowych 

Po usunięciu użytkownika z usługi Active Directory w Twojej organizacji usługi Azure ATP automatycznie usuwa profil użytkownika i wszelkie działania związane z siecią w ciągu roku. Możesz również [Usuń](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) alertów zabezpieczeń, które zawierają dane osobowe. 

## <a name="export-personal-data"></a>Eksportowanie danych osobowych 

W przypadku narzędzia Azure ATP masz możliwość [wyeksportować](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informacje o alertach zabezpieczeń do programu Excel. Spowoduje to również wyeksportować dane osobowe. 
 
## <a name="audit-personal-data"></a>Dane osobowe inspekcji

Narzędzie Azure ATP implementuje inspekcji zmian danych osobowych, włącznie z usunięciem i eksportowanie rekordów danych osobowych. Czas przechowywania dziennik inspekcji wynosi 90 dni. Inspekcji w usłudze Azure ATP jest funkcją zaplecza i nie jest dostępny dla klientów.
 
## <a name="additional-resources"></a>Dodatkowe zasoby

- Aby uzyskać informacje dotyczące relacji zaufania usługi Azure ATP i zgodności, zobacz [portal zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise RODO zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
