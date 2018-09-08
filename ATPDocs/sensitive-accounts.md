---
title: Tagowanie poufnych kont za pomocą narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano jak oznaczyć wrażliwych kont przy użyciu usługi Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8b48b8090e109c9fc23c52b05f986b34e2549eb
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165885"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="working-with-sensitive-accounts"></a>Praca z kontami poufnymi

## <a name="sensitive-groups"></a>Wrażliwe grupy

Poniższa lista grup są traktowane jako wrażliwe przez narzędzia Azure ATP. Każda jednostka, która należy do poniższych grup, jest traktowana jako wrażliwa:

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
-   Kontrolery domeny tylko do odczytu przedsiębiorstwa 
-   Administratorzy schematu 
-   Enterprise Admins


## <a name="tagging-sensitive-accounts"></a>Tagowanie poufnych kont

Oprócz tych grup, można ręcznie oznaczyć kont jako poufne lub grup w celu zwiększenia wykrywania. Jest to ważne, ponieważ niektóre narzędzia Azure ATP wykrywania zagrożeń, takich jak wykrywania modyfikacji wrażliwych grup i ścieżki ruchu poprzecznego zależą od tego, które grupy i konta są traktowane jako poufne. Można ręcznie oznaczyć innym użytkownikom lub grupom jako poufne, takie jak elementy członkowskie tablicy, kierownictwo firmy, Dyrektor ds. sprzedaży, itp., a zaawansowanej ochrony przed zagrożeniami w usłudze Azure traktuje je poufnych.

1.  W portalu usługi Azure ATP obszaru roboczego kliknij **konfiguracji** koło zębate na pasku menu.

2.  W obszarze **wykrywania** kliknij **tagów jednostki**.

    ![Tagi jednostki usługi Azure ATP](media/entity-tags.png)

3.  W **poufnych** sekcji, wpisz nazwę **wrażliwym kontom** i **wrażliwych grup** a następnie kliknij przycisk **+** Zaloguj się dodać je.

    ![Przykładowy poufne konto usługi Azure ATP](media/sensitive-account-sample.png)

4. Kliknij polecenie **Zapisz**.

    
## <a name="see-also"></a>Zobacz także

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)