---
title: "Azure instalacji Advanced Threat Protection — krok 6 | Dokumentacja firmy Microsoft"
description: "W tym kroku procesu instalowania ATP można zintegrować z sieci VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-6"></a>Zainstaluj Azure ATP — krok 6

>[!div class="step-by-step"]
[« Krok 5](install-atp-step5.md)
[Krok 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Krok 6. Integracja sieci VPN

Azure Advanced Threat ochrony (ATP) może zbierać informacji o kontach z rozwiązań VPN. Po skonfigurowaniu strony profilu użytkownika zawiera informacje z połączenia sieci VPN, takie jak adresy IP i lokalizacje, w którym zainicjowano połączenia. W procesie dochodzenia stanowi uzupełnienie zapewniając dodatkowe informacje o aktywności użytkownika, a także nowe wykrycie nadmiernego połączeń sieci VPN. Wywołanie rozpoznania zewnętrzny adres IP w lokalizacji jest anonimowy. Nie identyfikatora osobistego są wysyłane w tym wywołaniu.

Azure ATP integruje się z rozwiązanie sieci VPN przez nasłuchiwanie zdarzeń ewidencjonowania aktywności usługi RADIUS przekazywanych do czujników Azure ATP. Ten mechanizm opiera się na standardowych ewidencjonowanie aktywności usługi RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), i są obsługiwane w następujących dostawców:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć integrację sieci VPN, upewnij się, że można ustawić następujące parametry:

-   Otwórz port UDP 1813 Azure ATP autonomiczny czujników i czujnik Azure ATP.


W poniższym przykładzie użyto routingu i firmy Microsoft serwera dostępu zdalnego (RRAS) do opisywania proces konfiguracji sieci VPN.

Jeśli używasz rozwiązanie sieci VPN innych firm, w dokumentacji ich instrukcje dotyczące włączania ewidencjonowanie aktywności usługi RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Skonfiguruj ewidencjonowanie aktywności usługi RADIUS sieci VPN

Wykonaj następujące czynności na serwerze RRAS.
 
1.  Otwórz konsolę usługi Routing i dostęp zdalny.
2.  Kliknij prawym przyciskiem myszy nazwę serwera, a następnie kliknij przycisk **właściwości**.
3.  W **zabezpieczeń** , w obszarze **Dostawca kont**, wybierz pozycję **ewidencjonowanie aktywności usługi RADIUS** i kliknij przycisk **Konfiguruj**.

    ![Instalator usługi RADIUS](./media/radius-setup.png)

4.  W **Dodawanie serwera RADIUS** wpisz **nazwy serwera** najbliższego czujnik autonomiczny Azure ATP lub czujnik Azure ATP. W obszarze **portu**, upewnij się, że jest skonfigurowana domyślna 1813. Kliknij przycisk **zmiany** i wpisz nową udostępnionych tajny ciąg znaków alfanumerycznych, które można zapamiętać. Należy wypełnić później w konfiguracji ATP Azure. Sprawdź **wiadomości wysyłania RADIUS konta i ewidencjonowanie aktywności wyłączanie** a następnie kliknij przycisk **OK** na wszystkich otwartych oknach dialogowych.
 
     ![Konfiguracja sieci VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurowanie sieci VPN w ATP

Azure ATP zbiera dane sieci VPN, które pomaga profilu lokalizacji, z których komputerach połączenia z siecią oraz wykryć nietypowe połączeń sieci VPN.

Aby skonfigurować danych sieci VPN w ATP:

1.  W portalu Azure ATP obszaru roboczego kliknij koło zębate konfiguracji, a następnie **VPN**.
 

2.  Włącz **ewidencjonowanie aktywności usługi Radius**, a następnie wpisz **wspólny klucz tajny** został wcześniej skonfigurowany na serwerze sieci VPN usługi RRAS. Następnie kliknij przycisk **Zapisz**.
 

  ![Konfigurowanie usługi Azure ATP sieci VPN](./media/atp-vpn-radius.png)


Po ta opcja jest włączona, wszystkie Azure ATP autonomiczny czujników i czujników nasłuchiwania na port 1813 zdarzenia ewidencjonowania aktywności usługi RADIUS. 

Twoje instalacja została ukończona. 

Po czujnik Azure ATP odbiera zdarzenia sieci VPN i wysyła je do usługi w chmurze Azure ATP do przetwarzania, profilu jednostki będą wskazywać różne lokalizacje uzyskał dostęp do sieci VPN i działań w profilu poinformuje o lokalizacji.





>[!div class="step-by-step"]
[«Krok 6](install-atp-step5.md)
[krok 7»](install-atp-step7.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
