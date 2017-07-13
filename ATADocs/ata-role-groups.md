---
title: "Grupy ról usługi Advanced Threat Analytics do zarządzania dostępem | Dokumentacja firmy Microsoft"
description: "Szczegółowe omówienie pracy z grupami ról usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/13/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1afb8e728fa359721d78833f8220cae3f65bd896
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*




# Grupy ról usługi ATA
<a id="ata-role-groups" class="xliff"></a>

Grupy ról umożliwiają zarządzanie dostępem do usługi ATA. Korzystając z grup ról, można segregować obowiązki w obrębie zespołu zabezpieczeń i udzielać uprawnień dostępu w minimalnym zakresie potrzebnym użytkownikom do wykonania zadań. W tym artykule przedstawiono sposób zarządzania dostępem i autoryzacji ról usługi ATA, co ułatwia rozpoczęcie korzystania z grup ról w usłudze w ATA.

> [!NOTE]
> Każdy lokalny administrator centrum usługi ATA jest automatycznie administratorem usługi Microsoft Advanced Threat Analytics.

## Typy grup ról usługi ATA
<a id="types-of-ata-role-groups" class="xliff"></a> 

Usługa ATA wprowadza 3 typy grup ról: administratorzy ATA, użytkownicy ATA oraz osoby przeglądające ATA. W poniższej tabeli opisano typy dostępu w usłudze ATA, z których mogą korzystać poszczególne role. W zależności od przypisanej roli różne ekrany i opcje menu w usłudze ATA będą niedostępne, zgodnie z poniższym zestawieniem:

|Aktywność |Administratorzy usługi Microsoft Advanced Threat Analytics|Użytkownicy usługi Microsoft Advanced Threat Analytics|Osoby przeglądające usługę Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Logowanie|Dostępne|Dostępne|Dostępne|
|Wprowadzanie danych wejściowych dotyczących podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Udostępnianie/eksportowanie podejrzanych działań za pośrednictwem poczty e-mail/pobrania linku|Dostępne|Dostępne|Niedostępne|
|Dodawanie/edytowanie komentarzy dotyczących podejrzanych działań|Dostępne|Dostępne|Niedostępne|
|Zmiana stanu alertów monitorowania|Dostępne|Dostępne|Niedostępne|
|Aktualizacja konfiguracji usługi ATA|Dostępne|Niedostępne|Niedostępne|
|Brama — dodawanie|Dostępne|Niedostępne|Niedostępne|
|Brama — usuwanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — dodawanie |Dostępne|Niedostępne|Niedostępne|
|Monitorowane DC — usuwanie|Dostępne|Niedostępne|Niedostępne|
|Wyświetlanie alertów i podejrzanych działań|Dostępne|Dostępne|Dostępne|


W przypadku próby uzyskania dostępu do strony, która nie jest dostępna dla danej grupy ról, użytkownicy zostaną przekierowani do nieautoryzowanej strony usługi ATA. 

## Dodawanie\usuwanie użytkowników — grupy ról usługi ATA
<a id="add--remove-users---ata-role-groups" class="xliff"></a> 

Usługa ATA korzysta z lokalnych grup systemu Windows jako podstawy dla grup ról. Grupy ról muszą być zarządzane na serwerze centrum usługi ATA.
Aby dodać lub usunąć użytkowników, należy użyć konsoli MMC **Użytkownicy i grupy lokalne** (Lusrmgr.msc). Na komputerze dołączonym do domeny można dodać konta domeny, a także konta lokalne. 

