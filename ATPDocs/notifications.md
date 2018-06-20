---
title: Ustawianie powiadomień Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje sposób ustawiania alertów Azure ATP, użytkownik jest powiadamiany o wykryciu podejrzanych działań.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 85fe887df373d8132df932cdb3d1eaf5ab954a1d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445980"
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="set-azure-atp-notifications"></a>Ustawianie powiadomień Azure ATP

Azure ATP mogą wyświetlać powiadomienia po wykryciu podejrzanego działania lub w przypadku wystąpienia alertu health za pośrednictwem poczty e-mail. 

Aby otrzymywać powiadomienia na konkretny adres e-mail, ustaw następujące parametry:


1. W portalu Azure ATP obszaru roboczego wybierz opcję ustawień, na pasku narzędzi i wybierz **konfiguracji**.

![Ikona ustawień konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

2. Kliknij przycisk **powiadomienia**.
3. W obszarze **powiadomienia E-mail**, określ powiadomienia, które mają być wysyłane za pośrednictwem poczty e-mail — mogą być wysyłane do nowych alertów (podejrzanych działań) i nowe problemy kondycji. 
 
 >  [!NOTE]
 >   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.

5. Kliknij polecenie **Zapisz**.

 ![Azure powiadomienia ATP](media/atp-notifications.png)



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Ustawienia dziennika systemowego](setting-syslog.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)