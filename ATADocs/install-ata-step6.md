---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 6 | Dokumentacja firmy Microsoft"
description: "W ramach tego kroku instalowania usługi ATA są konfigurowane źródła danych."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ffab11a99ae62c1c0b37c43ee212d87508f886b8
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Instalowanie usługi ATA — Krok 6
<a id="install-ata---step-6" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6. Konfigurowanie zbierania zdarzeń i sieci VPN
<a id="step-6-configure-event-collection-and-vpn" class="xliff"></a>
### Konfigurowanie zbierania zdarzeń
<a id="configure-event-collection" class="xliff"></a>
W celu zwiększenia możliwości wykrywania usługa ATA potrzebuje zdarzeń systemu Windows z identyfikatorami 4776, 4732, 4733, 4728, 4729, 4756, 4757. Uproszczona brama usługi ATA może odczytywać je automatycznie. W przypadku gdy nie jest ona wdrożona, zdarzenia mogą być przekazywane do bramy usługi ATA na jeden z dwóch sposobów: przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń rozwiązania SIEM lub przez [skonfigurowanie przekazywania zdarzeń systemu Windows](#configuring-windows-event-forwarding).

> [!NOTE]
> W przypadku usługi ATA w wersji 1.8 i nowszych nie trzeba już konfigurować zbierania zdarzeń dla uproszczonych bram usługi ATA. Uproszczona brama usługi ATA może teraz odczytywać zdarzenia lokalnie — bez potrzeby konfigurowania przekazywania zdarzeń.

Oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny usługa ATA może dodatkowo ulepszyć wykrywanie przy użyciu zdarzeń systemu Windows. Zdarzenie 4776 protokołu NTLM jest stosowane w celu udoskonalenia różnych typów wykrywania, a zdarzenia 4732, 4733 4728, 4729, 4756 i 4757 w celu udoskonalenia wykrywania modyfikacji wrażliwych grup. Mogą być one odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.

#### SIEM/Syslog
<a id="siemsyslog" class="xliff"></a>
Aby usługa ATA mogła wykorzystywać dane z serwera Syslog, konieczne jest wykonanie następujących czynności:

-   Skonfigurowanie serwerów bramy usługi ATA do nasłuchiwania i akceptowania zdarzeń przekazywanych z serwera SIEM/Syslog.
> [!NOTE]
> Usługa ATA nasłuchuje tylko protokołu IPv4, nie protokołu IPv6. 
-   Skonfigurowanie serwera SIEM/Syslog do przekazywania określonych zdarzeń do bramy usługi ATA.

> [!IMPORTANT]
> -   Nie należy przekazywać wszystkich danych z serwera Syslog do bramy usługi ATA.
> -   Usługa ATA obsługuje ruch UDP z serwera SIEM/Syslog.

Zapoznaj się z dokumentacją produktu serwera SIEM/Syslog, aby uzyskać informacje o tym, jak skonfigurować przekazywanie określonych zdarzeń do innego serwera. 

> [!NOTE]
>Jeśli nie używasz serwera SIEM/Syslog, możesz skonfigurować kontrolery domeny systemu Windows do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 w celu zbierania i analizowania przez usługę ATA. Zdarzenie systemu Windows o identyfikatorze 4776 udostępnia dane dotyczące uwierzytelniania NTLM.

#### Konfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM
<a id="configuring-the-ata-gateway-to-listen-for-siem-events" class="xliff"></a>

1.  W obszarze Konfiguracja usługi ATA w polu **Źródła danych** kliknij pozycję **Rozwiązanie SIEM**, włącz pozycję **Dziennik systemu** i kliknij polecenie **Zapisz**.

    ![Obraz włączania protokołu UDP odbiornika programu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Skonfiguruj serwer SIEM lub Syslog do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 na adres IP jednej z bram usługi ATA. Dodatkowe informacje na temat konfigurowania rozwiązania SIEM można znaleźć w pomocy online rozwiązania SIEM lub opcjach pomocy technicznej dotyczących specyficznych wymagań formatowania dla każdego serwera SIEM.

Usługa ATA obsługuje zdarzenia SIEM w następujących formatach:  

#### RSA Security Analytics
<a id="rsa-security-analytics" class="xliff"></a>
&lt;Nagłówek programu Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Nagłówek programu Syslog jest opcjonalny.

-   Znak separatora „\n” jest wymagany między wszystkimi polami.

-   Pola wymienione w odpowiedniej kolejności:

    1.  Stała RsaSA (musi się pojawiać).

    2.  Sygnatura czasowa rzeczywistego zdarzenia (upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do usługi ATA). Najlepiej z milisekundową dokładnością (jest to bardzo ważne).

    3.  Identyfikator zdarzenia systemu Windows

    4.  Nazwa dostawcy zdarzeń systemu Windows

    5.  Nazwa dziennika zdarzeń systemu Windows

    6.  Nazwa komputera odbierającego zdarzenie (w tym przypadku kontrolera domeny)

    7.  Nazwa uwierzytelniania użytkownika

    8.  Nazwa hosta źródłowego

    9. Kod wyniku protokołu NTLM

-   Ważna jest kolejność i nic innego nie powinno być umieszczone w komunikacie.

#### HP Arcsight
<a id="hp-arcsight" class="xliff"></a>
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Kontroler domeny podjął próbę sprawdzenia poprawności poświadczeń konta.|Niski| externalId=4776 cat=Zabezpieczenia rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Przyczyna lub kod błędu

-   Muszą być zgodne z definicją protokołu.

-   Brak nagłówka programu Syslog.

-   Część nagłówka (część oddzielona znakiem kreski pionowej) musi istnieć (zgodnie z protokołem).

-   Następujące klucze w części _rozszerzenie_ muszą być obecne w zdarzeniu:

    -   externalId = identyfikator zdarzenia systemu Windows

    -   rt = sygnatura czasowa rzeczywistego zdarzenia (upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do firmy Microsoft). Najlepiej z milisekundową dokładnością (jest to bardzo ważne).

    -   cat = nazwa dziennika zdarzeń systemu Windows

    -   shost = nazwa hosta źródłowego

    -   dhost = nazwa komputera odbierającego zdarzenie (w tym przypadku kontrolera domeny)

    -   duser = uwierzytelnianie użytkownika

-   W części _rozszerzenie_ kolejność nie jest ważna.

-   Musi być obecny klucz niestandardowy i etykieta klucza dla tych dwóch pól:

    -   EventSource

    -   Przyczyna lub kod błędu = kod wyniku protokołu NTLM

#### Splunk
<a id="splunk" class="xliff"></a>
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

    -   TimeGenerated = sygnatura czasowa rzeczywistego zdarzenia (upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do usługi ATA). Format powinien być zgodny z rrrrMMddGGmmss.UUUUUU, najlepiej z dokładnością do milisekund (jest to bardzo ważne).

    -   ComputerName = nazwa hosta źródłowego

    -   Message = oryginalny tekst zdarzenia ze zdarzenia systemu Windows

-   Klucz Message i jego wartość MUSZĄ być ostatnie.

-   Kolejność nie jest ważna dla par klucz=wartość.

#### QRadar
<a id="qradar" class="xliff"></a>
Platforma QRadar umożliwia zbieranie zdarzeń za pośrednictwem agenta. Gdy dane są gromadzone przy użyciu agenta, format czasu jest gromadzony bez danych milisekund. Ponieważ usługa ATA wymaga danych milisekund, platformę QRadar należy ustawić tak, aby zbieranie zdarzeń systemu Windows odbywało się bez użycia agentów. Aby uzyskać więcej informacji, zobacz [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: zbieranie zdarzeń systemu Windows bez agenta przy użyciu protokołu MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Wymagane pola to:

- Typ agenta dla kolekcji
- Nazwa dostawcy dziennika zdarzeń systemu Windows
- Źródło dziennika zdarzeń systemu Windows
- W pełni kwalifikowana nazwa domeny DC
- Identyfikator zdarzenia systemu Windows

TimeGenerated to sygnatura czasowa rzeczywistego zdarzenia (upewnij się, że nie jest to sygnatura czasowa odebrania w rozwiązaniu SIEM lub wysłania do usługi ATA). Format powinien być zgodny z rrrrMMddGGmmss.UUUUUU, najlepiej z dokładnością do milisekund (jest to bardzo ważne).

Message to oryginalny tekst zdarzenia ze zdarzenia systemu Windows

Upewnij się, że między parami klucz=wartość znajduje się parametr \t.

>[!NOTE] 
> Zbieranie zdarzeń systemu Windows przy użyciu modułu WinCollect nie jest obsługiwane.


### Konfigurowanie sieci VPN
<a id="configuring-vpn" class="xliff"></a>

Usługa ATA zbiera dane sieci VPN ułatwiające profilowanie lokalizacji, z których komputery łączą się z siecią.

Aby skonfigurować dane sieci VPN, przejdź do pozycji **Konfiguracja** > **Sieć VPN** i określ wartość **Wspólny klucz tajny konta usługi Radius** dla sieci VPN.

![Konfigurowanie sieci VPN](./media/vpn.png)

Aby uzyskać wspólny wpis tajny, zapoznaj się z dokumentacją sieci VPN. Obsługiwani dostawcy sieci VPN:

- Microsoft
- F5
- Check Point
- Cisco ASA



>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)
[Krok 7 »](install-ata-step7.md)


## Zobacz też
<a id="see-also" class="xliff"></a>

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

