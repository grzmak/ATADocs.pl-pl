---
# required metadata

title: Co to jest usługa Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics
description: Informacje dotyczące usługi Microsoft Advanced Threat Analytics (ATA) i wykrywanych przez nią podejrzanych działań
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## Co to jest usługa ATA?
Usługa Microsoft Advanced Threat Analytics (ATA) jest rozwiązaniem w zakresie zabezpieczeń, które ułatwia specjalistom ds. zabezpieczeń IT ochronę organizacji przed zaawansowanymi atakami ukierunkowanymi i zagrożeniami wewnętrznymi. Usługa ATA automatycznie analizuje, rozpoznaje i identyfikuje typowe i nietypowe zachowania jednostek (użytkownicy, urządzenia i zasoby) w celu identyfikowania zagrożeń, takich jak znane złośliwe ataki i techniki, oraz problemów z bezpieczeństwem. Dzięki wiedzy i zdolnościom światowej klasy pracowników naukowo-badawczych ta nowatorska technologia ułatwia przedsiębiorstwom koncentrowanie się na identyfikowaniu naruszeń zabezpieczeń zanim spowodują one szkody.

## Jakie zadania wykonuje usługa ATA?
Usługa ATA wykrywa:

  - Zaawansowane zagrożenia ciągłe na wstępnym etapie przeprowadzenia ataku, zanim spowodują one szkody

  - Zagrożenia wewnętrzne

  Usługa ATA umożliwia również oddzielenie informacji istotnych od nieistotnych i skupienie się na najważniejszych problemach.

Aparat wykrywania usługi ATA wykorzystuje uczenie maszynowe, głęboką inspekcję pakietów w kontekście jednostki, analizę dzienników oraz informacje z usługi Active Directory do analizy zachowania użytkowników i jednostek.
Ten aparat wykrywania wykonuje głęboką analizę ruchu i za pomocą uczenia maszynowego tworzy mapę typowych działań, ruchu i użycia zasobów w organizacji. Następnie usługa ATA wyszukuje i sygnalizuje nietypowe zdarzenia. W tym celu jest używana technologia głębokiej inspekcji pakietów opracowana przez firmę Microsoft. Ta technologia umożliwia inspekcję pakietów w kontekście jednostki, zapewniającą głębszą analizę ruchu sieciowego, dlatego usługa ATA może analizować wszystkie poziomy ruchu sieciowego. Usługa ATA zbiera również istotne zdarzenia z systemów SIEM i kontrolerów domeny. 

Po analizie usługa ATA tworzy dynamiczny, nieustannie aktualizowany widok wszystkich osób, urządzeń i zasobów w organizacji. Korzystając z tego kompleksowego widoku, usługa ATA może wykrywać znane złośliwe ataki, takie jak Pass-the-Hash, Pass-the-Ticket, i rekonesans. Usługa ATA wyszukuje również nietypowe zachowania jednostek w sieci.  

Po wykryciu podejrzanego działania usługa ATA zgłasza alert, minimalizując liczbę fałszywych alarmów przy użyciu zaawansowanych algorytmów do agregacji i weryfikacji kontekstu.


## Jakie zagrożenia wyszukuje usługa ATA?

Usługa ATA wykrywa następujące fazy zaawansowanego ataku: rekonesans, przejęcie poświadczeń, penetracja sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne. Celem jest wykrycie zaawansowanych ataków i zagrożeń wewnętrznych zanim spowodują one szkody w organizacji.

Wykrywanie w każdej fazie obejmuje wyszukiwanie kilku typów podejrzanych działań właściwych dla danej fazy. Poszczególne podejrzane działania są powiązane z różnymi odmianami możliwych ataków.


### Rekonesans
Usługa ATA wykrywa wiele odmian rekonesansu. Na przykład podejrzane działanie **Rekonesans przy użyciu wyliczania kont** obejmuje próby ustalenia przez atakujących przy użyciu protokołu Kerberos, czy określone konto użytkownika istnieje, nawet jeśli to działanie nie zostało zarejestrowane jako zdarzenie na kontrolerze domeny.

### Przejęcie poświadczeń

Usługa ATA wykrywa przejęcie poświadczeń przy użyciu zarówno analizy behawioralnej opartej na uczeniu maszynowym, jak i wykrywania znanych złośliwych ataków i technik.  

Usługa ATA może wykrywać podejrzane działania, takie jak nietypowe logowania, nietypowy dostęp do zasobów i nietypowe godziny pracy. Dowolne z tych podejrzanych działań może wskazywać przejęcie poświadczeń.

Aby zapewnić ochronę przed przejęciem poświadczeń, usługa ATA wykrywa następujące znane złośliwe ataki i techniki:

 - **Atak siłowy** — osoby atakujące usiłują odgadnąć poświadczenia użytkowników, podejmując dla wielu użytkowników próby uwierzytelnienia przy użyciu różnych haseł. Osoby atakujące często używają złożonych algorytmów lub słowników, aby wypróbować maksymalną liczbę wartości dozwoloną w danym systemie.

