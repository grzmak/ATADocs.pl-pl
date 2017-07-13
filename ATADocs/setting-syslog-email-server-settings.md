---
title: "Konfigurowanie ustawień powiadomień e-mail w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opis sposobu ustawiania powiadomień usługi ATA wysyłanych do użytkownika (za pośrednictwem poczty e-mail lub funkcji przekazywania zdarzeń usługi ATA) w przypadku wykrycia podejrzanych działań"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 47d1125856631ecedcbc7779bf0529741c3da61f
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Udostępnianie usłudze ATA ustawień serwera poczty e-mail
<a id="provide-ata-with-your-email-server-settings" class="xliff"></a>
Usługa ATA może generować powiadomienia po wykryciu podejrzanych działań. Aby umożliwić usłudze ATA wysyłanie powiadomień e-mail, najpierw musisz skonfigurować **ustawienia serwera poczty e-mail**.

1.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

2.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**.

3.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

4.  W sekcji **Powiadomienia** w obszarze **Serwer poczty** wprowadź następujące informacje:

    |Pole|Opis|Wartość|
    |---------|---------------|---------|
    |Punkt końcowy serwera SMTP (wymagane)|Wprowadź nazwę FQDN serwera SMTP i opcjonalnie zmień numer portu (domyślnie 25).|Na przykład:<br />smtp.contoso.com|
    |Protokół SSL|Włącz protokół SSL, jeśli serwer SMTP wymaga protokołu SSL. **Uwaga:** w przypadku włączenia protokołu SSL należy również zmienić numer portu.|Ta opcja jest domyślnie wyłączona.|
    |Uwierzytelnianie|Tę opcję należy włączyć, jeśli serwer SMTP wymaga uwierzytelniania. **Uwaga:** w przypadku włączenia uwierzytelniania należy wprowadzić nazwę użytkownika i hasło konta e-mail mającego uprawnienia do nawiązywania połączeń z serwerem SMTP.|Ta opcja jest domyślnie wyłączona.|
    |Wyślij z (wymagane)|Wprowadź adres e-mail, z którego wiadomości e-mail będą wysyłane.|Na przykład:<br />ATA@contoso.com|
    ![Ilustracja ustawień serwera poczty e-mail usługi ATA](media/ata-email-server.png)

## Udostępnianie usłudze ATA ustawień serwera Syslog
<a id="provide-ata-with-your-syslog-server-settings" class="xliff"></a>
W przypadku wykrycia podejrzanych działań usługa ATA może generować powiadomienia i wysyłać je do serwera Syslog. Po włączeniu powiadomień Syslog możesz określić dla nich poniższe ustawienia.

1.  Przed rozpoczęciem konfigurowania powiadomień Syslog skontaktuj się z administratorem rozwiązania SIEM, aby uzyskać następujące informacje:

    -   Nazwa FQDN lub adres IP serwera rozwiązania SIEM

    -   Port, na którym nasłuchuje serwer rozwiązania SIEM

    -   Transport, który ma być używany: UDP, TCP lub TLS (zabezpieczony protokół Syslog)

    -   Format przesyłania danych: RFC 3164 lub 5424

2.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

3.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**.

4.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

5.  W sekcji Powiadomienia wybierz obszar **Serwer Syslog** i wprowadź następujące informacje:

    |Pole|Opis|
    |---------|---------------|
    |Punkt końcowy serwera Syslog|Wprowadź nazwę FQDN serwera Syslog i opcjonalnie zmień numer portu (domyślnie 514).|
    |Transport|Do wyboru: UDP, TCP lub TLS (zabezpieczony protokół Syslog)|
    |Format|Format używany przez usługę ATA do wysyłania zdarzeń do serwera rozwiązania SIEM — RFC 5424 lub RFC 3164.|

 ![Obraz ustawień serwera Syslog usługi ATA](media/ata-syslog-server-settings.png)



## Zobacz też
<a id="see-also" class="xliff"></a>
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
