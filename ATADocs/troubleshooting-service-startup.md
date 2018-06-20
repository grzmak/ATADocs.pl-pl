---
title: Rozwiązywanie problemów z uruchomienia usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można rozwiązywać problemy z uruchamianiem usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 87d3f1de8167c1198e6b334826f90df83cc96780
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009272"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="troubleshooting-service-startup"></a>Rozwiązywanie problemów z uruchomienia usługi

## <a name="troubleshooting-ata-center-service-startup"></a>Rozwiązywanie problemów z uruchomieniem centrum usługi ATA

Jeśli nie można uruchomić Centrum usługi ATA, wykonaj następującą procedurę rozwiązywania problemów:

1.  Uruchom następujące polecenie programu Windows PowerShell: `Get-Service Pla | Select Status` się upewnić, że działa usługa licznika wydajności. Jeśli nie, wówczas jest to problem z platformą i musisz się upewnić, że ta usługa zostanie uruchomiona ponownie.
2.  Jeśli była uruchomiona, spróbuj uruchomić go ponownie i zobacz, czy spowodowało to rozwiązanie problemu: `Restart-Service Pla`
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

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Rozwiązywanie problemów z uruchomienia bramy ATA Lightweight Gateway

**Symptom**

Nie można uruchomić bramy usługi ATA, a ten błąd:<br></br>
*System.Net.Http.HttpRequestException: Kod stanu odpowiedzi nie wskazuje powodzenia: 500 (wewnętrzny błąd serwera)*

**Opis**

Dzieje się tak, ponieważ w ramach procesu instalacji Lightweight Gateway, usługa ATA przydziela próg procesora CPU, umożliwiającą bramy Lightweight mogą korzystać z buforu, 15% procesora CPU. Jeśli niezależnie wybrano progu za pomocą klucza rejestru: ten konflikt uniemożliwi uruchamianie bramy Lightweight. 

**Rozdzielczość**

1. W rejestrze kluczy, jeśli istnieje wartość DWORD o nazwie **Wyłącz liczniki wydajności** upewnij się, że jest ustawiona na **0**:  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Następnie uruchom ponownie usługę Pla. Brama ATA Lightweight Gateway automatycznie wykryje zmianę i ponownie uruchom usługę.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
