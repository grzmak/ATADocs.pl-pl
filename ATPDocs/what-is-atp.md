---
title: Co to jest Azure Advanced Threat Protection (ATP)? | Microsoft Docs
description: Wyjaśnia, co to jest Azure Advanced Threat Protection (ATP) i jakiego rodzaju podejrzane działania może wykryć
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
ms.openlocfilehash: c889fc070ffaf79a89c072d83edf6cc6f1cd0413
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734809"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="what-is-azure-advanced-threat-protection"></a>Co to jest Zaawansowana ochrona przed zagrożeniami dla platformy Azure?
Zaawansowana ochrona przed zagrożeniami na platformie Azure to usługa w chmurze zapewniająca ochronę środowisk hybrydowych przedsiębiorstwa przed wieloma typami zaawansowanych, ukierunkowanych cyberataków i zagrożeniami wewnętrznymi.

## <a name="how-azure-atp-works"></a>Sposób działania usługi Azure ATP

Narzędzie Azure ATP korzysta z własnego aparatu do przechwytywania i analizowania ruchu sieciowego wielu protokołów (takich jak Kerberos, DNS, RPC, NTLM i inne) do analizowania sieci do uwierzytelniania, autoryzacji i gromadzenia informacji. Te informacje są zbierane przez narzędzia Azure ATP usługę:

-   Wdrażanie usługi Azure ATP czujników bezpośrednio na kontrolerach domeny
-   Dublowanie portów z kontrolerów domeny i serwerów DNS do usługi Azure ATP czujnik autonomiczny

Narzędzie Azure ATP przyjmuje informacje z wielu źródeł danych, takie jak dzienniki i zdarzenia w sieci, aby poznać zachowanie użytkowników i innych podmiotów w organizacji oraz utworzyć tej podstawie profil behawioralny.
Narzędzie Azure ATP może odbierać zdarzenia i dzienniki z:

-   Integracja rozwiązań SIEM
-   Przesyłanie dalej zdarzeń systemu Windows (WEF)
-   Bezpośrednio z kolektora zdarzeń Windows (dla czujnika)
-   RADIUS konta z wirtualnych sieci prywatnych


Aby uzyskać więcej informacji na temat architektury usługi Azure ATP, zobacz [architektura zaawansowanej ochrony przed zagrożeniami platformy](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Do czego służy narzędzia Azure ATP

Technologii Azure ATP wykrywa wiele podejrzanych działań, skupiając się na poszczególnych fazach ataku cybernetycznego ataku typu kill chain, takich jak:

-   Są jaki różne zasoby Rekonesans, podczas którego osoby atakujące zbierają informacje, w jaki zaprojektowano środowisko i którymi obiektami istnieje. Kompilowanie one zazwyczaj ogólny plan następnych faz ataku.
-   Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.
-   W którym osoba atakująca przechwytuje informacje pozwalające na wznowienie kampanii przy użyciu różnych zestawów punkty wejścia, poświadczeń i technik zdominowanie domeny (trwałość). 

Te fazy ataku cybernetycznego są podobne i przewidywalne, niezależnie od tego, jakiego rodzaju firma jest atakowana ani jakiego typu informacje są celem ataku.
Narzędzie Azure ATP wyszukuje trzy główne typy ataków: złośliwe ataki, nietypowe zachowanie oraz problemy z zabezpieczeniami i ryzyka.

**Złośliwe ataki** są wykrywane sposób deterministyczny, jak również za pośrednictwem analizy nietypowe zachowanie. Zawiera pełną listę znanych typów ataków:

-   Ataki typu Pass-the-Ticket (PtT)
-   Ataki typu Pass-the-Hash (PtH)
-   Ataki typu Overpass-the-Hash
-   Sfałszowany element PAC (MS14-068)
-   Sfałszowany bilet uwierzytelniania Golden Ticket
    -   czas anomoly
    -   Konto nieistniejącej — nowe
-   Złośliwa replikacja
-   Wyliczania usług katalogowych
-   Wyliczanie sesji SMB
-   Rekonesans DNS
-   Poziomy atak Siłowy 
-   Pionowe atak Siłowy
-   Wytrych
-   Nietypowego protokołu
-   Obniżenie poziomu szyfrowania
-   Zdalne wykonywanie kodu
-   Tworzenie usługi złośliwy
-   Podwyższanie poziomu kontrolera domeny podejrzane (potencjalny atak DCShadow) — nowe
-   Podejrzana replikacja żądania (potencjalny atak DCShadow) — nowe
-   VPN 


Narzędzie Azure ATP wykrywa te podejrzane działania i udostępnia informacje w portalu obszaru roboczego usługi Azure ATP, przedstawiając sprawcę, przedmiot, czas i sposób. Jak widać, monitorując ten prosty, przyjazny dla użytkownika pulpit nawigacyjny, zostanie wyświetlony alert usługi Azure ATP podejrzenia, że atak Pass--Ticket podjęto próbę na komputerach Client 1 i Client 2 w sieci.

 ![Przykładowe narzędzie Azure ATP ekranu pass--ticket](media/pass-the-ticket-sa.png)


Narzędzie Azure ATP wykrywa także **problemy z zabezpieczeniami i ryzyka**, w tym:

-   Słabe protokoły
-   Znane luki w zabezpieczeniach protokołów
-   [Ścieżki ruchu poprzecznego do wrażliwych kont](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Jakie zagrożenia usługi Azure ATP szukać?

Narzędzie Azure ATP udostępnia następujące fazy zaawansowanego ataku: Rekonesans, przejęcie poświadczeń, penetracji sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne. Celem jest wykrycie zaawansowanych ataków i zagrożeń wewnętrznych, zanim będą mogły spowodować szkody w organizacji.

Wykrycie każdej fazy wywołuje kilka podejrzanych działań odpowiednich dla danej fazy, gdzie poszczególne podejrzane działania są powiązane z różnymi odmianami możliwych ataków.
Te fazy ataku typu kill Chain, w których usługi Azure ATP aktualnie obsługuje wykrywanie, zostały wyróżnione na poniższej ilustracji:

![Usługa Azure ATP skupić się na penetracji sieci w ataku typu kill chain](media/attack-kill-chain-small.jpg)


Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md) i [Przewodnik po podejrzanych działaniach usługi Azure ATP](suspicious-activity-guide.md).

## <a name="whats-next"></a>Co dalej?

-   Aby uzyskać więcej informacji na temat jak narzędzia Azure ATP dopasowuje się do sieci: [architektury usługi Azure ATP](atp-architecture.md)

-   Aby rozpocząć wdrażanie zaawansowanej ochrony przed zagrożeniami: [zainstalować zaawansowanej ochrony przed zagrożeniami](install-atp-step1.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzie Azure ATP — często zadawane pytania](atp-technical-faq.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)