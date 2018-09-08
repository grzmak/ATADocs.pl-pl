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
ms.openlocfilehash: 080b3469c862d4063db5a4832f63dd3614905fac
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166068"
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

5. Kliknij polecenie **Zapisz**.

 ![Powiadomienia usługi Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Określanie ustawień usługi Syslog](setting-syslog.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)