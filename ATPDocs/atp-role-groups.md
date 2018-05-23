---
title: Azure Advanced Threat Protection roli grup do zarządzania dostępem | Dokumentacja firmy Microsoft
description: Przeprowadzi Cię przez Praca z grupami roli Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77a2464634b4286d2f6d35504e9ab7512cf7b612
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
*Dotyczy: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure grup ról ATP

Azure ATP oferuje opartej na rolach zabezpieczeń, aby chronić dane w zależności od określonych potrzeb zabezpieczeń i zgodności organizacji. Azure ATP obsługuje trzy poszczególne role: Administratorzy, użytkownicy i przeglądarki. 

> [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) i [GDPR sekcji witryny Microsoft 365 Enterprise zgodności](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Rola grupy umożliwiają zarządzanie dostępem dla platformy Azure ATP. Korzystając z grup ról, można segregować obowiązki w obrębie zespołu zabezpieczeń i udzielać uprawnień dostępu w minimalnym zakresie potrzebnym użytkownikom do wykonania zadań. W tym artykule opisano zarządzania dostępem i autoryzacji ról Azure ATP oraz pomaga w szybkim rozpoczynaniu pracy związanej z grupami roli w ATP.

> [!NOTE]
> Wszelkie administrator globalny lub administrator zabezpieczeń w dzierżawcy usługi Azure Active Directory jest automatycznie administrator Azure ATP.

## <a name="accessing-the-workspace-management-portal"></a>Uzyskiwanie dostępu do portalu zarządzania obszaru roboczego

Dostęp do portalu zarządzania obszaru roboczego (portal.atp.azure.com) można wykonywać tylko przez użytkownika usługi Azure AD z rolą katalogu globalnego administratora lub administratora zabezpieczeń. Po wprowadzeniu portalu można utworzyć różne obszary robocze. Dla każdego obszaru roboczego usługi Azure ATP tworzy trzech grup zabezpieczeń w dzierżawie usługi Azure Active Directory: Administratorzy, użytkownicy, przeglądarki. 

> [!NOTE]
> Dostęp do portalu Azure ATP obszaru roboczego otrzymuje się tylko do użytkowników w grupach zabezpieczeń usługi Azure AD dla tego obszaru roboczego, a administratorzy globalni i Administratorzy zabezpieczeń.


## <a name="types-of-azure-atp-security-groups"></a>Typy grup zabezpieczeń usługi Azure ATP 

Azure ATP przedstawiono trzy rodzaje grupy zabezpieczeń: Azure ATP *nazwa obszaru roboczego* Administratorzy, Azure ATP *nazwa obszaru roboczego* użytkowników i Azure ATP *nazwa obszaru roboczego* przeglądarki . W poniższej tabeli opisano typu dostępu w portalu obszaru roboczego Azure ATP dostępne dla każdej roli. W zależności od roli można przypisać, różnych ekrany i opcje menu w Azure ATP portalu obszaru roboczego nie są dostępne, w następujący sposób:

|Aktywność |Azure ATP *nazwa obszaru roboczego* administratorów|Azure ATP *nazwa obszaru roboczego* użytkowników|Azure ATP *nazwa obszaru roboczego* przeglądarki|
|----|----|----|----|
|Logowanie|Dostępne|Dostępne|Dostępne|
|Zmiana stanu podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Udostępnianie/eksportowanie podejrzanych działań za pośrednictwem poczty e-mail/pobrania linku|Dostępne|Dostępne|Dostępne|
|Zmiana stanu alertów monitorowania|Dostępne|Niedostępne|Niedostępne|
|Zaktualizuj konfigurację Azure ATP|Dostępne|Niedostępne|Niedostępne|
|Czujnik — Dodaj|Dostępne|Niedostępne|Niedostępne|
|Czujnik — Delete |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — dodawanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — usuwanie|Dostępne|Niedostępne|Niedostępne|
|Wyświetlanie alertów i podejrzanych działań|Dostępne|Dostępne|Dostępne|


Gdy użytkownicy próbują uzyskać dostęp do strony, która nie jest dostępna dla grupy, roli, zostanie przekierowany do strony nieautoryzowanego Azure ATP. 

## <a name="add-and-remove-users"></a>Dodawanie i usuwanie użytkowników 

Azure ATP używa grup zabezpieczeń usługi Azure AD jako podstawy do grup ról. Grupy roli można zarządzać za pomocą [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All grup](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  Tylko użytkowników usługi AAD może być dodane lub usunięte z grup zabezpieczeń. 


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/aatpsizingtool)
- [Architektura usługi ATA](atp-architecture.md)
- [Instalowanie usługi ATA](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)

