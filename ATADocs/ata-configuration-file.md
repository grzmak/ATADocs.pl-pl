---
title: Eksportowanie i importowanie konfiguracji usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Jak eksportować i importować konfigurację usługi ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3abe18d7da00e5af0373d74db2dc2dc1f91a6fc9
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133314"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Eksportowanie i importowanie konfiguracji usługi ATA
Konfiguracja usługi ATA jest przechowywana w kolekcji „SystemProfile” w bazie danych.
Ta kolekcja kopia zapasowa jest tworzona co 4 godziny Centrum usługi ATA do plików o nazwie: **SystemProfile_*sygnatura czasowa*.json**. 300 najnowsze wersje są przechowywane.
Ten plik znajduje się w podfolderze o nazwie **kopii zapasowej**. W przypadku domyślnej lokalizacji instalacji usługi ATA ścieżka do tego pliku ma postać: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* sygnatura czasowa *.json*. 

**Uwaga**: zalecane jest wykonanie kopii zapasowej tego pliku w innej lokalizacji w przypadku wprowadzania istotnych zmian w usłudze ATA.

Możesz przywrócić wszystkie ustawienia, uruchamiając następujące polecenie:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Zobacz też
- [Architektura usługi ATA](ata-architecture.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

