---
title: Ustawianie powiadomień usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak ustawić alerty usługi Azure ATP, dzięki czemu użytkownik jest powiadamiany o wykryciu podejrzanych działań.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362429"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="set-azure-atp-notifications"></a>Ustawianie powiadomień usługi Azure ATP

Narzędzie Azure ATP może generować powiadomienia po wykryciu podejrzanego działania i alertu kondycji, za pośrednictwem poczty e-mail. 

Aby otrzymywać powiadomienia na konkretny adres e-mail, ustaw następujące parametry:


1. W portalu usługi Azure ATP obszaru roboczego wybierz opcję Ustawienia na pasku narzędzi i wybierz **konfiguracji**.

![Ikona ustawień konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

2. Kliknij przycisk **powiadomienia**.
3. W obszarze **powiadomienia pocztowe**, określ powiadomienia, które mają być wysyłane za pośrednictwem poczty e-mail — mogą być wysyłane do nowych alertów (podejrzanych działań) i nowe problemy dotyczące kondycji. 
 
 >  [!NOTE]
 >   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.
 
4. Kliknij polecenie **Zapisz**.

 ![Powiadomienia usługi Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Określanie ustawień usługi Syslog](setting-syslog.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
