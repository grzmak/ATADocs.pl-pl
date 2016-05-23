---
# required metadata

title: Ustawianie alertów usługi ATA | Microsoft Advanced Threat Analytics
description: Opis sposobu ustawiania alertów usługi ATA wysyłanych do użytkownika (za pośrednictwem poczty e-mail lub funkcji przekazywania zdarzeń usługi ATA) w przypadku wykrycia podejrzanych działań 
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

# Ustawianie alertów usługi ATA
Usługa ATA może wysyłać alerty do użytkownika w przypadku wykrycia podejrzanych działań za pośrednictwem poczty e-mail lub przy użyciu funkcji przekazywania zdarzeń usługi ATA, przekazując zdarzenia do serwera SIEM/Syslog. W przypadku włączenia jednego lub obu typów alertów, można dla nich określić następujące ustawienia.

> [!NOTE]
> -   Powiadomienia e-mail zawierają link powodujący otwarcie informacji o podejrzanym działaniu, które zostało wykryte. Część linku zawierająca nazwę hosta jest pobierana z ustawienia adresu URL konsoli usługi ATA na stronie centrum usługi ATA. Domyślnie adres URL konsoli usługi ATA jest adresem IP wybranym podczas instalacji centrum usługi ATA.  Zalecane jest użycie nazwy FQDN jako adresu URL konsoli usługi ATA w celu skonfigurowania alertów e-mail.
> -   Alerty dotyczące kondycji systemu są wysyłane tylko za pośrednictwem poczty e-mail.
> -   Alerty są wysyłane z centrum usługi ATA do serwera SMTP i serwera Syslog.
> -   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.

## Ustawianie języka i częstotliwości
Ustawienie **Język** dotyczy powiadomień wysyłanych pocztą e-mail i powiadomień wysyłanych do serwera Syslog.

Ustawienie **Częstotliwość** dotyczy wyłącznie powiadomień wysyłanych do serwera Syslog.

1.  Otwórz konsolę usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**..

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Alerty**..

4.  W obszarze **Język** wybierz odpowiedni język.

5.  W obszarze **Częstotliwość** wybierz pozycję **Niska częstotliwość**, jeśli chcesz otrzymywać tylko skrócone powiadomienia po wygenerowaniu nowego alertu. Wybierz pozycję **Wysoka częstotliwość**, jeśli chcesz otrzymywać szczegółowe powiadomienia po wygenerowaniu nowego alertu oraz zmodyfikowaniu istniejących alertów.

    ![Obraz przedstawiający konfigurowanie poziomu szczegółowości alertów](media/ATA-alerts-verbosity-language.png)

6.  Kliknij polecenie **Zapisz**..

## Konfigurowanie alertów e-mail
Usługa ATA może generować alerty po wykryciu podejrzanych działań. Po włączeniu alertów e-mail można określić dla nich następujące ustawienia.

1.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

2.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**..

3.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**..

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

4.  Wybierz pozycję **Alerty**..

5.  Włącz opcję **Poczta**, aby włączyć alerty e-mail, i wprowadź następujące informacje:

    |Pole|Opis|Wartość|
    |---------|---------------|---------|
    |Punkt końcowy serwera SMTP (wymagane)|Wprowadź nazwę FQDN serwera SMTP.|Na przykład:<br />smtp.contoso.com|
    |Protokół SSL|Włącz protokół SSL, jeśli serwer SMTP wymaga protokołu SSL. **Uwaga:** w przypadku włączenia protokołu SSL należy również zmienić numer portu.|Ta opcja jest domyślnie wyłączona.|
    |Uwierzytelnianie|Tę opcję należy włączyć, jeśli serwer SMTP wymaga uwierzytelniania. **Uwaga:** w przypadku włączenia uwierzytelniania należy wprowadzić nazwę użytkownika i hasło konta e-mail mającego uprawnienia do nawiązywania połączeń z serwerem SMTP.|Ta opcja jest domyślnie wyłączona.|
    |Wyślij z (wymagane)|Wprowadź adres e-mail, z którego wiadomości e-mail będą wysyłane.|Na przykład:<br />ATA@contoso.com|
    |Wyślij do (wymagane)|Wprowadź adresy e-mail użytkowników lub grupy adresów e-mail, które mają otrzymywać wiadomości e-mail po wykryciu podejrzanych działań przez usługę ATA. **Uwaga:** wprowadzaj adresy e-mail pojedynczo i klikaj znak plusa, aby je dodać.|Na przykład:<br />zespolzabezpieczen@contoso.com|

## Konfigurowanie przekazywania zdarzeń usługi ATA do rozwiązania SIEM
W przypadku wykrycia podejrzanych działań usługa ATA może generować alerty, wysyłając alerty do serwera Syslog. Po włączeniu alertów Syslog można określić dla nich następujące ustawienia.

1.  Przed rozpoczęciem konfigurowania alertów Syslog skontaktuj się z administratorem rozwiązania SIEM, aby uzyskać następujące informacje:

    -   Nazwa FQDN lub adres IP serwera rozwiązania SIEM

    -   Port, na którym nasłuchuje serwer rozwiązania SIEM

    -   Transport, który ma być używany: UDP, TCP lub zabezpieczony protokół TCP

    -   Format przesyłania danych: RFC 3164 lub 5424

2.  Na serwerze centrum usługi ATA kliknij ikonę **Zarządzanie usługą Microsoft Advanced Threat Analytics** na pulpicie.

3.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**..

4.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**..

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

5.  Wybierz pozycję **Alerty**..

6.  Włącz pozycję **Syslog**, aby włączyć wysyłanie alertów dotyczących podejrzanych działań do serwera Syslog, i wprowadź następujące informacje:

    |Pole|Opis|
    |---------|---------------|
    |Punkt końcowy serwera Syslog|Nazwa FQDN serwera Syslog|
    |Transport|UDC, TCP lub zabezpieczony protokół TCP|
    |Format|Format używany przez usługę ATA do wysyłania zdarzeń do serwera rozwiązania SIEM — RFC 5424 lub RFC 3164.|

## Zobacz też
[Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->


