---
title: "Co to jest usługa Microsoft Advanced Threat Analytics (ATA)? | Microsoft ATA"
description: "Informacje dotyczące usługi Microsoft Advanced Threat Analytics (ATA) i wykrywanych przez nią podejrzanych działań"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 58afbae96bce0075f0a58be648e82744ce279997


---


## Co to jest usługa ATA?
Usługa Microsoft Advanced Threat Analytics (ATA) jest wiodącym rozwiązaniem na rynku analiz zachowania użytkowników i jednostek, które ułatwia specjalistom ds. zabezpieczeń IT ochronę organizacji przed zaawansowanymi atakami ukierunkowanymi (APT) i zagrożeniami wewnętrznymi. Usługa ATA, która automatycznie przeprowadza analizy, uczy się i identyfikuje prawidłowe oraz nieprawidłowe zachowania jednostek (użytkowników, urządzeń i zasobów) za pomocą zaawansowanej technologii uczenia maszynowego, pomaga w wykrywaniu znanych złośliwych ataków i technik, problemów z zabezpieczeniami i zagrożeń. Dzięki wiedzy i zdolnościom światowej klasy pracowników naukowo-badawczych ta nowatorska technologia ułatwia przedsiębiorstwom koncentrowanie się na identyfikowaniu naruszeń zabezpieczeń zanim spowodują one szkody.

## Jakie zadania wykonuje usługa ATA?
Usługa ATA wykrywa:

  - Zaawansowane zagrożenia ciągłe na wstępnym etapie przeprowadzenia ataku, zanim spowodują one szkody

  - Zagrożenia wewnętrzne

Usługa ATA pomaga oddzielić naprawdę podejrzane działania od szumu, aby skoncentrować się na problemach krytycznych.

Aparat wykrywania usługi ATA wykorzystuje uczenie maszynowe, głęboką inspekcję pakietów w kontekście jednostki, analizę dzienników oraz informacje z usługi Active Directory (AD) do analizy zachowania użytkowników i jednostek.

Usługa ATA wykonuje głęboką analizę ruchu w organizacji i za pomocą uczenia maszynowego tworzy mapę typowych działań, ruchu i użycia zasobów w organizacji. Następnie usługa ATA wyszukuje i sygnalizuje nietypowe zdarzenia. Można to osiągnąć, korzystając z technologii głębokiej inspekcji pakietów w kontekście jednostki, która zapewnia głębszą analizę ruchu sieciowego, dzięki czemu usługa ATA może analizować wszystkie poziomy ruchu sieciowego.

Usługa ATA zbiera również istotne zdarzenia z systemów SIEM i kontrolerów domeny. Po analizie usługa ATA tworzy dynamiczny, nieustannie aktualizowany widok wszystkich osób, urządzeń i zasobów w organizacji. Korzystając z tego kompleksowego widoku, usługa ATA jest w stanie wykrywać znane złośliwe ataki, takie jak pass-the-hash, pass-the-ticket, ataki typu rekonesans itd., a także wyszukiwać wszelkie nieprawidłowości w zachowaniu jednostek w sieci.

Po wykryciu podejrzanego działania usługa ATA zgłasza alert, minimalizując liczbę fałszywych alarmów przy użyciu zaawansowanych algorytmów do agregacji i weryfikacji kontekstu.



## Jakie zagrożenia wyszukuje usługa ATA?

Usługa ATA wykrywa następujące fazy zaawansowanego ataku: rekonesans, przejęcie poświadczeń, penetracja sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne. Celem jest wykrycie zaawansowanych ataków i zagrożeń wewnętrznych, zanim będą mogły spowodować szkody w organizacji.

Wykrycie każdej fazy wywołuje kilka podejrzanych działań odpowiednich dla danej fazy, gdzie poszczególne podejrzane działania są powiązane z różnymi odmianami możliwych ataków.

### Rekonesans
Usługa ATA wykrywa wiele odmian rekonesansu. Wykrywane odmiany to między innymi:

-   **Rekonesans przy użyciu wyliczania kont**<br>Obejmuje próby ustalenia przez osoby atakujące przy użyciu protokołu Kerberos, czy określone konto użytkownika istnieje, nawet jeśli to działanie nie zostało zarejestrowane jako zdarzenie na kontrolerze domeny.
-   **Wyliczenie sesji sieciowej**<br>
W fazie rekonesansu osoby atakujące mogą wysyłać do kontrolera domeny zapytania dotyczące wszystkich aktywnych sesji protokołu SMB na serwerze, dzięki czemu mogą uzyskać dostęp do wszystkich użytkowników i adresów IP skojarzonych z tymi sesjami protokołu SMB. Wyliczenie sesji SMB może posłużyć osobom atakującym do atakowania kont poufnych, ułatwiając im penetrację całej sieci.
-   **Rekonesans przy użyciu systemu DNS**<br>
Informacje dotyczące systemu DNS w sieci docelowej są często bardzo przydatnymi informacjami w rekonesansie. Informacje dotyczące systemu DNS zawierają listę wszystkich serwerów i często wszystkich klientów oraz mapowanie na ich adresy IP. Wyświetlenie informacji dotyczących systemu DNS może spowodować udostępnienie osobom atakującym szczegółowego widoku tych jednostek w danym środowisku, umożliwiając skoncentrowanie ich wysiłków na jednostkach odpowiednich dla kampanii.

