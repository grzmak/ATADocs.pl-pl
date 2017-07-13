---
title: "Eksportowanie i importowanie konfiguracji usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Jak eksportować i importować konfigurację usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a04378838fab20c43df159ef3259530b8a599ed4
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Eksportowanie i importowanie konfiguracji usługi ATA
<a id="export-and-import-the-ata-configuration" class="xliff"></a>
Konfiguracja usługi ATA jest przechowywana w kolekcji „SystemProfile” w bazie danych.
Kopia zapasowa tej kolekcji jest tworzona co godzinę przez centrum usługi ATA w pliku o nazwie: „SystemProfile_*sygnatura czasowa*.json”. Przechowywanych jest 10 najnowszych wersji.
Znajduje się on w podfolderze o nazwie „Backup”. W przypadku domyślnej lokalizacji instalacji usługi ATA ścieżka do tego pliku ma postać: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*sygnatura czasowa*.json*. 

**Uwaga**: zalecane jest wykonanie kopii zapasowej tego pliku w innej lokalizacji w przypadku wprowadzania istotnych zmian w usłudze ATA.

Możesz przywrócić wszystkie ustawienia, uruchamiając następujące polecenie:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Zobacz też
<a id="see-also" class="xliff"></a>
- [Architektura usługi ATA](ata-architecture.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

