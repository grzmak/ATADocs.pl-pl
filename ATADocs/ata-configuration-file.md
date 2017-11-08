---
title: "Eksportowanie i importowanie konfiguracji usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Jak eksportować i importować konfigurację usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e1e032adefc650bd4578f29043be313d2c44a866
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="export-and-import-the-ata-configuration"></a>Eksportowanie i importowanie konfiguracji usługi ATA
Konfiguracja usługi ATA jest przechowywana w kolekcji „SystemProfile” w bazie danych.
Ta kolekcja jest kopii zapasowej co godzinę przez Centrum usługi ATA do plików o nazwie:  **SystemProfile_*sygnatury czasowej*JSON**. Przechowywanych jest 10 najnowszych wersji. Ten plik znajduje się w podfolderze o nazwie **kopii zapasowej**. W przypadku domyślnej lokalizacji instalacji usługi ATA ścieżka do tego pliku ma postać: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*sygnatura czasowa*.json*. 

**Uwaga**: zalecane jest wykonanie kopii zapasowej tego pliku w innej lokalizacji w przypadku wprowadzania istotnych zmian w usłudze ATA.

Możesz przywrócić wszystkie ustawienia, uruchamiając następujące polecenie:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Zobacz też
- [Architektura usługi ATA](ata-architecture.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

