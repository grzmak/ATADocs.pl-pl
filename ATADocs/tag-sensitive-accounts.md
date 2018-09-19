---
title: Tagowanie poufnych kont za pomocą usługi ATA | Dokumentacja firmy Microsoft
description: W tym artykule opisano jak oznaczyć wrażliwych kont przy użyciu Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cea6d666d3d969070541fc8dcc4fd59726ac8c38
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134093"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="tag-sensitive-accounts"></a>Tagowanie poufnych kont

Można ręcznie oznaczyć kont jako poufne lub grup w celu zwiększenia wykrywania. Należy się upewnić, że to jest aktualizowany, ponieważ niektóre mechanizmy wykrywania usługi ATA, np. wykrywania modyfikacji wrażliwych grup i ścieżki ruchu poprzecznego zależą od tego, które grupy i konta są traktowane jako poufne. Wcześniej, usługa ATA automatycznie traktowane jako jednostki *poufnych* Jeśli był członkiem określonej listy grup. Innym użytkownikom lub grupom jako poufne, takie jak elementy członkowskie tablicy, kierownictwo firmy, Dyrektor ds. sprzedaży, itp. teraz możesz ręcznie oznaczyć, a usługa ATA będzie należy wziąć pod uwagę ich wielkość liter.

1.  W konsoli usługi ATA kliknij **konfiguracji** koło zębate na pasku menu.

2.  W obszarze **wykrywania,** kliknij **tagów jednostki**.

    ![Tagi jednostek usługi ATA](media/entity-tags.png)

3.  W **poufnych** sekcji, wpisz nazwę **wrażliwym kontom** i **wrażliwych grup** a następnie kliknij przycisk **+** Zaloguj się dodać je.

    ![Przykładowe poufne konto usługi ATA](media/sensitive-account-sample.png)

4. Kliknij polecenie **Zapisz**.

5. Przejdź do strony profilu jednostki, klikając nazwę jednostki. Tutaj można zobaczyć, dlaczego jednostki jest traktowana jako wrażliwa — czy ze względu na przynależność do grupy lub z powodu ręczne tagowania jako poufne.


## <a name="sensitive-groups"></a>Wrażliwe grupy

Poniższa lista grup są traktowane jako wrażliwe przez usługę ATA. Każda jednostka, która należy do poniższych grup, jest traktowana jako wrażliwa:

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
     
## <a name="see-also"></a>Zobacz także
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
