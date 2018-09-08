---
title: Konfigurowanie ustawień powiadomień e-mail w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opis sposobu ustawiania usługi Azure ATP informujące (za pośrednictwem poczty e-mail lub funkcji przekazywania zdarzeń usługi Azure ATP), w przypadku wykrycia podejrzanych działań
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 399773b174f52cfc26888fcaa9923de4f258e897
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166888"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="integrate-with-syslog"></a>Integracja z platformą Syslog

Narzędzie Azure ATP może generować powiadomienia po wykryciu podejrzanych działań i alertów dotyczących kondycji przez wysyłanie powiadomienia do serwera Syslog. Po włączeniu powiadomień Syslog możesz określić dla nich poniższe ustawienia.

1.  Przed rozpoczęciem konfigurowania powiadomień Syslog skontaktuj się z administratorem rozwiązania SIEM, aby uzyskać następujące informacje:

    -   Nazwa FQDN lub adres IP serwera rozwiązania SIEM

    -   Port, na którym nasłuchuje serwer rozwiązania SIEM

    -   Transport do użycia: UDP, TCP lub TLS (zabezpieczony protokół Syslog)

    -   Format przesyłania danych: RFC 3164 lub 5424

2.  Wprowadź portalem obszarów roboczych adresu URL.

3.  Wprowadź nazwę użytkownika usługi Azure Active Directory i hasło, a następnie kliknij przycisk **Zaloguj**.

4.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji w usłudze Azure ATP](media/ATP-config-menu.png)

5.  Kliknij przycisk **powiadomienia**, a następnie w obszarze **powiadomienia Syslog** kliknij **Konfiguruj** i wprowadź następujące informacje:

    |Pole|Opis|
    |---------|---------------|
    |Czujnik|Wybierz wyznaczonym czujnik odpowiedzialnych za agregowania zdarzeń dziennika systemu i przekazywania ich do serwera SIEM.|
    |Punkt końcowy usługi|Wprowadź nazwę FQDN serwera Syslog i opcjonalnie zmień numer portu (domyślnie 514).|
    |Transport|Może być UDP, TCP lub TLS (zabezpieczony protokół Syslog)|
    |Format|Jest to format, który korzysta z narzędzia Azure ATP do wysyłania zdarzeń do serwera rozwiązania SIEM — RFC 5424 lub RFC 3164.|

 ![Obraz ustawień serwera w usłudze Azure ATP Syslog](media/atp-syslog.png)

6. Możesz wybrać, które zdarzenia do wysłania do serwera Syslog. W obszarze **powiadomienia Syslog**, określ powiadomienia, które mają być wysyłane do serwera Syslog — nowe alerty zabezpieczeń, alertów zabezpieczeń zaktualizowano i nowe problemy dotyczące kondycji.


## <a name="see-also"></a>Zobacz też

- [Praca z kontami poufnymi](sensitive-accounts.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)