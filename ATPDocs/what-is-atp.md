---
title: Co to jest Azure Advanced Threat ochrony (ATP)? | Microsoft Docs
description: Wyjaśniono, co to jest Azure Advanced Threat ochrony (ATP) i jakiego rodzaju podejrzanych działań może wykryć
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446141"
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="what-is-azure-advanced-threat-protection"></a>Co to jest Azure Advanced Threat Protection?
Azure zaawansowane zagrożenia ochrony (ATP) to usługa w chmurze, która pomaga chronić środowiska hybrydowego przedsiębiorstwa z wielu rodzajów zaawansowanych ataków ukierunkowanych ataków i zagrożeń wewnętrznych.

## <a name="how-azure-atp-works"></a>Jak działa Azure ATP

Azure ATP wykorzystuje sieci własnościowych analizowania aparatu do przechwytywania i analizowania ruchu sieciowego na wiele protokołów (na przykład protokołu Kerberos, DNS, RPC, NTLM i inne) do uwierzytelniania, autoryzacji i zbierania informacji. Te informacje są zbierane przez Azure ATP za pośrednictwem albo:

-   Wdrażanie czujników Azure ATP bezpośrednio na kontrolerach domeny
-   Dublowanie z serwery DNS i kontrolery domeny czujnika autonomiczny Azure ATP portów

Azure ATP przyjmuje informacji z wielu-źródeł danych, takich jak dzienniki zdarzeń i w sieci, aby dowiedzieć się zachowania użytkowników i inne jednostki w organizacji i tworzenia profilu behawioralnej o nich.
Azure ATP mogą odbierać zdarzeń i dzienniki:

-   Integracja rozwiązań SIEM
-   Przesyłanie dalej zdarzeń systemu Windows (WEF)
-   Bezpośrednio z kolektora zdarzeń systemu Windows (dla czujnika)
-   RADIUS konta z sieci VPN


Aby uzyskać więcej informacji, w oparciu o architekturę Azure ATP, zobacz [architektura ATP Azure](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Do czego służy Azure ATP?

Technologia ATP Azure wykrywa wiele podejrzanych działań koncentrujących się na tym łańcuchu kill ataku przez kilka faz:

-   Rekonesans, podczas których osoby atakujące Zbierz informacje dotyczące sposobu środowiska są wbudowane i jakie różne zasoby są i którymi obiektami istnieje. Tworzenie one zazwyczaj ich planu dla następnej fazy ataku.
-   Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.
-   Podczas którego osoba atakująca przechwytuje informacje, dzięki czemu można wznowić ich kampanii przy użyciu różnych zestawów punktów wejścia, poświadczeń i technik zdominowanie domeny (trwałości). 

Te fazy ataku cybernetycznego są podobne i przewidywalne, niezależnie od tego, jakiego rodzaju firma jest atakowana ani jakiego typu informacje są celem ataku.
Azure ATP wyszukuje trzy rodzaje ataków: złośliwych ataków, nietypowe zachowanie i problemy z zabezpieczeniami i zagrożeń.

**Złośliwe ataki** są wykrywane sposób niejednoznaczny, jak również za pomocą analizy nietypowe zachowanie. Pełną listę typów znane ataki obejmuje:

-   Ataki typu Pass-the-Ticket (PtT)
-   Ataki typu Pass-the-Hash (PtH)
-   Ataki typu Overpass-the-Hash
-   Sfałszowany element PAC (MS14-068)
-   Sfałszowany bilet uwierzytelniania Golden Ticket
-   Złośliwe replikacji
-   Katalog usług — wyliczenie
-   Wyliczanie sesji SMB
-   Rekonesans DNS
-   Poziomy siłowymi 
-   Pionowy siłowymi
-   Wytrych
-   Nietypowego protokołu
-   Obniżenia poziomu szyfrowania
-   Zdalne wykonywanie kodu
-   Tworzenie złośliwe usługi


Azure ATP wykrywa tych podejrzanych działań i udostępnia informacje, w tym widzieć, która portalu obszaru roboczego Azure ATP co, kiedy i jak. Jak widać, monitorując ten prosty i przyjazny dla użytkownika pulpitu nawigacyjnego, zostanie wyświetlony alert Azure ATP podejrzewa, że ataku typu Pass--Ticket podjęto próbę na komputerach klienckich 1 i 2 klienta w sieci.

 ![Przykładowe Azure ATP ekranu pass--ticket](media/pass-the-ticket-sa.png)


Wykrywa także Azure ATP **problemy z zabezpieczeniami i ryzyka**, takie jak:

-   Słabe protokoły
-   Znane luki w zabezpieczeniach protokołów
-   [Penetracja sieci ścieżkę do kont poufnych](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Jakie zagrożenia Azure ATP szukać?

Azure ATP wykrywa następujące fazy zaawansowanego ataku: Rekonesans, przejęcie poświadczeń, penetracja sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne. Celem jest wykrycie zaawansowanych ataków i zagrożeń wewnętrznych, zanim będą mogły spowodować szkody w organizacji.

Wykrycie każdej fazy wywołuje kilka podejrzanych działań odpowiednich dla danej fazy, gdzie poszczególne podejrzane działania są powiązane z różnymi odmianami możliwych ataków.
Fazy te w łańcuchu kończenia którym Azure ATP zapewnia obecnie wykryć zostały wyróżnione na poniższej ilustracji:

![Azure ATP fokus na penetrację działania w ataku kill łańcucha](media/attack-kill-chain-small.jpg)


Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md) i [przewodnik podejrzanych działań Azure ATP](suspicious-activity-guide.md).

## <a name="whats-next"></a>Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań w sieci Azure ATP: [architektura Azure ATP](atp-architecture.md)

-   Aby rozpocząć wdrażanie ATP: [zainstalować ATP](install-atp-step1.md)


## <a name="see-also"></a>Zobacz też
- [Azure ATP — często zadawane pytania](atp-technical-faq.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)