---
title: Rozwiązywanie problemów z uruchamianiem usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można rozwiązywać problemy z uruchamianiem usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 637f26736a520def329ba8599c3927079fdf354d
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165919"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="troubleshooting-service-startup"></a>Rozwiązywanie problemów z uruchamianiem usługi

## <a name="troubleshooting-ata-center-service-startup"></a>Rozwiązywanie problemów z uruchomieniem centrum usługi ATA

Jeśli nie można uruchomić Centrum usługi ATA, wykonaj następującą procedurę rozwiązywania problemów:

1.  Uruchom następujące polecenie programu Windows PowerShell: `Get-Service Pla | Select Status`
    Aby upewnić się, że usługa licznika wydajności jest uruchomiona. Jeśli nie, wówczas jest to problem z platformą i musisz się upewnić, że ta usługa zostanie uruchomiona ponownie.
2.  Jeśli była uruchomiona, spróbuj uruchomić go ponownie i sprawdź, czy rozwiązało problemu: `Restart-Service Pla`
3.  Spróbuj ręcznie utworzyć nowy moduł zbierający dane (nada się dowolny moduł, nawet tylko zbierający dane procesorów CPU komputera).
Platforma jest prawdopodobnie nie jest uszkodzona, jeśli można go uruchomić. Jeśli nie, nadal jest to problem z platformą.

4.  Spróbuj ręcznie ponownie utworzyć ATA modułów zbierających dane, przy użyciu wiersza z podwyższonym poziomem uprawnień, uruchamiając następujące polecenia:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Rozwiązywanie problemów z uruchamiania uproszczonej bramy usługi ATA

**Objaw**

Nie można uruchomić bramy usługi ATA, a ten błąd:<br></br>
*System.Net.Http.HttpRequestException: Kod stanu odpowiedzi nie wskazuje Powodzenie: 500 (wewnętrzny błąd serwera)*

**Opis**

Dzieje się tak, ponieważ podczas procesu instalacji uproszczonej bramy usługi ATA przydziela progu procesora CPU, umożliwiająca uproszczonej bramy wykorzystanie procesora CPU z buforu, 15%. Jeśli ma niezależnie ustawić próg, przy użyciu klucza rejestru: ten konflikt uniemożliwi uproszczonej bramy uruchamianie. 

**Rozdzielczość**

1. W rejestrze kluczy, jeśli ma wartość DWORD o nazwie **Wyłącz liczniki wydajności** upewnij się, że jest ustawiona na **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\`
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Następnie uruchom ponownie usługę Pla. Uproszczona brama usługi ATA automatycznie wykryje zmianę i ponownie uruchomić usługę.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
