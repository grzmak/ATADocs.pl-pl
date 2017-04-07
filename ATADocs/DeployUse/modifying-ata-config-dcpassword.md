---
title: "Zmienianie konfiguracji usługi Advanced Threat Analytics — hasło do łączności z domeną | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu zmiany hasła do łączności z domeną w ramach bramy usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e9cb7bcf6f32559f7b2f330df4333c3fdc55a283
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Zmienianie konfiguracji usługi ATA — hasło do łączności z domeną

>[!div class="step-by-step"]
[« Adres URL konsoli usługi ATA](modifying-ata-config-consoleurl.md)


## <a name="change-the-domain-connectivity-password"></a>Zmienianie hasła do łączności z domeną
Podczas modyfikowania hasła do łączności z domeną upewnij się, czy wprowadzone hasło jest prawidłowe. Jeśli nie jest, usługa bramy usługi ATA przestanie działać w bramach usługi ATA.

Jeśli podejrzewasz, że taka sytuacja ma miejsce, w bramie usługi ATA sprawdź, czy w pliku Microsoft.Tri.Gateway-Errors.log znajduje się następujący komunikat: `The supplied credential is invalid.`

Aby rozwiązać ten problem, wykonaj poniższą procedurę w celu zaktualizowania hasła łączności z domeną w centrum usługi ATA:

1.  Otwórz konsolę usługi ATA w centrum usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Usługi katalogowe**.

    ![Obraz przedstawiający zmianę hasła bramy usługi ATA](media/ATA-GW-change-DC-password.png)

4.  W obszarze **Hasło** zmień hasło.

    Jeśli Centrum usługi ATA ma łączność z domeną, użyj przycisku **Testuj połączenie**, aby zweryfikować poświadczenia.

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie sprawdź, czy brama usługi ATA jest uruchomiona na serwerach bramy usługi ATA.

>[!div class="step-by-step"]
[« Adres URL konsoli usługi ATA](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
