---
title: Zmienianie konfiguracji usługi Advanced Threat Analytics — hasło do łączności z domeną | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu zmiany hasła do łączności z domeną w ramach bramy usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5c84806dd12e516d1d7b61064906ed57bfd6db72
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133280"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Zmienianie konfiguracji usługi ATA — hasło do łączności z domeną



## <a name="change-the-domain-connectivity-password"></a>Zmienianie hasła do łączności z domeną
Podczas modyfikowania hasła do łączności z domeną upewnij się, czy wprowadzone hasło jest prawidłowe. Jeśli nie jest dostępne, bramy usługi ATA przestaje działać w bramach usługi ATA.

Jeśli podejrzewasz, że to miejsce, w bramie usługi ATA Sprawdź w pliku Microsoft.Tri.Gateway-Errors.log wystąpiły następujące błędy: `The supplied credential is invalid.`

Aby rozwiązać ten problem, wykonaj poniższą procedurę w celu zaktualizowania hasła łączności z domeną w centrum usługi ATA:

1.  Otwórz konsolę usługi ATA w centrum usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

3.  Wybierz pozycję **Usługi katalogowe**.

    ![Obraz przedstawiający zmianę hasła bramy usługi ATA](media/ATA-GW-change-DC-password.png)

4.  W obszarze **Hasło** zmień hasło.

    Jeśli Centrum usługi ATA ma łączność z domeną, użyj **Testuj połączenie** przycisk, aby zweryfikować poświadczenia

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie sprawdź, czy brama usługi ATA jest uruchomiona na serwerach bramy usługi ATA.



## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
