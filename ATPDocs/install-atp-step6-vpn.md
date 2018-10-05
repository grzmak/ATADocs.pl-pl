---
title: Instalowanie usługi Azure Advanced Threat Protection. Integracja połączenia VPN | Dokumentacja firmy Microsoft
description: Zbierz informacje ewidencjonowania aktywności dla usługi Azure ATP, integrując sieci VPN.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 382b0f31cbc24dde3905d99bab7ed8be8feb5cb4
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783750"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="integrate-vpn"></a>Integracja sieci VPN

<<<<<<< Główny usługi Azure Advanced Threat Protection (ATP) umożliwia zbieranie informacji o kontach z rozwiązania VPN. Po skonfigurowaniu strony profilu użytkownika zawiera informacje z połączenia sieci VPN, takie jak adresy IP i lokalizacji, skąd pochodzi połączeń. W procesie badania stanowi uzupełnienie, zapewniając dodatkowe informacje w aktywność użytkowników, a także nowe wykrycie nietypowe połączeń sieci VPN. Wywołanie do rozpoznawania lokalizacji zewnętrzny adres IP jest anonimowy. Nie identyfikatorów osobistych jest wysyłana w tym wywołaniu.
=======
> [!div class="step-by-step"]
> [« Krok 5](install-atp-step5.md)
> [Krok 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Krok 6. Integracja sieci VPN

Usługi Azure Advanced Threat Protection (ATP) umożliwia zbieranie informacji o kontach z rozwiązania VPN. Po skonfigurowaniu strony profilu użytkownika zawiera informacje z połączenia sieci VPN, takie jak adresy IP i lokalizacji, skąd pochodzi połączeń. W procesie badania stanowi uzupełnienie, zapewniając dodatkowe informacje w aktywność użytkowników, a także nowe wykrycie nietypowe połączeń sieci VPN. Wywołanie do rozpoznawania lokalizacji zewnętrzny adres IP jest anonimowy. Nie identyfikatorów osobistych jest wysyłana w tym wywołaniu.
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

Narzędzie Azure ATP integruje się z Twoje rozwiązanie sieci VPN przez nasłuchiwanie w przekazywane do usługi Azure ATP czujników zdarzeń ewidencjonowania aktywności usługi RADIUS. Ten mechanizm opiera się na standardowych ewidencjonowanie aktywności usługi RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), i są obsługiwane w następujących dostawców:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć integrację sieci VPN, upewnij się, że można ustawić następujące parametry:

-   Otwórz port UDP 1813 narzędzia Azure ATP czujniki i/lub czujników autonomiczne narzędzia Azure ATP.


W poniższym przykładzie użyto routingu i firmy Microsoft serwera dostępu zdalnego (RRAS) do opisywania proces konfiguracji sieci VPN.

Jeśli używasz rozwiązania VPN innych firm, ich na dokumentacji instrukcje na temat włączania, ewidencjonowanie aktywności usługi RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Skonfiguruj ewidencjonowanie aktywności usługi RADIUS sieci VPN w systemie

Wykonaj następujące czynności na serwerze RRAS.
 
1.  Otwórz konsolę usługi Routing i dostęp zdalny.
2.  Kliknij prawym przyciskiem myszy nazwę serwera, a następnie kliknij przycisk **właściwości**.
3.  W **zabezpieczeń** , w obszarze **Dostawca kont**, wybierz opcję **ewidencjonowanie aktywności usługi RADIUS** i kliknij przycisk **Konfiguruj**.

    ![Instalator usługi RADIUS](./media/radius-setup.png)

4.  W **Dodawanie serwera RADIUS** okna, typ **nazwy serwera** najbliższego czujnik autonomiczny narzędzia Azure ATP lub czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. W obszarze **portu**, upewnij się, konfiguracja domyślna 1813. Kliknij przycisk **zmiany** i wpisz nową udostępnionych tajny ciąg znaków alfanumerycznych, które można zapamiętać. Należy wypełnić w dalszej części konfiguracji usługi Azure ATP. Sprawdź **Wyślij RADIUS konta i ewidencjonowanie aktywności wyłączać wiadomości** pole, a następnie kliknij przycisk **OK** na wszystkich otwartych oknach dialogowych.
 
     ![Konfiguracja sieci VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurowanie sieci VPN w usłudze ATP

Narzędzie Azure ATP zbiera dane sieci VPN, które pomagają profilu lokalizacji z komputerów, które połączenie z siecią oraz wykrywać podejrzane połączeń sieci VPN.

Aby skonfigurować dane sieci VPN w usłudze ATP:

1.  W portalu usługi Azure ATP kliknij koło zębate konfiguracji i następnie **VPN**.
 

2.  Włącz **ewidencjonowanie aktywności usługi Radius**, a następnie wpisz **wspólnego klucza tajnego** wcześniej skonfigurowane na serwerze sieci VPN usługi RRAS. Następnie kliknij przycisk **Zapisz**.
 

  ![Konfigurowanie usługi Azure VPN zaawansowanej ochrony przed zagrożeniami](./media/atp-vpn-radius.png)


Po ta opcja jest włączona, wszystkie czujniki narzędzia Azure ATP i czujniki autonomiczny nasłuchiwania na porcie 1813 zdarzeń ewidencjonowania aktywności usługi RADIUS, a Twoja instalacja została ukończona. 

 Po czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure odbiera zdarzenia sieci VPN i wysyła je do usługi Azure ATP w chmurze do przetwarzania, profilu jednostki będą wskazywać distinct dostęp do lokalizacji VPN i działań w profilu będą wskazywać lokalizacji.

<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [«Krok 6](install-atp-step5.md)
> [krok 7»](install-atp-step7.md)
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
