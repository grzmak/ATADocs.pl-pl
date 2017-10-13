---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 7 | Microsoft Docs"
description: "W tym kroku procesu instalowania usługi ATA można zintegrować z sieci VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02649a6acb6a083145ba81b3b9c1647e7f8ea2a
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/09/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="install-ata---step-7"></a>Instalowanie usługi ATA — Krok 7

>[!div class="step-by-step"]
[«Krok 5](install-ata-step5.md)
[kroku 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7. Integracja sieci VPN

### <a name="configuring-vpn"></a>Konfigurowanie sieci VPN

Usługa ATA zbiera dane sieci VPN, które pomaga profilu lokalizacji, z których komputerach połączenia z siecią oraz wykryć nietypowe połączeń sieci VPN.

Aby skonfigurować danych sieci VPN w usłudze ATA:

1. Przejdź do **konfiguracji** , a następnie kliknij przycisk **VPN** kartę.

2. Wprowadź **konta wspólny klucz tajny** serwera RADIUS. Aby uzyskać wspólny klucz tajny, zapoznaj się z dokumentacją sieci VPN.

 ![Konfigurowanie sieci VPN usługi ATA](media/vpn.png)

3.  Gdy ta opcja jest włączona, wszystkie bramy usługi ATA i bram Lightweight nasłuchiwanie na porcie 1813 zdarzenia ewidencjonowania aktywności usługi RADIUS. 

4.  Zdarzenia ewidencjonowania aktywności usługi RADIUS sieci VPN jest przekazywany do wszystkie bramy usługi ATA lub bramy ATA Lightweight Gateway, po to jest skonfigurowany.

5.  Po bramy usługi ATA odbiera zdarzenia sieci VPN i wysyła je do Centrum usługi ATA do przetwarzania, Centrum usługi ATA wymaga łączności z Internetem dla protokołu HTTPS portu 443, aby mogły rozpoznawać zewnętrzne adresy IP w zdarzeniach sieci VPN do ich używanie funkcji geolokalizacji.

Wywołanie rozpoznania zewnętrzny adres IP w lokalizacji jest anonimowy. Nie identyfikatora osobistego są wysyłane w tym wywołaniu.

Obsługiwani dostawcy sieci VPN:
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[« Krok 6](install-ata-step5.md)
[Krok 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Powiązane pliki wideo
- [Przegląd wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania usługi ATA fazy weryfikacji Koncepcji](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

