---
title: "Praca z dziennikami inspekcji usługi ATA | Microsoft Docs"
description: "W tym artykule opisano sposób pracy z dziennikami inspekcji usługi ATA w dzienniku zdarzeń systemu Windows."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2b7489e9057828ea452d55ddb01b37e0a1c16e2f
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*

# <a name="working-with-ata-audit-logs"></a>Praca z dziennikami inspekcji usługi ATA

Dzienniki inspekcji usługi ATA są przechowywane w dziennikach zdarzeń systemu Windows w obszarze **Aplikacje i usługi**, a następnie **Microsoft ATA** zarówno na komputerze centrum usługi ATA, jak i bramy usługi ATA.

Dziennik inspekcji centrum usługi ATA zawiera:
-   Informacje o podejrzanym działaniu
-   Alerty monitorowania (strona kondycji)
-   Logowania do konsoli usługi ATA
-   Wszystkie zmiany w konfiguracji*

Dziennik inspekcji bramy usługi ATA zawiera:
-   Zmiany konfiguracji bramy* 

(Wszystkie zmiany konfiguracji bramy usługi ATA są konfigurowane w centrum usługi ATA, ale nadal są poddawane inspekcji na samym komputerze bramy).

* Z dziennika inspekcji zmian konfiguracji zawiera poprzednią konfigurację i nowej konfiguracji.


## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
