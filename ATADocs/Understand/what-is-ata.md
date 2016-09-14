---
title: "Co to jest usługa Microsoft Advanced Threat Analytics (ATA)? | Microsoft ATA"
description: "Informacje dotyczące usługi Microsoft Advanced Threat Analytics (ATA) i wykrywanych przez nią podejrzanych działań"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: c2f8d642f5ab0927448730453873a5b6271b3d2b


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*


## Co to jest usługa Advanced Threat Analytics?
Usługa Advanced Threat Analytics (ATA) jest lokalną platformą, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych, ukierunkowanych ataków cybernetycznych oraz zagrożeniami wewnętrznymi.

## Działanie usługi ATA
Usługa ATA przyjmuje informacje z wielu źródeł danych, dzienników i zdarzeń w sieci, aby poznać zachowanie użytkowników i innych jednostek w organizacji oraz utworzyć na tej podstawie profil behawioralny.
Usługa ATA może odbierać zdarzenia i dzienniki z następujących źródeł:

-   Integracja rozwiązań SIEM
-   Przesyłanie dalej zdarzeń systemu Windows (WEF)

Ponadto usługa ATA korzysta z własnego aparatu do analizowania sieci w celu przechwytywania i analizowania ruchu sieciowego wielu protokołów (takich jak Kerberos, DNS, RPC, NTLM i inne) służących do uwierzytelniania, autoryzacji i gromadzenia informacji. Te informacje są zbierane przez usługę ATA przez:

-   Dublowanie portów z kontrolerów domeny i serwerów DNS do bramy usługi ATA
-   Wdrażanie bramy ATA Lightweight Gateway (LGW) bezpośrednio na kontrolerach domeny

Aby uzyskać więcej informacji, zobacz artykuł [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture).

Zobacz nasz film przedstawiający wprowadzenie do usługi ATA!
<iframe width="560" height="315" src="https://www.youtube.com/embed/0nA9FeTRZFw" frameborder="0" allowfullscreen></iframe>

## Jakie zadania wykonuje usługa ATA?

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
Usługa ATA wykrywa te podejrzane działania i udostępnia informacje w konsoli ATA, w jasny sposób przedstawiając sprawcę, przedmiot, czas i sposób działania. Jak widać, monitorując ten prosty, przyjazny dla użytkownika pulpit nawigacyjny, otrzymujemy alert dotyczący podejrzenia próby ataku typu Pass-the-Hash na komputerach Client 1 i Client 2 w sieci.

 ![Przykładowy ekran usługi ATA z alertem dotyczącym ataku typu Pass-the-Hash](media/sample screen pth.png)

**Nietypowe zachowanie** jest wykrywane przez usługę ATA dzięki analizie behawioralnej i wykorzystaniu uczenia maszynowego do wykrywania podejrzanych działań i nietypowych zachowań użytkowników i urządzeń w sieci, takich jak:

-   Nietypowe logowania
-   Nieznane zagrożenia
-   Udostępnianie haseł
-   Penetracja sieci


Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie usługa ATA zgłasza alert dotyczący dostępu użytkownika do 4 komputerów, z których ten użytkownik zwykle nie korzysta, co może być przyczyną alarmu.

 ![Przykładowy ekran usługi ATA z informacją o nietypowym zachowaniu](media/sample screen abnormal behavior.png) 

Usługa ATA wykrywa także **problemy dotyczące zabezpieczeń i czynniki ryzyka**, takie jak:

-   Zerwanie relacji zaufania
-   Słabe protokoły
-   Znane luki w zabezpieczeniach protokołów

Podejrzane działania tego typu można przeglądać na pulpicie nawigacyjnym usługi ATA. W poniższym przykładzie usługa ATA informuje, że istnieje zerwana relacja zaufania między komputerem w sieci a domeną.

  ![Przykładowy ekran usługi ATA przedstawiający zerwanie relacji zaufania](media/sample screen broken trust.png)


## Co dalej?

-   Aby uzyskać więcej informacji na temat zastosowań usługi ATA w Twojej sieci, zobacz [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Aby rozpocząć wdrażanie usługi ATA, zobacz [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-use/install-ata).

## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


