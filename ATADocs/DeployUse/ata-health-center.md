---
title: "Centrum kondycji usługi ATA | Microsoft ATA"
description: "Korzystając z centrum kondycji usługi ATA, można sprawdzić, czy usługa ATA działa prawidłowo, i otrzymywać alerty o potencjalnych problemach."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 9f408d7c2cb9c14caee175a1dd1c9ddb1baf9faa


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Centrum kondycji usługi ATA
Centrum kondycji usługi ATA umożliwia sprawdzenie, czy usługa ATA działa prawidłowo, i ostrzega o potencjalnych problemach.

## Praca z centrum kondycji usługi ATA
Centrum kondycji usługi ATA informuje o wystąpieniu problemu, wyświetlając symbol alertu (czerwoną kropkę) ponad ikoną centrum kondycji na pasku menu.

![Pasek narzędzi z centrum kondycji usługi ATA oznaczonym czerwoną kropką](media/ATA-Health-Center-Alert-red-dot.png)

### Zarządzanie kondycją usługi ATA
Aby sprawdzić ogólną kondycję systemu, kliknij ikonę centrum kondycji na pasku menu. ![Ikona centrum kondycji usługi ATA](media/ATA-red-dot.png)

-   Wszystkimi otwartymi alertami można zarządzać, zmieniając ich ustawienie na **Rozwiązane** lub **Odrzucone**. W oknie Alert kliknij pozycję **Otwarte**, a następnie przewiń w dół do pozycji **Rozwiązane** lub **Odrzucone**.

-   Jeśli problem zostanie rozwiązany, a usługa ATA wykryje, że problem nadal występuje, zostanie on automatycznie przeniesiony z powrotem na listę problemów **Otwarte**. Jeśli usługa ATA wykryje, że otwarty problem został rozwiązany, zostanie on automatycznie przeniesiony na listę problemów **Rozwiązane**.

-   Jeśli nie chcesz, aby usługa ATA kontynuowała sprawdzanie określonych problemów, przenieś je na listę **Odrzucone**. Jeśli na przykład otrzymasz alert dotyczący problemu, który znasz i nie planujesz go rozwiązywać, ale nie chcesz otrzymywać powiadomień o tym problemie i nie chcesz, aby ten problem był wyświetlany na liście **Otwarte**, możesz ustawić dla tego problemu stan **Odrzucone**.

![Obraz problemów w centrum kondycji usługi ATA](media/ATA-Health-Issue.JPG)

## Zobacz też
- [Praca z ustawieniami wykrywania usługi ATA](working-with-detection-settings.md)
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


