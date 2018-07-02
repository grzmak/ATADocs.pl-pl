---
title: Konfigurowanie serwera proxy lub zapory, aby umożliwić komunikację usługi Azure ATP z czujnikiem | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania zapory lub serwera proxy, aby umożliwić komunikację między czujniki zaawansowanej ochrony przed zagrożeniami w usłudze Azure i usługi w chmurze usługi Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2f39c0d3628c3a3cc9e034fa1da8bb5a66bc704b
ms.sourcegitcommit: 3eade64779002d2c8ae005565bc69e1b3f89fb7d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2018
ms.locfileid: "34560245"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurowanie serwera proxy punktu końcowego i ustawień połączenia internetowego dla czujnika zaawansowanej ochrony przed zagrożeniami usługi platformy Azure

Czujnik każdej usługi Azure Advanced Threat Protection (ATP) wymaga łączności z Internetem do usługi w chmurze usługi Azure ATP działanie pomyślnie. W niektórych organizacjach kontrolery domeny nie są bezpośrednio połączone z Internetem, ale są połączone za pośrednictwem połączenia serwera proxy sieci web. Każdy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wymaga korzystania z konfiguracji serwera proxy programu Microsoft Windows Internet (WinINET) raportować dane czujników, a następnie komunikować się z usługą Azure ATP. Jeśli używasz konfiguracji serwera proxy WinHTTP, nadal należy skonfigurować ustawienia serwera proxy przeglądarki Internet Windows (WinINet) do komunikacji między czujnikiem i usługą w chmurze usługi Azure ATP.


Podczas konfigurowania serwera proxy, konieczne będzie wiedzieć, że osadzony usługi czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure działa w kontekście systemu przy użyciu **LocalService** konta i usługę aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami Azure działa w kontekście systemowym, za pomocą **LocalSystem** konta. 

> [!NOTE]
> Jeśli używasz przezroczystym serwerem proxy lub WPAD w topologii sieci, nie ma potrzeby konfigurowania WinINET dla serwera proxy.

## <a name="configure-the-proxy"></a>Skonfiguruj serwer proxy 

Skonfiguruj serwer proxy ręcznie przy użyciu opartych na rejestrze statyczny serwera proxy, aby zezwolić na czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure raportować dane diagnostyczne i komunikować się z usługą w chmurze usługi Azure ATP, gdy komputer nie ma uprawnień do łączenia się z Internetem.

> [!NOTE]
> Zmiany w rejestrze powinna dotyczyć tylko Usługa lokalna i LocalSystem.

Statyczny serwera proxy jest konfigurowane za pomocą rejestru. System lokalny i Usługa lokalna, należy skopiować konfigurację serwera proxy, którego używasz w kontekście użytkownika. Aby skopiować ustawienia serwera proxy w kontekście użytkownika:

1.   Upewnij się utworzyć kopię zapasową kluczy rejestru, przed ich zmodyfikowaniem.

2. W rejestrze, wyszukaj wartość `DefaultConnectionSetting` jako REG_BINARY w kluczu rejestru `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` i skopiuj go.
 
2.  Jeśli system lokalny nie jest prawidłowe ustawienia serwera proxy (nie są skonfigurowane lub są one różne od Current_User), a następnie skopiuj ustawienia serwera proxy z Current_User LocalSystem. W kluczu rejestru `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Wklej wartość z Current_user `DefaultConnectionSetting` jako REG_BINARY.

4.  Jeśli Usługa lokalna nie ma prawidłowe ustawienia serwera proxy, następnie skopiować ustawienia serwera proxy z Current_User do Usługa lokalna. W kluczu rejestru `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Wklej wartość z Current_User `DefaultConnectionSetting` jako REG_BINARY.

> [!NOTE]
> Ma to wpływu na wszystkie aplikacje, w tym usługi Windows, które używają interfejsu WinINET z Usługa lokalna, LocalSytem kontekstu.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Zapewnianie dostępu do adresów URL usługi Azure ATP na serwerze proxy

Czy serwer proxy lub zapora blokuje cały ruch domyślnie i zezwolenie tylko do określonych domen za pośrednictwem protokołu HTTPS, skanowanie (inspekcji połączenia SSL) jest włączona, upewnij się, że następujące adresy URL są białe wymienionymi w celu zezwalania na komunikację z usługą Azure ATP w porcie 443:

|Lokalizacja usługi|. Rekord Atp.Azure.com DNS|
|----|----|
|USA |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Europa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Azja|triprd1wcasse1sensorapi.ATP.Azure.com|


Można również utrwalanie reguły zapory lub serwera proxy dla określonego obszaru roboczego, które zostało utworzone, tworząc reguły dla następujących rekordów DNS:
- < nazwa obszaru roboczego >. atp.azure.com — łączność z konsoli. Na przykład contosoATP.atp.azure.com
- < nazwa obszaru roboczego > sensorapi.atp.azure.com — łączność czujników. Na przykład contosoATPsensorapi.atp.azure.com

 
> [!NOTE]
> Podczas przeprowadzania inspekcji połączenia SSL dla usługi Azure ATP ruch sieciowy (między czujnikiem i usługi Azure ATP), inspekcji połączenia SSL musi obsługiwać wzajemnego inspekcji.


## <a name="see-also"></a>Zobacz też
- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)