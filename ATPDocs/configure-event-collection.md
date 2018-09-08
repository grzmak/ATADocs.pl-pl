---
title: Zainstaluj usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W tym kroku instalowania usługi ATP są konfigurowane źródła danych.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 91e3caf8e15313069e4c2cec194a11855fd45c24
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126182"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="configure-event-collection"></a>Konfigurowanie zbierania zdarzeń

W celu zwiększenia możliwości wykrywania, narzędzia Azure ATP potrzebuje następujących zdarzeń Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 i 7045. One może odczytywać je automatycznie za pomocą czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure lub w przypadku, gdy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure nie została wdrożona, zdarzenia mogą być przekazywane do czujnika autonomicznego narzędzia Azure ATP w jeden z dwóch sposobów, konfigurując czujnik autonomiczny narzędzia Azure ATP do nasłuchiwania zdarzeń SIEM lub przez [Konfigurowanie funkcji przekazywania zdarzeń Windows](configure-event-forwarding.md).

> [!NOTE]
> Należy przeprowadzić inspekcję skrypt przed skonfigurowaniem zbierania zdarzeń usługi ATA aby upewnić się, że kontrolery domeny są prawidłowo skonfigurowane i rejestrowanie zdarzeń niezbędne. 

Oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny, usługi Azure ATP może być dodatkowo ulepszyć wykrywanie zdarzeń Windows. Używa zdarzenie 4776 protokołu NTLM, różnymi rozwiązaniami do wykrywania i zdarzenia 4732, 4733, 4728, 4729, 4756, 4757 i 7045 wykrywania modyfikacji wrażliwych grup i tworzenia usługi. Mogą być one odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają narzędzia Azure ATP z dodatkowymi informacjami, która nie jest dostępna za pośrednictwem ruchu sieciowego kontrolera domeny.

## <a name="siemsyslog"></a>SIEM/Syslog
Narzędzia Azure ATP można było używać danych z serwera Syslog należy wykonać następujące czynności:

-   Skonfiguruj serwery czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure do nasłuchiwania i akceptowania zdarzeń przekazywanych z serwera SIEM/Syslog.

 > [!NOTE]
 > Narzędzie Azure ATP nasłuchuje tylko protokołu IPv4 i IPv6 nie. 

-   Skonfiguruj serwer SIEM/Syslog do przekazywania określonych zdarzeń do czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.

> [!IMPORTANT]
> -   Nie przekazuj wszystkie dane usługi Syslog do czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.
> -   Narzędzie Azure ATP obsługuje ruch UDP z serwera SIEM/Syslog.

Zapoznaj się z dokumentacją produktu serwera SIEM/Syslog, aby uzyskać informacje o tym, jak skonfigurować przekazywanie określonych zdarzeń do innego serwera. 

> [!NOTE]
>Jeśli nie używasz serwera SIEM/Syslog, możesz skonfigurować kontrolery domeny Windows do przekazywania wszystkich wymaganych zdarzeń do zbierania i analizowania przez zaawansowanej ochrony przed zagrożeniami.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Konfigurowanie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure do nasłuchiwania zdarzeń SIEM

1.  W konfiguracji zaawansowanej ochrony przed zagrożeniami dla platformy Azure w obszarze **źródeł danych** kliknij **SIEM** i Włącz **Syslog** i kliknij przycisk **Zapisz**.

    ![Obraz włączania protokołu UDP odbiornika programu Syslog](media/atp-siem-config.png)

2.  Skonfiguruj serwer SIEM lub Syslog do przekazywania wszystkich wymaganych zdarzeń na adres IP jednej z czujników narzędzia Azure ATP. Aby uzyskać dodatkowe informacje na temat konfigurowania rozwiązania SIEM Zobacz Twojej pomocy online rozwiązania SIEM lub opcjach pomocy technicznej dotyczących specyficznych wymagań formatowania dla każdego serwera SIEM.

Narzędzie Azure ATP obsługuje zdarzenia SIEM w następujących formatach:  

## <a name="rsa-security-analytics"></a>RSA Security Analytics
&lt;Nagłówek programu Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Nagłówek programu Syslog jest opcjonalny.

-   Znak separatora „\n” jest wymagany między wszystkimi polami.

-   Pola wymienione w odpowiedniej kolejności:

    1.  Stała RsaSA (musi się pojawiać).

    2.  Sygnatura czasowa rzeczywistego zdarzenia (Upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do zaawansowanej ochrony przed zagrożeniami). Najlepiej milisekundową dokładnością jest to ważne.

    3.  Identyfikator zdarzenia systemu Windows

    4.  Nazwa dostawcy zdarzeń systemu Windows

    5.  Nazwa dziennika zdarzeń systemu Windows

    6.  Nazwa komputera odbierającego zdarzenie (w tym przypadku kontrolera domeny)

    7.  Nazwa uwierzytelniania użytkownika

    8.  Nazwa hosta źródłowego

    9. Kod wyniku protokołu NTLM

