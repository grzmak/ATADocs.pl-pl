---
title: Zmienianie konfiguracji usługi Advanced Threat Analytics — hasło do łączności z domeną | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu zmiany hasła do łączności z domeną w ramach bramy usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 47bd7e9cdd97d8343202be86954e82e69948afed
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009313"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Zmienianie konfiguracji usługi ATA — hasło do łączności z domeną



## <a name="change-the-domain-connectivity-password"></a>Zmienianie hasła do łączności z domeną
Podczas modyfikowania hasła do łączności z domeną upewnij się, czy wprowadzone hasło jest prawidłowe. Jeśli nie, bramy usługi ATA przestanie działać w bramach usługi ATA.

Jeśli podejrzewasz, że to miejsce, w bramie usługi ATA przyjrzeć się pliku Microsoft.Tri.Gateway-Errors.log wystąpiły następujące błędy: `The supplied credential is invalid.`

Aby rozwiązać ten problem, wykonaj poniższą procedurę w celu zaktualizowania hasła łączności z domeną w centrum usługi ATA:

1.  Otwórz konsolę usługi ATA w centrum usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

3.  Wybierz pozycję **Usługi katalogowe**.

    ![Obraz przedstawiający zmianę hasła bramy usługi ATA](media/ATA-GW-change-DC-password.png)

4.  W obszarze **Hasło** zmień hasło.

    Jeśli Centrum usługi ATA ma łączności z domeną, użyj **Testuj połączenie** przycisk, aby zweryfikować poświadczenia

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie sprawdź, czy brama usługi ATA jest uruchomiona na serwerach bramy usługi ATA.



## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
