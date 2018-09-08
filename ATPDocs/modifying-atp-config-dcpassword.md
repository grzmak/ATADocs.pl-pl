---
title: Zmienianie konfiguracji usługi Azure Advanced Threat Protection — hasło do łączności z domeną | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak zmienić hasło łączności domenowej na czujnik autonomiczny narzędzia Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e5b3fd544fb52cd2979ab95d34918ffba3f56541
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166191"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Zmienianie konfiguracji portalu obszaru roboczego usługi Azure ATP — hasło do łączności z domeną



## <a name="change-the-domain-connectivity-password"></a>Zmienianie hasła do łączności z domeną
Jeśli trzeba zmodyfikować hasła do łączności z domeną, upewnij się, że wprowadzone hasło jest poprawne. Jeśli nie jest, usługa czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zatrzymuje się dla wszystkich czujników wdrożone.

Jeśli podejrzewasz, że to miejsce, w narzędzia Azure ATP czujnik autonomiczny, Przyjrzyj się plik Microsoft.Tri.sensor-Errors.log wystąpiły następujące błędy: `The supplied credential is invalid.`

Wykonaj poniższą procedurę w celu zaktualizowania hasła łączności z domeną, w portalu obszaru roboczego usługi Azure ATP:

> [!NOTE]
> Jest to nazwa użytkownika i hasło z lokalnego wdrożenia usługi Active Directory, a nie z usługi Azure AD.

1.  Otwórz portal obszaru roboczego usługi Azure ATP na, uzyskując dostęp do adresu URL obszaru roboczego.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

3.  Wybierz pozycję **Usługi katalogowe**.

    ![Czujnik autonomiczny usługi Azure ATP zmiany hasła obrazu](media/directory-services.png)

4.  W obszarze **Hasło** zmień hasło.

 > [!NOTE]
 > Wprowadź hasło w tym miejscu nie usługi Azure Active Directory i użytkownika usługi Active Directory.

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie Sprawdź, czy usługa czujnika autonomicznego narzędzia Azure ATP jest uruchomiona na serwerach czujnik autonomiczny narzędzia Azure ATP.

7. W portalu obszaru roboczego w obszarze **konfiguracji**, przejdź do **czujnik** strony, a następnie sprawdź stan czujników.

## <a name="see-also"></a>Zobacz też

- [Integracja z usługą Windows Defender ATP](integrate-wd-atp.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)