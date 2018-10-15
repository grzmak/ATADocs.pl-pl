---
title: Przewodnik usługi ATA dotyczący podejrzanych działań | Microsoft Docs
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: be1a699ffd1ab0925df43910aec7f8166d4e423d
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315850"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Przewodnik po podejrzanych działaniach zaawansowanej analizy zagrożeń

Następujące odpowiednie badania wszelkich podejrzanych działań, mogą być klasyfikowane jako:

-   **Prawdziwie dodatni**: złośliwa Akcja wykryta przez usługę ATA.

-   **Wynik niegroźny prawdziwie dodatni**: Akcja wykryta przez usługę ATA jest prawdziwe, ale nie złośliwego test penetracyjny.

-   **Wynik fałszywie dodatni**: alarm wartość false, co oznacza działania nie się zdarzyć.

Aby uzyskać więcej informacji na temat sposobu pracy z alertów usługi ATA, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

Pytania lub opinie, skontaktuj się z zespołem usługi ATA pod adresem [ ATAEval@microsoft.com ](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Nietypowa modyfikacja grupy poufnej


**Opis**

Osoby atakujące dodać użytkowników do grup o wysokim poziomie uprawnień. Mogą to zrobić na uzyskanie dostępu do większej ilości zasobów i uzyskanie stałego dostępu. Wykrywanie zależą od tego, profilowanie działania modyfikacja grupy użytkowników i alerty, gdy pojawia się nietypowy dodatku wrażliwych grup. Profilowanie stale odbywa się przez usługę ATA. Minimalny okres wywoła alertu jest jeden miesiąc na kontrolerze domeny.

Aby uzyskać pełną definicję wrażliwych grup w usłudze ATA, zobacz [Praca z konsolą usługi ATA](working-with-ata-console.md#sensitive-groups).


Ta metoda wykrywania polega na [zdarzenia poddawane inspekcji na kontrolerach domeny](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Aby upewnić się, wymagane zdarzenia inspekcji z kontrolerami domeny, należy użyć narzędzia, do którego odwołuje się [ATA inspekcji (AuditPol, zaawansowane wymuszania ustawień inspekcji, odnajdowanie usługi bramy uproszczonej)](https://aka.ms/ataauditingblog).

**Badanie**

1. Modyfikacja grupy jest uzasadnione? </br>Modyfikacje uzasadnione grupy, które rzadko występują i nie zostały rozpoznane jako "normal", może spowodować alertów, co mogłoby być uważane za niegroźnie prawdziwie dodatni.

2. Jeśli dodano obiekt był konto użytkownika, sprawdź akcje, które konto użytkownika miało po ich dodaniu do grupy administratorów. Przejdź do strony użytkownika w usłudze ATA, aby uzyskać dodatkowy kontekst. Pojawili się tam inne podejrzanych działań skojarzonych z kontem, przed lub po dodaniu miała miejsce? Pobierz **modyfikacji wrażliwych grup** raportu, aby zobaczyć, jakie były inne zmiany dokonane i przez kogo, w tym samym okresie czasu.

**Korygowanie**

Zminimalizowanie liczby użytkowników, które mają uprawnienia do modyfikowania grup poufnych.

Konfigurowanie [Privileged Access Management dla usługi Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) jeśli ma to zastosowanie.

## <a name="broken-trust-between-computers-and-domain"></a>Zerwanie relacji zaufania między komputerami i domeny

> [!NOTE]
> Zerwanie relacji zaufania między komputerami i domeny alertów została zakończona i jest wyświetlany tylko w wersjach usługi ATA przed 1.9.

**Opis**

Zerwanie relacji zaufania oznacza, że wymagania dotyczące zabezpieczeń usługi Active Directory, może nie być obowiązuje dla tych komputerów. To jest uważany za punkt odniesienia zabezpieczeń i błąd zgodności oraz atrakcyjny cel dla osób atakujących. W tym wykrywanie alert jest wyzwalany, jeśli więcej niż pięć niepowodzeń uwierzytelniania Kerberos są widoczne konta komputera w ciągu 24 godzin.

**Badanie**

Jest komputer badana, dzięki czemu użytkownicy domeny do logowania się? 
- Jeśli tak, możesz zignorować ten komputer w kroki korygowania.

**Korygowanie**

Przyłącz komputer do domeny, jeśli to konieczne, lub zresetuj hasło maszyny.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Atak siłowy przy użyciu prostego powiązania LDAP

**Opis**

>[!NOTE]
> Główna różnica między **podejrzane błędy uwierzytelniania** i wykrywanie, w tym wykrywania usługi ATA można określić, czy inne hasła były używane.

W ramach ataków siłowych osoba atakująca podejmuje próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont, aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Gdy zostanie znaleziony, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywanie alert jest wyzwalany, gdy usługa ATA wykrywa ogromną liczbę uwierzytelnień prostego powiązania. Może to być albo *poziomo* wprowadzaj w małej grupie haseł dla wielu użytkowników; lub *pionowo "* z dużym zestawem haseł na kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji.

**Badanie**

1. Jeśli zaangażowanych jest wiele kont, kliknij przycisk **Pobierz szczegóły** do wyświetlania listy w arkuszu kalkulacyjnym programu Excel.

2. Kliknij alert, aby przejść do jego dedykowaną stronę. Sprawdź, czy prób logowania wszystkie zakończone z pomyślnym uwierzytelnieniu. Próby pojawiał się jako **odgadnięte konta** po prawej stronie grafikę informacyjną. Jeśli tak, czy którakolwiek z **odgadnięte konta** normalnie używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

3. W przypadku nie **odgadnięte konta**, czy którakolwiek z **zaatakowane konta** normalnie używane z komputera źródłowego? Jeśli tak, **Pomiń** podejrzanych działań.

**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.

## <a name="encryption-downgrade-activity"></a>Działanie obniżenia poziomu szyfrowania

**Opis**

Obniżenie poziomu szyfrowania jest metodą osłabienia protokołu Kerberos przez obniżenie poziomu szyfrowania różnych pól protokołu, które zwykle są szyfrowane za pomocą najwyższego poziomu szyfrowania. Polem zaszyfrowanych obniżony poziom może być łatwiejsze docelowej do trybu offline ataków siłowych. Korzystanie z różnych metod ataków słabe cyfry szyfrowania protokołu Kerberos. W tym wykrywanie uczy się typów szyfrowania protokołu Kerberos, które są używane przez komputery i użytkownicy usługi ATA i ostrzega, gdy jest słabsza szyfrowania użyte w tym: (1) jest niczym niezwykłym, komputer źródłowy i/lub użytkownika. a (2) dopasowuje znane techniki ataku.

Istnieją trzy typy wykrywania:

1.  Złośliwe oprogramowanie Skeleton Key — to złośliwe oprogramowanie, które jest uruchamiane na kontrolerach domeny i umożliwia uwierzytelnianie domeny przy użyciu dowolnego konta bez znajomości hasła. To złośliwe oprogramowanie często używa słabszych algorytmów szyfrowania w celu wyznaczania wartości skrótu hasła użytkownika na kontrolerze domeny. W tym wykrywanie metody szyfrowania wiadomości KRB_ERR z kontrolera domeny do konta, pytanie o bilet został obniżony w porównaniu do uprzednio zapamiętane zachowanie.

2.  Bilet Golden — [bilet uwierzytelniania Golden Ticket](#golden-ticket) alertu, metodę szyfrowania dla pola TGT w żądaniu TGS_REQ (żądanie obsługi) komunikatu z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie. To nie jest oparty na anomalii czasu (tak jak inne wykrywania bilet uwierzytelniania Golden Ticket). Ponadto nie było żadnych żądaniu uwierzytelnienia protokołu Kerberos, skojarzone z poprzedniego żądania obsługi, wykrytych przez usługę ATA.

3.  Overpass--Hash — osoba atakująca można użyć słabe skradzionego skrótu, aby można było utworzyć bilet silne z żądaniem protokołu Kerberos AS. W tym wykrywanie AS_REQ typ szyfrowania wiadomości z komputera źródłowego został obniżony w porównaniu do uprzednio zapamiętane zachowanie (oznacza to, że komputer został przy użyciu szyfrowania AES).

**Badanie**

Najpierw sprawdź opis alertu, aby dowiedzieć się, które z powyższych trzech typów wykrywania są zajmujących. Aby uzyskać więcej informacji Pobierz arkusz kalkulacyjny programu Excel.
1.  Złośliwe oprogramowanie Skeleton Key — możesz sprawdzić, jeśli złośliwe oprogramowanie Skeleton Key ma wpływ na kontrolerach domeny przy użyciu [skanera przygotowanego przez zespół usługi ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Jeśli skaner wykryje złośliwe oprogramowanie na 1 lub więcej kontrolerów domeny, jest prawdziwie dodatni.
2.  Bilet uwierzytelniania Golden Ticket — w arkuszu kalkulacyjnym programu Excel, przejdź do **działań w sieci** kartę. Zobaczysz, że odpowiednie pole starszej jest **żądania typ szyfrowania biletu**, i **komputera źródłowego obsługiwane typy szyfrowania** Wyświetla silniejszych metod szyfrowania.
  a.    Sprawdź komputer źródłowy i konta lub w przypadku wielu źródłowych konta komputerów i sprawdzenia, czy ich coś mają wspólne, (na przykład wszystkie marketingu personelu użyj konkretnej aplikacji, które mogą być przyczyną alertu). Istnieją przypadki, w których niestandardową aplikację, która jest rzadko używana jest uwierzytelniany przy użyciu niższe szyfrowania szyfrowanie. Sprawdź, czy istnieją niestandardowe aplikacje na komputerze źródłowym. Jeśli tak, prawdopodobnie jest to wynik niegroźny prawdziwie dodatni i możesz **Pomiń** go.
  b.    Wyboru zasobu uzyskiwał dostęp do tych biletów, w przypadku jeden zasób, z których korzystają wszystkie zweryfikuje go, upewnij się, że jest prawidłowy zasób, które one powinien uzyskać dostęp. Ponadto sprawdź, czy zasób docelowy obsługuje metody silne szyfrowanie. Możesz to sprawdzić w usłudze Active Directory, sprawdzając atrybut `msDS-SupportedEncryptionTypes`, zasobów konta usługi.
3.  Overpass--Hash — w arkuszu kalkulacyjnym programu Excel, przejdź do **działań w sieci** kartę. Zobaczysz, że odpowiednie pole starszej jest **szyfrowany typ szyfrowania sygnatura czasowa** i **komputera źródłowego obsługiwane typy szyfrowania** zawiera silniejszych metod szyfrowania.
  a.    Istnieją przypadki, w których ten alert może być wyzwalany, gdy użytkownicy logują się przy użyciu kart inteligentnych, jeśli konfiguracja karty inteligentnej zostało niedawno zmienione. Sprawdź, czy wystąpiły zmiany następująco dla konta związane. Jeśli tak, prawdopodobnie jest to wynik niegroźny prawdziwie dodatni i możesz **Pomiń** go.
  b.    Wyboru zasobu uzyskiwał dostęp do tych biletów, w przypadku jeden zasób, z których korzystają wszystkie zweryfikuje go, upewnij się, że jest prawidłowy zasób, które one powinien uzyskać dostęp. Ponadto sprawdź, czy zasób docelowy obsługuje metody silne szyfrowanie. Możesz to sprawdzić w usłudze Active Directory, sprawdzając atrybut `msDS-SupportedEncryptionTypes`, zasobów konta usługi.

**Korygowanie**

1.  Szkielet klucza — Usuń złośliwe oprogramowanie. Aby uzyskać więcej informacji, zobacz [analizy złośliwe oprogramowanie Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Uwierzytelniania Golden Ticket — postępuj zgodnie z instrukcjami [bilet uwierzytelniania Golden Ticket](#golden-ticket) podejrzanych działań.   
    Implementuje są również, tworząc bilet uwierzytelniania Golden Ticket wymagają uprawnień administratora domeny, dlatego [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).

3.  Overpass--Hash — Jeśli zaangażowane konto nie jest uwzględniana wielkość liter, następnie zresetuj hasło tego konta. Zapobiega to osoba atakująca tworzenia nowych bilety protokołu Kerberos na podstawie skrótu hasła, mimo że nadal można używać istniejących biletów, dopóki nie wygasną. Jeśli jest kontem wrażliwym, należy rozważyć resetowania konta krbtgt w DOMENIE, dwa razy, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Zobacz też przy użyciu [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Ponieważ jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania z [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).


## <a name="honeytoken-activity"></a>Działanie wystawionego jako przynęta


**Opis**

Konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu identyfikacji i śledzenia złośliwych działań, które obejmuje te konta. Konta wystawione jako przynęta powinien pozostać nieużywane, mając atrakcyjny nazwę do nakłonienia osoby atakujące (na przykład administrator SQL). Wszystkie działania z nich może wskazywać na złośliwe działanie.

Aby uzyskać więcej informacji na temat konta wystawione jako przynęta, zobacz [Instalowanie usługi ATA — krok 7](install-ata-step7.md).

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

Sprawdź, czy skrót używana na komputerze od użytkownika docelowego, lub regularnie używa? Jeśli tak, ten alert jest fałszywie dodatni, jeśli nie, prawdopodobnie jest prawdziwie dodatni.

**Korygowanie**

1. Jeśli konto zaangażowane nie jest wielkość liter, zresetować hasło tego konta. Resetowanie hasła uniemożliwia tworzenie nowych bilety protokołu Kerberos z skrót hasła osoba atakująca. Istniejące bilety są nadal można używać, dopóki nie wygasną. 

2. Jeśli zaangażowane konto jest poufne, należy wziąć pod uwagę dwa razy, resetowanie konta krbtgt w DOMENIE, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwukrotnie unieważnia wszystkie bilety systemu Kerberos domeny, dlatego należy planować wokół wpływ przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), także odwoływać się do korzystania z [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Zazwyczaj jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania z [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Kradzież tożsamości za pomocą ataku typu Pass--Ticket

**Opis**

Pass--Ticket to technika ruchu poprzecznego, w którym osoby atakujące dokonują kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera, na podstawie kradzieży biletu. W tym wykrywanie biletu protokołu Kerberos występuje używanych na różnych komputerach (co najmniej dwa).

**Badanie**

1. Kliknij przycisk **Pobierz szczegóły** przycisk, aby wyświetlić pełną listę adresów IP, które są zaangażowani. Czy adres IP jednego lub obu komputerów częścią podsieci przydzielony z za małego rozmiaru puli DHCP, na przykład, sieci VPN lub Wi-Fi? Adres IP jest udostępniony? Na przykład przez urządzenie NAT? Jeśli odpowiedzi na dowolne z tych pytań jest twierdząca, ten alert jest fałszywie dodatni.

2. Czy istnieje niestandardową aplikację, która przekazuje bilety w imieniu użytkowników? Jeśli tak, to wynik niegroźny prawdziwie dodatni.

**Korygowanie**

1. Jeśli konto zaangażowane nie jest wielkość liter, następnie zresetuj hasło tego konta. Hasło powtórzona uniemożliwia tworzenie nowych bilety protokołu Kerberos z skrót hasła osoba atakująca. Wszystkie istniejące bilety nadal można używać, dopóki nie wygasł.  

2. Jeśli jest kontem wrażliwym, należy rozważyć resetowania konta krbtgt w DOMENIE, dwa razy, tak jak podejrzane działanie biletu uwierzytelniania Golden Ticket. Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem. Zobacz wskazówki zawarte w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), zobacz też przy użyciu [resetowanie haseł/kluczy narzędzie konta krbtgt w DOMENIE](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Ponieważ jest to technika ruchu poprzecznego, stosuj najlepsze rozwiązania w [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).

## Protokół Kerberos Golden Ticket<a name="golden-ticket"></a>

**Opis**

Osoby atakujące przy użyciu uprawnień administratora domeny może naruszyć Twoje [konta krbtgt w DOMENIE](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Osoby atakujące umożliwia utworzenie biletu Kerberos udzielania biletu (TGT), zapewniając autoryzacji do dowolnego zasobu konta krbtgt w DOMENIE. Na każdym dowolnego można ustawić czas wygaśnięcia biletu. To fałszywe biletu TGT jest nazywany "Złoty bilet" i umożliwia osoby atakujące w celu zapewnienia i utrzymania stały dostęp do sieci w sieci.

W tym wykrywanie alert jest wyzwalany, gdy Kerberos biletu udzielania biletu (TGT) jest używany dla więcej niż dozwolony czas dozwolone określonych w [maksymalny okres istnienia biletu użytkownika](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) zasady zabezpieczeń.

**Badanie**

1. Została każda zmiana ostatnio (w ciągu ostatnich kilku godzin), wprowadzone do **maksymalny okres istnienia biletu użytkownika** ustawienie w zasadach grupy? Jeśli tak, następnie **Zamknij** alertu (było to wynik fałszywie dodatni).

2. Brama usługi ATA jest zaangażowane w tym alercie maszynę wirtualną? Jeśli tak, on niedawno wychodzi z zapisanego stanu? Jeśli tak, następnie **Zamknij** ten alert.

3. Jeśli odpowiedź na powyższe pytania nie przyjęto założenie, jest to złośliwy.

**Korygowanie**

Zmień hasło biletu udzielania biletu protokołu Kerberos (KRBTGT) dwa razy, zgodnie z zaleceniami w [KRBTGT konta hasła resetowania skrypty teraz dostępna dla klientów](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/)przy użyciu [resetowania haseł kont KRBTGT/kluczy Narzędzie](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Resetowanie konta KRBTGT dwa razy powoduje unieważnienie wszystkich protokołu Kerberos, bilety w tej domenie, dlatego należy planować przedtem.  
Implementuje są również, tworząc bilet uwierzytelniania Golden Ticket wymagają uprawnień administratora domeny, dlatego [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).


## <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych

**Opis**

Interfejs API ochrony danych (DPAPI) umożliwia przez Windows bezpieczny sposób ochrony haseł, zapisane przez przeglądarek, zaszyfrowane pliki i innych poufnych danych. Kontrolery domeny przechowują zapasowy klucz główny, który może służyć do odszyfrowania wszystkich wpisów tajnych zaszyfrowanych przy użyciu interfejsu DPAPI na komputerach przyłączonych do domeny Windows. Osoby atakujące, można użyć klucza głównego do odszyfrowania wszystkich danych poufnych chroniony funkcją DPAPI na wszystkich komputerach przyłączonych do domeny.
W tym wykrywanie alert jest wyzwalany, gdy DPAPI służy do pobierania kopii zapasowej klucza głównego.

**Badanie**

1. Komputer źródłowy systemem zatwierdzonych organizacji, jest zaawansowane skaner zabezpieczeń w usłudze Active Directory?

2. Jeśli tak i jego powinna zawsze być tych czynności**Zamknij i Wyklucz** podejrzanych działań.

3. Jeśli tak i nie należy przeprowadzać tego ** zamknij podejrzanych działań.

**Korygowanie**

Aby korzystać z interfejsu DPAPI, osoba atakująca potrzebuje uprawnienia administratora domeny. Implementowanie [przekazać zalecenia wyznaczania wartości skrótu](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Złośliwa replikacja usług katalogowych


**Opis**

Replikacja usługi Active Directory to proces, za pomocą którego zmiany wprowadzone na jednym kontrolerze domeny są synchronizowane z innymi kontrolerami domeny. Biorąc pod uwagę niezbędne uprawnienia, atakujący może zainicjować żądanie replikacji, umożliwiając im danych przechowywanych w usłudze Active Directory, w tym skrótów haseł.

W tym wykrywanie alert jest wyzwalany, gdy żądanie replikacji jest inicjowane z komputera, który nie jest kontrolerem domeny.

**Badanie**

1.  Jest to komputer w pytanie kontrolera domeny? Na przykład nowo wypromowaną kontroler domeny, który ma problemy z replikacją. Jeśli tak, **Zamknij** podejrzanych działań. 
2.  Dany komputer powinien być replikowanie danych z usługi Active Directory? Na przykład, program Azure AD Connect. Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.
3.  Kliknij komputer źródłowy lub konta, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej replikacji, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. 


**Korygowanie**

Zweryfikuj następujące uprawnienia: 

- Replikuj zmiany katalogu   

- Replikuj wszystkie zmiany w katalogu  

Aby uzyskać więcej informacji, zobacz [uprawnienia Grant Active Directory Domain Services dla synchronizacji profilów w programie SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Możesz wykorzystać [skaner list ACL usługi AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub utworzyć skrypt programu Windows PowerShell, aby określić, kto w domenie ma te uprawnienia.

## <a name="massive-object-deletion"></a>Usunięcie dużej liczby obiektów

**Opis**

W niektórych scenariuszach osobom atakującym wykonywać typu odmowa usługi (DoS), a nie tylko kradzież informacji użytkownika. Usunięcie dużej liczby kont jest jedną z metod próby ataków DoS. 

W tym wykrywanie alert jest wyzwalany ilekroć więcej niż 5% wszystkich kont są usuwane. Wykrywanie wymaga dostępu do odczytu do kontenera usuniętych obiektów.  
Aby uzyskać informacje o konfigurowaniu uprawnień tylko do odczytu do kontenera usuniętego obiektu, zobacz **Zmienianie uprawnień do kontenera usuniętych obiektów** w [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Badanie**

Przejrzyj listę usuniętych kont i określ, czy wzorzec lub uzasadnienie biznesowe, która wyrównuje usunięcia na dużą skalę.

**Korygowanie**

Usuń uprawnienia użytkowników, którzy mogą usuwać konta w usłudze Active Directory. Aby uzyskać więcej informacji, zobacz [wyświetlanie lub ustawianie uprawnień do obiektu katalogu](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Eskalacja uprawnień przy użyciu sfałszowanych danych autoryzacji

**Opis**

Znane luki w zabezpieczeniach w starszych wersjach systemu Windows Server umożliwiają osobom atakującym manipulację certyfikat atrybutu uprzywilejowanego (PAC). Certyfikat PAC jest polem w bilecie protokołu Kerberos, która zawiera dane autoryzacji użytkownika (w usłudze Active Directory jest członkostwo w grupie) oraz udziela osobom atakującym dodatkowych uprawnień.

**Badanie**

1. Kliknij alert, aby uzyskać dostęp do strony szczegółów.

2. Jest komputerem docelowym (w obszarze **ACCESSED** kolumny) poprawiono MS14-068 (kontroler domeny) lub MS11-013 (serwer)? Jeśli tak, **Zamknij** podejrzanych działań (jest to wynik fałszywie dodatni).

3. Jeśli komputer docelowy nie jest zainstalowane odpowiednie poprawki, czy komputer źródłowy działa (w obszarze **FROM** kolumny) systemu operacyjnego/aplikacja modyfikują certyfikat PAC? Jeśli tak, **Pomiń** podejrzanych działań (jest to wynik niegroźny prawdziwie dodatni).

4. Jeśli odpowiedź na dwa pytania Wstecz nie przyjęto założenie, to działanie jest złośliwy.

**Korygowanie**

Upewnij się, że na wszystkich kontrolerach domen z systemami operacyjnymi starszymi niż system Windows Server 2012 R2 zainstalowano poprawkę [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege), a wszystkie serwery członkowskie i kontrolery domen do wersji 2012 R2 mają zainstalowaną poprawkę KB2496930. Aby uzyskać więcej informacji, zobacz [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) i [Forged PAC (Sfałszowany element PAC)](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Rekonesans przy użyciu wyliczania kont

**Opis**

W Rekonesans wyliczenie konta osoba atakująca używa słownik zawierający tysiące nazwy użytkowników lub narzędzi, takich jak KrbGuess próby odgadnięcia nazw użytkowników w domenie. Osoba atakująca sprawia, że żądania protokołu Kerberos, aby można było, spróbuj znaleźć prawidłowej nazwy użytkownika w domenie przy użyciu tych nazw. Jeśli wynik pomyślnie Określa nazwę użytkownika, osoba atakująca, zostanie wyświetlony błąd protokołu Kerberos **wstępnego uwierzytelniania wymagany** zamiast **nieznanego podmiotu zabezpieczeń**. 

W tym wykrywania usługa ATA może wykryć, skąd pochodzą ataku, całkowita liczba prób odgadnięcia i ile zostały dopasowane. W przypadku zbyt wielu użytkownikom nieznany, usługa ATA wykrywa ją jako podejrzane działanie. 

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów. 

2. Należy tej maszyny hosta zapytania do kontrolera domeny, do tego, czy istnieją konta (np. serwerów Exchange)? <br></br>
Czy istnieje, skryptu lub aplikacji uruchomionej na hoście, który można wygenerować ten problem? <br></br>
Jeśli odpowiedź na jedną z tych pytań jest twierdząca, **Zamknij** podejrzanych działań (jest to wynik niegroźny prawdziwie dodatni) i Wyklucz, który hostował na poziomie podejrzanego działania.

3. Pobierz szczegóły alertu w arkuszu kalkulacyjnym programu Excel, aby wygodnie lista prób konta, podzielone na istniejące i nieistniejące konta. Jeśli przyjrzymy się arkusza nieistniejące konta, w arkuszu kalkulacyjnym i kont wygląda znajomo, mogą być wyłączone konta lub pracowników, którzy opuścił firmę. W takich przypadkach jest mało prawdopodobne, że próba pochodzi ze słownika. Najbardziej prawdopodobne jest, aplikacji lub skryptu, który jest sprawdzanie, które konta nadal istnieć w usłudze Active Directory, co oznacza, że wynik niegroźny prawdziwie dodatni.

3. W przypadku większości nieznane nazwy wszystkich prób odgadnięcia pasowało istniejącymi nazwami kont w usłudze Active Directory? Jeśli nie ma żadnych dopasowań, próba została przełączona, ale należy zwrócić uwagę na alert, aby wyświetlić, jeśli jest aktualizowana wraz z upływem czasu.

4. Jeśli dowolny wynik próbuje dopasować istniejących nazw kont, osoba atakująca zna istnienia konta w danym środowisku i mogą próbować użyć ataków siłowych można uzyskiwać dostęp do domeny przy użyciu nazwy odnalezionych użytkowników. Sprawdź nazwy odgadnięte konta dla dodatkowych podejrzanych działań. Sprawdź, jeśli dopasowane kont są kont poufnych.


**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.


## <a name="reconnaissance-using-directory-services-queries"></a>Rekonesans przy użyciu zapytań usług katalogowych

**Opis**

Rekonesans usług katalogowych jest używana przez osoby atakujące do mapowania struktury katalogów i identyfikacji uprzywilejowanych kont do dalszych etapów w przypadku ataków. Protokół Security Account Manager Remote (SAM-R) to jedna z metody używane do wysyłania zapytań o katalog, aby wykonać takie mapowanie.

W tym wykrywanie alerty nie będą wyzwalane w pierwszym miesiącu po wdrożeniu usługi ATA. Podczas nauki okresu, profilów usługi ATA zapytania SAM-R, które zostały wprowadzone przez nich i komputery wyliczenia i pojedynczych zapytań kont poufnych.

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

Użyj [narzędzie SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) wzmacniania zabezpieczeń środowiska względem tej techniki.
Jeśli narzędzie nie ma zastosowania do poziomu kontrolera domeny:
1. Komputer działa luk w zabezpieczeniach, narzędzie do skanowania?  
2. Zbadaj, czy określone zapytanie o użytkowników i grup w ataku są kontami uprzywilejowanych lub o wysokiej wartości (to znaczy, Dyrektor Generalny, Dyrektor finansowy, zarządzanie infrastrukturą IT, itp.).  Jeśli tak, spójrz na inne działanie w punkcie końcowym również i monitorować komputery, które konta kwerendy jest się zalogowanym, ponieważ prawdopodobnie są elementy docelowe ruchu poprzecznego.

## <a name="reconnaissance-using-dns"></a>Rekonesans przy użyciu systemu DNS

**Opis**

Serwer DNS zawiera mapę wszystkich komputerów, adresów IP i usług w sieci. Te informacje są używane przez osoby atakujące do mapowania struktury sieci i interesujących komputerów docelowych do wykonania kolejnych kroków ataku.

W protokole DNS istnieje kilka typów zapytań. Usługa ATA wykrywa żądania AXFR (transferu) pochodzące z serwerów DNS bez.

**Badanie**

1. Maszyna źródłowa jest (**pochodzące z komputera...** ) serwera DNS? Jeśli tak, następnie jest to prawdopodobnie wynik fałszywie dodatni. Aby sprawdzić, kliknij alert, aby przejść do jego stronę szczegółów. W tabeli w obszarze **zapytania**, sprawdź, które domeny wykonano zapytanie. Czy te istniejących domen? Jeśli tak, następnie **Zamknij** podejrzanych działań (jest to wynik fałszywie dodatni). Ponadto upewnij się, że port 53 protokołu UDP między jest otwarty bramy usługi ATA i komputera źródłowego, aby uniknąć przyszłych wyników fałszywie dodatnich.
2.  Maszyna źródłowa działa skaner zabezpieczeń? Jeśli tak, **wykluczyć** jednostki w usłudze ATA bezpośrednio za pomocą **Zamknij i Wyklucz** lub za pośrednictwem **wykluczeń** strony (w obszarze **konfiguracji** — dostępne dla administratorów usługi ATA).
3.  Jeśli odpowiedzi na wszystkie pytania poprzedzającego jest nie, Zachowaj badania koncentrujące się na komputerze źródłowym. Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, jakie wystąpiły w okolicy czasowej żądania, wyszukując nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne.


**Korygowanie**

Aby zabezpieczyć wewnętrzny serwer DNS w celu uniemożliwienia przeprowadzenia rekonesansu przy użyciu systemu DNS, można wyłączyć transfery stref lub ograniczyć je tylko do określonych adresów IP. Aby uzyskać więcej informacji o ograniczaniu transferów stref, zobacz [Ograniczanie transferów stref](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Modyfikacja transferów stref jest jednym z zadań listę kontrolną, która powinny być kierowane do [zabezpieczenia serwerów DNS przed atakami wewnętrznymi i zewnętrznymi](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekonesans przy użyciu wyliczania sesji SMB


**Opis**

Wyliczanie bloku komunikatów (SMB) serwera pozwala osobom atakującym uzyskanie informacji którym ostatnio zalogowani użytkownicy. Gdy osoby atakujące już te informacje, mogą przenosić bok w sieci do określonych kont poufnych.

W tym wykrywanie alert jest wyzwalany, gdy wyliczenie sesji SMB jest wykonywane na kontrolerze domeny.

**Badanie**

1. Kliknij alert, aby przejść do jego stronę szczegółów. Sprawdź konto/s, który wykonał działanie, a także narażonych kontach, jeśli istnieje.

 - Czy istnieje pewnego rodzaju skaner zabezpieczeń, uruchomiony na komputerze źródłowym? Jeśli tak, **Zamknij i Wyklucz** podejrzanych działań.

2. Sprawdź, które zaangażowanych użytkowników/s wykonał operację. Są one zazwyczaj Zaloguj się do komputera źródłowego, czy też są one administratorów, którzy należy wykonać takie działania?  

3. Jeśli tak, jak i alertu zostanie zaktualizowany, **Pomiń** podejrzanych działań.  

4. Jeśli tak i nie powinna pobrać zaktualizowany, **Zamknij** podejrzanych działań.

5. Jeśli odpowiedzi na wszystkie powyższe nie, założono, że złośliwe działanie.

**Korygowanie**

Użyj [narzędzia Net zaprzestanie](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) wzmacniania zabezpieczeń środowiska na ten rodzaj ataku.

## <a name="remote-execution-attempt-detected"></a>Wykryto próbę zdalnego wykonania

**Opis**

Osoby atakujące, które złamanie poświadczeń administracyjnych lub użyj wykorzystać zero day mogą wykonywać polecenia zdalne na kontrolerze domeny. To może służyć do uzyskania trwałości, zbieranie informacji, atakom typu odmowa usługi (DOS) lub z innego powodu. Usługa ATA wykrywa połączeń narzędzia PSexec i usługi zdalnej usługi WMI.

**Badanie**

1. To jest typowe dla administracyjnych stacji roboczych oraz jak w przypadku członków zespołu IT oraz kont usług, które wykonują zadania administracyjne na kontrolerach domeny. Jeśli ma to miejsce, a alert zostanie zaktualizowany, ponieważ ten sam administratora lub komputer wykonuje zadania, **Pomiń** alertu.
2.  W danym komputerze może wykonywać to zdalne wykonywanie kodu na kontrolerze domeny?
  - Z danego konta może wykonywać to zdalne wykonywanie kodu na kontrolerze domeny?
  - Jeśli odpowiedzi na oba pytania będzie tak, **Zamknij** alertu.
3.  Jeśli odpowiedzi na pytania, albo nie, to działanie należy rozważyć prawdziwie dodatni. Spróbuj znaleźć źródło próby, sprawdzając profile komputera i konta. Kliknij komputer źródłowy lub konta, aby przejść do strony profilu. Sprawdź, co się stało z momentu te próby, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne.


**Korygowanie**

1. Ogranicz zdalny dostęp do kontrolerów domen z maszyn nienależących do warstwy 0.

2. Implementowanie [dostęp uprzywilejowany](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) umożliwia jedynie maszynom o wzmocnionych zabezpieczeniach nawiązać połączenia z kontrolerami domeny dla administratorów.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Ujawniono poufne poświadczenia konta & usługi ujawniające poświadczenia kont

> [!NOTE]
> To podejrzane działanie została zakończona i jest wyświetlany tylko w wersjach usługi ATA przed 1.9. Dla usługi ATA 1.9 i nowszych wersji, zobacz [raporty](reports.md).

**Opis**

Niektóre usługi wysyłają poświadczenia kont w postaci zwykłego tekstu. Można to zrobić nawet w przypadku kont poufnych. Osoby atakujące monitorujące ruch sieciowy może przechwytywać i korzystać z nich te poświadczenia do złośliwych celów. Wszystkie hasła nieszyfrowanego wrażliwe konta wyzwala alert, natomiast w przypadku kont zwykłych alert zostanie wywołany, jeśli co najmniej pięć różnych kont wysyłać hasła w postaci zwykłego tekstu z tym samym komputerem źródłowym. 

**Badanie**

Kliknij alert, aby przejść do jego stronę szczegółów. Zobacz, które konta nie zostały narażone. Jeśli istnieje wiele takich kont, kliknij przycisk **Pobierz szczegóły** do wyświetlania listy w arkuszu kalkulacyjnym programu Excel.

Zazwyczaj jest skrypt lub starsza wersja aplikacji na komputerach źródłowych, która korzysta z prostego powiązania LDAP.

**Korygowanie**

Sprawdź konfigurację komputerów źródłowych i upewnij się, że nie korzystają z prostych powiązań LDAP. Zamiast prostych powiązań LDAP można Użyj warstwy LDAP SALS lub protokołu LDAPS.

## <a name="suspicious-authentication-failures"></a>Podejrzane błędy uwierzytelniania

**Opis**

W ramach ataków siłowych osoba atakująca podejmuje próbę uwierzytelniania za pomocą wielu różnych haseł dla różnych kont, aż do znalezienia prawidłowego hasła dla co najmniej jedno konto. Gdy zostanie znaleziony, osoba atakująca może zalogować za pomocą tego konta.

W tym wykrywanie alert jest wyzwalany, gdy wystąpiło wiele błędów uwierzytelniania przy użyciu protokołu Kerberos lub NTLM, może to być albo poziomie wprowadzaj w małej grupie, haseł dla wielu użytkowników; lub w pionie o dużej haseł na tylko kilku użytkowników; lub dowolnej kombinacji tych dwóch opcji. Minimalny okres wywoła alertu jest jeden tydzień.

**Badanie**

1.  Kliknij przycisk **Pobierz szczegóły** Aby wyświetlić pełne informacje w arkuszu kalkulacyjnym programu Excel. Można uzyskać następujące informacje: 
  - Lista zaatakowane konta
  - Lista odgadnięte konta, w której próby logowania zakończone z pomyślnym uwierzytelnieniu
  - Jeśli prób uwierzytelnienia zostały wykonane przy użyciu metod NTLM, zostaną wyświetlone odpowiednie zdarzenie działania 
  - Jeśli prób uwierzytelnienia zostały wykonane przy użyciu protokołu Kerberos, zostanie wyświetlony działań w odpowiednich sieci
2.  Kliknij na komputerze źródłowym, aby przejść do strony profilu. Sprawdź, co się stało z momentu te próby, wyszukiwanie nietypowych działań, takich jak: kto zalogowano, które zasoby w przypadku, gdy dostępne. 
3.  Jeśli uwierzytelnianie zostało wykonane przy użyciu metod NTLM, a zobaczysz, że występuje alert o wiele razy i nie jest dostępny dotyczące serwera, na którym maszyna źródłowa próbował uzyskać dostęp do wystarczająco dużo informacji, należy włączyć **inspekcji NTLM** na kontrolery domeny zaangażowane. Aby to zrobić, należy włączyć zdarzenia 8004. To zdarzenie uwierzytelniania NTLM, które zawiera informacje dotyczące komputera źródłowego, konto użytkownika i **serwera** , maszyna źródłowa próbowano uzyskać dostęp. Gdy dowiesz się, które serwer wysłał weryfikacji za pomocą uwierzytelniania, serwer powinien być sprawdzony, sprawdzając jego zdarzenia, takie jak 4624, aby lepiej zrozumieć proces uwierzytelniania. 


**Korygowanie**

[Złożone, długie hasła](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) zapewnić wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi.

## Podejrzanie utworzenie usługi <a name="suspicious-service-creation"></a>

**Opis**

Osoby atakujące usiłują podwyższyć do uruchamiania usług podejrzane w sieci. Usługa ATA zgłasza alert, gdy nowa usługa, która jest podejrzana została utworzona na kontrolerze domeny. Ten alert, który opiera się na zdarzenie 7045 i zostanie wykryty w każdym kontrolerze domeny, który jest objęty przez bramę usługi ATA lub uproszczonej bramy.

**Badanie**

1. Jeśli dany komputer jest stacji roboczej administratora lub na komputerze, na którym członków zespołu IT i usługi konta wykonywania zadań administracyjnych, może to być wynik fałszywie dodatni i może być konieczne **Pomiń** alertu i dodaj go do Listy wykluczeń, jeśli to konieczne.

2. Element, który rozpoznaje na tym komputerze jest usługa?

 - Jest **konta** danego mogła zainstalować tę usługę?

 - Jeśli odpowiedzi na oba pytania *tak*, następnie **Zamknij** alertu, albo dodaj go do listy wykluczeń.

3. Jeśli odpowiedzi na pytania albo *nie*, a następnie należy to uwzględnić prawdziwie dodatni.

**Korygowanie**

- Implementowanie mniej uprzywilejowanego dostępu domeny na maszynach w celu zezwalanie wyłącznie określonym użytkownikom uprawnienia do tworzenia nowych usług.


## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podejrzenie kradzieży tożsamości na podstawie nietypowego zachowania

**Opis**

Usługa ATA uzyskuje informacje o zachowania jednostek dla użytkowników, komputerów i zasobów okresie przewijania trzy tygodnie. Model zachowanie zależy od następujących działań: maszyn jednostek zalogowało się na komputerze, jednostki żądane zasoby dostęp do, a czas tych operacji miało miejsce. Usługa ATA wysyła alert, gdy ma odchylenie od zachowanie jednostki, w oparciu o algorytmów uczenia maszynowego. 

**Badanie**

1. Użytkownik powinien wykonywać te operacje?

2. Należy wziąć pod uwagę następujące przypadki jako potencjalnych fałszywych alarmów: użytkownik, który jest zwracany z urlopu, personel działu informatycznego, które wykonują nadmiarowe dostępu o obowiązku (na przykład wzrost pomocy technicznej w danym dniu lub tygodnia), w ramach zdalnego pulpitu aplikacje. + If możesz **Zamknij i Wyklucz** alert, a użytkownik nie będzie należeć do wykrywania


**Korygowanie**

 Różne działania powinny zostać podjęte w zależności od tego, co spowodowało to nietypowe zachowanie, wystąpią. Na przykład jeśli został zeskanowany sieci, na maszynie źródłowej powinien zostać zablokowany sieci (o ile nie została zatwierdzona).

## <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu


**Opis**

Osoby atakujące wykorzystywać narzędzia stosujące różnych protokołów (SMB, protokołu Kerberos, NTLM) w sposób niestandardowy. Chociaż ten typ ruchu sieciowego jest akceptowany przez Windows bez ostrzeżeń, ATA jest w stanie rozpoznać potencjalne złośliwego działania. To zachowanie jest wskaźnikiem technik, takich jak protokołu-Pass--Hash, a także luki w zabezpieczeniach używany przez oprogramowanie wymuszające okup zaawansowanych, takich jak WannaCry.

**Badanie**

Identyfikowanie protokół, który jest nietypowy — z osi czasu podejrzanych działań, kliknij pozycję podejrzanego działania, aby uzyskać dostęp do strony szczegółów; Protokół, który pojawia się nad strzałkę: Kerberos lub NTLM.

- **Protokół Kerberos**: często wyzwolony, jeśli stosowanie metod hakerskich narzędzia, takie jak program Mimikatz potencjalnie był używany atak Overpass--Hash. Sprawdź, czy komputer źródłowy jest uruchomiona aplikacja, która implementuje własnego stosu protokołu Kerberos, który nie jest zgodne z RFC protokołu Kerberos. W takim przypadku jest niegroźnie prawdziwie dodatni i alert może być **zamknięte**. Jeśli alert, utrzymuje jest uruchomiony i nadal jest tak, możesz to zrobić **Pomiń** alertu.

- **NTLM**: może być WannaCry lub narzędzi, takich jak Metasploit, Medusa i Hydra.  

Aby określić, czy działania jest to atak WannaCry, wykonaj następujące czynności:

1. Sprawdź, czy komputer źródłowy działa narzędzie ataków, takich jak Metasploit, Medusa lub Hydra.

2. Jeśli nie zostaną znalezione żadne narzędzia ataku, sprawdź, czy komputer źródłowy jest uruchomiona aplikacja, która implementuje stos protokołu NTLM lub SMB.

3. Jeśli nie, sprawdź, czy przyczyną WannaCry, uruchamiając skrypt skanera WannaCry, na przykład [tego skanera](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) względem komputera źródłowego związane z podejrzanych działań. Jeżeli skaner stwierdza, że komputer jako zainfekowane lub narażone, praca na instalowaniu poprawek maszyny i usuwania złośliwego oprogramowania i blokowanie go z sieci.

4. Nie znaleziono skryptu, czy maszyny są zainfekowane lub narażone, a następnie nadal mogą być zainfekowane, ale może być wyłączone SMBv1 lub ma została zainstalowana poprawka zapewniająca maszyną, która wpłynie na narzędzie do skanowania.

**Korygowanie**

Zastosuj najnowsze poprawki do wszystkich maszyn i sprawdź, wszystkie aktualizacje zabezpieczeń są stosowane.

1. [Wyłącz SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Usuń WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3.  Czasami można odszyfrować danych w formancie niektóre programy ransom. Odszyfrowywanie jest możliwe tylko wtedy, jeśli użytkownik nie została uruchomiona ponownie lub wyłączony komputer. Aby uzyskać więcej informacji, zobacz [chcesz krzykiem przed oprogramowaniem wymuszającym Okup](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


>[!NOTE]
> Aby wyłączyć alert dotyczący podejrzanego działania, skontaktuj się z działem pomocy technicznej.

## <a name="related-videos"></a>Pokrewne wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Zobacz też
- [Podręcznik dotyczący podejrzanych działań usługi ATA](http://aka.ms/ataplaybook)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