### Przejęcie poświadczeń

Aby umożliwiać wykrywanie przejęcia poświadczeń, usługa ATA używa zarówno analizy behawioralnej opartej na uczeniu maszynowym, jak i wykrywania znanych złośliwych ataków i technik.

Korzystając z analizy behawioralnej i uczenia maszynowego, usługa ATA jest w stanie wykrywać podejrzane działania, takie jak nietypowe logowania, nietypowy dostęp do zasobów i nietypowe godziny pracy, które mogą wskazywać na przejęcie poświadczeń.
Aby zapewnić ochronę przed przejęciem poświadczeń, usługa ATA wykrywa następujące znane złośliwe ataki i techniki:

 - **Atak siłowy** <br>Osoby atakujące usiłują odgadnąć poświadczenia użytkowników, podejmując dla wielu użytkowników próby uwierzytelnienia przy użyciu różnych haseł. Osoby atakujące często używają złożonych algorytmów lub słowników, aby wypróbować maksymalną liczbę wartości dozwoloną w danym systemie.

- **Poufne konto ujawnione podczas uwierzytelniania przy użyciu zwykłego tekstu**<br>
Jeśli poświadczenia konta z wysokim poziomem uprawnień są wysyłane w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

- **Ujawnienie kont przez usługę podczas uwierzytelniania przy użyciu zwykłego tekstu** <br>
Jeśli usługa na komputerze wysyła poświadczenia wielu kont w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

- **Podejrzane działania związane z kontem wystawionym jako przynęta**<br>
Konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu przechwytywania, identyfikowania i śledzenia złośliwych działań podejmowanych w celu użycia tych kont. Usługa ATA ostrzega o wszelkich działaniach związanych z tymi kontami wystawionymi jako przynęta.
-   **Implementacja nietypowego protokołu**<br>
Żądania uwierzytelniania (Kerberos lub NTLM) zazwyczaj są realizowane przy użyciu zwykłego zestawu metod i protokołów. Jednak w celu pomyślnego uwierzytelnienia żądanie musi jedynie spełniać określony zestaw wymagań. Osoby atakujące mogą zaimplementować te protokoły z drobnymi odchyleniami od normalnego wdrożenia w danym środowisku. Tego rodzaju odchylenia mogą wskazywać na obecność osoby atakującej, która próbuje przejąć lub pomyślnie przejmuje poświadczenia.
-   **Złośliwe żądanie informacji prywatnych z zakresu ochrony danych**<br>
Interfejs API ochrony danych (DPAPI) to usługa ochrony danych oparta na hasłach. Ta usługa ochrony jest używana przez różne aplikacje, które przechowują Twoje tajemnice, takie jak hasła witryn internetowych i poświadczenia udziałów plików. W celu obsługi scenariuszy utraty hasła użytkownicy mogą odszyfrowywać chronione dane za pomocą klucza odzyskiwania, który nie zawiera ich hasła. W środowisku domeny osoby atakujące mogą zdalnie wykraść klucz odzyskiwania i użyć go do odszyfrowywania chronionych danych na wszystkich komputerach przyłączonych do domeny.
-   **Nietypowe zachowanie**<br>
Często w przypadku zagrożeń wewnętrznych, a także ataków zaawansowanych poświadczenia konta mogą zostać przejęte przy użyciu metod inżynierii społecznej lub nowych, jeszcze nieznanych metod i technik. Usługa ATA jest w stanie wykryć tego rodzaju przejęcia, analizując zachowanie jednostki oraz wykrywając nieprawidłowości operacji wykonywanych przez jednostki i alarmując o nich.

### Penetracja sieci
Aby zapewnić wykrywanie penetracji sieci, gdy użytkownicy korzystają z poświadczeń umożliwiających dostęp do niektórych zasobów, do których nie powinni mieć dostępu, usługa ATA stosuje zarówno uczenie maszynowe oparte na analizie behawioralnej, jak również wykrywanie znanych złośliwych ataków i technik.

Korzystając z analizy behawioralnej i uczenia maszynowego, usługa ATA wykrywa nietypowy dostęp do zasobów, użycie nietypowych urządzeń i występowanie innych okoliczności świadczących o penetracji sieci.

Ponadto usługa ATA może wykrywać penetrację sieci, rozpoznając między innymi następujące techniki penetracji sieci używane przez osoby atakujące:

