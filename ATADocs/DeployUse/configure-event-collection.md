---
title: "Konfigurowanie zbierania zdarzeń w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opisuje opcje konfigurowania zbierania zdarzeń w usłudze ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: bc9bee71273fba1df0b62dbaf162570b22c49b44


---

*Dotyczy: Advanced Threat Analytics, wersje 1.6 i 1.7*



# <a name="configure-event-collection"></a>Konfigurowanie zbierania zdarzeń
W celu zwiększenia możliwości wykrywania usługa ATA potrzebuje identyfikatora 4776 z dziennika zdarzeń systemu Windows. Może on zostać przekazany do bramy usługi ATA na jeden z dwóch sposobów: przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM lub przez [skonfigurowanie funkcji przekazywania zdarzeń systemu Windows](#configuring-windows-event-forwarding).

## <a name="event-collection"></a>Zbieranie zdarzeń
Oprócz zbierania i analizowania ruchu sieciowego do i z kontrolerów domeny usługa ATA może dodatkowo ulepszyć wykrywanie ataków typu Pass-the-Hash przy użyciu zdarzenia 4776 systemu Windows. Mogą być one odbierane z rozwiązania SIEM lub przez ustawienie funkcji przekazywania zdarzeń systemu Windows z poziomu kontrolera domeny. Zebrane zdarzenia zapewniają usłudze ATA dodatkowe informacje niedostępne za pośrednictwem ruchu sieciowego kontrolera domeny.

### <a name="siemsyslog"></a>SIEM/Syslog
Aby usługa ATA mogła wykorzystywać dane z serwera Syslog, konieczne jest wykonanie następujących czynności:

-   Skonfigurowanie serwerów bramy usługi ATA do nasłuchiwania i akceptowania zdarzeń przekazywanych z serwera SIEM/Syslog.
> [!NOTE]
> Usługa ATA nasłuchuje tylko protokołu IPv4, nie protokołu IPv6. 
-   Skonfigurowanie serwera SIEM/Syslog do przekazywania określonych zdarzeń do bramy usługi ATA.

> [!IMPORTANT]
> -   Nie należy przekazywać wszystkich danych z serwera Syslog do bramy usługi ATA.
> -   Usługa ATA obsługuje ruch UDP z serwera SIEM/Syslog.

Zapoznaj się z dokumentacją produktu serwera SIEM/Syslog, aby uzyskać informacje o tym, jak skonfigurować przekazywanie określonych zdarzeń do innego serwera. 

### <a name="windows-event-forwarding"></a>Przekazywanie zdarzeń systemu Windows
Jeśli nie używasz serwera SIEM/Syslog, możesz skonfigurować kontrolery domeny systemu Windows do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 w celu zbierania i analizowania przez usługę ATA. Zdarzenie systemu Windows o identyfikatorze 4776 udostępnia dane dotyczące uwierzytelniania NTLM.

## <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Konfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM

1.  Na karcie „Zdarzenia” w konfiguracji usługi ATA włącz opcję **Syslog** i naciśnij przycisk **Zapisz**.

    ![Obraz włączania protokołu UDP odbiornika programu Syslog](media/ATA-enable-siem-forward-events.png)

2.  Skonfiguruj serwer SIEM lub Syslog do przekazywania zdarzenia systemu Windows o identyfikatorze 4776 na adres IP jednej z bram usługi ATA. Dodatkowe informacje na temat konfigurowania rozwiązania SIEM można znaleźć w pomocy online rozwiązania SIEM lub opcjach pomocy technicznej dotyczących specyficznych wymagań formatowania dla każdego serwera SIEM.

### <a name="siem-support"></a>Obsługa rozwiązania SIEM
Usługa ATA obsługuje zdarzenia SIEM w następujących formatach:  

#### <a name="rsa-security-analytics"></a>RSA Security Analytics
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

#### <a name="hp-arcsight"></a>HP Arcsight
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

#### <a name="splunk"></a>Splunk
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

#### <a name="qradar"></a>QRadar
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

## <a name="configuring-windows-event-forwarding"></a>Konfigurowanie funkcji przekazywania zdarzeń systemu Windows

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfiguracja funkcji przekazywania zdarzeń (WEF) bramy usługi ATA z dublowaniem portów

Po skonfigurowaniu dublowania portów z kontrolerów domeny z bramą usługi ATA postępuj zgodnie z poniższymi instrukcjami, aby skonfigurować przekazywanie zdarzeń systemu Windows za pomocą konfiguracji inicjowanej przez obiekt źródłowy. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows. 

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

W tym scenariuszu zakładamy, że brama usługi ATA należy do domeny.

1.  Otwórz narzędzie Użytkownicy i komputery usługi Active Directory, przejdź do folderu **BuiltIn** i dwukrotnie kliknij grupę **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
4.  Jeśli pozycji **Usługa sieciowa** nie ma na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

**Krok 2: Utwórz zasady na kontrolerach domeny, aby skonfigurować ustawienie Konfiguruj docelowego Menedżera subskrypcji** 
> [!Note] 
> Można tworzyć dla tych ustawień zasady grupy i stosować zasady grupy do każdego kontrolera domeny monitorowanego przez bramę usługi ATA. Poniższe kroki umożliwiają modyfikację zasad lokalnych kontrolera domeny.     

1.  Uruchom następujące polecenie na każdym kontrolerze domeny: *winrm quickconfig*
2.  W wierszu polecenia wpisz ciąg *gpedit.msc*.
3.  Rozwiń węzeł **Konfiguracja komputera > Szablony administracyjne > Składniki systemu Windows > Przesyłanie dalej zdarzeń**

 ![Obraz edytora lokalnych zasad grupy](media/wef 1 local group policy editor.png)

4.  Kliknij dwukrotnie opcję **Konfiguruj docelowego Menedżera subskrypcji**.
   
    1.  Wybierz opcję **Włączono**.
    2.  W obszarze **Opcje** kliknij opcję **Pokaż**.
    3.  W obszarze **Menedżerowie subskrypcji** wprowadź poniższą wartość, a następnie kliknij przycisk **OK**:  *Server = http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (na przykład: Server = http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Obraz konfigurowania subskrypcji docelowej](media/wef 2 config target sub manager.png)
   
    5.  Kliknij przycisk **OK**.
    6.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *gpupdate /force*. 

**Krok 3: W odniesieniu do bramy usługi ATA wykonaj następujące kroki** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *wecutil qc*
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy węzeł **Subskrypcje** i wybierz polecenie **Utwórz subskrypcję**. 

   1.   Wprowadź nazwę i opis subskrypcji. 
   2.   Upewnij się, że w obszarze **Dziennik docelowy** jest zaznaczona opcja **Zdarzenia przesyłane dalej**. Aby usługa ATA mogła odczytywać zdarzenia, dla dziennika docelowego musi być wybrana opcja **Zdarzenia przesyłane dalej**. 
   3.   Wybierz opcję **Zainicjowane przez komputer źródłowy** i kliknij przycisk **Select Computers Groups** (Wybierz grupy komputerów).
        1.  Kliknij przycisk **Add Domain Computer** (Dodaj komputer w domenie).
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**. 
       
        ![Obraz Podglądu zdarzeń](media/wef3 event viewer.png)
   
        
        3.  Kliknij przycisk **OK**.
   4.   Kliknij przycisk **Wybierz zdarzenia**.

        1. Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2. W polu **Includes/Excludes Event ID** (Obejmuje/wyklucza zdarzenie o identyfikatorze) wpisz **4776** i kliknij przycisk **OK**. 

 ![Obraz przedstawiający filtr kwerendy](media/wef 4 query filter.png)

   5.   Kliknij prawym przyciskiem myszy utworzoną subskrypcję i wybierz pozycję **Stan czasu wykonywania**, aby zobaczyć, czy występują problemy dotyczące stanu. 
   6.   Po kilku minutach sprawdź, czy zdarzenie 4776 jest wyświetlane w zdarzeniach przekazywanych w bramie ATA.


### <a name="wef-configuration-for-the-ata-lightweight-gateway"></a>Konfiguracja funkcji WEF dla bramy ATA Lightweight Gateway
Po zainstalowaniu bramy ATA Lightweight Gateway na kontrolerach domeny, można skonfigurować kontrolery domeny do przesyłania dalej zdarzeń do siebie samych. Wykonaj poniższe kroki, aby skonfigurować funkcję przesyłania dalej zdarzeń systemu Windows podczas używania bramy ATA Lightweight Gateway. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows.  

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

1.  Otwórz narzędzie Użytkownicy i komputery usługi Active Directory, przejdź do folderu **BuiltIn** i dwukrotnie kliknij grupę **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
3.  Jeśli **Usługa sieciowa** nie jest wymieniona na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

**Krok 2: Po zainstalowaniu bramy ATA Lightweight Gateway wykonaj następujące czynności na kontrolerze domeny** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *winrm quickconfig* oraz *wecutil qc* 
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy węzeł **Subskrypcje** i wybierz polecenie **Utwórz subskrypcję**. 

   1.   Wprowadź nazwę i opis subskrypcji. 
   2.   Upewnij się, że w obszarze **Dziennik docelowy** jest zaznaczona opcja **Zdarzenia przesyłane dalej**. Aby usługa ATA mogła odczytywać zdarzenia, dziennik docelowy musi dotyczyć zdarzeń przesyłanych dalej.

        1.  Wybierz opcję **Zainicjowane przez kolektor** i kliknij przycisk **Wybierz komputery**. Następnie kliknij przycisk **Add Domain Computer** (Dodaj komputer w domenie).
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**.

            ![Obraz właściwości subskrypcji](media/wef 5 sub properties computers.png)

        3.  Kliknij przycisk **OK**.
   3.   Kliknij przycisk **Wybierz zdarzenia**.

        1.  Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2.  W polu **Includes/Excludes Event ID** (Obejmuje/wyklucza zdarzenie o identyfikatorze) wpisz *4776* i kliknij przycisk **OK**. 

![Obraz przedstawiający filtr kwerendy](media/wef 4 query filter.png)


  4.    Kliknij prawym przyciskiem myszy utworzoną subskrypcję i wybierz pozycję **Stan czasu wykonywania**, aby zobaczyć, czy występują problemy dotyczące stanu. 

> [!Note] 
> Może być konieczne ponowne uruchomienie kontrolera domeny, aby ustawienia zaczęły obowiązywać. 

Po kilku minutach sprawdź, czy zdarzenie 4776 jest wyświetlane w zdarzeniach przekazywanych w bramie ATA.



Aby uzyskać więcej informacji, zobacz [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Zobacz też
- [Instalowanie usługi ATA](install-ata-step1.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


