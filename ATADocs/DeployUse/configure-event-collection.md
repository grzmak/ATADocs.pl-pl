---
# required metadata

title: Konfigurowanie zbierania zdarzeń | Usługa Microsoft Advanced Threat Analytics
description: Opisuje opcje konfigurowania zbierania zdarzeń w usłudze ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Konfigurowanie zbierania zdarzeń
W celu zwiększenia możliwości wykrywania usługa ATA potrzebuje identyfikatora 4776 z dziennika zdarzeń systemu Windows. Może on zostać przekazany do bramy usługi ATA na jeden z dwóch sposobów: przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM lub przez [skonfigurowanie funkcji przekazywania zdarzeń systemu Windows](#configuring-windows-event-forwarding)..

## Zbieranie zdarzeń
Oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny usługa ATA może dodatkowo ulepszyć wykrywanie ataków typu Pass-the-Hash przy użyciu zdarzenia 4776 systemu Windows. Może być ono odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.

### SIEM/Syslog
Aby usługa ATA mogła wykorzystywać dane z serwera Syslog, konieczne jest wykonanie następujących czynności:

-   Skonfigurowanie jednego z serwerów bramy ATA do nasłuchiwania i akceptowania zdarzeń przekazywanych z serwera SIEM/Syslog.

-   Skonfigurowanie serwera SIEM/Syslog do przekazywania określonych zdarzeń do bramy usługi ATA.

> [!IMPORTANT]
> -   Nie należy przekazywać wszystkich danych z serwera Syslog do bramy usługi ATA.
> -   Usługa ATA obsługuje ruch UDP z serwera SIEM/Syslog.

Zapoznaj się z dokumentacją produktu serwera SIEM/Syslog, aby uzyskać informacje o tym, jak skonfigurować przekazywanie określonych zdarzeń do innego serwera. 

### Przekazywanie zdarzeń systemu Windows
Jeśli nie używasz serwera SIEM/Syslog, możesz skonfigurować kontrolery domeny systemu Windows do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 w celu zbierania i analizowania przez usługę ATA. Zdarzenie systemu Windows o identyfikatorze 4776 udostępnia dane dotyczące uwierzytelniania NTLM.

## Konfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM

1.  W konfiguracji bramy usługi ATA włącz **Protokół UDP odbiornika programu Syslog**.

    Ustaw adres IP nasłuchiwania zgodnie z opisem na obrazku poniżej. Domyślny port to 514.

    ![Obraz włączania protokołu UDP odbiornika programu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Skonfiguruj serwer SIEM lub Syslog do przekazywania zdarzenia 4776 systemu Windows na adres IP wybrany powyżej. Dodatkowe informacje na temat konfigurowania rozwiązania SIEM można znaleźć w pomocy online rozwiązania SIEM lub opcjach pomocy technicznej dla specyficznych wymagań formatowania dla każdego serwera SIEM.

### Obsługa rozwiązania SIEM
Usługa ATA obsługuje zdarzenia SIEM w następujących formatach:

#### RSA Security Analytics
&lt;Nagłówek programu Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Nagłówek programu Syslog jest opcjonalny.

-   Znak separatora „\n” jest wymagany między wszystkimi polami.

-   Pola, w kolejności, są następujące:

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

>[!NOTE] Zbieranie zdarzeń systemu Windows przy użyciu modułu WinCollect nie jest obsługiwane.

## Konfigurowanie funkcji przekazywania zdarzeń systemu Windows
Jeśli nie masz serwera SIEM, możesz skonfigurować kontrolery domeny do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 bezpośrednio do jednej z bram usługi ATA.

1.  Zaloguj się na wszystkich kontrolerach domeny i komputerach bram usługi ATA przy użyciu konta domeny z uprawnieniami administratora.
2. Upewnij się, że wszystkie kontrolery domeny i bramy usługi ATA, z którymi się łączysz, są przyłączone do tej samej domeny.
3.  Na każdym kontrolerze domeny wpisz następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień:
```
winrm quickconfig
```
4.  W bramie usługi ATA wpisz następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień:
```
wecutil qc
```
5.  Na każdym kontrolerze domeny w **Użytkownicy i komputery usługi Active Directory** przejdź do folderu **Wbudowane** i dwukrotnie kliknij grupę **Czytelnicy dzienników zdarzeń**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Kliknij ją prawym przyciskiem myszy i wybierz polecenie **Właściwości**. Na karcie **Członkowie** dodaj konto komputera dla każdej bramy usługi ATA.
![Okienko wyskakujące czytnika dziennika zdarzeń wef_ad](media/wef_ad-event-log-reader-popup.png)
6.  W bramie usługi ATA otwórz Podgląd zdarzeń, a następnie kliknij prawym przyciskiem myszy pozycję **Subskrypcje** i wybierz polecenie **Utwórz subskrypcję**.  

    a. W obszarze **Typ subskrypcji i komputery źródłowe** kliknij przycisk **Wybierz komputery**, dodaj kontrolery domeny i przetestuj połączenie.
    ![Właściwość wef_subscription](media/wef_subscription-prop.png)

    b. W obszarze **Zdarzenia do zbierania** kliknij przycisk **Wybierz zdarzenia**. Wybierz pozycję **Według dziennika** i przewiń w dół, aby wybrać pozycję **Zabezpieczenia**. Następnie w polu **Dołącza/wyklucza identyfikatory zdarzeń** wpisz identyfikator **4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. W obszarze **Zmień konto użytkownika lub skonfiguruj ustawienia zaawansowane** kliknij przycisk **Zaawansowane**.
Ustaw **Protokół** na **HTTP** i **Port** na **5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [Opcjonalnie] Aby ustawić krótszy interwał sondowania, w bramie usługi ATA ustaw puls subskrypcji na 5 sekund w celu zwiększenia częstotliwości sondowania.
    wecutil ss <CollectionName>/cm:custom
    wecutil ss <CollectionName> /hi:5000

8. Na stronie konfiguracji bramy usługi ATA włącz **zbieranie przekazywania zdarzeń systemu Windows**.

> [!NOTE]
Po włączeniu tego ustawienia brama usługi ATA będzie w dzienniku zdarzeń przesłanych dalej szukać zdarzeń systemu Windows, które zostały przekazane do niej z kontrolerów domeny.

Aby uzyskać więcej informacji, zobacz [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/en-us/library/cc748890)

## Zobacz też
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


