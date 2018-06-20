---
title: Monitorowanie kondycji systemu Azure Advanced Threat Protection i zdarzenia | Dokumentacja firmy Microsoft
description: Sprawdź, jak działa usługa Azure ATP za pomocą Centrum kondycji obszaru roboczego Azure ATP oraz otrzymywać alerty o potencjalnych problemach i wyświetlać zdarzenia systemowe w Podglądzie zdarzeń.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86eb90f452d5aee2504e525e64bfc62c22207880
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446022"
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Praca z Azure ATP obszaru roboczego kondycji i zdarzeń

## <a name="azure-atp-workspace-health-center"></a>Centrum kondycji obszaru roboczego w usłudze Azure ATP 

Centrum kondycji obszaru roboczego Azure ATP informuje o tym, jak działa obszaru roboczego Azure ATP i problemów, jeśli występują problemy.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Praca z Centrum kondycji Azure ATP obszaru roboczego

Centrum kondycji obszaru roboczego Azure ATP informuje o tym, że występuje problem, wyświetlając symbol alertu (czerwoną kropkę) ponad ikoną Centrum kondycji na pasku menu.

![Azure narzędzi czerwonej kropki Centrum kondycji ATP obszaru roboczego](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Zarządzanie Azure ATP kondycji obszaru roboczego
Aby sprawdzić ogólną kondycję obszaru roboczego, kliknij ikonę Centrum kondycji na pasku menu ![Ikona Centrum kondycji Azure ATP obszaru roboczego](media/atp-red-dot.png)

-   Wszystkie otwarte problemy mogą być zarządzane przez ustawienie **Zamknij**, lub **Pomiń**, klikając wielokropek rogu alert i dokonaniu wyboru.

-   **Otwórz**: Na tej liście są wyświetlane wszystkie nowe podejrzane działania.

-   **Zamknij**: służy do śledzenia podejrzanych działań, które zidentyfikowane, zbadane i naprawione lub uniemożliwione.

    > [!NOTE]
    > W przypadku wykrycia tego samego działania ponownie w krótkim czasie Azure ATP może ponownie otworzyć zamkniętego działania.
    > Każdy obszar roboczy ma własne Centrum kondycji.

-   **Pomiń**: Pomijanie działania oznacza, że chcesz je na razie zignorować i otrzymywać alerty ponownie tylko w przypadku nowego wystąpienia. Jeśli alert podobne Azure ATP nie otwórz go ponownie. Jednak jeśli alert zatrzymuje na siedem dni, a następnie pojawia się ponownie, zostanie wyświetlony alert ponownie.

-   **Otwórz ponownie**: Jeśli zamknąć lub pominąć problemu, możesz uruchomić go zostanie otwarty ponownie na osi czasu.
- 
- **Usuń**: Z wewnątrz osi czasu podejrzanych działań, masz również opcję, aby usunąć problem z kondycją. Jeśli usuniesz alertu, zostaje usunięte z obszaru roboczego i nie można go przywrócić. Po kliknięciu przycisku usuwania będzie można usunąć wszystkie podejrzane działania tego samego typu.



![Azure obraz problemów Centrum kondycji ATP obszaru roboczego](media/atp-health-issue.png)






## <a name="see-also"></a>Zobacz też

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
