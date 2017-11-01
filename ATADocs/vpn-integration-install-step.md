---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 7 | Microsoft Docs"
description: "W tym kroku procesu instalowania usługi ATA można zintegrować z sieci VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 748121a709ac05756edf34e04e13b996190e9711
ms.sourcegitcommit: b951c64228d4f165ee1fcc5acc0ad6bb8482d6a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="install-ata---step-7"></a>Instalowanie usługi ATA — Krok 7

>[!div class="step-by-step"]
[«Krok 5](install-ata-step5.md)
[kroku 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7. Integracja sieci VPN

Microsoft Advanced Threat Analytics (ATA) w wersji 1.8 może zbierać informacji o kontach z rozwiązań VPN. Po skonfigurowaniu strony profilu użytkownika będzie zawierać informacje z połączenia sieci VPN, takie jak adresy IP i lokalizacje, w którym zainicjowano połączenia. Uzupełnią procesie dochodzenia podając dodatkowe informacje o aktywności użytkownika. Wywołanie rozpoznania zewnętrzny adres IP w lokalizacji jest anonimowy. Nie identyfikatora osobistego są wysyłane w tym wywołaniu.

Usługa ATA integruje się z rozwiązanie sieci VPN, ponieważ nasłuchuje zdarzeń ewidencjonowania aktywności usługi RADIUS przekazywane do bramy usługi ATA. Ten mechanizm opiera się na standardowych ewidencjonowanie aktywności usługi RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), i są obsługiwane w następujących dostawców:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć sieć VPN integracji upewnij się, że można ustawić następujące czynności:

-   Otwórz port UDP 1813 bram usługi ATA i bram ATA Lightweight Gateway.

-   Centrum usługi ATA należy połączyć się z Internetem, aby wykonać zapytanie lokalizacji przychodzących adresów IP.

W poniższym przykładzie używamy routingu i firmy Microsoft serwera dostępu zdalnego (RRAS) do opisywania proces konfiguracji sieci VPN.

Jeśli używasz 3 rozwiązania sieci VPN firmy, w dokumentacji ich instrukcje dotyczące włączania ewidencjonowanie aktywności usługi RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Skonfiguruj ewidencjonowanie aktywności usługi RADIUS sieci VPN

Wykonaj następujące czynności na serwerze RRAS.
 
1.  Otwórz konsolę usługi Routing i dostęp zdalny.
2.  Kliknij prawym przyciskiem myszy nazwę serwera, a następnie kliknij przycisk **właściwości**.
3.  W **zabezpieczeń** , w obszarze **Dostawca kont**, wybierz pozycję **ewidencjonowanie aktywności usługi RADIUS** i kliknij przycisk **Konfiguruj**.

    ![Instalator usługi RADIUS](./media/radius-setup.png)

4.  W **Dodawanie serwera RADIUS** wpisz **nazwy serwera** najbliższego bramy usługi ATA lub bramy ATA Lightweight Gateway. W obszarze **portu**, upewnij się, że jest skonfigurowana domyślna 1813. Kliknij przycisk **zmiany** i wpisz nową udostępnionych tajny ciąg znaków alfanumerycznych, które można zapamiętać. Należy wypełnić później w konfiguracji usługi ATA. Sprawdź **wiadomości wysyłania RADIUS konta i ewidencjonowanie aktywności wyłączanie** a następnie kliknij przycisk **OK** na wszystkich otwartych oknach dialogowych.
 
     ![Konfiguracja sieci VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurowanie sieci VPN w usłudze ATA

Usługa ATA zbiera dane sieci VPN, które pomaga profilu lokalizacji, z których komputerach połączenia z siecią oraz wykryć nietypowe połączeń sieci VPN.

Aby skonfigurować danych sieci VPN w usłudze ATA:

1.  W konsoli usługi ATA Otwórz stronę konfiguracji usługi ATA i przejść do **VPN**.
 
  ![Menu konfiguracji usługi ATA](./media/config-menu.png)

2.  Włącz **ewidencjonowanie aktywności usługi Radius** , a następnie wpisz **wspólny klucz tajny** został wcześniej skonfigurowany na serwerze sieci VPN usługi RRAS. Następnie kliknij przycisk **Zapisz**.
 

  ![Konfigurowanie sieci VPN usługi ATA](./media/vpn.png)


Po ta opcja jest włączona, wszystkie bramy usługi ATA i bram Lightweight nasłuchiwanie na porcie 1813 zdarzenia ewidencjonowania aktywności usługi RADIUS. 

Instalacja została zakończona i znajduje się teraz działania sieci VPN w strony profilu użytkownika:
 
   ![Konfiguracja sieci VPN](./media/vpn-user.png)

Po bramy usługi ATA odbiera zdarzenia sieci VPN i wysyła je do Centrum usługi ATA do przetwarzania, Centrum usługi ATA wymaga łączności z Internetem dla protokołu HTTPS portu 443, aby mogły rozpoznawać zewnętrzne adresy IP w zdarzeniach sieci VPN do ich używanie funkcji geolokalizacji.





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

