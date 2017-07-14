---
title: "Monitorowanie kondycji i zdarzeń systemu Advanced Threat Analytics | Microsoft Docs"
description: "Korzystając z centrum kondycji usługi ATA, można sprawdzić, czy usługa ATA działa prawidłowo, otrzymywać alerty o potencjalnych problemach i wyświetlać zdarzenia systemowe w podglądzie zdarzeń."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 59e5cafcff7b84ffb9dc161cd0b50cd3014e455a
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# Praca z kondycją i zdarzeniami systemu ATA
<a id="working-with-ata-system-health-and-events" class="xliff"></a>

## Centrum kondycji usługi ATA
<a id="ata-health-center" class="xliff"></a>
Centrum kondycji usługi ATA umożliwia sprawdzenie, czy usługa ATA działa prawidłowo, i ostrzega o potencjalnych problemach.

## Praca z centrum kondycji usługi ATA
<a id="working-with-the-ata-health-center" class="xliff"></a>
Centrum kondycji usługi ATA informuje o wystąpieniu problemu, wyświetlając symbol alertu (czerwoną kropkę) ponad ikoną centrum kondycji na pasku menu.

![Pasek narzędzi z centrum kondycji usługi ATA oznaczonym czerwoną kropką](media/ATA-Health-Center-Alert-red-dot.png)

### Zarządzanie kondycją usługi ATA
<a id="managing-ata-health" class="xliff"></a>
Aby sprawdzić ogólną kondycję systemu, kliknij ikonę centrum kondycji na pasku menu. ![Ikona centrum kondycji usługi ATA](media/ATA-red-dot.png)

-   Wszystkimi otwartymi alertami można zarządzać, zmieniając ich ustawienie na **Rozwiązane** lub **Odrzucone**. W oknie Alert kliknij pozycję **Otwarte**, a następnie przewiń w dół do pozycji **Rozwiązane** lub **Odrzucone**.

-   Jeśli problem zostanie rozwiązany, a usługa ATA wykryje, że problem nadal występuje, zostanie on automatycznie przeniesiony z powrotem na listę problemów **Otwarte**. Jeśli usługa ATA wykryje, że otwarty problem został rozwiązany, zostanie on automatycznie przeniesiony na listę problemów **Rozwiązane**.

-   Jeśli nie chcesz, aby usługa ATA kontynuowała sprawdzanie określonych problemów, przenieś je na listę **Odrzucone**. Jeśli na przykład otrzymasz alert dotyczący problemu, który znasz i nie planujesz go rozwiązywać, ale nie chcesz otrzymywać powiadomień o tym problemie i nie chcesz, aby ten problem był wyświetlany na liście **Otwarte**, możesz ustawić dla tego problemu stan **Odrzucone**.

![Obraz problemów w centrum kondycji usługi ATA](media/ATA-Health-Issue.JPG)






## Zobacz też
<a id="see-also" class="xliff"></a>

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
