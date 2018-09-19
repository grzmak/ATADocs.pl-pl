---
title: Instalowanie usługi Advanced Threat Analytics — Krok 7 | Microsoft Docs
description: W tym kroku instalowania usługi ATA możesz zintegrować sieci VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 409dfa161c12c22d41deb399e9d4e256fa2863dc
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133841"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-7"></a>Instalowanie usługi ATA — Krok 7

>[!div class="step-by-step"]
[«Krok 5](install-ata-step5.md)
[krok 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7. Integracja sieci VPN

Microsoft Advanced Threat Analytics (ATA) w wersji 1.8 umożliwia zbieranie informacji o kontach z rozwiązania VPN. Po skonfigurowaniu strony profilu użytkownika zawiera informacje z połączenia sieci VPN, takie jak adresy IP i lokalizacji, skąd pochodzi połączeń. W procesie badania stanowi uzupełnienie, zapewniając dodatkowe informacje o aktywności użytkownika. Wywołanie do rozpoznawania lokalizacji zewnętrzny adres IP jest anonimowy. Nie identyfikatorów osobistych jest wysyłana w tym wywołaniu.

Usługa ATA integruje się z Twoje rozwiązanie sieci VPN przez nasłuchiwanie w zdarzeń ewidencjonowania aktywności usługi RADIUS, przekazywane do bramy usługi ATA. Ten mechanizm opiera się na standardowych ewidencjonowanie aktywności usługi RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), i są obsługiwane w następujących dostawców:

-   Microsoft
-   F5
-   Cisco ASA

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć integrację sieci VPN, upewnij się, że można ustawić następujące parametry:

-   Otwórz port UDP 1813 na bram usługi ATA i uproszczonych bram usługi ATA.

-   Centrum usługi ATA, musi być w stanie uzyskać dostęp do *ti.ata.azure.com* przy użyciu protokołu HTTPS (port 443), dzięki czemu może wysyłać zapytania lokalizacji przychodzących adresów IP.

W poniższym przykładzie użyto routingu i firmy Microsoft serwera dostępu zdalnego (RRAS) do opisywania proces konfiguracji sieci VPN.

Jeśli używasz rozwiązania VPN innych firm, ich na dokumentacji instrukcje na temat włączania, ewidencjonowanie aktywności usługi RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Skonfiguruj ewidencjonowanie aktywności usługi RADIUS sieci VPN w systemie

Wykonaj następujące czynności na serwerze RRAS.
 
1.  Otwórz konsolę usługi Routing i dostęp zdalny.
2.  Kliknij prawym przyciskiem myszy nazwę serwera, a następnie kliknij przycisk **właściwości**.
3.  W **zabezpieczeń** , w obszarze **Dostawca kont**, wybierz opcję **ewidencjonowanie aktywności usługi RADIUS** i kliknij przycisk **Konfiguruj**.

    ![Instalator usługi RADIUS](./media/radius-setup.png)

4.  W **Dodawanie serwera RADIUS** okna, typ **nazwy serwera** najbliższego bramy usługi ATA lub uproszczonej bramy usługi ATA. W obszarze **portu**, upewnij się, konfiguracja domyślna 1813. Kliknij przycisk **zmiany** i wpisz nową udostępnionych tajny ciąg znaków alfanumerycznych, które można zapamiętać. Należy wypełnić w dalszej części konfiguracji usługi ATA. Sprawdź **Wyślij RADIUS konta i ewidencjonowanie aktywności wyłączać wiadomości** pole, a następnie kliknij przycisk **OK** na wszystkich otwartych oknach dialogowych.
 
     ![Konfiguracja sieci VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurowanie sieci VPN w usłudze ATA

Usługa ATA zbiera dane sieci VPN i określa, kiedy i, w których poświadczenia są używane za pośrednictwem sieci VPN i integruje badania tych danych. Zapewnia to dodatkowe informacje, aby badać alerty zgłaszane przez usługę ATA.

Aby skonfigurować dane sieci VPN w usłudze ATA:

1.  W konsoli usługi ATA Otwórz stronę konfiguracji usługi ATA i przejść do **VPN**.
 
  ![Menu konfiguracji usługi ATA](./media/config-menu.png)

2.  Włącz **ewidencjonowanie aktywności usługi Radius**, a następnie wpisz **wspólnego klucza tajnego** wcześniej skonfigurowane na serwerze sieci VPN usługi RRAS. Następnie kliknij przycisk **Zapisz**.
 

  ![Konfigurowanie sieci VPN usługi ATA](./media/vpn.png)


Po ta opcja jest włączona, wszystkie bramy usługi ATA i uproszczonych bram nasłuchiwania na porcie 1813 zdarzeń ewidencjonowania aktywności usługi RADIUS. 

Twoja instalacja została ukończona, a obecnie można przeglądać działania sieci VPN, na stronie profilu użytkownika:
 
   ![Konfiguracja sieci VPN](./media/vpn-user.png)

Po bramy usługi ATA odbiera zdarzenia sieci VPN i wysyła je do Centrum usługi ATA do przetwarzania, Centrum usługi ATA wymaga dostępu do *ti.ata.azure.com* mogły rozpoznawać zewnętrzne adresy IP w sieci VPN zdarzenia do przy użyciu protokołu HTTPS (port 443) ich lokalizacji geograficznej.




>[!div class="step-by-step"]
[« Krok 6](install-ata-step5.md)
[Krok 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/aatpsizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

