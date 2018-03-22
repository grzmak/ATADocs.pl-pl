---
title: "Eksportowanie i importowanie konfiguracji usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Jak eksportować i importować konfigurację usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: edbf553bf48d984f4864264643d197362c3d6042
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Eksportowanie i importowanie konfiguracji usługi ATA
Konfiguracja usługi ATA jest przechowywana w kolekcji „SystemProfile” w bazie danych.
Ta kolekcja jest kopii zapasowej co godzinę przez Centrum usługi ATA do plików o nazwie: **SystemProfile_*sygnatury czasowej*JSON**. Przechowywanych jest 10 najnowszych wersji.
Ten plik znajduje się w podfolderze o nazwie **kopii zapasowej**. W przypadku domyślnej lokalizacji instalacji usługi ATA ścieżka do tego pliku ma postać: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*sygnatura czasowa*.json*. 

**Uwaga**: zalecane jest wykonanie kopii zapasowej tego pliku w innej lokalizacji w przypadku wprowadzania istotnych zmian w usłudze ATA.

Możesz przywrócić wszystkie ustawienia, uruchamiając następujące polecenie:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Zobacz też
- [Architektura usługi ATA](ata-architecture.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

