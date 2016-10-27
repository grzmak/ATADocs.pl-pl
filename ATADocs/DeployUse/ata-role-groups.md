---
title: "Kończenie pracy z grupami ról | Microsoft ATA"
description: "Szczegółowe omówienie pracy z grupami ról usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*




# Grupy ról usługi ATA

Grupy ról umożliwiają zarządzanie dostępem do usługi ATA. Korzystając z grup ról, można segregować obowiązki w obrębie zespołu zabezpieczeń i udzielać uprawnień dostępu w minimalnym zakresie potrzebnym użytkownikom do wykonania zadań. W tym artykule przedstawiono sposób zarządzania dostępem i autoryzacji ról usługi ATA, co ułatwia rozpoczęcie korzystania z grup ról w usłudze w ATA.
## Typy grup ról usługi ATA 

Usługa ATA wprowadza 3 typy grup ról: administratorzy ATA, analitycy ATA oraz kierownicy ATA. W poniższej tabeli opisano typy dostępu w usłudze ATA, z których mogą korzystać poszczególne role. W zależności od przypisanej roli różne ekrany i opcje menu w usłudze ATA będą niedostępne, zgodnie z poniższym zestawieniem:

|Aktywność |Administrator usługi Microsoft Advanced Threat Analytics|Analityk usługi Microsoft Advanced Threat Analytics|Kierownik usługi Microsoft Advanced Threat Analytics|
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

W przypadku próby uzyskania dostępu do strony, która nie jest dostępna dla danej grupy ról, użytkownicy zostaną przekierowani do nieautoryzowanej strony usługi ATA. 

## Dodawanie\usuwanie użytkowników — grupy ról usługi ATA 

Usługa ATA korzysta z lokalnych grup systemu Windows jako podstawy dla grup ról. Aby dodać lub usunąć użytkowników, należy użyć konsoli MMC **Użytkownicy i grupy lokalne** (Lusrmgr.msc). Na komputerze dołączonym do domeny można dodać konta domeny, a także konta lokalne. 




<!--HONumber=Sep16_HO4-->

