---
title: "Azure Advanced Threat Protection roli grup do zarządzania dostępem | Dokumentacja firmy Microsoft"
description: "Przeprowadzi Cię przez Praca z grupami roli Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86cb55fd2b5ce81460dead4b8b753c88f79edd7b
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure grup ról ATP

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
|Wprowadzanie danych wejściowych dotyczących podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Udostępnianie/eksportowanie podejrzanych działań za pośrednictwem poczty e-mail/pobrania linku|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu alertów monitorowania|Dostępne|Dostępne|Niedostępne|
|Zaktualizuj konfigurację Azure ATP|Dostępne|Niedostępne|Niedostępne|
|Czujnik — Dodaj|Dostępne|Niedostępne|Niedostępne|
|Czujnik — Delete |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — dodawanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — usuwanie|Dostępne|Niedostępne|Niedostępne|
|Wyświetlanie alertów i podejrzanych działań|Dostępne|Dostępne|Dostępne|


Gdy użytkownicy próbują uzyskać dostęp do strony, która nie jest dostępna dla grupy, roli, zostanie przekierowany do strony nieautoryzowanego Azure ATP. 

## <a name="add-and-remove-users"></a>Dodawanie i usuwanie użytkowników 

Azure ATP używa grup zabezpieczeń usługi Azure AD jako podstawy do grup ról. Grupy roli można zarządzać za pomocą [grup https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  Tylko użytkowników usługi AAD może być dodane lub usunięte z grup zabezpieczeń. 


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/aatpsizingtool)
- [Architektura usługi ATA](atp-architecture.md)
- [Instalowanie usługi ATA](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)

