---
title: Ustawianie powiadomień usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak ustawić alerty zabezpieczeń usługi Azure ATP, dzięki czemu użytkownik jest powiadamiany o wykryciu podejrzanych działań.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: acbab806e7f49052e0789927f452217c12efd992
ms.sourcegitcommit: 8cb370eab974652451066570e435d8a4f304fa29
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/15/2018
ms.locfileid: "49326765"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="set-azure-atp-notifications"></a>Ustawianie powiadomień usługi Azure ATP

Narzędzie Azure ATP może generować powiadomienia w przypadku wykrycia podejrzanych działań i generuje alert zabezpieczeń lub alertu kondycji, za pośrednictwem poczty e-mail. 

Aby otrzymywać powiadomienia na konkretny adres e-mail, ustaw następujące parametry:


1. W portalu usługi Azure ATP wybierz opcję ustawień, na pasku narzędzi i wybierz **konfiguracji**.

 ![Ikona ustawień konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

2. Kliknij przycisk **powiadomienia**.
3. W obszarze **powiadomienia pocztowe**, określ powiadomienia, które mają być wysyłane za pośrednictwem poczty e-mail — mogą być wysyłane do nowych alertów (podejrzanych działań) i nowe problemy dotyczące kondycji. 
 
 >  [!NOTE]
 > Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.
 
4. Kliknij polecenie **Zapisz**.

 ![Powiadomienia usługi Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Określanie ustawień usługi Syslog](setting-syslog.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
