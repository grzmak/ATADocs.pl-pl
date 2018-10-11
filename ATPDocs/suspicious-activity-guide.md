---
title: Podręcznik usługi Azure ATP zabezpieczeń alertów | Dokumentacja firmy Microsoft
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/10/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ca22fc6430556d49a6709be2f46c0c0b8746fa38
ms.sourcegitcommit: 0c05308c832e4b03ea3945788de39feabfdb5671
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/10/2018
ms.locfileid: "48914506"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Usługa Azure Advanced Threat Protection alertu Przewodnik po zabezpieczeniach

Następujące odpowiednie badania wszystkie alerty zabezpieczeń usługi Azure ATP mogą być klasyfikowane jako:

-   **Prawdziwie dodatni**: złośliwa Akcja wykryta przez narzędzia Azure ATP.

-   **Wynik niegroźny prawdziwie dodatni**: Akcja wykryta przez narzędzia Azure ATP jest prawdziwe, ale nie złośliwego test penetracyjny.

-   **Wynik fałszywie dodatni**: alarm wartość false, co oznacza działania nie się zdarzyć.

Aby uzyskać więcej informacji na temat pracy z alertami zabezpieczeń usługi Azure ATP, zobacz [Praca z alertami zabezpieczeń](working-with-suspicious-activities.md).




## <a name="brute-force-attack-using-ldap-simple-bind"></a>Atak siłowy przy użyciu prostego powiązania LDAP

**Opis**

>[!NOTE]
> Główna różnica między **podejrzane błędy uwierzytelniania** i wykrywanie, w tym wykrywanie narzędzia Azure ATP można określić, czy inne hasła były używane.

W ramach ataków siłowych osoba atakująca podejmuje próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont, aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Gdy zostanie znaleziony, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywanie alert jest wyzwalany, gdy usługi Azure ATP wykrywa ogromną liczbę uwierzytelnień prostego powiązania. Może to być albo *poziomo* wprowadzaj w małej grupie haseł dla wielu użytkowników; lub *pionowo "* z dużym zestawem haseł na kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji.

**Badanie**

1. Jeśli zaangażowanych jest wiele kont, kliknij przycisk **Pobierz szczegóły** do wyświetlania listy w arkuszu kalkulacyjnym programu Excel.

2. Kliknij alert, aby przejść do jego dedykowaną stronę. Sprawdź, czy prób logowania wszystkie zakończone z pomyślnym uwierzytelnieniu. Próby pojawiał się jako **odgadnięte konta** po prawej stronie grafikę informacyjną. Jeśli tak, czy którakolwiek z **odgadnięte konta** normalnie używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

3. W przypadku nie **odgadnięte konta**, czy którakolwiek z **zaatakowane konta** normalnie używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.

## <a name="encryption-downgrade-activity"></a>Działanie obniżenia poziomu szyfrowania

**Opis**

Obniżenie poziomu szyfrowania jest metodą osłabienia protokołu Kerberos przez obniżenie poziomu szyfrowania różnych pól protokołu, które jest zazwyczaj zaszyfrowana za pomocą najwyższego poziomu szyfrowania. Polem zaszyfrowanych obniżony poziom może być łatwiejsze docelowej do trybu offline ataków siłowych. Korzystanie z różnych metod ataków słabe cyfry szyfrowania protokołu Kerberos. W tym wykrywanie narzędzia Azure ATP uczy się typów szyfrowania protokołu Kerberos, które są używane przez komputery i użytkownicy i alerty, gdy jest słabsza szyfrowania użyte w tym: (1) jest niczym niezwykłym, komputer źródłowy i/lub użytkownika. a (2) dopasowuje znane techniki ataku.

Istnieją trzy typy wykrywania:

1.  Złośliwe oprogramowanie Skeleton Key — to złośliwe oprogramowanie, które jest uruchamiane na kontrolerach domeny i umożliwia uwierzytelnianie domeny przy użyciu dowolnego konta bez znajomości hasła. To złośliwe oprogramowanie często używa słabszych algorytmów szyfrowania w celu wyznaczania wartości skrótu hasła użytkownika na kontrolerze domeny. W tym wykrywanie metody szyfrowania wiadomości KRB_ERR z kontrolera domeny do konta, pytanie o bilet został obniżony w porównaniu do uprzednio zapamiętane zachowanie.

