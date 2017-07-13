---
title: "Rozwiązywanie problemów z usługą Advanced Threat Analytics przy użyciu dzienników | Dokumentacja firmy Microsoft"
description: "Opis sposobu rozwiązywania problemów przy użyciu dzienników usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1291281273188a21b61b29f06a5220eee589767c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Rozwiązywanie problemów z uruchomieniem centrum usługi ATA
<a id="troubleshooting-ata-center-service-startup" class="xliff"></a>

Jeśli nie możesz uruchomić centrum usługi ATA, wykonaj następującą procedurę rozwiązywania problemów:

1.  Uruchom następujące polecenie programu Windows PowerShell: Get-Service Pla | Select Status w celu upewnienia się, że usługa licznika wydajności działa. Jeśli nie, wówczas jest to problem z platformą i musisz się upewnić, że ta usługa zostanie uruchomiona ponownie.
2.  Jeśli usługa działa, spróbuj uruchomić ją ponownie, a następnie sprawdź, czy rozwiązało to problem: Restart-Service Pla
3.  Spróbuj ręcznie utworzyć nowy moduł zbierający dane (nada się dowolny moduł, nawet tylko zbierający dane procesorów CPU komputera).
Jeśli można go uruchomić, z platformą jest prawdopodobnie wszystko w porządku, a jeśli nie, nadal jest to problem z platformą.

4.  Spróbuj ręcznie ponownie utworzyć moduł zbierający dane usługi ATA przy użyciu wiersza polecenia z podwyższonym poziomem uprawnień, uruchamiając następujące polecenia: sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



## Zobacz też
<a id="see-also" class="xliff"></a>
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
