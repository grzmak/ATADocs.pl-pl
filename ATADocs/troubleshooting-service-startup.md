---
title: "Rozwiązywanie problemów z usługą Advanced Threat Analytics przy użyciu dzienników | Dokumentacja firmy Microsoft"
description: "Opis sposobu rozwiązywania problemów przy użyciu dzienników usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Rozwiązywanie problemów z uruchomieniem centrum usługi ATA

Jeśli nie można uruchomić Centrum usługi ATA, wykonaj następującą procedurę rozwiązywania problemów:

1.  Uruchom następujące polecenie programu Windows PowerShell: `Get-Service Pla | Select Status` się upewnić, że działa usługa licznika wydajności. Jeśli nie, wówczas jest to problem z platformą i musisz się upewnić, że ta usługa zostanie uruchomiona ponownie.
2.  Jeśli była uruchomiona, spróbuj uruchomić go ponownie i zobacz, czy spowodowało to rozwiązanie problemu:`Restart-Service Pla`
3.  Spróbuj ręcznie utworzyć nowy moduł zbierający dane (nada się dowolny moduł, nawet tylko zbierający dane procesorów CPU komputera).
Jeśli można go uruchomić, platforma to prawdopodobnie nie jest uszkodzona. Jeśli nie, nadal jest to problem platformy.

4.  Spróbuj ponownie ręcznie utworzyć ATA modułów zbierających dane, przy użyciu wierszu polecenia z podwyższonym poziomem uprawnień, uruchomienie tych poleceń:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
