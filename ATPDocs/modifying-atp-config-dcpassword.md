---
title: Zmienianie konfiguracji usługi Azure Advanced Threat Protection — hasło do łączności z domeną | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu zmiany hasła do łączności domeny w czujnik autonomiczny Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 369f00b1b33fe509850bc331b0d5b45ae161f91c
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445966"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Zmienianie konfiguracji portalu obszaru roboczego Azure ATP — hasło do łączności z domeną



## <a name="change-the-domain-connectivity-password"></a>Zmienianie hasła do łączności z domeną
Jeśli trzeba zmodyfikować hasła do łączności z domeną, upewnij się, że wprowadzone hasło jest poprawna. Jeśli nie jest, usługa czujnik Azure ATP zatrzymuje się do wszystkich czujników wdrożone.

Jeśli podejrzewasz, że to miejsce, na czujnika autonomiczny Azure ATP przyjrzeć się plik Microsoft.Tri.sensor-Errors.log wystąpiły następujące błędy: `The supplied credential is invalid.`

Wykonaj tę procedurę, aby zaktualizować hasło łączności z domeną, w portalu Azure ATP obszaru roboczego:

> [!NOTE]
> Jest to nazwa użytkownika i hasło, z lokalnego wdrożenia usługi Active Directory, a nie z usługi Azure AD.

1.  Otwórz portal obszaru roboczego Azure ATP na uzyskując dostęp do adresu URL obszaru roboczego.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

3.  Wybierz pozycję **Usługi katalogowe**.

    ![Azure czujnik autonomiczny ATP zmiany hasła obrazu](media/directory-services.png)

4.  W obszarze **Hasło** zmień hasło.

 > [!NOTE]
 > Wprowadź użytkownika usługi Active Directory i hasło w tym miejscu nie usługi Azure Active Directory.

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie Sprawdź, czy Azure ATP autonomiczna czujnik usługa jest uruchomiona na serwerach czujnik autonomiczny Azure ATP.

7. W portalu obszaru roboczego w obszarze **konfiguracji**, przejdź do **czujnik** sprawdzić stan czujników i strony.

## <a name="see-also"></a>Zobacz też

- [Integracja z usługą Windows Defender ATP](integrate-wd-atp.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)