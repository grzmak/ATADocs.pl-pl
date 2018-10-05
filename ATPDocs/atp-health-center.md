---
title: Monitorowanie usługi Azure Advanced Threat Protection kondycją i zdarzeniami systemu | Dokumentacja firmy Microsoft
description: Użyj Centrum kondycji usługi Azure ATP obszar roboczy, aby sprawdzić, czy działa usługa Azure ATP i otrzymywać alerty o potencjalnych problemach i wyświetlać zdarzenia systemowe w Podglądzie zdarzeń.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8fdaa7311d39680ed8e9389f5dc9b7cdeca73197
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782900"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Praca z kondycją obszaru roboczego usługi Azure ATP i zdarzeniami

## <a name="azure-atp-workspace-health-center"></a>Centrum kondycji obszaru roboczego usługi Azure ATP 

Centrum kondycji obszaru roboczego usługi Azure ATP informuje o tym, jak działa obszaru roboczego usługi Azure ATP i ostrzega, gdy występują problemy.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Praca z Centrum kondycji usługi Azure ATP obszaru roboczego

Centrum kondycji obszaru roboczego usługi Azure ATP poinformuje Cię o tym, że występuje problem, wyświetlając symbol alertu (czerwoną kropkę) ponad ikoną Centrum kondycji na pasku menu.

![Usługa Azure narzędzi czerwonej kropki Centrum kondycji zaawansowanej ochrony przed zagrożeniami obszaru roboczego](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Zarządzanie kondycji obszaru roboczego usługi Azure ATP
Aby sprawdzić ogólną kondycję obszaru roboczego, kliknij ikonę Centrum kondycji na pasku menu ![Ikona Centrum kondycji platformy Azure ATP obszaru roboczego](media/atp-red-dot.png)

-   Wszystkie otwarte problemy mogą być zarządzane przez ich ustawienie **Zamknij**, lub **Pomiń**, klikając trzy kropki znajdujące się w górnym roku alertu i dokonaniu wyboru.

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: jest używane do śledzenia podejrzanych działań, które identyfikowane, zbadane i stałej uniemożliwione.

    > [!NOTE]
    > Narzędzie Azure ATP może ponownie otworzyć zamknięte działanie w przypadku wykrycia tego samego działania ponownie w krótkim czasie.
    
-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Jeśli istnieje podobny alert usługi Azure ATP nie otworzyć go ponownie. Ale jeśli alert zatrzymuje przez siedem dni, a następnie zostanie zauważony ponownie, zostanie wyświetlony alert ponownie.

-   **Otwórz ponownie**: Możesz ponownie otworzyć problem zamknięte lub pominięte wygląda tak, jakby Otwórz ponownie na osi czasu.

-   **Usuń**: Z w obrębie osi czasu podejrzanych działań, masz również opcję, aby usunąć problem z kondycją. Jeśli usuniesz alert, jest on usuwany z obszaru roboczego i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.



![Obraz problemów z Centrum kondycji usługi Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Zobacz też

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
