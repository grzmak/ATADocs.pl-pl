---
title: "Co to jest usługa Microsoft Advanced Threat Analytics (ATA)? | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące usługi Microsoft Advanced Threat Analytics (ATA) i wykrywanych przez nią podejrzanych działań"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1afaf258198c1b18aca5cc2e4be6774600f72a73
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/09/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="what-is-advanced-threat-analytics"></a>Co to jest usługa Advanced Threat Analytics?
Usługa Advanced Threat Analytics (ATA) jest lokalną platformą, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych, ukierunkowanych ataków cybernetycznych oraz zagrożeniami wewnętrznymi.

## <a name="how-ata-works"></a>Działanie usługi ATA

Usługa ATA korzysta z własnego aparatu do analizowania sieci w celu przechwytywania i analizowania ruchu sieciowego wielu protokołów (takich jak Kerberos, DNS, RPC, NTLM i inne) służących do uwierzytelniania, autoryzacji i zbierania informacji. Te informacje są zbierane przez usługę ATA przez:

-   Dublowanie portów z kontrolerów domeny i serwerów DNS do bramy usługi ATA i/lub
-   Wdrażanie uproszczonej bramy usługi ATA (LGW) bezpośrednio na kontrolerach domeny

Usługa ATA uzyskuje informacje z wielu źródeł danych, takich jak dzienniki i zdarzenia w sieci, aby poznać zachowanie użytkowników i innych jednostek w organizacji oraz utworzyć na tej podstawie profil behawioralny.
Usługa ATA może odbierać zdarzenia i dzienniki z następujących źródeł:

-   Integracja rozwiązań SIEM
-   Przesyłanie dalej zdarzeń systemu Windows (WEF)
-   Bezpośrednio z kolektora zdarzeń systemu Windows (w przypadku bramy uproszczonej)


Aby uzyskać więcej informacji, zobacz artykuł [Architektura usługi ATA](ata-architecture.md).

## <a name="what-does-ata-do"></a>Jakie zadania wykonuje usługa ATA?

Technologia ATA wykrywa wiele podejrzanych działań, skupiając się na poszczególnych fazach ataku cybernetycznego typu kill chain, takich jak:

-   Rekonesans, w którym osoby atakujące zbierają informacje dotyczące konstrukcji środowiska oraz istniejących zasobów i jednostek, tworząc ogólny plan następnych faz ataku.
-   Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.
-   Zdominowanie domeny (trwałość), kiedy osoba atakująca przechwytuje informacje pozwalające na wznowienie kampanii przy użyciu różnorodnego zestawu punktów wejścia, poświadczeń i technik. 

Te fazy ataku cybernetycznego są podobne i przewidywalne, niezależnie od tego, jakiego rodzaju firma jest atakowana ani jakiego typu informacje są celem ataku.
Usługa ATA wyszukuje trzy główne typy ataków: złośliwe ataki, nietypowe zachowanie oraz problemy i czynniki ryzyka związane z zabezpieczeniami.

**Złośliwe ataki** są wykrywane w sposób deterministyczny, przez wyszukiwanie pełnej listy znanych typów ataków, która obejmuje:

-   Ataki typu Pass-the-Ticket (PtT)
-   Ataki typu Pass-the-Hash (PtH)
-   Ataki typu Overpass-the-Hash
-   Sfałszowany element PAC (MS14-068)
-   Sfałszowany bilet uwierzytelniania Golden Ticket
-   Złośliwe żądania replikacji
-   Rekonesans
-   Atak siłowy
-   Zdalne wykonywanie kodu

Aby uzyskać pełną listę wykrywanych zagrożeń wraz z opisami, zobacz artykuł [Jakie podejrzane działania może wykryć usługa ATA?](ata-threats.md)
Usługa ATA wykrywa te podejrzane działania i udostępnia informacje w konsoli ATA, w jasny sposób przedstawiając sprawcę, przedmiot, czas i sposób działania. Jak widać, monitorując ten prosty, przyjazny dla użytkownika pulpit nawigacyjny, otrzymujemy alert dotyczący podejrzenia próby ataku typu Pass-the-Ticket na komputerach Client 1 i Client 2 w sieci.

 ![Przykładowy ekran usługi ATA z alertem dotyczącym ataku typu Pass-the-Ticket](media/pass_the_ticket_sa.png)

**Nietypowe zachowanie** jest wykrywane przez usługę ATA dzięki analizie behawioralnej i wykorzystaniu uczenia maszynowego do wykrywania podejrzanych działań i nietypowych zachowań użytkowników i urządzeń w sieci, takich jak:

-   Nietypowe logowania
-   Nieznane zagrożenia
-   Udostępnianie haseł
-   Penetracja sieci
-   Modyfikacja wrażliwych grup


Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie usługa ATA zgłasza alert dotyczący dostępu użytkownika do 4 komputerów, z których ten użytkownik zwykle nie korzysta, co może być przyczyną alarmu.

 ![Przykładowy ekran usługi ATA z informacją o nietypowym zachowaniu](media/abnormal-behavior-sa.png) 

Usługa ATA wykrywa także **problemy dotyczące zabezpieczeń i czynniki ryzyka**, takie jak:

-   Zerwanie relacji zaufania
-   Słabe protokoły
-   Znane luki w zabezpieczeniach protokołów

Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie usługa ATA informuje, że istnieje zerwana relacja zaufania między komputerem w sieci a domeną.

  ![Przykładowy ekran usługi ATA przedstawiający zerwanie relacji zaufania](media/broken-trust-sa.png)


## <a name="known-issues"></a>Znane problemy

- W przypadku aktualizacji do usługi ATA 1.7 i następującej natychmiast po niej aktualizacji do usługi ATA 1.8, bez wcześniejszego zaktualizowania bram usługi ATA, nie będzie można przeprowadzić migracji do usługi ATA 1.8. Należy najpierw zaktualizować wszystkie bramy do wersji 1.7.1 lub 1.7.2 przed aktualizowaniem centrum usługi ATA do wersji 1.8.

- Jeśli wybierzesz opcję pełnej migracji, może ona potrwać bardzo długo w zależności od rozmiaru bazy danych. Podczas wybierania opcji migracji jest wyświetlany szacowany czas — należy zwrócić na niego uwagę przed podjęciem decyzji. 


## <a name="whats-next"></a>Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](ata-architecture.md).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](install-ata-step1.md).

## <a name="related-videos"></a>Powiązane pliki wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)
- [Przegląd wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Zobacz też
[Podręcznika dotyczącego podejrzanego działania usługa ATA](http://aka.ms/ataplaybook)
[zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
