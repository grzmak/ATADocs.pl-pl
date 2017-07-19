---
title: "Jakie zagrożenia wykrywa usługa Advanced Threat Analytics? | Microsoft Docs"
description: "Lista zagrożeń, które wykrywa usługa Advanced Threat Analytics"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 630bb2b74dafcf9ab9b3469c2afbf8abc59c2dbf
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/03/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# <a name="what-threats-does-ata-look-for"></a>Jakie zagrożenia wyszukuje usługa ATA?

Usługa ATA wykrywa następujące fazy zaawansowanego ataku: rekonesans, przejęcie poświadczeń, penetracja sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne. Celem jest wykrycie zaawansowanych ataków i zagrożeń wewnętrznych, zanim będą mogły spowodować szkody w organizacji.
Wykrycie każdej fazy wywołuje kilka podejrzanych działań odpowiednich dla danej fazy, gdzie poszczególne podejrzane działania są powiązane z różnymi odmianami możliwych ataków.
Fazy ataku typu kill chain, w których usługa ATA aktualnie obsługuje wykrywanie, zostały wyróżnione na poniższej ilustracji.

![Usługa ATA skupia się na penetracji sieci w ataku typu kill chain](media/attack-kill-chain-small.jpg)


### <a name="reconnaissance"></a>Rekonesans

Usługa ATA wykrywa wiele odmian rekonesansu. Wykrywane odmiany to między innymi:

-   **Rekonesans przy użyciu funkcji wyliczania kont**<br></br>Obejmuje próby ustalenia przez osoby atakujące przy użyciu protokołu Kerberos, czy określone konto użytkownika istnieje, nawet jeśli to działanie nie zostało zarejestrowane jako zdarzenie na kontrolerze domeny.

-   **Wyliczanie sesji sieciowych**<br></br>W fazie rekonesansu osoby atakujące mogą wysyłać do kontrolera domeny zapytania dotyczące wszystkich aktywnych sesji protokołu SMB na serwerze, dzięki czemu mogą uzyskać dostęp do wszystkich użytkowników i adresów IP skojarzonych z tymi sesjami protokołu SMB. Wyliczenie sesji SMB może posłużyć osobom atakującym do atakowania kont poufnych, ułatwiając im penetrację całej sieci.

-   **Rekonesans przy użyciu systemu DNS**<br></br>Informacje dotyczące systemu DNS w sieci docelowej są często bardzo przydatnymi informacjami w rekonesansie. Informacje dotyczące systemu DNS zawierają listę wszystkich serwerów i często wszystkich klientów oraz mapowanie na ich adresy IP. Wyświetlenie informacji dotyczących systemu DNS może spowodować udostępnienie osobom atakującym szczegółowego widoku tych jednostek w danym środowisku, umożliwiając skoncentrowanie ich wysiłków na jednostkach odpowiednich dla kampanii.

-   **Rekonesans przy użyciu funkcji wyliczania usług katalogowych**<br></br>Rekonesans wykrywający jednostki (użytkowników, grupy itp.) i wykonywany przy użyciu zdalnego protokołu SAM w celu uruchamiania zapytań względem kontrolerów domeny. Ta metoda rozpoznawcza przeważa w wielu typach złośliwego oprogramowania w rzeczywistych scenariuszach ataków. 


### <a name="compromised-credentials"></a>Przejęcie poświadczeń

Aby umożliwiać wykrywanie przejęcia poświadczeń, usługa ATA używa zarówno analizy behawioralnej opartej na uczeniu maszynowym, jak i wykrywania znanych złośliwych ataków i technik.
Korzystając z analizy behawioralnej i uczenia maszynowego, usługa ATA jest w stanie wykrywać podejrzane działania, takie jak nietypowe logowania, nietypowy dostęp do zasobów i nietypowe godziny pracy, które mogą wskazywać na przejęcie poświadczeń. Aby zapewnić ochronę przed przejęciem poświadczeń, usługa ATA wykrywa następujące znane złośliwe ataki i techniki:

-   **Atak siłowy**<br></br>Osoby atakujące usiłują odgadnąć poświadczenia użytkowników, podejmując dla wielu użytkowników próby uwierzytelnienia przy użyciu różnych haseł. Osoby atakujące często używają złożonych algorytmów lub słowników, aby wypróbować maksymalną liczbę wartości dozwoloną w danym systemie.

- **Podejrzane niepowodzenia uwierzytelniania** (behawioralny atak siłowy) <br></br> Atakujący próbują użyć ataków siłowych na poświadczenia w celu naruszenia bezpieczeństwa kont. Usługa ATA zgłasza alert po wykryciu nietypowych błędów uwierzytelniania.