- **Poufne konto ujawnione podczas uwierzytelniania przy użyciu zwykłego tekstu** — jeśli poświadczenia konta z wysokim poziomem uprawnień są wysyłane w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

- **Ujawnienie kont przez usługę podczas uwierzytelniania przy użyciu zwykłego tekstu** — jeśli usługa na komputerze wysyła poświadczenia wielu kont w postaci zwykłego tekstu, usługa ATA ostrzega użytkownika, aby umożliwić aktualizację konfiguracji komputera.

- **Podejrzane działania związane z kontem wystawionym jako przynęta** — konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu przechwytywania, identyfikowania i śledzenia złośliwych działań podejmowanych w celu użycia tych kont. Usługa ATA ostrzega o wszelkich działaniach związanych z tymi kontami wystawionymi jako przynęta.

### Penetracja sieci
Penetracja sieci polega na wykorzystaniu przez użytkowników poświadczeń umożliwiających dostęp do niektórych zasobów w celu uzyskania nieautoryzowanego dostępu do innych zasobów. Usługa ATA identyfikuje penetrację sieci tego typu przy użyciu zarówno analizy behawioralnej opartej na uczeniu maszynowym, jak i wykrywania znanych złośliwych ataków i technik.  

Usługa ATA wykrywa nietypowy dostęp do zasobów, gdy są używane nietypowe urządzenia i występują inne okoliczności świadczące o penetracji sieci. Ponadto usługa ATA może wykrywać penetrację sieci, rozpoznając między innymi następujące techniki penetracji sieci używane przez osoby atakujące:
- **Ataki typu Pass-the-Ticket** — osoby atakujące dokonują kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskują dostęp do innego komputera, personifikując jednostkę w sieci.
- **Ataki typu Pass-the-Hash** — osoby atakujące dokonują kradzieży skrótu NTLM jednostki, uwierzytelniają się za pomocą protokołu NTLM przy jego użyciu, a następnie uzyskują dostęp do zasobów w sieci, personifikując daną jednostkę.
- **Ataki typu Over-Pass-the-Hash** — uwierzytelniając się przy użyciu protokołu Kerberos i skradzionego skrótu NTLM, osoba atakująca uzyskuje prawidłowy bilet uprawniający do przyznania biletu protokołu Kerberos, a następnie używa tego biletu do uwierzytelnienia się jako prawidłowy użytkownik i uzyskania dostępu do zasobów w sieci.

### Podwyższenie poziomu uprawnień
Atak polegający na podwyższeniu poziomu uprawnień ma miejsce wtedy, gdy osoby atakujące usiłują podwyższyć poziom uprawnień i wykorzystać je wielokrotnie do przejęcia pełnej kontroli nad atakowanym środowiskiem. Usługa ATA wykrywa zarówno skuteczne, jak i nieskuteczne ataki polegające na podwyższeniu poziomu uprawnień. Usługa ATA używa analizy behawioralnej do wykrywania nietypowego zachowania kont z uprawnieniami. Usługa ATA wykrywa również znane złośliwe ataki i techniki, które są często używane do podwyższania poziomu uprawnień, na przykład:
- **Programy wykorzystujące lukę MS14-068 (sfałszowany element PAC)** — tego typu ataki polegają na umieszczeniu danych autoryzacji przez osoby atakujące w prawidłowym bilecie uprawniającym do przyznania biletu w formie sfałszowanego nagłówka autoryzacji. W przypadku tej techniki osoba atakująca uzyskuje uprawnienia, które nie zostały przyznane przez jej organizację.
- Używane są poświadczenia, które zostały przejęte lub przechwycone podczas penetracji sieci.

### Zdominowanie domeny
Zdominowanie domeny następuje wtedy, gdy osoby atakujące podejmują skuteczne lub nieskuteczne próby przejęcia pełnej kontroli nad atakowanym środowiskiem i zdominowania go. Usługa ATA wykrywa te próby, rozpoznając następujące znane techniki stosowane przez osoby atakujące:
- **Złośliwe oprogramowanie Skeleton Key** — osoba atakująca instaluje na kontrolerze domeny złośliwe oprogramowanie, które umożliwia jej uwierzytelnienie się jako dowolny użytkownik, nie ograniczając logowania autoryzowanych użytkowników.
- **Sfałszowany bilet uwierzytelniania Golden Ticket** — osoba atakująca dokonuje kradzieży poświadczeń KBTGT (bilet Golden Ticket protokołu Kerberos). Korzystając z tego biletu, osoba atakująca tworzy bilet uprawniający do przyznania biletu offline, którego następnie używa do uzyskania dostępu do zasobów w sieci.
- **Zdalne wykonywanie kodu** — osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny.


## Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](ata-architecture.md).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-useinstall-ata).

## Zobacz też
[Aby uzyskać pomoc techniczną dla usługi ATA, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO4-->


