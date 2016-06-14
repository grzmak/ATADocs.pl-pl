---
# required metadata

title: Ustawianie powiadomień usługi ATA | Microsoft Advanced Threat Analytics
description: Opis sposobu ustawiania powiadomień usługi ATA wysyłanych do użytkownika (za pośrednictwem poczty e-mail lub funkcji przekazywania zdarzeń usługi ATA) w przypadku wykrycia podejrzanych działań 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

## Udostępnianie usłudze ATA ustawień serwera poczty e-mail
Usługa ATA może generować powiadomienia po wykryciu podejrzanych działań. Aby umożliwić usłudze ATA wysyłanie powiadomień e-mail, najpierw musisz skonfigurować **ustawienia serwera poczty e-mail**..

1.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

2.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**..

3.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**..

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

4.  Na karcie **Ogólne** w obszarze **Serwer poczty e-mail** wprowadź następujące informacje:

    |Pole|Opis|Wartość|
    |---------|---------------|---------|
    |Punkt końcowy serwera SMTP (wymagane)|Wprowadź nazwę FQDN serwera SMTP.|Na przykład:<br />smtp.contoso.com|
    |Protokół SSL|Włącz protokół SSL, jeśli serwer SMTP wymaga protokołu SSL. **Uwaga:** w przypadku włączenia protokołu SSL należy również zmienić numer portu.|Ta opcja jest domyślnie wyłączona.|
    |Uwierzytelnianie|Tę opcję należy włączyć, jeśli serwer SMTP wymaga uwierzytelniania. **Uwaga:** w przypadku włączenia uwierzytelniania należy wprowadzić nazwę użytkownika i hasło konta e-mail mającego uprawnienia do nawiązywania połączeń z serwerem SMTP.|Ta opcja jest domyślnie wyłączona.|
    |Wyślij z (wymagane)|Wprowadź adres e-mail, z którego wiadomości e-mail będą wysyłane.|Na przykład:<br />ATA@contoso.com|
    ![Ilustracja ustawień serwera poczty e-mail usługi ATA](media/ATA-email-server.png)

## Udostępnianie usłudze ATA ustawień serwera Syslog
W przypadku wykrycia podejrzanych działań usługa ATA może generować powiadomienia i wysyłać je do serwera Syslog. Po włączeniu powiadomień Syslog możesz określić dla nich poniższe ustawienia.

1.  Przed rozpoczęciem konfigurowania powiadomień Syslog skontaktuj się z administratorem rozwiązania SIEM, aby uzyskać następujące informacje:

    -   Nazwa FQDN lub adres IP serwera rozwiązania SIEM

    -   Port, na którym nasłuchuje serwer rozwiązania SIEM

    -   Transport, który ma być używany: UDP, TCP lub TLS (zabezpieczony protokół Syslog)

    -   Format przesyłania danych: RFC 3164 lub 5424

2.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

3.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**..

4.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**..

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

5.  Wybierz pozycję **Serwer Syslog** i wprowadź następujące informacje:

    |Pole|Opis|
    |---------|---------------|
    |Punkt końcowy serwera Syslog|Nazwa FQDN serwera Syslog|
    |Transport|Do wyboru: UDC, TCP lub TLS (zabezpieczony protokół Syslog)|
    |Format|Format używany przez usługę ATA do wysyłania zdarzeń do serwera rozwiązania SIEM — RFC 5424 lub RFC 3164.|





## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


