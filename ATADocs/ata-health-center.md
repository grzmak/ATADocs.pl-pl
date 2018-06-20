---
title: Monitorowanie kondycji i zdarzeń systemu Advanced Threat Analytics | Microsoft Docs
description: Korzystając z centrum kondycji usługi ATA, można sprawdzić, czy usługa ATA działa prawidłowo, otrzymywać alerty o potencjalnych problemach i wyświetlać zdarzenia systemowe w podglądzie zdarzeń.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0c8eb2c368a81a64e62f79b9fb606b9fc04efd8b
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009789"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*


# <a name="working-with-ata-system-health-and-events"></a>Praca z kondycją i zdarzeniami systemu ATA

## <a name="ata-health-center"></a>Centrum kondycji usługi ATA
Centrum kondycji usługi ATA umożliwia sprawdzenie, czy usługa ATA działa prawidłowo, i ostrzega o potencjalnych problemach.

## <a name="working-with-the-ata-health-center"></a>Praca z centrum kondycji usługi ATA
Centrum kondycji usługi ATA informuje o wystąpieniu problemu, wyświetlając symbol alertu (czerwoną kropkę) ponad ikoną centrum kondycji na pasku menu.

![Pasek narzędzi z centrum kondycji usługi ATA oznaczonym czerwoną kropką](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Zarządzanie kondycją usługi ATA
Aby sprawdzić ogólną kondycję systemu, kliknij ikonę centrum kondycji na pasku menu. ![Ikona centrum kondycji usługi ATA](media/ATA-red-dot.png)

-   Wszystkimi otwartymi alertami można zarządzać zmieniając ich ustawienie na **Zamknij**, **Pomiń**, lub **usunąć** klikając wielokropek rogu alert i dokonaniu wyboru.

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: służy do śledzenia podejrzanych działań, które zidentyfikowane, zbadane i naprawione lub uniemożliwione.

    > [!NOTE]
    > Usługa ATA może ponownie otworzyć zamknięte działanie w przypadku wykrycia tego samego działania ponownie w krótkim czasie.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. W przypadku podobnych alertów usługi ATA nie otwórz go ponownie. Jednak jeśli alert zatrzymuje na siedem dni, a następnie pojawia się ponownie, zostanie wyświetlony alert ponownie.

- **Usuń**: Jeśli usuniesz alertu, zostaje usunięte z systemu z bazy danych i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.



![Obraz problemów w centrum kondycji usługi ATA](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Zobacz też

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
