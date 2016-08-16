---
title: "Zmienianie konfiguracji usługi ATA — hasło do łączności z domeną | Microsoft ATA"
description: "Zawiera opis sposobu zmiany hasła do łączności z domeną w ramach bramy usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 7b8904bcb379004b2038e6b9a14c87c3914f1e1f


---

# Zmienianie konfiguracji usługi ATA — hasło do łączności z domeną

>[!div class="step-by-step"]
[« Certyfikat usług IIS](modifying-ata-config-iiscert.md)


## Zmienianie hasła do łączności z domeną
Podczas modyfikowania hasła do łączności z domeną upewnij się, czy wprowadzone hasło jest prawidłowe. Jeśli nie jest, usługa bramy usługi ATA przestanie działać w bramach usługi ATA.

Jeśli podejrzewasz, że taka sytuacja ma miejsce, w bramie usługi ATA sprawdź, czy w pliku Microsoft.Tri.Gateway-Errors.log znajduje się następujący komunikat:
`The supplied credential is invalid.`

Aby rozwiązać ten problem, wykonaj poniższą procedurę w celu zaktualizowania hasła do łączności z domeną w bramie usługi ATA:

1.  Otwórz konsolę usługi ATA w bramie usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Ogólne**.

    ![Obraz przedstawiający zmianę hasła bramy usługi ATA](media/ATA-GW-change-DC-password.JPG)

4.  W obszarze **Ogólne** zmień hasło.

5.  Kliknij polecenie **Zapisz**.

6.  Po zmianie hasła ręcznie sprawdź, czy brama usługi ATA jest uruchomiona na serwerach bramy usługi ATA.

>[!div class="step-by-step"]
[« Certyfikat usług IIS](modifying-ata-config-iiscert.md)

## Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


