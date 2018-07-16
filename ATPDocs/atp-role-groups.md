---
title: Usługa Azure grupy ról zaawansowanej ochrony przed zagrożeniami dla zarządzania dostępem | Dokumentacja firmy Microsoft
description: Szczegółowe omówienie pracy z grupami ról usługi Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e7af3846d31031b645c65c7550b696fe4738e5d
ms.sourcegitcommit: a9b8bc26d3cb5645f21a68dc192b4acef8f54895
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2018
ms.locfileid: "39064070"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*




# <a name="azure-atp-role-groups"></a>Grupy ról usługi Azure ATP

Narzędzie Azure ATP oferuje oparte na rolach zabezpieczeń, aby chronić dane zgodnie z konkretnych potrzeb bezpieczeństwa i zgodności w organizacji. Narzędzie Azure ATP obsługuje trzy osobne role: Administratorzy, użytkownicy i osoby przeglądające. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Grupy ról umożliwiają zarządzanie dostępem do usługi Azure ATP. Korzystając z grup ról, można segregować obowiązki w obrębie zespołu zabezpieczeń i udzielać uprawnień dostępu w minimalnym zakresie potrzebnym użytkownikom do wykonania zadań. W tym artykule opisano zarządzanie dostępem i autoryzacji ról usługi Azure ATP oraz ułatwia rozpoczęcie pracy z grupami ról w usłudze ATP.

> [!NOTE]
> Wszelkie administratorem globalnym lub administratorem zabezpieczeń w ramach dzierżawcy usługi Azure Active Directory jest automatycznie administratorem usługi Azure ATP.

## <a name="accessing-the-workspace-management-portal"></a>Uzyskiwanie dostępu do portalu zarządzania obszarami roboczymi

Dostęp do portalu zarządzania obszarami roboczymi (portal.atp.azure.com) można wykonywać tylko przez użytkownika usługi Azure AD z rolą katalogu administratora globalnego lub administratora zabezpieczeń. Po wprowadzeniu portalu, można utworzyć różne obszary robocze. Dla każdego obszaru roboczego usługi Azure ATP tworzy trzy grupy zabezpieczeń w swojej dzierżawie usługi Azure Active Directory: Administratorzy, użytkownicy, przeglądarki. 

> [!NOTE]
> Dostęp do portalu obszaru roboczego usługi Azure ATP jest udzielone tylko do użytkowników w grupach zabezpieczeń usługi Azure AD dla tego obszaru roboczego, a administratorzy globalni i Administratorzy zabezpieczeń.


## <a name="types-of-azure-atp-security-groups"></a>Typy grup zabezpieczeń usługi Azure ATP 

Narzędzie Azure ATP wprowadza trzy typy grup zabezpieczeń: narzędzia Azure ATP *nazwa obszaru roboczego* Administratorzy, narzędzia Azure ATP *nazwa obszaru roboczego* użytkowników i usługi Azure ATP *nazwa obszaru roboczego* osoby przeglądające . W poniższej tabeli opisano typy dostępu w portalu obszaru roboczego usługi Azure ATP dostępne w poszczególnych ról. W zależności od rolę, która zostanie przypisana, różne ekrany i opcje menu w zaawansowanej ochrony przed zagrożeniami w usłudze Azure portal w obszarze roboczym nie są dostępne, w następujący sposób:

|Aktywność |Narzędzie Azure ATP *nazwa obszaru roboczego* administratorów|Narzędzie Azure ATP *nazwa obszaru roboczego* użytkowników|Narzędzie Azure ATP *nazwa obszaru roboczego* osoby przeglądające|
|----|----|----|----|
|Logowanie|Dostępne|Dostępne|Dostępne|
|Zmiana stanu podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Udostępnianie/eksportowanie podejrzanych działań za pośrednictwem poczty e-mail/pobrania linku|Dostępne|Dostępne|Dostępne|
|Zmiana stanu alertów monitorowania|Dostępne|Niedostępne|Niedostępne|
|Zaktualizuj konfigurację usługi Azure ATP|Dostępne|Niedostępne|Niedostępne|
|Czujnik — Dodaj|Dostępne|Niedostępne|Niedostępne|
|Czujnik — usuwanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — dodawanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — usuwanie|Dostępne|Niedostępne|Niedostępne|
|Wyświetlanie alertów i podejrzanych działań|Dostępne|Dostępne|Dostępne|


Gdy użytkownicy próbują uzyskać dostęp do strony, która nie jest dostępna dla danej grupy ról, zostanie przekierowany do nieautoryzowanej strony usługi Azure ATP. 

## <a name="add-and-remove-users"></a>Dodawanie i usuwanie użytkowników 


Narzędzie Azure ATP używa grup zabezpieczeń usługi Azure AD jako podstawy dla grup ról. Grupy ról, można zarządzać przy użyciu [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups ](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Tylko usługa Azure AD użytkownicy mogą dodane lub usunięte z grup zabezpieczeń. 

## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/aatpsizingtool)
- [Architektura usługi ATA](atp-architecture.md)
- [Instalowanie usługi ATA](install-atp-step1.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)