- **Ataki typu Pass-the-Ticket** <br>
Osoby atakujące dokonują kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera, personifikując jednostkę w sieci.
- **Ataki typu Pass-the-Hash** <br>
Osoby atakujące dokonują kradzieży skrótu NTLM jednostki, uwierzytelniają się za pomocą protokołu NTLM przy jego użyciu, a następnie uzyskują dostęp do zasobów w sieci, personifikując daną jednostkę.
- **Ataki typu Over-Pass-the-Hash**<br>
Uwierzytelniając się przy użyciu protokołu Kerberos i skradzionego skrótu NTLM, osoba atakująca uzyskuje prawidłowy bilet uprawniający do przyznania biletu protokołu Kerberos, a następnie używa tego biletu do uwierzytelnienia się jako prawidłowy użytkownik i uzyskania dostępu do zasobów w sieci.
-   **Nietypowe zachowanie**<br>
Penetracja sieci to technika, którą osoby atakujące często stosują, aby poruszać się między urządzeniami i obszarami w sieci ofiary w celu uzyskania dostępu do poświadczeń uprzywilejowanych lub informacji poufnych dla osoby atakującej. Usługa ATA jest w stanie wykryć penetrację sieci, analizując zachowania użytkowników i urządzeń oraz ich relacje w sieci firmowej, a także wykryć wszelkie nietypowe wzorce dostępu, które mogą wskazywać na penetrację sieci przez osobę atakującą.

### Podwyższenie poziomu uprawnień
Usługa ATA wykrywa udane ataki polegające na podwyższeniu poziomu uprawnień oraz próby takich ataków, podczas których osoby atakujące usiłują podwyższyć poziom uprawnień i wykorzystać je wielokrotnie do przejęcia pełnej kontroli nad atakowanym środowiskiem. 

Usługa ATA włącza wykrywanie podwyższenia poziomu uprawnień, łącząc analizę behawioralną umożliwiającą wykrywanie nietypowego zachowania kont uprzywilejowanych, a także wykrywanie znanych i złośliwych ataków i technik, które są często używane do podwyższania poziomu uprawnień, takich jak:

- **Programy wykorzystujące lukę MS14-068 (sfałszowany element PAC)**<br>
Tego typu ataki polegają na umieszczeniu danych autoryzacji przez osoby atakujące w prawidłowym bilecie uprawniającym do przyznania biletu w formie sfałszowanego nagłówka autoryzacji, który przyznaje im dodatkowe uprawnienia nieprzyznane przez organizację. W tym scenariuszu osoba atakująca wykorzystuje poświadczenia, które zostały przejęte lub przechwycone podczas penetracji sieci.
- **Programy wykorzystujące lukę MS11-013 (Silver PAC)**<br>
Ataki wykorzystujące lukę MS11-013 stanowią zagrożenie podniesieniem poziomu uprawnień w protokole Kerberos, co umożliwia sfałszowanie niektórych aspektów biletu usługi Kerberos. Złośliwy użytkownik lub osoba atakująca, która z sukcesem wykorzystała tę lukę w zabezpieczeniach, może uzyskać token z podwyższonym poziomem uprawnień na kontrolerze domeny. W tym scenariuszu osoba atakująca wykorzystuje poświadczenia, które zostały przejęte lub przechwycone podczas penetracji sieci.

### Zdominowanie domeny
Usługa ATA wykrywa osoby atakujące, które próbują uzyskać lub uzyskują całkowitą kontrolę i dominację nad środowiskiem ofiary, sprawdzając znane techniki stosowane przez osoby atakujące, między innymi:

- **Złośliwe oprogramowanie Skeleton Key**<br>
Osoba atakująca instaluje na kontrolerze domeny złośliwe oprogramowanie, które umożliwia jej uwierzytelnienie się jako dowolny użytkownik, nie ograniczając logowania autoryzowanych użytkowników.
- **Sfałszowany bilet uwierzytelniania Golden Ticket**<br>
Osoba atakująca dokonuje kradzieży poświadczeń KBTGT (bilet Golden Ticket protokołu Kerberos). Korzystając z tego biletu, osoba atakująca tworzy bilet uprawniający do przyznania biletu offline, którego następnie używa do uzyskania dostępu do zasobów w sieci.
- **Zdalne wykonywanie kodu**<br>
Osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny.
-   **Złośliwe żądania replikacji** W środowiskach usługi Active Directory (AD) replikacja między kontrolerami domeny odbywa się regularnie. Osoba atakująca może spreparować żądanie replikacji usługi AD (czasami podszywając się pod kontroler domeny), co umożliwi jej uzyskanie danych przechowywanych w usłudze AD, między innymi skrótów haseł, bez konieczności zastosowania bardziej natrętnych technik, takich jak kopiowanie woluminów w tle.

## Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-use/install-ata).

## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