-   **Poufne konto ujawnione podczas uwierzytelniania przy użyciu zwykłego tekstu**<br></br>Jeśli poświadczenia konta z wysokim poziomem uprawnień są wysyłane w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

-   **Ujawnienie kont przez usługę podczas uwierzytelniania przy użyciu zwykłego tekstu** <br></br>Jeśli usługa na komputerze wysyła poświadczenia wielu kont w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

-   **Podejrzane działania związane z kontem wystawionym jako przynęta**<br></br>Konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu przechwytywania, identyfikowania i śledzenia złośliwych działań podejmowanych w celu użycia tych kont. Usługa ATA ostrzega o wszelkich działaniach związanych z tymi kontami wystawionymi jako przynęta.

-   **Nietypowa implementacja protokołu**<br></br>Żądania uwierzytelniania (Kerberos lub NTLM) zazwyczaj są realizowane przy użyciu zwykłego zestawu metod i protokołów. Jednak w celu pomyślnego uwierzytelnienia żądanie musi jedynie spełniać określony zestaw wymagań. Osoby atakujące mogą zaimplementować te protokoły z drobnymi odchyleniami od normalnego wdrożenia w danym środowisku. Tego rodzaju odchylenia mogą wskazywać na obecność osoby atakującej, która próbuje przejąć lub pomyślnie przejmuje poświadczenia.

-   **Złośliwe żądanie informacji prywatnych z zakresu ochrony danych**<br></br>Interfejs API ochrony danych (DPAPI) to usługa ochrony danych oparta na hasłach. Ta usługa ochrony jest używana przez różne aplikacje, które przechowują Twoje tajemnice, takie jak hasła witryn internetowych i poświadczenia udziałów plików. W celu obsługi scenariuszy utraty hasła użytkownicy mogą odszyfrowywać chronione dane za pomocą klucza odzyskiwania, który nie zawiera ich hasła. W środowisku domeny osoby atakujące mogą zdalnie wykraść klucz odzyskiwania i użyć go do odszyfrowywania chronionych danych na wszystkich komputerach przyłączonych do domeny.

-   **Nietypowe zachowanie**<br></br>Często w przypadku zagrożeń wewnętrznych, a także ataków zaawansowanych poświadczenia konta mogą zostać przejęte przy użyciu metod inżynierii społecznej lub nowych, jeszcze nieznanych metod i technik. Usługa ATA jest w stanie wykryć tego rodzaju przejęcia, analizując zachowanie jednostki oraz wykrywając nieprawidłowości operacji wykonywanych przez jednostki i alarmując o nich.

### <a name="lateral-movement"></a>Penetracja sieci

Aby zapewnić wykrywanie penetracji sieci, gdy użytkownicy korzystają z poświadczeń umożliwiających dostęp do niektórych zasobów, do których nie powinni mieć dostępu, usługa ATA stosuje zarówno uczenie maszynowe oparte na analizie behawioralnej, jak również wykrywanie znanych złośliwych ataków i technik.
Korzystając z analizy behawioralnej i uczenia maszynowego, usługa ATA wykrywa nietypowy dostęp do zasobów, użycie nietypowych urządzeń i występowanie innych okoliczności świadczących o penetracji sieci.
Ponadto usługa ATA może wykrywać penetrację sieci, rozpoznając między innymi następujące techniki penetracji sieci używane przez osoby atakujące:

-   **Ataki typu Pass-the-Ticket** <br></br>Osoby atakujące dokonują kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera, personifikując jednostkę w sieci.

-   **Ataki typu Pass-the-Hash** <br></br>Osoby atakujące dokonują kradzieży skrótu NTLM jednostki, uwierzytelniają się za pomocą protokołu NTLM przy jego użyciu, a następnie uzyskują dostęp do zasobów w sieci, personifikując daną jednostkę.

-   **Ataki typu Over-Pass-the-Hash**<br></br>Uwierzytelniając się przy użyciu protokołu Kerberos i skradzionego skrótu NTLM, osoba atakująca uzyskuje prawidłowy bilet uprawniający do przyznania biletu protokołu Kerberos, a następnie używa tego biletu do uwierzytelnienia się jako prawidłowy użytkownik i uzyskania dostępu do zasobów w sieci.

