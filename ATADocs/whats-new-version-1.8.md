---
title: "Co nowego w wersji 1.8 usługi ATA | Microsoft Docs"
description: "Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.8 usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/03/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 71e7f723d02b4e86f1799e5a92998363766de7a2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
# <a name="whats-new-in-ata-version-18"></a>Co nowego w wersji 1.8 usługi ATA

Najnowszą wersję aktualizacji usługi ATA można [pobrać z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=55536), a pełną wersję można pobrać z centrum [Eval Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Te informacje o wersji obejmują aktualizacje, nowe funkcje, poprawki i znane problemy w tej wersji usługi Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Nowe i zaktualizowane funkcje wykrywania

- Implementacja nietypowego protokołu została ulepszona, aby umożliwić wykrycie złośliwego oprogramowania WannaCry.

- NOWOŚĆ! **Odbiegająca od normy modyfikacja poufnych grup** — W fazie podwyższenia poziomu uprawnień osoby atakujące modyfikują grupy z wysokim poziomem uprawnień w celu uzyskania dostępu do wrażliwych zasobów. Usługa ATA wykrywa teraz odbiegające od normy zmiany w grupach z podwyższonym poziomem uprawnień.
- NOWOŚĆ! **Podejrzane niepowodzenia uwierzytelniania** (behawioralne ataki siłowe) — osoby atakujące usiłują użyć ataku siłowego na poświadczenia, aby naruszyć bezpieczeństwo kont. Usługa ATA zgłasza teraz alert po wykryciu odbiegających od normy niepowodzeń uwierzytelniania.   

- **Próba zdalnego wykonania kodu — metoda WMI exec** — osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny. Usługa ATA ma rozszerzone wykrywanie zdalnego wykonywania kodu w celu uwzględnienia wykrywania metod WMI do zdalnego uruchamiania kodu.

- Rekonesans przy użyciu zapytań usługi katalogowej — to wykrywanie zostało rozszerzone, aby można było przechwycić zapytania względem pojedynczej wrażliwej jednostki i zmniejszyć liczbę fałszywych alarmów, które były generowane w poprzedniej wersji. Jeśli ta funkcja została wyłączona w wersji 1.7, to zainstalowanie wersji 1.8 włączy ją teraz automatycznie.

- Działanie biletu uwierzytelniania Golden Ticket protokołu Kerberos — usługa ATA 1.8 zawiera dodatkową technikę do wykrywania ataków na bilet uwierzytelniania Golden Ticket.
    - Usługa ATA wykrywa teraz podejrzane działania, w których okres istnienia biletu uwierzytelniania Golden Ticket wygasł. Jeśli bilet protokołu Kerberos jest używany przez więcej niż dozwolony okres istnienia, usługa ATA wykryje go jako podejrzane działanie oznaczające, że prawdopodobnie został utworzony bilet uwierzytelniania Golden Ticket.
- Aby usunąć znane fałszywe alarmy, wprowadzono ulepszenia następujących wykryć:  
    - Wykrywanie podwyższenia poziomu uprawnień (sfałszowany element PAC) 
    - Działanie obniżenia poziomu szyfrowania (wytrych)
    - Implementacja nietypowego protokołu
    - Zerwanie relacji zaufania

## <a name="improved-triage-of-suspicious-activities"></a>Ulepszona klasyfikacja podejrzanych działań

-   NOWOŚĆ! Usługa ATA 1.8 umożliwia uruchamianie następujących akcji podejrzanych działań w trakcie procesu klasyfikacji: 
    - **Wykluczanie jednostek** ze zgłaszania przyszłych podejrzanych działań, aby zapobiec alertom, gdy usługa ATA wykryje niegroźne fałszywe alarmy (na przykład uruchamianie zdalnego kodu przez administratora lub wykrywanie skanerów zabezpieczeń).
    - **Pomijanie powtarzających się** podejrzanych działań z generowania alertów.
    - **Usuwanie podejrzanych działań** z osi czasu ataków.
-   Proces wykonywania kolejnych czynności dla alertów podejrzanych działań jest teraz efektywniejszy. Oś czasu podejrzanych działań została przeprojektowana. W usłudze ATA 1.8 będzie można wyświetlić o wiele więcej podejrzanych działań na jednym ekranie zawierającym lepsze informacje dla celów klasyfikacji i badania. 

## <a name="new-reports-to-help-you-investigate"></a>Nowe raporty pomagają w badaniach 
-   NOWOŚĆ! Dodano **raport z podsumowaniem** w celu umożliwienia wyświetlenia wszystkich danych podsumowania z usługi ATA, w tym podejrzanych działań, problemów z kondycją itd. Możesz nawet określić dostosowany raport, który jest automatycznie generowany cyklicznie.
-   NOWOŚĆ! Dodano **raport wrażliwych grup** w celu umożliwienia wyświetlenia wszystkich zmian wprowadzonych we wrażliwych grupach w danym okresie.


## <a name="infrastructure-improvements"></a>Ulepszenia infrastruktury

-   Wydajność centrum usługi ATA została ulepszona. W usłudze ATA 1.8 centrum usługi ATA może obsługiwać więcej niż 1 mln pakietów na sekundę.
-   Uproszczona brama usługi ATA może teraz odczytywać zdarzenia lokalnie — bez potrzeby konfigurowania przekazywania zdarzeń.
-   Możesz teraz oddzielnie skonfigurować pocztę e-mail do monitorowania alertów i podejrzanych działań.

## <a name="security-improvements"></a>Ulepszenia zabezpieczeń

-   NOWOŚĆ! **Logowanie jednokrotne do zarządzania usługą ATA**. Usługa ATA obsługuje logowanie jednokrotne zintegrowane z uwierzytelnianiem systemu Windows — jeśli użytkownik jest już zalogowany na komputerze, usługa ATA użyje tego tokenu do zalogowania na konsoli usługi ATA. Możesz również się zalogować przy użyciu karty inteligentnej. Skrypty instalacji dyskretnej dla bramy usługi ATA i uproszczonej bramy usługi ATA używają teraz kontekstu zalogowanego użytkownika bez konieczności podawania poświadczeń.
-   Lokalne uprawnienia systemu zostały usunięte z procesu bramy usługi ATA, dzięki czemu można teraz używać kont wirtualnych (dostępnych tylko dla autonomicznych bram usługi ATA), zarządzanych kont usług i kont usług zarządzanych przez grupę do uruchamiania procesu bramy usługi ATA.   
-   Zostały dodane dzienniki inspekcji dla centrum usługi ATA i bram. Wszystkie akcje są obecnie rejestrowane w dzienniku zdarzeń systemu Windows.
-   Dodano obsługę certyfikatów dostawcy magazynu kluczy dla centrum usługi ATA.

## <a name="additional-changes"></a>Dodatkowe zmiany

- Usunięto opcję dodawania notatek z podejrzanych działań
- Zalecenia dotyczące eliminacji podejrzanych działań zostały usunięte z ich osi czasu.
- Począwszy od wersji 1.8 usługi ATA bramy usługi ATA i bram Lightweight zarządzanym własne certyfikaty i wymagają interakcji ze strony administratora do zarządzania nimi.

## <a name="known-issues"></a>Znane problemy

> [!WARNING]
> Aby uniknąć tych znanych problemów można aktualizacji lub wdrożyć przy użyciu 1.8 aktualizacji 1.

### <a name="ata-gateway-on-windows-server-core"></a>Brama usługi ATA w systemie Windows Server Core

**Objawy**: Uaktualnienie bramy usługi ATA do wersji 1.8 w systemie Windows Server 2012 R2 Core z programem .NET Framework 4.7 może zakończyć się niepowodzeniem z powodu błędu: *Brama usługi Microsoft Advanced Threat Analytics przestała działać*. 

![Błąd bramy w systemie Core](./media/gateway-core-error.png)

W systemie Windows Server 2016 Core błąd może nie zostać wyświetlony, ale proces zakończy się niepowodzeniem podczas próby zainstalowania, a w dzienniku zdarzeń aplikacji na serwerze zostaną zarejestrowane zdarzenia 1000 i 1001 (awaria procesu).

**Opis**: Istnieje problem z programem .NET Framework 4.7, który powoduje, że ładowanie aplikacji korzystających z technologii WPF (na przykład usługi ATA) kończy się niepowodzeniem. Aby uzyskać więcej informacji, zobacz [artykuł w bazie wiedzy o identyfikatorze 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on). 

**Obejście**: Odinstaluj program .NET 4.7 ([zobacz artykuł w bazie wiedzy o identyfikatorze 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows)) i przywróć wersję 4.6.2 programu .NET, a następnie zaktualizuj bramę usługi ATA do wersji 1.8. Po uaktualnieniu usługi ATA możesz ponownie zainstalować program .NET 4.7.  W przyszłej wersji zostanie wprowadzona aktualizacja rozwiązująca ten problem.

### <a name="lightweight-gateway-event-log-permissions"></a>Uprawnienia dziennika zdarzeń uproszczonej bramy

**Objawy**: Podczas uaktualniania usługi ATA do wersji 1.8 aplikacje lub usługi, którym wcześniej udzielono uprawnień dostępu do dziennika zdarzeń zabezpieczeń, mogą utracić te uprawnienia. 

**Opis**: Aby ułatwić wdrożenie usługi ATA, wersja 1.8 tej usługi uzyskuje dostęp do dziennika zdarzeń zabezpieczeń bezpośrednio, bez konieczności konfigurowania przekazywania zdarzeń systemu Windows. Jednocześnie usługa ATA działa jako usługa lokalna o niskich uprawnieniach w celu zachowania większego bezpieczeństwa. Aby zapewnić sobie dostęp do odczytu zdarzeń, usługa ATA udziela sobie uprawnień do dziennika zdarzeń zabezpieczeń. W takim przypadku mogą zostać wyłączone uprawnienia ustawione wcześniej dla innych usług.

**Obejście**: Uruchom następujący skrypt programu Windows PowerShell. Spowoduje on usunięcie uprawnień w rejestrze nieprawidłowo dodanych z poziomu usługi ATA oraz dodanie ich za pomocą innego interfejsu API. Może to przywrócić uprawnienia innych aplikacji. Jeśli tak się nie stanie, trzeba je przywrócić ręcznie. W przyszłej wersji zostanie wprowadzona aktualizacja rozwiązująca ten problem. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Zakłócenia spowodowane przez serwer proxy

**Objawy**: Po uaktualnieniu usługi ATA do wersji 1.8 uruchomienie bramy usługi ATA może się nie powieść. W dzienniku błędów usługi ATA może znajdować się następujący wyjątek: *System.Net.Http.HttpRequestException: Wystąpił błąd podczas wysyłania żądania. ---> System.Net.WebException: Serwer zdalny zwrócił błąd: (407) Wymagane uwierzytelnianie serwera proxy.*

**Opis**: Począwszy od wersji 1.8 usługi ATA, brama usługi ATA komunikuje się z Centrum usługi ATA przy użyciu protokołu HTTP. Jeśli maszyna, na której zainstalowano bramę usługi ATA, korzysta z serwera proxy do nawiązywania połączeń z Centrum usługi ATA, może to spowodować przerwanie tej komunikacji. 

**Obejście**: Nie używaj serwera proxy na koncie bramy usługi ATA. W przyszłej wersji zostanie wprowadzona aktualizacja rozwiązująca ten problem.

### <a name="report-settings-reset"></a>Resetowanie ustawień raportu

**Objawy**: wszystkie ustawienia, które zostały wprowadzone Zaplanowane raporty są czyszczone po zaktualizowaniu do 1,8 update 1.

**Opis elementu**: aktualizowanie 1,8 aktualizacji 1 z resetowaniem 1,8 raporty ustawienia harmonogramu.

**Obejście**: przed zaktualizowaniem 1,8 aktualizacji 1, Utwórz kopię ustawień raportu i wprowadź je ponownie, może to być również za pomocą skryptu, aby uzyskać więcej informacji, zobacz [eksportowania i importowania konfiguracji usługi ATA](ata-configuration-file.md).


## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.8 — przewodnik migracji](ata-update-1.8-migration-guide.md)

