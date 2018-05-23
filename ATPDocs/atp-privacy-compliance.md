---
title: Azure zasad danych osobowych Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Zawiera linki do informacji na temat sposobu usuwania prywatne informacje i dane osobowe z Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 1e890491b44bcf97a7f0f19d825155072ac1a2f4
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP danych zabezpieczenia i prywatność

> [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) i [GDPR sekcji witryny Microsoft 365 Enterprise zgodności](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="search-for-and-identify-personal-data"></a>Wyszukiwanie i identyfikowanie danych osobowych 

W usłudze Azure Advanced Threat Protection można wyświetlić identyfikowalne dane osobowe z [portalu obszaru roboczego](workspace-portal.md) przy użyciu [pasek wyszukiwania](workspace-portal.md#search-bar). 

Możesz wyszukać określonego użytkownika lub komputera, a kliknięcie jednostki spowoduje do użytkownika lub komputera [strony profilu](entity-profiles.md). Profil zapewnia kompleksowe szczegóły jednostki z usługi Active Directory, w tym sieci działania związane z jednostki i jej historii.

Azure danych osobowych ATP jest zbieranych z usługi Active Directory za pomocą czujnika Azure ATP i przechowywane w bazie danych zaplecza.

## <a name="update-personal-data"></a>Aktualizowanie danych osobowych 

Ponieważ dane osobiste użytkownika Azure ATP pochodzi z obiektu użytkownika w usłudze Active Directory organizacji, wszelkie zmiany wprowadzone do profilu użytkownika w usłudze AD zostaną odzwierciedlone w Azure ATP.


## <a name="delete-personal-data"></a>Usuwanie danych osobowych 

Po usunięciu użytkownika z usługi Active Directory w organizacji, Azure ATP automatycznie usuwa profilu użytkownika i wszelkie działania związane z siecią w roku. Możesz również [usunąć](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) alerty zabezpieczeń, które zawierają dane osobowe. 

## <a name="export-personal-data"></a>Eksportuj dane osobowe 

W usłudze Azure ATP masz możliwość [export]((working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) zabezpieczeń informacji o alertach do programu Excel. Będzie to również eksportować dane osobowe. 
 
## <a name="audit-personal-data"></a>Dane osobowe inspekcji

 
Azure ATP implementuje inspekcji zmian danych osobowych, włącznie z usunięciem i eksportowanie rekordów danych osobowych. Czas przechowywania dziennik inspekcji wynosi 90 dni. Inspekcji w usłudze Azure ATP jest funkcją zaplecza i nie jest dostępna dla klientów.
 

 

## <a name="additional-resources"></a>Dodatkowe zasoby

- Informacje dotyczące zaufania Azure ATP i zgodności, zobacz [portal usługi zaufania](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise GDPR zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
