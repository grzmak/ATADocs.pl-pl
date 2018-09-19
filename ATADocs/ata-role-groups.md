---
title: Grupy ról usługi Advanced Threat Analytics do zarządzania dostępem | Dokumentacja firmy Microsoft
description: Szczegółowe omówienie pracy z grupami ról usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ed4d112cda614053aa20a6a486cb29baa1fed58a
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133637"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*




# <a name="ata-role-groups"></a>Grupy ról usługi ATA

Grupy ról umożliwiają zarządzanie dostępem do usługi ATA. Korzystając z grup ról, można segregować obowiązki w obrębie zespołu zabezpieczeń i udzielać uprawnień dostępu w minimalnym zakresie potrzebnym użytkownikom do wykonania zadań. W tym artykule przedstawiono sposób zarządzania dostępem i autoryzacji ról usługi ATA, co ułatwia rozpoczęcie korzystania z grup ról w usłudze w ATA.

> [!NOTE]
> Każdy lokalny administrator centrum usługi ATA jest automatycznie administratorem usługi Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Typy grup ról usługi ATA 

Usługa ATA wprowadza trzy typy grup ról: Administratorzy ATA, użytkownicy ATA oraz osoby przeglądające ATA. W poniższej tabeli opisano typy dostępu w usłudze ATA, z których mogą korzystać poszczególne role. W zależności od roli, które można przypisać różne ekrany i menu opcji w usłudze ATA nie są dostępne, w następujący sposób:

|Aktywność |Administratorzy usługi Microsoft Advanced Threat Analytics|Użytkownicy usługi Microsoft Advanced Threat Analytics|Osoby przeglądające usługę Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Logowanie|Dostępne|Dostępne|Dostępne|
|Wprowadzanie danych wejściowych dotyczących podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Udostępnianie/eksportowanie podejrzanych działań za pośrednictwem poczty e-mail/pobrania linku|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu alertów monitorowania|Dostępne|Dostępne|Niedostępne|
|Aktualizacja konfiguracji usługi ATA|Dostępne|Niedostępne|Niedostępne|
|Brama — dodawanie|Dostępne|Niedostępne|Niedostępne|
|Brama — usuwanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — dodawanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — usuwanie|Dostępne|Niedostępne|Niedostępne|
|Wyświetlanie alertów i podejrzanych działań|Dostępne|Dostępne|Dostępne|


Gdy użytkownicy próbują uzyskać dostęp do strony, która nie jest dostępna dla danej grupy ról, zostanie przekierowany do nieautoryzowanej strony usługi ATA. 

## <a name="add--remove-users---ata-role-groups"></a>Dodawanie\usuwanie użytkowników — grupy ról usługi ATA 

Usługa ATA korzysta z lokalnych grup systemu Windows jako podstawy dla grup ról. Grupy ról muszą być zarządzane na serwerze centrum usługi ATA.
Aby dodać lub usunąć użytkowników, należy użyć konsoli MMC **Użytkownicy i grupy lokalne** (Lusrmgr.msc). Na komputerze dołączonym do domeny można dodać konta domeny, a także konta lokalne. 