-   Ważna jest kolejność i nic innego nie powinno być umieszczone w komunikacie.

## <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Kontroler domeny podjął próbę sprawdzenia poprawności poświadczeń konta.|Niski| externalId=4776 cat=Zabezpieczenia rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Przyczyna lub kod błędu

-   Muszą być zgodne z definicją protokołu.

-   Brak nagłówka programu Syslog.

-   Część nagłówka (część oddzielona znakiem kreski pionowej) musi istnieć (zgodnie z protokołem).

-   Następujące klucze w części _rozszerzenie_ muszą być obecne w zdarzeniu:

    -   externalId = identyfikator zdarzenia systemu Windows

    -   RT = sygnatura czasowa rzeczywistego zdarzenia (Upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do zaawansowanej ochrony przed zagrożeniami). Najlepiej milisekundową dokładnością jest to ważne.

    -   cat = nazwa dziennika zdarzeń systemu Windows

    -   shost = nazwa hosta źródłowego

    -   dhost = nazwa komputera odbierającego zdarzenie (w tym przypadku kontrolera domeny)

    -   duser = uwierzytelnianie użytkownika

-   W części _rozszerzenie_ kolejność nie jest ważna.

-   Musi być obecny klucz niestandardowy i etykieta klucza dla tych dwóch pól:

    -   EventSource

    -   Przyczyna lub kod błędu = kod wyniku protokołu NTLM

## <a name="splunk"></a>Splunk
&lt;Nagłówek programu Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Komputer podjął próbę zweryfikowania poświadczeń dla konta.

Authentication Package:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Konto logowania: Administrator

Źródłowa stacja robocza:       SIEM

Kod błędu:         0x0

-   Nagłówek programu Syslog jest opcjonalny.

-   Między wszystkimi wymaganymi polami znajduje się znak separatora „\r\n”.

-   Pola mają format klucz=wartość.

-   Następujące klucze muszą istnieć i mieć wartość:

    -   EventCode = identyfikator zdarzenia systemu Windows

    -   Logfile = nazwa dziennika zdarzeń systemu Windows

    -   SourceName = nazwa dostawcy zdarzeń systemu Windows

    -   TimeGenerated = sygnatura czasowa rzeczywistego zdarzenia (Upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do zaawansowanej ochrony przed zagrożeniami). Format powinien być zgodny z rrrrmmddggmmss.uuuuuu, najlepiej z dokładnością do milisekund, jest to ważne.

    -   ComputerName = nazwa hosta źródłowego

    -   Message = oryginalny tekst zdarzenia ze zdarzenia systemu Windows

-   Klucz Message i jego wartość MUSZĄ być ostatnie.

-   Kolejność nie jest ważna dla par klucz=wartość.

## <a name="qradar"></a>QRadar
Platforma QRadar umożliwia zbieranie zdarzeń za pośrednictwem agenta. Gdy dane są gromadzone przy użyciu agenta, format czasu jest gromadzony bez danych milisekund. Ponieważ usługi Azure ATP wymaga danych milisekund, to należy ustawić QRadar umożliwia zbieranie zdarzeń Windows bez agenta. Aby uzyskać więcej informacji, zobacz [ http://www-01.ibm.com/support/docview.wss?uid=swg21700170 ] (http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: zbieranie zdarzeń Windows bez agenta przy użyciu protokołu MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Wymagane pola to:

- Typ agenta dla kolekcji
- Nazwa dostawcy dziennika zdarzeń systemu Windows
- Źródło dziennika zdarzeń systemu Windows
- W pełni kwalifikowana nazwa domeny DC
- Identyfikator zdarzenia systemu Windows

TimeGenerated to sygnatura czasowa rzeczywistego zdarzenia (Upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do zaawansowanej ochrony przed zagrożeniami). Format powinien być zgodny z rrrrmmddggmmss.uuuuuu, najlepiej z dokładnością do milisekund, jest to ważne.

Message to oryginalny tekst zdarzenia ze zdarzenia systemu Windows

Upewnij się, że między parami klucz=wartość znajduje się parametr \t.

>[!NOTE] 
> Zbieranie zdarzeń systemu Windows przy użyciu modułu WinCollect nie jest obsługiwane.




## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Dokumentacja dziennika rozwiązania SIEM zaawansowanej ochrony przed zagrożeniami usługi Azure](cef-format-sa.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
