---
title: "Tag kont poufnych przy użyciu usługi ATA | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tagu kont poufnych przy użyciu Advanced Threat Analytics (ATA)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d9666c0a4fb3aad027ac1f85719bc533e919d75a
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="tag-sensitive-accounts"></a>Konta poufne tag

Można ręcznie oznaczać grup lub kont jako poufne, w celu ułatwienia wykrycia. Koniecznie upewnij się, że ta wartość jest aktualizowana, ponieważ niektóre wykrywania usługi ATA, takich jak grupy poufnej modyfikacji wykrywania i ścieżka penetracja sieci, zależą od tego, które grupy i konta są traktowane jako poufne. Wcześniej, usługa ATA automatycznie traktowane jednostki *poufnych* Jeśli jest członkiem określonej listy grup. Można teraz ręcznie oznaczyć innym użytkownikom lub grupom jako poufne, takich jak elementy członkowskie tablicy, członkowie kadry kierowniczej w firmie, dyrektor sprzedaży itd., a usługi ATA będzie uwzględniać ich poufnych.

1.  W konsoli usługi ATA kliknij **konfiguracji** przypominającą koło zębate ikonę na pasku menu.

2.  W obszarze **wykrywania,** kliknij **tagi jednostek**.

    ![Tagi jednostek usługi ATA](media/entity-tags.png)

3.  W **poufnych** sekcji, wpisz nazwę **kont poufnych** i **poufnych grup** , a następnie kliknij przycisk  **+**  Zaloguj się dodać je.

    ![Przykładowe poufne konto usługi ATA](media/sensitive-account-sample.png)

4. Kliknij polecenie **Zapisz**.

5. Przejdź do strony profilu jednostki, klikając nazwę podmiotu. Tutaj można zobaczyć, dlaczego jednostki jest traktowane jako poufne — z powodu przynależności do grupy lub z powodu Ręczne znakowanie jako poufne.

     
## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
