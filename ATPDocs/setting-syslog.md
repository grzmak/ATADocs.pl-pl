---
title: Konfigurowanie ustawień powiadomień poczty e-mail w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opis sposobu ustawiania ATP Azure powiadamiają użytkownika (za pośrednictwem poczty e-mail lub funkcji przekazywania zdarzeń usługi Azure ATP) po wykryciu podejrzanych działań
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445994"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="integrate-with-syslog"></a>Integracja z Syslog

Azure ATP mogą wyświetlać powiadomienia po wykryciu podejrzanych działań i alerty dotyczące kondycji poprzez wysłanie powiadomienia do serwera Syslog. Po włączeniu powiadomień Syslog możesz określić dla nich poniższe ustawienia.

1.  Przed rozpoczęciem konfigurowania powiadomień Syslog skontaktuj się z administratorem rozwiązania SIEM, aby uzyskać następujące informacje:

    -   Nazwa FQDN lub adres IP serwera rozwiązania SIEM

    -   Port, na którym nasłuchuje serwer rozwiązania SIEM

    -   Transport do użycia: UDP, TCP lub TLS (zabezpieczony protokół Syslog)

    -   Format przesyłania danych: RFC 3164 lub 5424

2.  Przejście do portalu obszaru roboczego adresu URL.

3.  Wprowadź nazwę użytkownika usługi Azure Active Directory i hasło, a następnie kliknij przycisk **Zaloguj**.

4.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji w usłudze Azure ATP](media/ATP-config-menu.png)

5.  Kliknij przycisk **powiadomienia**, a następnie w obszarze **powiadomienia Syslog** kliknij **Konfiguruj** i wprowadź następujące informacje:

    |Pole|Opis|
    |---------|---------------|
    |Czujnik|Wybierz wyznaczonych czujnik odpowiedzialne za agregowania wszystkie zdarzenia dziennika systemowego i przekazywania ich do serwera SIEM.|
    |Punkt końcowy usługi|Wprowadź nazwę FQDN serwera Syslog i opcjonalnie zmień numer portu (domyślnie 514).|
    |Transport|UDP, TCP lub TLS (zabezpieczony protokół Syslog)|
    |Format|Jest to format, używaną do wysyłania zdarzeń do serwera rozwiązania SIEM — RFC 5424 lub RFC 3164 Azure ATP.|

 ![Obraz ustawień serwera ATP Syslog Azure](media/atp-syslog.png)

6. Możesz wybrać zdarzeń do wysyłania do serwera Syslog. W obszarze **powiadomienia Syslog**, określ powiadomienia, które mają być wysyłane do serwera Syslog - nowe alerty zabezpieczeń, alertów zabezpieczeń zaktualizowano i nowe problemy kondycji.


## <a name="see-also"></a>Zobacz też

- [Praca z kontami poufnymi](sensitive-accounts.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)