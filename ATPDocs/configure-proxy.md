---
title: Konfigurowanie serwera proxy lub zapory, aby umożliwić komunikację Azure ATP z czujnika | Dokumentacja firmy Microsoft
description: Opisuje sposób skonfigurować zaporę lub serwer proxy, aby umożliwić komunikację między czujniki Azure ATP i usługi w chmurze Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/11/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1e5e0d0665dfcf5251954cd8b0916c7cf80a722c
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurowanie serwera proxy punktu końcowego i ustawień połączeń internetowych z czujnika ATP Azure

Każdy czujnik Azure Advanced Threat ochrony (ATP) wymaga łączności z Internetem do usługi w chmurze Azure ATP poprawne działanie. W niektórych organizacjach kontrolery domeny nie są połączone bezpośrednio z Internetem, ale są połączone za pośrednictwem połączenia serwera proxy sieci web. Każdego czujnik Azure ATP wymaga użycia conifguration proxy Microsoft Windows Internet (WinINET) na dane czujników raportu i komunikować się z usługą Azure ATP. Użycie konfiguracji serwera proxy WinHTTP, nadal jest konieczne skonfigurowanie ustawień serwera proxy przeglądarki Internet systemu Windows (WinINet) do komunikacji między czujnika i usługą w chmurze Azure ATP.


Podczas konfigurowania serwera proxy, należy znać osadzonych usługa czujnik Azure ATP była uruchamiana w kontekście systemu za pomocą **Usługa lokalna** konta i usługę aktualizacji czujnik ATP Azure działa w kontekście systemu za pomocą **LocalSystem** konta. 

> [!NOTE]
> Jeśli używasz przezroczystego obiektu pośredniczącego lub WPAD w topologii sieci, nie ma potrzeby konfigurowania WinINET dla serwera proxy.

## <a name="configure-the-proxy"></a>Skonfiguruj serwer proxy 

Skonfiguruj serwer proxy ręcznie przy użyciu opartych na rejestrze statycznych serwera proxy, aby umożliwić czujnik Azure ATP do raportu danych diagnostycznych i komunikować się z usługą w chmurze Azure ATP po komputer nie ma uprawnień do łączenia się z Internetem.

> [!NOTE]
> Zmiany w rejestrze powinny być stosowane tylko do Usługa lokalna i system lokalny.

Statyczne serwera proxy jest konfigurowany za pomocą rejestru. Konfiguracja serwera proxy, którego można używać w kontekście użytkownika należy skopiować do systemu lokalnego, a Usługa lokalna. Aby skopiować ustawienia serwera proxy kontekst użytkownika:

1.   Upewnij się utworzyć kopię zapasową kluczy rejestru przed ich modyfikować.

2. W rejestrze, wyszukaj wartość `DefaultConnectionSetting` jako REG_BINARY w kluczu rejestru `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` i skopiuj go.
 
2.  Jeśli system lokalny nie ma ustawienia serwera proxy poprawne (nie są skonfigurowane lub są one różne od Current_User), następnie skopiować ustawienia serwera proxy z Current_User jako LocalSystem. W kluczu rejestru `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Wklej wartość Current_user `DefaultConnectionSetting` jako REG_BINARY.

4.  Jeśli Usługa lokalna nie ma ustawienia serwera proxy poprawne, następnie skopiować ustawienia serwera proxy z Current_User do Usługa lokalna. W kluczu rejestru `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Wklej wartość Current_User `DefaultConnectionSetting` jako REG_BINARY.

> [!NOTE]
> To będzie miało wpływ na wszystkie aplikacje w tym usług systemu Windows, które wykorzystują WinINET z Usługa lokalna, LocalSytem kontekstu.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Zapewnianie dostępu do adresów URL usługi Azure ATP na serwerze proxy

Jeśli serwer proxy lub zapora blokuje cały ruch przez domyślny, dzięki czemu tylko określonych domen za pośrednictwem lub HTTPS skanowania (inspekcji SSL) jest włączona, upewnij się, że następujące adresy URL są wymienione biały Aby zezwolić na komunikację z usługą Windows Defender ATP w porcie 443:

|Lokalizacja usługi|. Rekord Atp.Azure.com DNS|
|----|----|
|US |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Europa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Azja|triprd1wcasse1sensorapi.ATP.Azure.com|

> [!NOTE]
> Podczas przeprowadzania inspekcji SSL na ruch sieciowy Azure ATP (między czujnika i usługę Azure ATP), kontroli SSL musi obsługiwać wzajemne inspekcji.


## <a name="see-also"></a>Zobacz też
- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)