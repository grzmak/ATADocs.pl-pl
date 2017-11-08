---
title: "Przewodnik usługi ATA dotyczący podejrzanych działań | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bff477a66b837d82bb10a43a0dad7d36c6542d9f
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Advanced Threat Analytics podejrzanych działań przewodnik

Po właściwego dochodzenia wszelkich podejrzanych działań mogą być klasyfikowane jako:

-   **Dodatnia wartość TRUE**: złośliwą akcję wykrytych przez usługę ATA.

-   **Dodatnia wartość true niegroźne**: działań wykrytych przez usługę ATA, do rzeczywistych, ale nie złośliwe, takich jak testu penetracji.

-   **Wynik fałszywie dodatni**: false alarm, co oznacza działania nie stanie.

Aby uzyskać więcej informacji na temat pracy z alertami usługi ATA, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

Pytania lub opinie, skontaktuj się z zespołu usługi ATA na [ ATAEval@microsoft.com ](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Nietypowa modyfikacja grupy poufnej


**Opis**

Osoby atakujące Dodawanie użytkowników do grup wysoko uprzywilejowane. W tym celu uzyskania dostępu do większej ilości zasobów i uzyskanie utrwalenie. Wykrywanie zależy od profilowania działania modyfikacji grupy użytkowników i alerty, gdy występuje nietypowe dodanie do grupy poufnych. Profilowanie stale jest wykonywane przez usługę ATA. Minimalny okres wywoła alertu jest jednego miesiąca na każdym kontrolerze domeny.

Dla definicji poufnych grup w usłudze ATA, zobacz [Praca z konsolą usługi ATA](working-with-ata-console.md#sensitive-groups).


Wykrywanie polega na [zdarzeń inspekcji na kontrolerach domeny](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Aby upewnić się, wymagane zdarzenia inspekcji z kontrolerów domeny, należy użyć narzędzia, do którego odwołuje się [ATA inspekcji (AuditPol, zaawansowane wymuszania ustawienia inspekcji, odnajdowanie usługi bramy Lightweight)](https://aka.ms/ataauditingblog).

**Badanie**

1. Modyfikacja grupy jest uzasadnione? </br>Zmiany uzasadnionych grupy, które rzadko występuje i nie zostały rozpoznane jako "normal", może spowodować alertu, które mogą być uważane za niegroźne pozytywną wartość true.

2. Jeśli dodany obiekt znajduje się konto użytkownika, sprawdź akcje, które konto użytkownika miało po dodaniu do grupy administratorów. Przejdź do strony użytkownika w usłudze ATA, aby uzyskać więcej kontekstu. Były inne podejrzane działania związane z kontem przed lub po dodaniu miały miejsce? Pobierz **modyfikacji grupy poufnej** raportu, aby zobaczyć, jakie były inne zmiany dokonane i przez kogo w tym samym czasie.

**Korygowania**

Zminimalizowanie liczby użytkowników, którzy autoryzację do modyfikowania grup poufnych.

Konfigurowanie [Privileged Access Management dla usługi Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) jeśli ma to zastosowanie.

## <a name="broken-trust-between-computers-and-domain"></a>Zerwaniem relacji zaufania między komputerami i domeny

**Opis**

Zerwane relacje zaufania oznacza, że wymagania dotyczące zabezpieczeń usługi Active Directory może nie być obowiązywać dla komputerów w. Taka sytuacja jest często uznawana za podstawowy błąd zabezpieczeń i zgodności oraz atrakcyjny cel dla osób atakujących. W tym wykrywania alert jest wyzwalany, jeśli więcej niż 5 niepowodzenia uwierzytelniania Kerberos są widoczne z konta komputera w ciągu 24 godzin.

**Badanie**

Czy danego komputera zezwala logowania użytkowników domeny? 
- Jeśli tak, możesz zignorować ten komputer w czynności korygujące.

**Korygowania**

Przyłącz komputer do domeny, w razie potrzeby lub zresetowania hasła na komputerze.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>Ataków siłowych przy użyciu prostego powiązania LDAP

**Opis**

>[!NOTE]
> Główną różnicą między **niepowodzenia uwierzytelniania podejrzane** i wykryciem jest, że w tym wykrywania usługi ATA można określić, czy różne hasła były używane.

W ataków siłowych atakujący podejmie próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Znaleziono jeden raz, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywania alert zostanie wywołany, gdy usługa ATA wykrywa wiele różnych używanych haseł. Może to być albo *poziomie* z niewielki zestaw hasła przez wielu użytkowników; lub *pionowo "* z dużym zestawem hasła w przypadku kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji.

**Badanie**

1. Obejmuje wiele kont, kliknij przycisk **Pobierz szczegóły** Aby wyświetlić listę w arkuszu programu Excel.

2. Kliknij alert, aby przejść do strony dedykowanych. Sprawdź, czy próby logowania wszystkie zakończone z pomyślnym uwierzytelnieniu. Prób zostanie wyświetlony jako **odgadnąć kont** po prawej stronie infographic. Jeśli tak, czy jakakolwiek **odgadnąć kont** zwykle używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

3. Jeśli istnieją nie **odgadnąć kont**, są **ataku kont** zwykle używane z komputera źródłowego? Jeśli tak,**Pomiń** podejrzanych działań.

**Korygowania**

[Złożone i długich haseł](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) podaj niezbędne pierwszy poziom zabezpieczeń przed atakami siłowymi.

## <a name="encryption-downgrade-activity"></a>Działanie obniżenia poziomu szyfrowania

**Opis**

Korzystanie z różnych metod ataku słabe cyfry szyfrowania protokołu Kerberos. W wykrywanie, uzyskuje informacje o typy szyfrowania protokołu Kerberos, które są używane przez komputery i użytkowników usługi ATA i alerty, gdy słabszego szyfrowania jest używany: (1) jest typowe dla komputera źródłowego i/lub użytkownika. i (2) dopasowań znane techniki ataku.

Istnieją trzy typy wykrywania:

1.  Skeleton Key — to złośliwe oprogramowanie, która działa na kontrolerach domeny i umożliwia użycie uwierzytelniania z dowolnego konta do domeny bez uprzedniego uzyskania informacji o jego hasło. Złośliwe oprogramowanie często używa słabszych algorytmów szyfrowania w celu encipher hasła użytkownika na kontrolerze domeny. W tym wykrywania metody szyfrowania wiadomości KRB_ERR z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie.

2.  Bilet Golden — [bilet uwierzytelniania Golden Ticket](#golden-ticket) alertu, metody szyfrowania biletu TGT pola wiadomości TGS_REQ (żądanie obsługi) z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie. To nie jest oparty na czasie anomalii (tak jak inne wykrywania bilet uwierzytelniania Golden Ticket). Ponadto nie było żadnych żądanie uwierzytelniania Kerberos skojarzone z poprzedniego żądania obsługi, wykrytych przez usługę ATA.

3.  Overpass--Hash — typ szyfrowania wiadomości AS_REQ z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie (oznacza to, że komputer został przy użyciu AES).

**Badanie**

Najpierw sprawdź opis alertu, aby zobaczyć z powyższych trzech typów wykrywania jest zajmujących.

1.  Skeleton Key — można sprawdzić, czy Skeleton Key wpłynęła na kontrolerach domeny przy użyciu [skanera napisane przez zespół usługi ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
    Jeśli skaner wykryje złośliwe oprogramowanie na 1 lub więcej kontrolerów domeny, jest dodatnia wartość true.

2.  Bilet uwierzytelniania Golden Ticket — istnieją przypadki, w których niestandardową aplikację, która jest rzadko używana jest uwierzytelniania za pomocą dolnej szyfrowania szyfrowania. Sprawdź, czy istnieją takie niestandardowe aplikacje na komputerze źródłowym. Jeśli tak, prawdopodobnie niegroźne pozytywną wartość true i można pominąć.

3.  Overpass--Hash — istnieją przypadki, w których tego alertu mogą być wyzwalane, gdy użytkownicy skonfigurowani przy użyciu kart inteligentnych są wymagane do logowania interakcyjnego, a to ustawienie jest wyłączone i włączone. Sprawdź, czy wystąpiły zmiany podobny do tego konta związane. Jeśli tak, prawdopodobnie jest niegroźne pozytywną wartość true, można pominąć.

**Korygowania**

1.  Szkielet klucza — Usuń złośliwe oprogramowanie. Aby uzyskać więcej informacji, zobacz [analizy złośliwe oprogramowanie Skeleton Key](https://www.secureworks.com/research/skeleton-key-malware-analysis) przez SecureWorks.

2.  Golden Ticket — postępuj zgodnie z instrukcjami [bilet uwierzytelniania Golden Ticket](#golden-ticket) podejrzanych działań.   
    Ponadto tworzenie bilet uwierzytelniania Golden Ticket wymaga uprawnień administratora domeny, dlatego wdrożenie [przekazać zalecenia skrótu](http://aka.ms/PtH).

3.  Overpass--Hash — Jeśli zaangażowany konta nie jest wielkość liter, następnie zresetować hasło tego konta. Zapobiega to osobie atakującej tworzenie nowych biletów Kerberos z skrót hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną. Jeśli jest poufne konto, należy rozważyć zresetowanie konto KRBTGT dwukrotnie jak bilet uwierzytelniania Golden Ticket podejrzanych działań. Resetowanie KRBTGT dwukrotnie unieważnia wszystkie Kerberos biletów w tej domenie dlatego należy planować przedtem. Patrz wskazówki w [KRBTGT konta hasło zresetować skrypty teraz dostępne dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Zobacz też przy użyciu [resetowania haseł/kluczy narzędzie konto KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Ponieważ jest to metoda penetracja sieci, stosuj najlepsze rozwiązania z [przekazać zalecenia skrótu](http://aka.ms/PtH).

## Bilet uwierzytelniania Golden Ticket<a name="golden-ticket"></a>

**Opis**

Osoby atakujące mającego uprawnienia administratora domeny może naruszyć [konto KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Używane konto KRBTGT, można utworzyć biletu Kerberos przyznania biletu (TGT), udostępnia autoryzacji do dowolnego zasobu i wartość żadnych dowolną wartością czasu wygaśnięcia biletu. Tego BILETU fałszywych nazywa się "Bilet uwierzytelniania Golden" i pozwala osobie atakującej uzyskanie utrwalenie w sieci.

W tym wykrywania alertu jest wyzwalane, gdy bilet Kerberos przyznania biletu jest używany dla więcej niż dozwolony czas dozwolone określonych w [maksymalny okres istnienia biletu użytkownika](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) zasady zabezpieczeń.

**Badanie**

1. Były ostatnio (w ciągu ostatnich kilku godzin) zmiany wprowadzone do **maksymalny okres istnienia biletu użytkownika** ustawienie w zasadach grupy? Jeśli tak, następnie **Zamknij** alert (był wynik fałszywie dodatni).

2. Uczestniczy w tym alercie maszyny wirtualnej bramy usługi ATA? Jeśli tak, on niedawno wznowić z zapisanym stanie? Jeśli tak, następnie **Zamknij** ten alert.

3. Jeśli odpowiedzi na te pytania są nie, założono jest złośliwe.

**Korygowania**

Zmień hasło biletu przyznania biletu protokołu Kerberos (KRBTGT) dwukrotnie zgodnie z instrukcjami podanymi w [KRBTGT konta hasło zresetować skrypty teraz dostępne dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)za pomocą [zresetować hasło konta KRBTGT/kluczy Narzędzie](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Resetowanie KRBTGT dwukrotnie unieważnia wszystkie Kerberos biletów w tej domenie dlatego należy planować przedtem.  
Ponadto tworzenie bilet uwierzytelniania Golden Ticket wymaga uprawnień administratora domeny, dlatego wdrożenie [przekazać zalecenia skrótu](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Działanie wystawionego jako przynęta


**Opis**

Kont wystawionych jako przynęta są konta decoy skonfigurowane do identyfikacji i śledzenia złośliwych działań, która obejmuje tych kont. Kont wystawionych jako przynęta powinny pozostać nieużywane podczas o nazwie atrakcyjne do nakłonienia osoby atakujące (na przykład administrator SQL). Wszystkie działania z nich może wskazywać na złośliwe działanie.

Aby uzyskać więcej informacji dotyczących kont wystawionych jako przynęta, zobacz [Instalowanie usługi ATA — krok 7](install-ata-step7.md).

**Badanie**

1.  Sprawdź, czy z właścicielem komputera źródłowego używane kont wystawionych jako przynęta w celu uwierzytelnienia przy użyciu metody opisanej na stronie podejrzanych działań (na przykład protokołu Kerberos, LDAP, NTLM).

2.  Przejdź do strony profilu komputery źródła i Sprawdź inne konta uwierzytelnione z nich. Użycie kont wystawionych jako przynęta, należy skontaktować się z właścicieli tych kont.

3.  Może to być logowania nieinterakcyjnego, więc upewnij się sprawdzić aplikacje lub skrypty, które są uruchomione na komputerze źródłowym.

Jeśli po wykonaniu kroki od 1 do 3, jeśli istnieją dowody niegroźne użytkowania, przyjęto założenie, że jest to złośliwe.

**Korygowania**

Upewnij się, że wystawionego jako przynęta kont są używane tylko w przypadku ich przeznaczenie, w przeciwnym razie może wygenerować wiele alertów.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Kradzieży tożsamości za pomocą ataku Pass--Hash

**Opis**

Pass--Hash to technika penetracja sieci, w którym osoby atakujące kradzieży skrótu NTLM użytkownika z jednego komputera i przy jego użyciu uzyskują dostęp do innego komputera. 

**Badanie**

Skrót użyto z komputera, że wybrany użytkownik jest właścicielem lub regularnie korzysta? Jeśli tak, to wynik fałszywie dodatni. Jeśli nie, prawdopodobnie jest dodatnia wartość true.

**Korygowania**

1. Jeśli zaangażowany konta nie jest wielkość liter, następnie zresetować hasło tego konta. Zapobiega to osobie atakującej tworzenie nowych biletów Kerberos z skrót hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną. 

2. Jeśli jest poufne konto, należy rozważyć zresetowanie konto KRBTGT dwukrotnie jak bilet uwierzytelniania Golden Ticket podejrzanych działań. Resetowanie KRBTGT dwukrotnie unieważnia wszystkie Kerberos biletów w tej domenie dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasło zresetować skrypty teraz dostępne dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), zobacz też przy użyciu [resetowania haseł/kluczy narzędzie konto KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Ponieważ jest to metoda penetracja sieci, stosuj najlepsze rozwiązania z [przekazać zalecenia skrótu](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Kradzieży tożsamości za pomocą ataku Pass--Ticket

**Opis**

Pass--Ticket to technika penetracja sieci, w którym osoby atakujące kradzieży biletu Kerberos z jednego komputera i przy jego użyciu uzyskują dostęp do innego komputera, na podstawie kradzieży biletu. W tym wykrywania biletu protokołu Kerberos występuje używanych na różnych komputerach (co najmniej dwa).

**Badanie**

1. Kliknij przycisk **Pobierz szczegóły** przycisk, aby wyświetlić pełną listę adresów IP związanych. Czy adres IP jednego lub obu komputerów należy do podsieci, która jest przydzielony na przykład z puli niewymiarowe DHCP w sieci VPN lub Wi-Fi? Adres IP jest udostępniane? Na przykład przez urządzenie NAT? Jeśli odpowiedź na dowolne z tych pytań jest tak, to wynik fałszywie dodatni.

2. Istnieje już niestandardową aplikację, która przekazuje biletów w imieniu użytkowników? Jeśli tak, czy niegroźne pozytywną wartość true.

**Korygowania**

1. Jeśli zaangażowany konta nie jest wielkość liter, następnie zresetować hasło tego konta. Zapobiega to osobie atakującej tworzenie nowych biletów Kerberos z skrót hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną.  

2. Jeśli jest poufne konto, należy rozważyć zresetowanie konto KRBTGT dwukrotnie jak bilet uwierzytelniania Golden Ticket podejrzanych działań. Resetowanie KRBTGT dwukrotnie unieważnia wszystkie Kerberos biletów w tej domenie dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasło zresetować skrypty teraz dostępne dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), zobacz też przy użyciu [resetowania haseł/kluczy narzędzie konto KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Ponieważ jest to metoda penetracja sieci, stosuj najlepsze rozwiązania w [przekazać zalecenia skrótu](http://aka.ms/PtH).

## <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych

**Opis**

Interfejsu API ochrony danych (DPAPI) jest używany przez system Windows do ochrony bezpiecznego hasła zapisane przez przeglądarki, pliki zaszyfrowane i innych poufnych danych. Kontrolery domeny przechowywania kopii zapasowej klucza głównego, który może służyć do odszyfrowywania wszystkich kluczy tajnych zaszyfrowanych za pomocą DPAPI na komputerach przyłączonych do domeny systemu Windows. Atakujący może użyć klucza głównego do odszyfrowania żadnych kluczy tajnych chroniony funkcją DPAPI na wszystkich komputerach przyłączonych do domeny.
W tym wykrywania alert zostanie wywołany, gdy DPAPI służy do pobierania kopii zapasowej klucza głównego.

**Badanie**

1. Komputer źródłowy systemem zatwierdzone organizacji jest zaawansowane skanera zabezpieczeń w usłudze Active Directory?

2. Jeśli tak i jego powinna zawsze być tych czynności **Zamknij i Wyklucz** podejrzanych działań.

3. Jeśli tak i nie należy przeprowadzać tego, **Zamknij** podejrzanych działań.

**Korygowania**

Aby użyć DPAPI, osoba atakująca wymaga uprawnień administratora domeny. Implementowanie [przekazać zalecenia skrótu](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Złośliwe żądania replikacji


**Opis**

Replikacja usługi Active Directory to proces, za pomocą którego zmian wprowadzonych na jeden kontroler domeny są synchronizowane z innymi kontrolerami domeny. Wymagane uprawnienia, osoby atakujące mogą inicjować żądanie replikacji, dzięki czemu można pobrać danych przechowywanych w usłudze Active Directory, w tym skrótów haseł.

W tym wykrywania alert zostanie wywołany po zainicjowaniu żądania replikacji z komputera, który nie jest kontrolerem domeny.

**Badanie**

1. Jest to komputer danego kontrolera domeny? Na przykład nowo utworzonego kontroler domeny, który ma problemów z replikacją. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.  

2. Danego komputera powinien być replikowanie danych z usługi Active Directory? Na przykład Azure AD Connect. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.

**Korygowania**

Sprawdź następujące uprawnienia: 

- Replikować zmiany katalogu   

- Replikuj wszystkie zmiany katalogu  

Aby uzyskać więcej informacji, zobacz [uprawnienia Grant usług domenowych Active Directory synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Można wykorzystać [AD ACL skanera](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub Utwórz skrypt programu Windows PowerShell, aby określić, kto w domenie ma te uprawnienia.

## <a name="massive-object-deletion"></a>Usunięcie dużej liczby obiektów

**Opis**

W niektórych scenariuszach osoby atakujące, należy przeprowadzić odmowa usługi (DoS) zamiast tylko kradzież informacji. Usuwanie dużej liczby kont jest jeden technika DoS.

W tym wykrywania alertu jest wyzwalane, gdy więcej niż 5% wszystkie konta zostaną usunięte. Wykrywanie wymaga dostępu do odczytu do kontenera usuniętych obiektów.  
Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu kontenera usuniętych obiektów, zobacz **Zmienianie uprawnień do kontenera usuniętych obiektów** w [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Badanie**

Przejrzyj listę usuniętych kont i zrozumieć, jeśli istnieje wzorca lub z powodu biznesowych, która może uzasadnić tego ogromną usunięcia.

**Korygowania**

Usuń uprawnienia użytkowników, którzy mogą usuwać konta w usłudze Active Directory. Aby uzyskać więcej informacji, zobacz [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Przy użyciu eskalacji uprawnień sfałszowane danych autoryzacji

**Opis**

Znane luki w zabezpieczeniach w starszych wersjach systemu Windows Server osobom atakującym do manipulowania uprzywilejowanych atrybutu certyfikatu (PAC), pole w bilecie protokołu Kerberos, który zawiera dane autoryzacji użytkownika (w usłudze Active Directory jest członkostwo w grupie), udzielanie osoby atakujące dodatkowych uprawnień.

**Badanie**

1. Kliknij alert, aby uzyskać dostęp do jego stronę szczegółów.

2. Jest komputerem docelowym (w obszarze **ACCESSED** kolumny) poprawiono MS14-068 (kontroler domeny) lub MS11-013 (serwer)? Jeśli tak, **Zamknij** podejrzanych działań (jest wynik fałszywie dodatni).

3. Jeśli nie, komputer źródłowy jest uruchamiane (w obszarze **FROM** kolumny) systemu operacyjnego/aplikacji znane, aby zmodyfikować plik PAC? Jeśli tak, **Pomiń** podejrzanych działań (jest niegroźne pozytywną wartość true).

4. Jeśli odpowiedź była nie powyżej dwóch pytania, założono jest złośliwe.

**Korygowania**

Upewnij się, że na wszystkich kontrolerach domen z systemami operacyjnymi starszymi niż system Windows Server 2012 R2 zainstalowano poprawkę [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege), a wszystkie serwery członkowskie i kontrolery domen do wersji 2012 R2 mają zainstalowaną poprawkę KB2496930. Aby uzyskać więcej informacji, zobacz [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) i [Forged PAC (Sfałszowany element PAC)](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-directory-services-queries"></a>Rekonesans przy użyciu zapytań usług katalogowych

**Opis**

Rekonesans usług katalogu jest używany przez osoby atakujące do mapowania strukturę katalogów i stosowanie uprzywilejowanych kont do wykonania kolejnych kroków atak. Protokół zdalnego Menedżera kont zabezpieczeń (SAM-R) to jedna z metod wykorzystywane do badania katalogu, aby wykonać takie mapowanie.

W tym wykrywania alerty nie będą wyzwalane w pierwszym miesiącu po wdrożeniu usługi ATA. Podczas nauki okresu, profile usługi ATA których kwerendy SAM-R są wykonywane z komputerów, które zarówno wyliczenie i poszczególnych kwerend kont poufnych.

**Badanie**

1. Kliknij alert, aby uzyskać dostęp do jego stronę szczegółów. Sprawdź, które zapytania zostały wykonane (na przykład, Administratorzy przedsiębiorstwa lub administratora) i czy mu się to udało.

2. Przetwarzanie takich zapytań powinni ma zostać wykonane z komputera źródłowego zagrożona?

3. Jeśli tak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.

4. Jeśli tak i go nie należy tego robić, **Zamknij** podejrzanych działań.

5. Jeśli informacje o koncie zaangażowany: przetwarzanie takich zapytań powinni przez tego konta lub jest to konto zwykle Zaloguj się do komputera źródłowego?

 - Jeśli tak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.

 - Jeśli tak i go nie należy tego robić, **Zamknij** podejrzanych działań.

 - Jeśli nie nie do wszystkich odpowiedzi z powyższych, założono jest złośliwe.

**Korygowania**

Użyj [narzędzie SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) zabezpieczyć środowiska przed tej metody.

## <a name="reconnaissance-using-dns"></a>Rekonesans przy użyciu systemu DNS

**Opis**

Serwer DNS zawiera mapę wszystkich komputerów, adresów IP i usług w sieci. Te informacje są używane przez osoby atakujące do mapowania struktury sieci i interesujących komputerów docelowych do wykonania kolejnych kroków ataku.

W protokole DNS istnieje kilka typów zapytań. Usługa ATA wykrywa pochodzące z serwerów DNS z systemem innym niż żądania AXFR (Transfer).

**Badanie**

1. Jest maszyną źródłową (**pochodzące z...** ) serwera DNS? Jeśli tak, to wówczas prawdopodobnie wynik fałszywie dodatni. Aby sprawdzić, kliknij alert, aby uzyskać dostęp do jego stronę szczegółów. W tabeli w obszarze **zapytania**, sprawdź skierowano domen. Czy te istniejących domen? Jeśli tak, następnie **Zamknij** podejrzanych działań (jest wynik fałszywie dodatni). Ponadto upewnij się, że UDP port 53 został otwarty między bram usługi ATA i komputera źródłowego, aby uniknąć przyszłych fałszywych alarmów.

2. Maszyna źródłowa jest uruchomiona skanera zabezpieczeń? Jeśli tak, **wykluczanie jednostek** w usłudze ATA bezpośrednio za pomocą **Zamknij i Wyklucz** lub za pośrednictwem **wykluczeń** strony (w obszarze **konfiguracji** — dostępne dla administratorów usługi ATA).

3. Jeśli odpowiedź na wszystkie powyższe nie, założono, że jest to złośliwe.

**Korygowania**

Aby zabezpieczyć wewnętrzny serwer DNS w celu uniemożliwienia przeprowadzenia rekonesansu przy użyciu systemu DNS, można wyłączyć transfery stref lub ograniczyć je tylko do określonych adresów IP. Aby uzyskać więcej informacji o ograniczaniu transferów stref, zobacz [ograniczyć transferów stref](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Modyfikowanie transferów stref jest jedno zadanie między listę kontrolną, która powinna być kierowane do [zabezpieczanie serwerów DNS z atakami wewnętrznymi i zewnętrznymi](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekonesans przy użyciu wyliczania sesji SMB


**Opis**

Wyliczenie komunikatów Block (SMB) serwera umożliwia osoby atakujące uzyskać informacje którym ostatnio zalogowani użytkownicy. Po te informacje, osoby atakujące mogą przenosić bok w sieci na uzyskanie dostępu do określonego konta poufnych.

Wykrywanie alert zostanie wywołany po wykonaniu wyliczenie sesji SMB na kontrolerze domeny, ponieważ to nie powinno się zdarzyć.

**Badanie**

1. Kliknij alert, aby uzyskać dostęp do jego stronę szczegółów. Sprawdź, które konta/s wykonać operację i kont, które zostały udostępnione, ile.

 - Czy jest jakaś skanera zabezpieczeń na komputerze źródłowym? Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.

2. Sprawdź, które zaangażowany użytkownika/s wykonać operację. Są one zazwyczaj Zaloguj się do komputera źródłowego lub są one administratorów, którzy powinien wykonywać takie zadania?  

3. Jeśli tak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.  

4. Jeśli tak i go nie należy tego robić, **Zamknij** podejrzanych działań.

5. Jeśli odpowiedź na wszystkie powyższe nie, założono, że jest to złośliwe.

**Korygowania**

Użyj [Net zaprzestanie narzędzia](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) zabezpieczyć środowiska przed takiego ataku.

## <a name="remote-execution-attempt-detected"></a>Wykryto próbę zdalne wykonywanie kodu

**Opis**

Osoby atakujące, którzy złamanie poświadczeń administracyjnych, lub użyj wykorzystać dzień zero zdalnego polecenia można wykonywać na kontrolerze domeny. Umożliwia to stały dostęp do sieci, zbieranie informacji, przeprowadzanie ataków typu „odmowa usługi” (DoS, denial of service) oraz wykonywanie innych działań. Usługa ATA wykrywa połączeń PSexec i zdalną usługę WMI.

**Badanie**

1. To jest typowe dla administracyjnych stacji roboczych i członków zespołu IT oraz kont usług, które wykonują zadania administracyjne na kontrolerze domeny. Jeśli to jest wielkość liter, a alert pobiera zaktualizowane od tego samego administratora i/lub komputer jest następnie wykonania zadania, **Pomiń** alertu.

2. Jest **komputera** zagrożona może wykonać wykonania zdalnego na kontrolerze domeny?

 - Jest **konta** zagrożona może wykonać wykonania zdalnego na kontrolerze domeny?

 - Jeśli odpowiedzi na oba pytania *tak*, następnie **Zamknij** alertu.

3. Jeśli odpowiedzi na pytania albo jest *nie*, a następnie to należy traktować jako dodatnią wartość true.

**Korygowania**

1. Ogranicz zdalny dostęp do kontrolerów domen z maszyn nienależących do warstwy 0.

2. Implementowanie [uprzywilejowany dostęp](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) aby komputery tylko ze wzmocnionymi zabezpieczeniami mogły łączyć się z kontrolerami domeny dla administratorów.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Poufne konto poświadczeniami ujawnionymi & udostępnianie poświadczeń konta usługi

**Opis**

Niektóre usługi wysłać poświadczenia konta w postaci zwykłego tekstu. Możliwe, nawet w przypadku kont poufnych. Osoby atakujące monitorowanie ruchu w sieci można catch, a następnie używać tych poświadczeń do celów złośliwe. Wszystkie hasła nieszyfrowanego poufne konto wyzwalać alert, gdy dla kont niepoufnych alert zostanie wywołany, jeśli pięć lub więcej różnych kont wysyła haseł w postaci zwykłego tekstu z tym samym komputerem źródłowym. 

**Badanie**

Kliknij alert, aby uzyskać dostęp do jego stronę szczegółów. Zobacz konta, które zostały udostępnione. Jeśli istnieje wiele takich kont, kliknij przycisk **Pobierz szczegóły** Aby wyświetlić listę w arkuszu programu Excel.

Zazwyczaj jest skrypt lub starszych aplikacji na komputerach źródłowych, która używa proste powiązanie LDAP.

**Korygowania**

Sprawdź konfigurację komputerów źródłowych i upewnij się, że nie korzystają z prostych powiązań LDAP. Zamiast przy użyciu prostego powiązania LDAP można użyć sal LDAP lub LDAPS.

## <a name="suspicious-authentication-failures"></a>Niepowodzenia uwierzytelniania podejrzanych

**Opis**

W ataków siłowych atakujący podejmie próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Znaleziono jeden raz, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywania alert zostanie wywołany, gdy wystąpienia wielu błędów uwierzytelniania, może to być albo poziomie za pomocą niewielki zestaw hasła przez wielu użytkowników. lub pionie o dużej zestawu haseł na tylko w przypadku kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji.

**Badanie**

1. Obejmuje wiele kont, kliknij przycisk **Pobierz szczegóły** Aby wyświetlić listę w arkuszu programu Excel.

2. Kliknij alert, aby przejść do strony szczegółów. Sprawdź czy próby logowania dowolnego została zakończona z pomyślnym uwierzytelnieniu, czy są one wyświetlane jako **odgadnąć kont** po prawej stronie infographic. Jeśli tak, czy jakakolwiek **odgadnąć kont** zwykle używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

3. Jeśli istnieją nie **odgadnąć kont**, są **ataku kont** zwykle używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

**Korygowania**

[Złożone i długich haseł](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) podaj niezbędne pierwszy poziom zabezpieczeń przed atakami siłowymi.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podejrzenie kradzieży tożsamości na podstawie nietypowego zachowania

**Opis**

Usługa ATA uzyskuje informacje o zachowania jednostek dla użytkowników, komputerów i zasobów w metodzie przesuwanego okresie trzech tygodni. Model zachowanie jest oparty na następujących działań: maszyn jednostek zalogowany, jednostka żądane zasoby dostęp do i czas te operacje miało miejsce. Usługa ATA wysyła alert po odchylenia od zachowanie jednostki oparte na algorytmów uczenia maszynowego. 

**Badanie**

1. Użytkownik powinien wykonywać te operacje?

2. Należy rozważyć w następujących przypadkach jako potencjalnych fałszywych alarmów: użytkownika, który zwrócił z urlopu, personel działu, które wykonują nadmiarowe dostępu w ramach obowiązku (na przykład kolekcji w pomocy technicznej w przypadku danego dnia lub tygodnia) zdalnego pulpitu aplikacji. + Jeśli możesz **Zamknij i Wyklucz** alertu, użytkownik nie będzie należeć do wykrywania


**Korygowania**

W zależności od tego, co spowodowało to nietypowe zachowanie występuje należy wykonać różne akcje. Na przykład jeśli jest to spowodowane skanowanie sieci, komputer, z którego ten błąd wystąpił powinien zostać zablokowany sieci (o ile nie zostało zatwierdzone).

## <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu


**Opis**

Osoby atakujące użyj narzędzi, które implementują różnych protokołów (protokół SMB, protokołu Kerberos, NTLM) w niestandardowy sposób. Podczas tego typu ruchu sieciowego jest akceptowana przez system Windows bez ostrzeżenia, usługi ATA jest w stanie rozpoznać potencjalnych złośliwymi działaniami. Zachowanie jest wskaźnikiem technik, takich jak życie nadmiernego-Pass--Hash i atakami, jak również używane przez ransomware zaawansowane, na przykład WannaCry luki w zabezpieczeniach.

**Badanie**

Określenie protokołu, z którą jest rzadko używana — od osi czasu podejrzanych działań, kliknij na podejrzane działanie, aby uzyskać dostęp do jego stronę szczegółów; Protokół pojawia się powyżej strzałkę: Kerberos lub NTLM.

- **Kerberos**: to będzie często wyzwalany Jeśli przejęcie narzędzia, takie jak używane Mimikatz, potencjalnie wykonywania ataku Overpass--Hash. Sprawdź, czy komputer źródłowy działa aplikacja, która implementuje własną stosu protokołu Kerberos, nie zgodnie z RFC protokołu Kerberos. Jeśli tak jest, jest niegroźne pozytywną wartość true i możesz **Zamknij** alertu. Jeśli alert śledzi jest uruchomiony i nadal jest wielkość liter, możesz **Pomiń** alertu.

- **NTLM**: może być WannaCry lub narzędzi, takich jak Metasploit Medusa i Hydra.  

Aby określić, czy to jest atak WannaCry, wykonaj następujące czynności:

1. Sprawdź, czy komputer źródłowy działa narzędzie ataku, takie jak Metasploit, Medusa lub Hydra.

2. Jeśli nie zostaną znalezione żadne narzędzia ataku, należy sprawdzić, jeśli komputer źródłowy jest uruchomiona aplikacja, która implementuje własną stosu protokołu NTLM lub SMB.

3. Jeśli nie, sprawdź, czy jest to spowodowane WannaCry przez uruchomienie skryptu skanera WannaCry, na przykład [ten skaner](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) przed objętego podejrzanych działań komputera źródłowego. Jeśli skaner stwierdzi, że komputer jako zainfekowane lub narażony, pracy na stosowanie poprawek do komputera i usuwania złośliwego oprogramowania i blokuje ją z sieci.

4. Nie znaleziono skryptu, że komputer jest zainfekowany lub narażony, następnie nadal mogą być zainfekowane, ale usługi SMBv1 mogły zostać wyłączone lub maszynie została zastosowana poprawka, która wpłynie narzędzie skanowania.

**Korygowania**

Poprawka programu maszyny, szczególnie stosowania aktualizacji zabezpieczeń.

1. [Wyłącz usługi SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Usuń WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi może odszyfrować danych w ręce niektóre programy ransom, ale tylko wtedy, jeśli użytkownik nie ma ponownie uruchomiona lub ją wyłączyć komputer. Aby uzyskać więcej informacji, zobacz [chcesz Ransomware krzykiem](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)

## <a name="related-videos"></a>Powiązane pliki wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Zobacz też
- [Podręcznika dotyczącego podejrzanych działań usługi ATA](http://aka.ms/ataplaybook)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
