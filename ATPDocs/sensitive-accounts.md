---
title: Tag kont poufnych z Azure ATP | Dokumentacja firmy Microsoft
description: "Opisuje sposób tagu kont poufnych przy użyciu usługi Azure Advanced Threat ochrony (ATP)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4270ebda76309e19518f9d49b72bbce7f9bb5f32
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection wersji 1.9*



# <a name="working-with-sensitive-accounts"></a>Praca z kont poufnych

## <a name="sensitive-groups"></a>Wrażliwe grupy

Poniższa lista grup są traktowane jako wrażliwe przez Azure ATP. Każda jednostka, która należy do poniższych grup, jest traktowana jako wrażliwa:

-   Administratorzy
-   Użytkownicy zaawansowani
-   Operatorzy kont
-   Operatorzy serwerów
-   Operatorzy drukowania
-   Operatorzy kopii zapasowych
-   Replikatorzy
-   Użytkownicy pulpitu zdalnego 
-   Operatorzy konfiguracji sieci 
-   Konstruktorzy przychodzących zaufań lasu
-   Administratorzy domeny
-   Kontrolery domeny
-   Twórcy-właściciele zasad grupy 
-   Kontrolery domeny tylko do odczytu 
-   Kontrolery domeny tylko do odczytu 
-   Administratorzy schematu 
-   Enterprise Admins


## <a name="tagging-sensitive-accounts"></a>Znakowanie kont poufnych

Oprócz tych grup można ręcznie oznaczać grup lub kont jako poufne, w celu ułatwienia wykrycia. Jest to ważne, ponieważ korzystają wykryć niektórych ATP Azure, takich jak grupy poufnej modyfikacji wykrywania i ścieżka penetracja sieci, na które grupy i konta są traktowane jako poufne. Można ręcznie oznaczyć innym użytkownikom lub grupom jako poufne, takich jak elementy członkowskie tablicy, członkowie kadry kierowniczej w firmie, dyrektor sprzedaży itd., a Azure ATP uzna je poufnych.

1.  W portalu Azure ATP obszaru roboczego kliknij **konfiguracji** przypominającą koło zębate ikonę na pasku menu.

2.  W obszarze **wykrywania** kliknij **tagi jednostek**.

    ![Azure tagi jednostek ATP](media/entity-tags.png)

3.  W **poufnych** sekcji, wpisz nazwę **kont poufnych** i **poufnych grup** , a następnie kliknij przycisk  **+**  Zaloguj się dodać je.

    ![Przykładowe poufne konto w usłudze Azure ATP](media/sensitive-account-sample.png)

4. Kliknij polecenie **Zapisz**.

    
## <a name="see-also"></a>Zobacz też

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)