-   **Nietypowe zachowanie**<br></br>Penetracja sieci to technika, którą osoby atakujące często stosują, aby poruszać się między urządzeniami i obszarami w sieci ofiary w celu uzyskania dostępu do poświadczeń uprzywilejowanych lub informacji poufnych dla osoby atakującej. Usługa ATA jest w stanie wykryć penetrację sieci, analizując zachowania użytkowników i urządzeń oraz ich relacje w sieci firmowej, a także wykryć wszelkie nietypowe wzorce dostępu, które mogą wskazywać na penetrację sieci przez osobę atakującą.

### <a name="privilege-escalation"></a>Podwyższenie poziomu uprawnień

Usługa ATA wykrywa udane ataki polegające na podwyższeniu poziomu uprawnień oraz próby takich ataków, podczas których osoby atakujące usiłują podwyższyć poziom uprawnień i wykorzystać je wielokrotnie do przejęcia pełnej kontroli nad atakowanym środowiskiem.
Usługa ATA włącza wykrywanie podwyższenia poziomu uprawnień, łącząc analizę behawioralną umożliwiającą wykrywanie nietypowego zachowania kont uprzywilejowanych, a także wykrywanie znanych i złośliwych ataków i technik, które są często używane do podwyższania poziomu uprawnień, takich jak:

-   **Programy wykorzystujące lukę MS14-068 (sfałszowany element PAC)**<br></br>Tego typu ataki polegają na umieszczeniu danych autoryzacji przez osoby atakujące w prawidłowym bilecie uprawniającym do przyznania biletu w formie sfałszowanego nagłówka autoryzacji, który przyznaje im dodatkowe uprawnienia nieprzyznane przez organizację. W tym scenariuszu osoba atakująca wykorzystuje poświadczenia, które zostały przejęte lub przechwycone podczas penetracji sieci.

-   **Programy wykorzystujące lukę MS11-013 (Silver PAC)**<br></br>Ataki wykorzystujące lukę MS11-013 stanowią zagrożenie podniesieniem poziomu uprawnień w protokole Kerberos, co umożliwia sfałszowanie niektórych aspektów biletu usługi Kerberos. Złośliwy użytkownik lub osoba atakująca, która z sukcesem wykorzystała tę lukę w zabezpieczeniach, może uzyskać token z podwyższonym poziomem uprawnień na kontrolerze domeny. W tym scenariuszu osoba atakująca wykorzystuje poświadczenia, które zostały przejęte lub przechwycone podczas penetracji sieci.

-   **Nietypowa modyfikacja wrażliwych grup**  <br></br>W fazie podwyższenia poziomu uprawnień atakujący modyfikują grupy z wysokim poziomem uprawnień w celu uzyskania dostępu do poufnych zasobów. Usługa ATA wykrywa teraz odbiegające od normy zmiany w grupach z podwyższonym poziomem uprawnień.

### <a name="domain-dominance"></a>Zdominowanie domeny

Usługa ATA wykrywa osoby atakujące, które próbują uzyskać lub uzyskują całkowitą kontrolę i dominację nad środowiskiem ofiary, sprawdzając znane techniki stosowane przez osoby atakujące, między innymi:

-   **Złośliwe oprogramowanie Skeleton Key**<br></br>Osoba atakująca instaluje na kontrolerze domeny złośliwe oprogramowanie, które umożliwia jej uwierzytelnienie się jako dowolny użytkownik, nie ograniczając logowania autoryzowanych użytkowników.

-   **Sfałszowany bilet uwierzytelniania Golden Ticket**<br></br>Osoba atakująca dokonuje kradzieży poświadczeń KBTGT (bilet Golden Ticket protokołu Kerberos). Korzystając z tego biletu, osoba atakująca tworzy bilet uprawniający do przyznania biletu offline, którego następnie używa do uzyskania dostępu do zasobów w sieci.

-   **Zdalne wykonywanie**<br></br>Osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny.

- **Próba wykonania zdalnego — metoda exec WMI**<br></br>Osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny. Usługa ATA wykrywa zdalne wykonywanie kodu za pomocą metod WMI.

-   **Złośliwe żądania replikacji** <br></br>W środowiskach usługi Active Directory (AD) replikacja między kontrolerami domeny odbywa się regularnie. Osoba atakująca może spreparować żądanie replikacji usługi AD (czasami podszywając się pod kontroler domeny), co umożliwi jej uzyskanie danych przechowywanych w usłudze AD, między innymi skrótów haseł, bez konieczności zastosowania bardziej natrętnych technik, takich jak kopiowanie woluminów w tle.


## <a name="whats-next"></a>Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](ata-architecture.md).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](install-ata-step1.md).

## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
