---
title: Usługa Azure policy danych osobowych zaawansowanej ochrony przed zagrożeniami | Dokumentacja firmy Microsoft
description: Zawiera łącza do informacji o tym, jak usunąć informacje prywatne, jak i dane osobiste z narzędzia Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: e4aad8af65c27f351185808585aea37a8a67de42
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734757"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="azure-atp-data-security-and-privacy"></a>Bezpieczeństwo danych w usłudze Azure ATP i ochrona prywatności

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Wyszukiwanie i zidentyfikować dane osobowe 

W usłudze Azure Advanced Threat Protection można wyświetlić identyfikowalne dane osobowe [portalem obszarów roboczych](workspace-portal.md) przy użyciu [paska wyszukiwania](workspace-portal.md#search-bar). 

Wyszukiwanie określonego użytkownika lub komputera, a następnie kliknij jednostkę którą chcesz wyświetlić użytkownika lub komputera [stronę profilu](entity-profiles.md). Profil, który zapewnia kompleksowe szczegóły jednostki z usługi Active Directory, w tym powiązane z daną jednostką a jego historię aktywności w sieci.

Azure ATP dane osobowe są zbierane z usługi Active Directory przy użyciu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i przechowywane w wewnętrznej bazy danych.

## <a name="update-personal-data"></a>Zaktualizuj dane osobowe 

Dane osobiste użytkownika usługi Azure ATP jest tworzony na podstawie obiektu użytkownika w usłudze Active Directory w organizacji. W związku z tym zmiany wprowadzone do profilu użytkownika w organizacji AD są odzwierciedlane w narzędzia Azure ATP.


## <a name="delete-personal-data"></a>Usunięcie danych osobowych 

Po usunięciu użytkownika z usługi Active Directory w Twojej organizacji usługi Azure ATP automatycznie usuwa profil użytkownika i wszelkie działania związane z siecią w ciągu roku. Możesz również [Usuń](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) alertów zabezpieczeń, które zawierają dane osobowe. 

## <a name="export-personal-data"></a>Eksportowanie danych osobowych 

W przypadku narzędzia Azure ATP masz możliwość [wyeksportować](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informacje o alertach zabezpieczeń do programu Excel. Ta funkcja eksportuje również dane osobowe. 
 
## <a name="audit-personal-data"></a>Inspekcja danych osobowych

Narzędzie Azure ATP implementuje inspekcji zmian danych osobowych, włącznie z usunięciem i eksportowanie rekordów danych osobowych. Czas przechowywania dziennik inspekcji wynosi 90 dni. Inspekcji w usłudze Azure ATP jest funkcją zaplecza i nie jest dostępny dla klientów.
 
## <a name="additional-resources"></a>Dodatkowe zasoby

- Aby uzyskać informacje dotyczące relacji zaufania usługi Azure ATP i zgodności, zobacz [portal zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise RODO zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