2.  Bilet Golden — [bilet uwierzytelniania Golden Ticket](#golden-ticket) alertu, metodę szyfrowania dla pola TGT w żądaniu TGS_REQ (żądanie obsługi) komunikatu z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie. To nie jest oparty na anomalii czasu (tak jak inne wykrywania bilet uwierzytelniania Golden Ticket). Ponadto nie było żadnych żądaniu uwierzytelnienia protokołu Kerberos, skojarzone z poprzedniego żądania obsługi, wykrytych przez zaawansowanej ochrony przed zagrożeniami.

3.  Overpass--Hash — osoba atakująca można użyć słabe skradzionego skrótu, aby można było utworzyć bilet silne z żądaniem protokołu Kerberos AS. W tym wykrywanie AS_REQ typ szyfrowania wiadomości z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie (oznacza to, że komputer został przy użyciu szyfrowania AES).

**Badanie**

Najpierw sprawdź opis alertu, aby zobaczyć, z trzech typów wykrywania wymienione powyżej są zajmujących się. Aby uzyskać więcej informacji Pobierz arkusz kalkulacyjny programu Excel.

1.  Złośliwe oprogramowanie Skeleton Key — możesz sprawdzić, jeśli złośliwe oprogramowanie Skeleton Key ma wpływ na kontrolerach domeny przy użyciu [skanera przygotowanego przez zespół usługi Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Jeśli skaner wykryje złośliwe oprogramowanie na 1 lub więcej kontrolerów domeny, jest prawdziwie dodatni.

2.  Bilet uwierzytelniania Golden Ticket — w arkuszu kalkulacyjnym programu excel, przejdź na kartę działań sieci. Zobaczysz, że odpowiednie pole starszej jest **żądania typ szyfrowania biletu**, i **komputera źródłowego obsługiwane typy szyfrowania** zawiera silniejszych metod szyfrowania.

  1. Wyboru zasobu uzyskiwał dostęp do tych biletów, w przypadku jeden zasób, z których korzystają wszystkie zweryfikuje go, upewnij się, że jest prawidłowy zasób, które one powinien uzyskać dostęp. Ponadto sprawdź, czy zasób docelowy obsługuje metody silne szyfrowanie. Możesz sprawdzić to w usłudze Active Directory, sprawdzając atrybutu msDS-SupportedEncryptionTypes, zasobów konta usługi.
  
  2. Sprawdź komputer źródłowy i konta lub w przypadku wielu źródłowych konta komputerów i sprawdzenia, czy ich mają coś wspólnych. Na przykład wszystkich pracowników marketingu użyj konkretnej aplikacji, które mogą być przyczyną alertu. Istnieją przypadki, w których niestandardową aplikację, która jest rzadko używana jest uwierzytelniany przy użyciu niższe szyfrowania szyfrowanie. Sprawdź, czy istnieją niestandardowe aplikacje na komputerze źródłowym. Jeśli tak, prawdopodobnie jest niegroźnie prawdziwie dodatni i można pominąć.
  


3.  Overpass--Hash — w arkuszu kalkulacyjnym programu excel, przejdź na kartę działań sieci. Zobaczysz, że odpowiednie pole starszej jest **szyfrowany typ szyfrowania sygnatura czasowa** i **komputera źródłowego obsługiwane typy szyfrowania** zawiera silniejszych metod szyfrowania.

  1. Istnieją przypadki, w których ten alert może być wyzwalany, gdy użytkownicy logują się przy użyciu kart inteligentnych, jeśli konfiguracja karty inteligentnej zostało niedawno zmienione. Sprawdź, czy wystąpiły zmiany następująco dla konta związane. Jeśli tak, to prawdopodobnie jest niegroźnie prawdziwie dodatni i można pominąć.
  2. Wyboru zasobu uzyskiwał dostęp do tych biletów, w przypadku jeden zasób, z których korzystają wszystkie zweryfikuje go, upewnij się, że jest prawidłowy zasób, które one powinien uzyskać dostęp. Ponadto sprawdź, czy zasób docelowy obsługuje metody silne szyfrowanie. Możesz sprawdzić to w usłudze Active Directory, sprawdzając atrybutu msDS-SupportedEncryptionTypes, zasobów konta usługi.

**Korygowanie**

1.  Szkielet klucza — Usuń złośliwe oprogramowanie. Aby uzyskać więcej informacji, zobacz [analizy złośliwe oprogramowanie Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Uwierzytelniania Golden Ticket — postępuj zgodnie z instrukcjami [bilet uwierzytelniania Golden Ticket](#golden-ticket) podejrzanych działań.   
    Implementuje są również, tworząc bilet uwierzytelniania Golden Ticket wymagają uprawnień administratora domeny, dlatego [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).

3.  Overpass--Hash — Jeśli zaangażowane konto nie jest uwzględniana wielkość liter, następnie zresetuj hasło tego konta. Zapobiega to osoba atakująca tworzenia nowych bilety protokołu Kerberos na podstawie skrótu hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną. Jeśli jest kontem wrażliwym, należy rozważyć resetowania konta krbtgt w DOMENIE, dwa razy, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Zobacz też przy użyciu [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Ponieważ jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania z [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Działanie wystawionego jako przynęta


**Opis**

Konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu identyfikacji i śledzenia złośliwych działań, które obejmuje te konta. Konta wystawione jako przynęta powinien pozostać nieużywane, mając atrakcyjny nazwę do nakłonienia osoby atakujące (na przykład administrator SQL). Wszystkie działania z nich może wskazywać na złośliwe działanie.

Aby uzyskać więcej informacji na temat konta wystawione jako przynęta, zobacz [zainstalować narzędzia Azure ATP — krok 7](install-atp-step7.md).

**Badanie**

1.  Sprawdź, czy właściciela komputera źródłowego użyto konta wystawionego jako przynęta na potrzeby uwierzytelniania, przy użyciu metody opisanej na stronie podejrzanych działań (na przykład protokołu Kerberos, LDAP, NTLM).

2.  Przejdź do strony profilu komputery źródłowy i Sprawdź inne konta, które uwierzytelniony z nich. Jeśli używane konto wystawione jako przynęta, należy skontaktować się z właścicielami tych kont.

3.  Może to być logowania nieinterakcyjnego, więc upewnij się wyszukać aplikacje lub skrypty, które są uruchomione na komputerze źródłowym.

Jeśli po wykonaniu kroki od 1 do 3, jeśli istnieją dowody użytkowania niegroźne, zakłada się, że jest to złośliwy.

**Korygowanie**

Upewnij się, że pułapki konta są używane tylko dla ich przeznaczenie, w przeciwnym razie może wygenerować wiele alertów.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Kradzież tożsamości za pomocą ataku typu Pass--Hash

**Opis**

Pass--Hash to technika ruchu poprzecznego, w którym osoby atakujące kradzieży skrótu NTLM użytkownika z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera. 

**Badanie**

Skrót użyto z komputera, że wybrany użytkownik jest właścicielem lub regularnie korzysta? Jeśli tak, to wynik fałszywie dodatni. W przeciwnym razie jest to prawdopodobnie prawdziwie dodatni.

**Korygowanie**

1. Jeśli konto zaangażowane nie jest wielkość liter, następnie zresetuj hasło tego konta. Zapobiega to osoba atakująca tworzenia nowych bilety protokołu Kerberos na podstawie skrótu hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną. 

2. Jeśli jest kontem wrażliwym, należy rozważyć resetowania konta krbtgt w DOMENIE, dwa razy, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), zobacz też przy użyciu [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Ponieważ jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania z [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Kradzież tożsamości za pomocą ataku typu Pass--Ticket

**Opis**

Pass--Ticket to technika ruchu poprzecznego, w którym osoby atakujące dokonują kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera, na podstawie kradzieży biletu. W tym wykrywanie biletu protokołu Kerberos występuje używanych na różnych komputerach (co najmniej dwa).

**Badanie**

1. Kliknij przycisk **Pobierz szczegóły** przycisk, aby wyświetlić pełną listę adresów IP, które są zaangażowani. Nie adres IP jednego lub obu komputerów należy do podsieci, przydzielany z za małego rozmiaru puli DHCP, na przykład, sieci VPN lub Wi-Fi? Adres IP jest udostępniony? Na przykład przez urządzenie NAT? Czy na co najmniej jeden źródłowych adresów IP rozpoznane przez czujnik? (może to wskazywać, odpowiednie porty z czujnika na urządzeniach nie są poprawnie otwarty.) Jeśli odpowiedzi na dowolne z tych pytań jest tak, to wynik fałszywie dodatni.

2. Czy istnieje niestandardową aplikację, która przekazuje bilety w imieniu użytkowników? Jeśli tak, to wynik niegroźny prawdziwie dodatni.

**Korygowanie**

1. Jeśli konto zaangażowane nie jest wielkość liter, następnie zresetuj hasło tego konta. Zapobiega to osoba atakująca tworzenia nowych bilety protokołu Kerberos na podstawie skrótu hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną.  

2. Jeśli jest kontem wrażliwym, należy rozważyć resetowania konta krbtgt w DOMENIE, dwa razy, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), zobacz też przy użyciu [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Ponieważ jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania w [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).

## Bilet uwierzytelniania golden protokołu Kerberos<a name="golden-ticket"></a>

**Opis**

Osoby atakujące przy użyciu uprawnień administratora domeny może naruszyć [konta krbtgt w DOMENIE](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Przy użyciu konta krbtgt w DOMENIE, można utworzyć biletu protokołu Kerberos udzielania biletu (TGT) zapewniający autoryzację do dowolnego zasobu i ustawienia wygasania biletu do dowolnego dowolnego czasu. Tego BILETU fałszywych nosi nazwę "goldentTicket" i pozwala osobom atakującym na uzyskanie stałego dostępu do sieci.

W tym wykrywanie alert jest wyzwalany, gdy bilet protokołu Kerberos przyznania biletu jest używany dla więcej niż dozwolony czas dozwolone określonych w [maksymalny okres istnienia biletu użytkownika](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx), to **anomalii czasu**atak metodą złotego biletu lub nieistniejące konta, to **nieistniejące konto** atak metodą złotego biletu.


**Badanie**

- **Czas anomalii**
   1.   Czy były wszelkie zmiany ostatnio (w ciągu ostatnich kilku godzin), wprowadzone do maksymalny okres istnienia biletu użytkownika w zasadach grupy — ustawienie? Sprawdź, czy określone wartości i sprawdzić, czy jest niższy niż czas, jaki był używany--ticket. Jeśli tak, zamknij alert (było to wynik fałszywie dodatni).
   2.   Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest zaangażowane w tym alercie maszynę wirtualną? Jeśli tak, on niedawno wychodzi z zapisanego stanu? Jeśli tak, zamknij ten alert.
   3.   Jeśli odpowiedź na powyższe pytania nie przyjęto założenie, jest to złośliwy.

- **Nieistniejące konto — nowe** 
   1.   Należy odpowiedzieć na następujące pytania:
         - Czy użytkownik jest użytkownikiem domeny znane i prawidłowe? Jeśli tak, zamknij alert (było to wynik fałszywie dodatni).
         - Użytkownik zostało ostatnio dodane? Jeśli tak, zamknij ten alert, zmiana może nie zostały jeszcze zsynchronizowane.
         - Użytkownik został ostatnio usunięty z usługi AD? Jeśli tak, zamknij ten alert.
   2.   Jeśli odpowiedź na powyższe pytania nie przyjęto założenie, jest to złośliwy.

1. Oba rodzaje ataków na bilet uwierzytelniania golden ticket, kliknij polecenie na komputerze źródłowym, aby przejść do jego **profilu** strony. Sprawdź, jakie wystąpiły w okolicy czasowej działania, a wyszukiwanie nietypowych działań, w tym, kto został zalogowany, jakie zasoby są dostępne? 

2.  Czy wszyscy użytkownicy, którzy są zalogowani do komputera powinien być zalogowany do? Co to są ich uprawnienia? 

3.  Ci użytkownicy mają mieć dostęp do tych zasobów?<br>
Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![wskaźnika WD](./media/wd-badge.png).
 
 4. Aby badać maszyny, w usłudze Windows Defender ATP, sprawdź, które procesy i alerty wystąpił zbliżonym do momentu alertu.

**Korygowanie**


Zmień hasło biletu udzielania biletu protokołu Kerberos (KRBTGT) dwa razy, zgodnie z zaleceniami w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)przy użyciu [resetowania haseł kont KRBTGT/kluczy Narzędzie](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Implementuje są również, tworząc bilet uwierzytelniania Golden Ticket wymagają uprawnień administratora domeny, dlatego [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).




## <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych

**Opis**

Interfejs API ochrony danych (DPAPI) umożliwia przez Windows bezpieczny sposób ochrony haseł, zapisane przez przeglądarek, zaszyfrowane pliki i innych poufnych danych. Kontrolery domeny przechowują zapasowy klucz główny, który może służyć do odszyfrowania wszystkich wpisów tajnych zaszyfrowanych przy użyciu interfejsu DPAPI na komputerach przyłączonych do domeny Windows. Osoby atakujące, można użyć klucza głównego do odszyfrowania wszystkich danych poufnych chroniony funkcją DPAPI na wszystkich komputerach przyłączonych do domeny.
W tym wykrywanie alert jest wyzwalany, gdy DPAPI służy do pobierania kopii zapasowej klucza głównego.

**Badanie**

1. Komputer źródłowy systemem zatwierdzonych organizacji, jest zaawansowane skaner zabezpieczeń w usłudze Active Directory?

2. Jeśli tak i jego powinna zawsze być tych czynności **Zamknij i Wyklucz** podejrzanych działań.

3. Jeśli tak i nie należy przeprowadzać tego **Zamknij** podejrzanych działań.

**Korygowanie**

Aby korzystać z interfejsu DPAPI, osoba atakująca potrzebuje uprawnienia administratora domeny. Implementowanie [przekazać zalecenia wyznaczania wartości skrótu](http://aka.ms/PtH).

## <a name="malicious-replication-of-directory-services"></a>Złośliwa replikacja usług katalogowych


**Opis**

Replikacja usługi Active Directory to proces, za pomocą którego zmiany wprowadzone na jednym kontrolerze domeny są synchronizowane z innymi kontrolerami domeny. Biorąc pod uwagę niezbędne uprawnienia, atakujący może zainicjować żądanie replikacji, umożliwiając im danych przechowywanych w usłudze Active Directory, w tym skrótów haseł.

W tym wykrywanie alert jest wyzwalany, gdy żądanie replikacji jest inicjowane z komputera, który nie jest kontrolerem domeny.

**Badanie**

> [!NOTE]
> W przypadku kontrolerów domeny, na których nie zainstalowano narzędzia Azure ATP czujniki te kontrolery domeny nie są objęte usługi Azure ATP. W takim przypadku w przypadku wdrożenia nowego kontrolera domeny na kontrolerze domeny wyrejestrowany lub niechronione go nie zostaną zidentyfikowane przez narzędzia Azure ATP jako kontroler domeny, na początku. Zdecydowanie zaleca się instalowanie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure na każdym kontrolerze domeny, aby uzyskać pełne.

1. Jest to komputer w pytanie kontrolera domeny? Na przykład nowo wypromowaną kontroler domeny, który ma problemy z replikacją. Jeśli tak, **Zamknij** podejrzanych działań. 
2.  Dany komputer powinien być replikowanie danych z usługi Active Directory? Na przykład usługi Azure AD Connect lub sieci monitorowanie wydajności urządzeń. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.
3. Czy adres IP, z której wysłano żądanie replikacji NAT lub serwer proxy? Jeśli tak, sprawdź w przypadku nowego kontrolera domeny za urządzeniem czy wystąpiły inne podejrzanych działań z niego. 

4. Kliknij komputer źródłowy lub konta, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej replikacji, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![Znaczek usługi Windows Defender ATP](./media/wd-badge.png) Aby badać na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu. 


**Korygowanie**

Zweryfikuj następujące uprawnienia: 

- Replikuj zmiany katalogu   

- Replikuj wszystkie zmiany w katalogu  

Aby uzyskać więcej informacji, zobacz [uprawnienia Grant Active Directory Domain Services dla synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Możesz wykorzystać [skaner list ACL usługi AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub utworzyć skrypt programu Windows PowerShell, aby określić, kto w domenie ma te uprawnienia.


## <a name="privilege-escalation-using-forged-authorization-data"></a>Eskalacja uprawnień przy użyciu sfałszowanych danych autoryzacji

**Opis**

Znane luki w zabezpieczeniach w starszych wersjach systemu Windows Server umożliwiają osobom atakującym manipulację uprzywilejowanych certyfikat atrybutu (PAC), polem w bilecie protokołu Kerberos, który zawiera dane autoryzacji użytkownika (w usłudze Active Directory jest członkostwo w grupie), udzielanie osoby atakujące dodatkowych uprawnień.

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów.

2. Jest komputerem docelowym (w obszarze **ACCESSED** kolumny) poprawiono MS14-068 (kontroler domeny) lub MS11-013 (serwer)? Jeśli tak, **Zamknij** podejrzanych działań (jest to wynik fałszywie dodatni).

3. Jeśli nie, komputer źródłowy jest uruchamiany (w obszarze **FROM** kolumny) systemu operacyjnego/aplikacja modyfikują certyfikat PAC? Jeśli tak, **Pomiń** podejrzanych działań (jest to wynik niegroźny prawdziwie dodatni).

4. Jeśli odpowiedź była nie na dwa pytania powyżej przyjęto założenie, jest to złośliwy.

**Korygowanie**

Upewnij się, że na wszystkich kontrolerach domen z systemami operacyjnymi starszymi niż system Windows Server 2012 R2 zainstalowano poprawkę [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege), a wszystkie serwery członkowskie i kontrolery domen do wersji 2012 R2 mają zainstalowaną poprawkę KB2496930. Aby uzyskać więcej informacji, zobacz [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) i [Forged PAC (Sfałszowany element PAC)](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekonesans przy użyciu wyliczania kont

**Opis**

W Rekonesans wyliczenie konta osoba atakująca używa słownik zawierający tysiące nazwy użytkowników lub narzędzi, takich jak KrbGuess próby odgadnięcia nazw użytkowników w domenie. Osoba atakująca sprawia, że żądania protokołu Kerberos, aby można było, spróbuj znaleźć prawidłowej nazwy użytkownika w domenie przy użyciu tych nazw. Jeśli wynik pomyślnie Określa nazwę użytkownika, osoba atakująca otrzyma błąd protokołu Kerberos **wstępnego uwierzytelniania wymagany** zamiast **nieznanego podmiotu zabezpieczeń**. 

W tym wykrywania usługi Azure ATP może wykryć pochodzenia ataku, całkowita liczba prób odgadnięcia i ile zostały dopasowane. W przypadku zbyt wielu użytkownikom nieznany narzędzia Azure ATP wykrywa ją jako podejrzane działanie. 

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów. 

2. Należy tej maszyny hosta zapytania do kontrolera domeny, do tego, czy istnieją konta (np. serwerów Exchange)? <br></br>
Czy istnieje, skryptu lub aplikacji uruchomionej na hoście, który można wygenerować ten problem? <br></br>
Jeśli odpowiedź na jedną z tych pytań jest twierdząca, **Zamknij** podejrzanych działań (jest to wynik niegroźny prawdziwie dodatni) i Wyklucz, który hostował na poziomie podejrzanego działania.

3. Pobierz szczegóły alertu w arkuszu kalkulacyjnym programu Excel, aby wygodnie lista prób konta, podzielone na istniejące i nieistniejące konta. Jeśli przyjrzymy się bez istniejącego konta arkusza w arkuszu kalkulacyjnym i kont wygląda znajomo, mogą być wyłączone konta lub pracowników, którzy opuścił firmę. W takich przypadkach jest mało prawdopodobne, że próba pochodzi ze słownika. Najbardziej prawdopodobne jest, aplikacji lub skryptu, który jest sprawdzanie, które konta nadal istnieć w usłudze Active Directory, co oznacza, że wynik niegroźny prawdziwie dodatni.

3. W przypadku większości nieznane nazwy wszystkich prób odgadnięcia pasowało istniejącymi nazwami kont w usłudze Active Directory? Jeśli nie ma żadnych dopasowań, próba została przełączona, ale należy zwrócić uwagę na alert, aby wyświetlić, jeśli jest aktualizowana wraz z upływem czasu.

4. Jeśli dowolny wynik próbuje dopasować istniejących nazw kont, osoba atakująca zna istnienia konta w danym środowisku i mogą próbować użyć ataków siłowych można uzyskiwać dostęp do domeny przy użyciu nazwy odnalezionych użytkowników. Sprawdź nazwy odgadnięte konta dla dodatkowych podejrzanych działań. Sprawdź, jeśli dopasowane kont są kont poufnych.


**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.


## <a name="reconnaissance-using-directory-services-queries"></a>Rekonesans przy użyciu zapytań usług katalogowych

**Opis**

Rekonesans usług katalogowych jest używana przez osoby atakujące do mapowania struktury katalogów i identyfikacji uprzywilejowanych kont do dalszych etapów w przypadku ataków. Protokół Security Account Manager Remote (SAM-R) to jedna z metody używane do wysyłania zapytań o katalog, aby wykonać takie mapowanie.

W tym wykrywanie alerty nie będą wyzwalane w pierwszym miesiącu po wdrożeniu usługi Azure ATP. Podczas nauki okresu, profile narzędzia Azure ATP zapytania SAM-R, które zostały wprowadzone przez nich i komputery wyliczenia i pojedynczych zapytań kont poufnych.

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów. Sprawdź zapytania, które zostały wykonane (na przykład, Administratorzy przedsiębiorstwa lub administratora) i czy mu się to udało.

2. Takie zapytania powinny być przeprowadzone z komputera źródłowego w danym?

3. Jeśli tak, jak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.

4. Jeśli tak i jej nie należy tego robić, **Zamknij** podejrzanych działań.

5. W przypadku informacji o koncie zaangażowane: takich zapytań mają być wprowadzone przez tego konta lub jest to konto zwykle Zaloguj się do komputera źródłowego?

 - Jeśli tak, jak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.

 - Jeśli tak i jej nie należy tego robić, **Zamknij** podejrzanych działań.

 - Jeśli odpowiedź była nie do wszystkich powyższych, założono to złośliwy.

6. Jeśli nie ma dostępnych informacji o koncie, które brały udział, możesz przejść do punktu końcowego i sprawdź konto, które zostało zarejestrowane w chwili alertu.

**Korygowanie**

Utrwalanie środowiska przed ta technika, za pomocą następującego procesu:
1. Komputer działa luk w zabezpieczeniach, narzędzie do skanowania?  
2. Zbadaj, czy określone zapytanie o użytkowników i grup w ataku są kontami uprzywilejowanych lub o wysokiej wartości (to znaczy, Dyrektor Generalny, Dyrektor finansowy, zarządzanie infrastrukturą IT, itp.).  Jeśli tak, spójrz na inne działanie w punkcie końcowym również i monitorować komputery, które konta kwerendy jest się zalogowanym, ponieważ prawdopodobnie są elementy docelowe ruchu poprzecznego.

## <a name="reconnaissance-using-dns"></a>Rekonesans przy użyciu systemu DNS

**Opis**

Serwer DNS zawiera mapę wszystkich komputerów, adresów IP i usług w sieci. Te informacje są używane przez osoby atakujące do mapowania struktury sieci i interesujących komputerów docelowych do wykonania kolejnych kroków ataku.

W protokole DNS istnieje kilka typów zapytań. Narzędzie Azure ATP wykrywa żądania AXFR (transferu) pochodzące z serwerów DNS bez.

**Badanie**

1. Maszyna źródłowa jest (**pochodzące z komputera...** ) serwera DNS? Jeśli tak, następnie jest to prawdopodobnie wynik fałszywie dodatni. Aby sprawdzić, kliknij alert, aby przejść do jego stronę szczegółów. W tabeli w obszarze **zapytania**, sprawdź, które domeny wykonano zapytanie. Czy te istniejących domen? Jeśli tak, następnie **Zamknij** podejrzanych działań (jest to wynik fałszywie dodatni). Ponadto upewnij się, że port 53 protokołu UDP między i jest otwarty narzędzia Azure ATP czujnik autonomiczny komputer źródłowy, aby uniknąć przyszłych wyników fałszywie dodatnich.

2. Maszyna źródłowa działa skaner zabezpieczeń? Jeśli tak, **wykluczanie jednostek** w zaawansowanej ochrony przed zagrożeniami, albo bezpośrednio za pomocą **Zamknij i Wyklucz** lub za pośrednictwem **wykluczeń** strony (w obszarze **konfiguracji** — dostępne dla administratorów usługi Azure ATP).

3. Jeśli odpowiedzi na wszystkie pytania poprzedzającego jest nie, Zachowaj badania koncentrujące się na komputerze źródłowym. Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej żądania, wyszukując nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![Znaczek usługi Windows Defender ATP](./media/wd-badge.png) Aby badać na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu. 

**Korygowanie**

Aby zabezpieczyć wewnętrzny serwer DNS w celu uniemożliwienia przeprowadzenia rekonesansu przy użyciu systemu DNS, można wyłączyć transfery stref lub ograniczyć je tylko do określonych adresów IP. Aby uzyskać więcej informacji o ograniczaniu transferów stref, zobacz [Ograniczanie transferów stref](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Modyfikacja transferów stref jest jednym z zadań listę kontrolną, która powinny być kierowane do [zabezpieczenia serwerów DNS przed atakami wewnętrznymi i zewnętrznymi](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekonesans przy użyciu wyliczania sesji SMB


**Opis**

Wyliczanie bloku komunikatów (SMB) serwera pozwala osobom atakującym uzyskanie informacji którym ostatnio zalogowani użytkownicy. Gdy osoby atakujące już te informacje, mogą przenosić bok w sieci do określonych kont poufnych.

Wykrywanie alert zostanie wywołany podczas wyliczania sesji SMB jest wykonywane na kontrolerze domeny, ponieważ to nie powinny występować.

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów. Sprawdź konta/s, który wykonał operację i narażonych kontach, jeśli istnieje.

 - Czy istnieje pewnego rodzaju skaner zabezpieczeń, uruchomiony na komputerze źródłowym? Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.

2. Sprawdź, które zaangażowanych użytkowników/s wykonał operację. Są one zazwyczaj Zaloguj się do komputera źródłowego, czy też są one administratorów, którzy należy wykonać takie działania?  

3. Jeśli tak, jak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.  

4. Jeśli tak i jej nie należy tego robić, **Zamknij** podejrzanych działań.

5. Jeśli odpowiedzi na wszystkie powyższe nie, założono, że to złośliwy.

**Korygowanie**

Użyj [narzędzia Net zaprzestanie](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) wzmacniania zabezpieczeń środowiska na atak.

## <a name="remote-code-execution-attempt"></a>Próba wykonania zdalnego kodu

**Opis**

Osoby atakujące, które złamanie poświadczeń administracyjnych lub użyj wykorzystać zero day mogą wykonywać polecenia zdalne na kontrolerze domeny. Umożliwia to stały dostęp do sieci, zbieranie informacji, przeprowadzanie ataków typu „odmowa usługi” (DoS, denial of service) oraz wykonywanie innych działań. Narzędzie Azure ATP wykrywa połączeń narzędzia PSexec i usługi zdalnej usługi WMI.

**Badanie**

1. To jest typowe dla administracyjnych stacji roboczych i członków zespołu IT oraz kont usług, które wykonują zadania administracyjne na kontrolerach domeny. Jeśli jest to przypadek, a alert jest aktualizowany od samego administratora i/lub komputer są następnie wykonuje zadanie, **Pomiń** alertu.

2. Jest **komputera** danego możliwość wykonywania działań zdalnych względem kontrolera domeny?

 - Jest **konta** danego możliwość wykonywania działań zdalnych względem kontrolera domeny?

 - Jeśli odpowiedzi na oba pytania *tak*, następnie **Zamknij** alertu.

3. Jeśli odpowiedzi na pytania, albo nie, następnie należy to uwzględnić prawdziwie dodatni. Spróbuj znaleźć źródło próby, sprawdzając profile komputera i konta. Kliknij komputer źródłowy lub konta, aby przejść do strony profilu. Sprawdź, co się stało z momentu te próby, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. Włączenie programu Windows Defender ATPintegration kliknij wskaźnik usługi Windows Defender ATP ![Znaczek usługi Windows Defender ATP](./media/wd-badge.png) Aby badać na maszynie. W Windows Defender ATPyou zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu. 

**Korygowanie**

1. Ogranicz zdalny dostęp do kontrolerów domen z maszyn nienależących do warstwy 0.

2. Implementowanie [dostęp uprzywilejowany](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) umożliwia jedynie maszynom o wzmocnionych zabezpieczeniach nawiązać połączenia z kontrolerami domeny dla administratorów.

## <a name="suspicious-authentication-failures"></a>Podejrzane błędy uwierzytelniania

**Opis**

W ramach ataków siłowych osoba atakująca podejmuje próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont, aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Gdy zostanie znaleziony, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywanie alert jest wyzwalany, gdy wystąpiło wiele błędów uwierzytelniania przy użyciu protokołu Kerberos lub NTLM, może to być albo poziomie wprowadzaj w małej grupie, haseł dla wielu użytkowników; lub w pionie o dużej haseł na tylko kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji. Minimalny okres wywoła alertu jest jeden tydzień.

**Badanie**

1.  Kliknij przycisk **Pobierz szczegóły** Aby wyświetlić pełne informacje w arkuszu kalkulacyjnym programu Excel. Można uzyskać następujące informacje: 
   -    Lista zaatakowane konta
   -    Lista odgadnięte konta, w której próby logowania zakończone z pomyślnym uwierzytelnieniu
   -    Jeśli prób uwierzytelnienia zostały wykonane przy użyciu metod NTLM, zostaną wyświetlone odpowiednie zdarzenie działania 
   -    Jeśli prób uwierzytelnienia zostały wykonane przy użyciu protokołu Kerberos, zostanie wyświetlony działań w odpowiednich sieci

2.  Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, co się stało z momentu te próby, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![Znaczek usługi Windows Defender ATP](./media/wd-badge.png) Aby badać na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu. 

3.  Jeśli uwierzytelnianie zostało wykonane przy użyciu metod NTLM, a zobaczysz, że występuje alert o wiele razy, a Brak dostępnej wystarczającej ilości informacji o serwerze, na którym maszyna źródłowa próbował uzyskać dostęp do, należy włączyć **inspekcji NTLM** na kontrolery domeny zaangażowane. Aby to zrobić, należy włączyć zdarzenia 8004. To zdarzenie uwierzytelniania NTLM, które zawiera informacje dotyczące komputera źródłowego, konto użytkownika i **serwera** której maszyna źródłowa próbowano uzyskać dostęp. Gdy dowiesz się, które serwer wysłał weryfikacji za pomocą uwierzytelniania, serwer powinien być sprawdzony, sprawdzając jego zdarzenia, takie jak 4624, aby lepiej zrozumieć proces uwierzytelniania. 

**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.

## <a name="suspicious-communication-over-dns---preview"></a>Podejrzane komunikacji za pośrednictwem DNS — wersja zapoznawcza

**Opis**

Protokół DNS w większości organizacji zwykle nie jest monitorowane i rzadko zablokowane przed złośliwymi działaniami. Dzięki temu osoba atakująca na zainfekowanym komputerze nadużywają protokołu DNS. Złośliwy komunikacji za pośrednictwem DNS może służyć do wykradanie danych, poleceń i kontroli i/lub uniknięcia ograniczenia sieci firmowej.

**Badanie**
> [!NOTE]
> *Podejrzane komunikacji za pośrednictwem DNS* alerty zabezpieczeń listy podejrzanych domen. Nowe domenach lub domenach ostatnio dodane, które nie są jeszcze znane lub rozpoznawane przez narzędzia Azure ATP, ale nie są znany lub w ramach danej organizacji może zostać zamknięty. 


1.  Niektóre firmy uzasadnione używają DNS do regularnego komunikacji. Sprawdź, czy domena zarejestrowane kwerendy należy do zaufanego źródła, takich jak dostawcy programu antywirusowego. Jeśli domena jest znane i zaufane i zapytania DNS są dozwolone, alert może zostać zamknięty, a domena może być [wykluczone](excluding-entities-from-detections.md) z następnych alertów. 
3.   Jeśli domena zarejestrowane zapytanie nie jest zaufany, zidentyfikuj proces tworzenia żądania na maszynie źródłowej. Użyj [Monitor procesu](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) do pomocy dotyczącej tego zadania.
4.  Określa, kiedy rozpocząć podejrzanego działania? Zostały dowolne nowe programy wdrożony lub zainstalowany (AV?) w organizacji Czy istnieją inne alerty z tym samym czasie?
5.  Kliknij komputer źródłowy dostępu do swojej strony profilu. Sprawdź, co się stało z momentu zapytanie DNS, wyszukiwanie nietypowych działań, takich jak który zostało zarejestrowane w i które zostały użyte zasoby. Jeśli integracja usługi Windows Defender ATP jest już włączony, kliknij wskaźnik usługi Windows Defender ATP ![Znaczek usługi Windows Defender ATP](./media/wd-badge.png) Aby badać na maszynie. Za pomocą usługi Windows Defender ATP możesz zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu.

**Korygowanie** Jeśli domeny zarejestrowane zapytanie nie jest zaufany po badania, firma Microsoft zaleca blokuje domenę docelową, aby uniknąć całej komunikacji w przyszłości. 

## <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Podwyższanie poziomu kontrolera domeny podejrzane (potencjalny atak DCShadow)

**Opis**

Atak w tle (DCShadow) kontroler domeny jest atakiem przeznaczone do modyfikowania obiektów katalogu przy użyciu złośliwa replikacja. Atak można wykonać z dowolnego komputera, tworząc nieautoryzowany kontrolera domeny przy użyciu procesu replikacji.
 
DCShadow używa RPC i protokołu LDAP na:
1. Zarejestruj konto komputera jako kontrolera domeny (przy użyciu uprawnień administratora domeny), a
2. Wykonaj replikację (z wykorzystaniem udzielone prawa replikacji) za pośrednictwem interfejsu DRSUAPI i wysłać zmiany do obiektów katalogu.
 
W tym wykrywanie alert jest wyzwalany, gdy komputer w sieci próbuje zarejestrować się jako kontroler domeny nieautoryzowany. 

**Badanie**
 
1. Jest to komputer w pytanie kontrolera domeny? Na przykład nowo wypromowaną kontroler domeny, który ma problemy z replikacją. Jeśli tak, **Zamknij** podejrzanych działań.
2. Dany komputer powinien być replikowanie danych z usługi Active Directory? Na przykład, program Azure AD Connect. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.
3. Kliknij komputer źródłowy lub konta, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej replikacji, wyszukiwanie nietypowych działań, takich jak: kto został zalogowany do określonych zasobów i co to jest komputer system operacyjny?
   1. Czy wszyscy użytkownicy, którzy są zalogowani do komputera powinien zalogowanie do niej? Co to są ich uprawnienia? Czy mają uprawnienia do podwyższenia poziomu serwera do kontrolera domeny (są one Administratorzy domeny)?
   2. Użytkownicy mają dostęp do tych zasobów?
   3. Czy komputer jest uruchomiony system operacyjny Windows Server (lub systemu Windows/Linux)? Machine-serwer nie powinien replikacji danych.
Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![znaczek usługi Windows Defender ATP](./media/wd-badge.png) do dalszego zbadania problemu na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu.

4. Przyjrzyj się Podgląd zdarzeń, aby zobaczyć [zdarzenia usługi Active Directory, które rejestruje w dzienniku usługi katalogowej](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)). Dziennik umożliwia monitorowanie zmian w usłudze Active Directory. Domyślnie usługi Active Directory tylko rekordy zdarzeń z powodu krytycznego błędu, ale jeśli ten alert zostanie wyświetlony ponownie, należy włączyć tej inspekcji na kontrolerze domeny odpowiednie do dalszych poszukiwań.

**Korygowanie**

Sprawdź, kto w organizacji ma następujące uprawnienia: 
- Replikuj zmiany katalogu 
- Replikuj wszystkie zmiany w katalogu 
 
 
Aby uzyskać więcej informacji, zobacz [uprawnienia Grant Active Directory Domain Services dla synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). 

Możesz wykorzystać [skaner list ACL usługi AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub utworzyć skrypt programu Windows PowerShell, aby określić, kto w domenie ma te uprawnienia.
 
> [!NOTE]
> Wykrywanie podwyższania poziomu (potencjalny atak DCShadow) kontrolera domeny podejrzane są obsługiwane przez tylko czujników zaawansowanej ochrony przed zagrożeniami. 

## <a name="suspicious-modification-of-sensitive-groups"></a>Podejrzane modyfikacja wrażliwych grup

**Opis**

Osoby atakujące dodać użytkowników do grup o wysokim poziomie uprawnień. To zrobią, aby uzyskać dostęp do większej ilości zasobów i uzyskanie stałego dostępu. Ta metoda wykrywania polega na profilowaniu działania modyfikacja grupy użytkowników oraz alerty, gdy pojawia się nietypowy dodatku wrażliwych grup. Profilowanie stale odbywa się przez narzędzia Azure ATP. Minimalny okres wywoła alertu jest jeden miesiąc na każdym kontrolerze domeny.

Aby uzyskać pełną definicję wrażliwych grup w usłudze Azure ATP, zobacz [Praca z kontami poufnymi](sensitive-accounts.md).


Ta metoda wykrywania polega na [zdarzenia poddawane inspekcji na kontrolerach domeny](configure-event-collection.md).
Aby upewnić się, że domeny kontrolerów inspekcji wymaganych zdarzeń.

**Badanie**

1. Modyfikacja grupy jest uzasadnione? </br>Modyfikacje uzasadnione grupy, które rzadko występują i nie zostały rozpoznane jako "normal", może spowodować alertów, co mogłoby być uważane za niegroźnie prawdziwie dodatni.

2. Jeśli dodano obiekt był konto użytkownika, sprawdź akcje, które konto użytkownika miało po ich dodaniu do grupy administratorów. Przejdź do strony użytkownika narzędzia Azure ATP, aby uzyskać dodatkowy kontekst. Pojawili się tam inne podejrzanych działań skojarzonych z kontem, przed lub po dodaniu miała miejsce? Pobierz **modyfikacji wrażliwych grup** raportu, aby zobaczyć, jakie były inne zmiany dokonane i przez kogo, w tym samym okresie czasu.

**Korygowanie**

Zminimalizowanie liczby użytkowników, które mają uprawnienia do modyfikowania grup poufnych.

Konfigurowanie [Privileged Access Management dla usługi Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) jeśli ma to zastosowanie.



## <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Podejrzana replikacja żądania (potencjalny atak DCShadow) 

**Opis** 

Replikacja usługi Active Directory to proces, za pomocą którego zmiany wprowadzone na jednym kontrolerze domeny są synchronizowane z innymi kontrolerami domeny. Biorąc pod uwagę niezbędne uprawnienia, osoby atakujące można przyznać uprawnienia dla konta komputera umożliwiające podszyć się pod kontroler domeny. Osoby atakujące będzie Dokładamy wszelkich starań zainicjować żądanie złośliwa replikacja, umożliwiając im do modyfikowania obiektów usługi Active Directory na kontrolerze domeny oryginalnego osoby atakujące mogą dawać trwałości w domenie.
W tym wykrywanie alert jest wyzwalany, gdy żądanie podejrzana replikacja jest generowane przy użyciu kontrolera domeny oryginalny, chronione przez usługi Azure ATP. To zachowanie jest wskaźnikiem technik stosowanych w atakach w tle kontrolera domeny.

**Badanie** 
 
1. Jest to komputer w pytanie kontrolera domeny? Na przykład nowo wypromowaną kontroler domeny, który ma problemy z replikacją. Jeśli tak, **Zamknij** podejrzanych działań.
2. Dany komputer powinien być replikowanie danych z usługi Active Directory? Na przykład, program Azure AD Connect. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.
3. Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, co się stało **zbliżonym do momentu** replikacji, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby zostały użyte i komputer system operacyjny?

   1.  Czy wszyscy użytkownicy, którzy są zalogowani do komputera powinien zalogowanie do niej? Co to są ich uprawnienia? Czy mają uprawnienia do wykonywać replikacje (są one Administratorzy domeny)
   2.  Użytkownicy mają dostęp do tych zasobów?
   3. Czy komputer jest uruchomiony system operacyjny Windows Server (lub systemu Windows/Linux)? Machine-serwer nie powinien replikacji danych.
Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![znaczek usługi Windows Defender ATP](./media/wd-badge.png) do dalszego zbadania problemu na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu.
1. Przyjrzyj się Podgląd zdarzeń, aby zobaczyć [zdarzenia usługi Active Directory, które rejestruje w dzienniku usługi katalogowej](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)). Dziennik umożliwia monitorowanie zmian w usłudze Active Directory. Domyślnie usługi Active Directory tylko rekordy zdarzeń z powodu krytycznego błędu, ale jeśli ten alert zostanie wyświetlony ponownie, należy włączyć tej inspekcji na kontrolerze domeny odpowiednie do dalszych poszukiwań.

**Korygowanie**

Sprawdź, kto w organizacji ma następujące uprawnienia: 
- Replikuj zmiany katalogu 
- Replikuj wszystkie zmiany w katalogu 

Aby to zrobić, można wykorzystać [skaner list ACL usługi AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub utworzyć skrypt programu Windows PowerShell, aby określić, kto w domenie ma te uprawnienia.

> [!NOTE]
> Podejrzana replikacja żądania (potencjalny atak DCShadow) wykrywania są obsługiwane przez tylko czujników zaawansowanej ochrony przed zagrożeniami. 


## <a name="suspicious-service-creation"></a>Podejrzanie utworzenie usługi

**Opis**

Podejrzane usługi został utworzony na kontrolerze domeny w Twojej organizacji. Ten alert opiera się na zdarzenie 7045 w celu identyfikacji tego podejrzanych działań. 

**Badanie**

1. Jeśli dany komputer jest stacji roboczej administratora lub na komputerze, na którym członków zespołu IT i usługi konta wykonywania zadań administracyjnych, może to być wynik fałszywie dodatni i może być konieczne **Pomiń** alertu i dodaj go do Listy wykluczeń, jeśli to konieczne.

2. Element, który rozpoznaje na tym komputerze jest usługa?

 - Jest **konta** danego mogła zainstalować tę usługę?

 - Jeśli odpowiedzi na oba pytania *tak*, następnie **Zamknij** alertu, albo dodaj go do listy wykluczeń.

3. Jeśli odpowiedzi na pytania albo *nie*, a następnie należy to uwzględnić prawdziwie dodatni.

**Korygowanie**

- Implementowanie mniej uprzywilejowanego dostępu do domeny na maszynach w celu zezwalanie wyłącznie określonym użytkownikom uprawnienia do tworzenia nowych usług.


## Podejrzane połączenia sieci VPN <a name="suspicious-vpn-detection"></a>

**Opis**

Narzędzie Azure ATP uczy się zachowania jednostek dla użytkowników połączeń sieci VPN w przewijania okresie jednego miesiąca. 

Model zachowanie sieci VPN jest oparty na następujących działaniach: maszyny użytkowników zalogowało się na komputerze i lokalizacje użytkowników, Połącz z. 

Alert zostanie otwarty po odchylenie od zachowanie użytkowników, w oparciu o algorytmu uczenia maszynowego.

**Badanie**

1.  Użytkownik powinien wykonywać te operacje?
2.  Należy wziąć pod uwagę następujące przypadki jako potencjalnych fałszywych alarmów: użytkownik, który zmienił jego lokalizacji, użytkownik, który jest w podróży i połączyć się z nowego urządzenia.

**Korygowanie**

1.  Należy wziąć pod uwagę, zresetowanie hasła tego użytkownika. Zapobiega to tworzenia nowych połączeń sieci VPN przy użyciu poświadczeń stare osoba atakująca.
2.  Należy wziąć pod uwagę blokowania tego użytkownika na połączenie za pośrednictwem sieci VPN.

## <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu


**Opis**

Osoby atakujące wykorzystywać narzędzia stosujące różnych protokołów (SMB, protokołu Kerberos, NTLM) w sposób niestandardowy. Podczas tego rodzaju ruch sieciowy jest akceptowany przez Windows bez ostrzeżeń, narzędzia Azure ATP jest w stanie rozpoznać potencjalne wyrządzenia. To zachowanie jest wskaźnikiem technik, takich jak Wymuszanie protokołu-Pass--Hash i atak, a także luki w zabezpieczeniach posługują się zaawansowane oprogramowanie wymuszające okup, na przykład WannaCry.

**Badanie**

Identyfikowanie protokół, który jest nietypowy — z osi czasu podejrzanych działań, kliknij pozycję podejrzanego działania, aby uzyskać dostęp do ich strony szczegółów; Protokół, który pojawia się nad strzałkę: Kerberos lub NTLM.

- **Protokół Kerberos**: ten zostanie często wyzwolony, jeśli stosowanie metod hakerskich narzędzia, takie jak używany program Mimikatz, potencjalnie wykonując atak Overpass--Hash. Sprawdź, czy komputer źródłowy jest uruchomiona aplikacja, która implementuje własnego stosu protokołu Kerberos, nie zgodnie z RFC protokołu Kerberos. Jeśli tak jest rzeczywiście, to wynik niegroźny prawdziwie dodatni i możesz **Zamknij** alertu. Jeśli alert, utrzymuje jest uruchomiony i nadal jest tak, możesz to zrobić **Pomiń** alertu.

- **NTLM**: może być WannaCry lub narzędzi, takich jak Metasploit, Medusa i Hydra.  

Aby ustalić, czy jest to atak WannaCry, wykonaj następujące czynności:

1. Sprawdź, czy komputer źródłowy działa narzędzie ataków, takich jak Metasploit, Medusa lub Hydra.

2. Jeśli nie zostaną znalezione żadne narzędzia ataku, sprawdź, czy komputer źródłowy jest uruchomiona aplikacja, która implementuje stos protokołu NTLM lub SMB.

3. Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej alertu wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. Włączenie integracji usługi Windows Defender ATP kliknij wskaźnik usługi Windows Defender ATP ![WD wskaźnika](./media/wd-badge.png) Aby badać na maszynie. W usłudze Windows Defender ATP można zobaczyć, które procesy i alerty wystąpił zbliżonym do momentu alertu.



**Korygowanie**

Stosowanie poprawek do wszystkich maszyn, szczególnie stosowania aktualizacji zabezpieczeń.

1. [Wyłącz SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Usuń WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi może odszyfrować danych w ręce niektóre programy ransom, ale tylko wtedy, jeśli użytkownik został ponownie uruchomiony lub nie wyłączony komputer. Aby uzyskać więcej informacji, zobacz [chcesz krzykiem przed oprogramowaniem wymuszającym Okup](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


> [!NOTE]
> Aby wyłączyć alert zabezpieczeń, skontaktuj się z działem pomocy technicznej.


## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
