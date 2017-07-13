---
title: "Praca z dziennikami inspekcji usługi ATA | Microsoft Docs"
description: "W tym artykule opisano sposób pracy z dziennikami inspekcji usługi ATA w dzienniku zdarzeń systemu Windows."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 54f17bc4775868e380586822456330dfc2d45c29
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# Praca z dziennikami inspekcji usługi ATA
<a id="working-with-ata-audit-logs" class="xliff"></a>

Dzienniki inspekcji usługi ATA są przechowywane w dziennikach zdarzeń systemu Windows w obszarze **Aplikacje i usługi**, a następnie **Microsoft ATA** zarówno na komputerze centrum usługi ATA, jak i bramy usługi ATA.

Dziennik inspekcji centrum usługi ATA zawiera:
-   Informacje o podejrzanym działaniu
-   Alerty monitorowania (strona kondycji)
-   Logowania do konsoli usługi ATA
-   Wszystkie zmiany w konfiguracji*

Dziennik inspekcji bramy usługi ATA zawiera:
-   Zmiany konfiguracji bramy* 

(Wszystkie zmiany konfiguracji bramy usługi ATA są konfigurowane w centrum usługi ATA, ale nadal są poddawane inspekcji na samym komputerze bramy).

*Dziennik inspekcji zmian konfiguracji będzie zawierać zarówno poprzednią konfigurację, jak i nową konfigurację.


## Zobacz też
<a id="see-also" class="xliff"></a>
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
