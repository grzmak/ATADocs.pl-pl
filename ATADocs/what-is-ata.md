---
title: Co to jest usługa Microsoft Advanced Threat Analytics (ATA)? | Microsoft Docs
description: Informacje dotyczące usługi Microsoft Advanced Threat Analytics (ATA) i wykrywanych przez nią podejrzanych działań
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/24/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: adca31a6767031fce19f1a14bf8031c911717c9c
ms.sourcegitcommit: 63a36cd96aec30e90dd77bee1d0bddb13d2c4c64
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2018
ms.locfileid: "39227244"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="what-is-advanced-threat-analytics"></a>Co to jest usługa Advanced Threat Analytics?
Usługa Advanced Threat Analytics (ATA) jest lokalną platformą, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych, ukierunkowanych ataków cybernetycznych oraz zagrożeniami wewnętrznymi.

## <a name="how-ata-works"></a>Działanie usługi ATA

Usługa ATA korzysta z własnego aparatu do przechwytywania i analizowania ruchu sieciowego wielu protokołów (takich jak Kerberos, DNS, RPC, NTLM i inne) do analizowania sieci do uwierzytelniania, autoryzacji i gromadzenia informacji. Te informacje są zbierane przez usługę ATA przez:

-   Dublowanie portów z kontrolerów domeny i serwerów DNS do bramy usługi ATA i/lub
-   Wdrażanie uproszczonej bramy usługi ATA (LGW) bezpośrednio na kontrolerach domeny

Usługa ATA przyjmuje informacje z wielu źródeł danych, takie jak dzienniki i zdarzenia w sieci, aby poznać zachowanie użytkowników i innych jednostek w organizacji i tworzy na tej podstawie profil behawioralny.
Usługa ATA może odbierać zdarzenia i dzienniki z następujących źródeł:

-   Integracja rozwiązań SIEM
-   Przesyłanie dalej zdarzeń systemu Windows (WEF)
-   Bezpośrednio z kolektora zdarzeń systemu Windows (w przypadku bramy uproszczonej)


Aby uzyskać więcej informacji na temat architektury usługi ATA, zobacz [Architektura usługi ATA](ata-architecture.md).

## <a name="what-does-ata-do"></a>Jakie zadania wykonuje usługa ATA?

Technologia ATA wykrywa wiele podejrzanych działań, skupiając się na poszczególnych fazach ataku cybernetycznego typu kill chain, takich jak:

-   Są jaki różne zasoby Rekonesans, podczas którego osoby atakujące zbierają informacje, w jaki zaprojektowano środowisko i którymi obiektami istnieje. Zazwyczaj jest to, gdy osoby atakujące Tworzenie planów dla ich następnych faz ataku.
-   Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.
-   W którym osoba atakująca przechwytuje informacje pozwalające im na wznowienie kampanii przy użyciu różnych zestawów punkty wejścia, poświadczeń i technik zdominowanie domeny (trwałość). 

Te fazy ataku cybernetycznego są podobne i przewidywalne, niezależnie od tego, jakiego rodzaju firma jest atakowana ani jakiego typu informacje są celem ataku.
Usługa ATA wyszukuje trzy główne typy ataków: złośliwe ataki, nietypowe zachowanie oraz problemy z zabezpieczeniami i ryzyka.

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

Aby uzyskać pełną listę wykrywanych zagrożeń wraz z opisami, zobacz [jakie podejrzane działania może wykryć usługa ATA?](ata-threats.md). 

Usługa ATA wykrywa te podejrzane działania i udostępnia informacje w konsoli ATA, w jasny sposób przedstawiając sprawcę, przedmiot, czas i sposób działania. Jak widać, monitorując ten prosty, przyjazny dla użytkownika pulpit nawigacyjny, użytkownik jest podejrzenia, że podjęto próbę ataku Pass--Ticket na komputerach Client 1 i Client 2 w sieci.

 ![Przykładowy ekran usługi ATA z alertem dotyczącym ataku typu Pass-the-Ticket](media/pass_the_ticket_sa.png)

**Nietypowe zachowanie** jest wykrywane przez usługę ATA dzięki analizie behawioralnej i wykorzystaniu uczenia maszynowego do wykrywania podejrzanych działań i nietypowych zachowań użytkowników i urządzeń w sieci, takich jak:

-   Nietypowe logowania
-   Nieznane zagrożenia
-   Udostępnianie haseł
-   Penetracja sieci
-   Modyfikacja wrażliwych grup


Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie Usługa ATA ostrzega, gdy użytkownik uzyskuje dostęp do czterech komputerów, które normalnie nie są dostępne przez tego użytkownika, który może być przyczyną alarmu.

 ![Przykładowy ekran usługi ATA z informacją o nietypowym zachowaniu](media/abnormal-behavior-sa.png) 

Usługa ATA wykrywa także **problemy dotyczące zabezpieczeń i czynniki ryzyka**, takie jak:

-   Zerwanie relacji zaufania
-   Słabe protokoły
-   Znane luki w zabezpieczeniach protokołów

Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie usługa ATA informuje, że istnieje zerwana relacja zaufania między komputerem w sieci a domeną.

  ![Przykładowy ekran usługi ATA przedstawiający zerwanie relacji zaufania](media/broken-trust-sa.png)


## <a name="known-issues"></a>Znane problemy

- Jeżeli zostanie zaktualizowany do wersji 1.7 usługi ATA i od razu do usługi ATA 1.8, bez wcześniejszego zaktualizowania bram usługi ATA, nie można migrować do usługi ATA 1.8. Należy najpierw zaktualizować wszystkie bramy do wersji 1.7.1 lub 1.7.2 przed aktualizowaniem centrum usługi ATA do wersji 1.8.

- Jeśli wybierzesz opcję pełnej migracji, może ona potrwać bardzo długo w zależności od rozmiaru bazy danych. Podczas wybierania opcji migracji jest wyświetlany szacowany czas — należy zwrócić na niego uwagę przed podjęciem decyzji, którą opcję wybrać. 


## <a name="whats-next"></a>Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](ata-architecture.md).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](install-ata-step1.md).

## <a name="related-videos"></a>Pokrewne wideo
- [Dołączenie do społeczności zabezpieczeń](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Zobacz też
[Podręcznik dotyczący podejrzanych działań usługa ATA](http://aka.ms/ataplaybook)
[zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
