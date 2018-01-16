---
title: "Advanced Threat Analytics zasobów i gotowości roadamp | Dokumentacja firmy Microsoft"
description: "Zawiera listę ATA zasobów, wideo, wprowadzenie, wdrażania i linki plan gotowości."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/15/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 33aec9dd89fc189144387e59c3b48b9d440936d2
ms.sourcegitcommit: 55f7ac32bcd4ac8edb8b8b3b47993bf96b9acce2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2018
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# <a name="ata-readiness-roadmap"></a>Plan gotowości usługi ATA 
Ten dokument zawiera plan gotowości, która pomoże rozpocząć pracę z Advanced Threat Analytics.

## <a name="understanding-ata"></a>Opis usługi ATA

Usługa Advanced Threat Analytics (ATA) jest lokalną platformą, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych, ukierunkowanych ataków cybernetycznych oraz zagrożeniami wewnętrznymi. Aby dowiedzieć się więcej na temat usługi ATA, należy użyć następujących zasobów:

- [Omówienie usługi ATA](https://aka.ms/ATAOverview)

- [Usługa ATA wprowadzenie wideo - krótki](https://aka.ms/ATAShort)

- [Wprowadzenie wideo usługi ATA — pełne](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Decyzji dotyczących wdrożenia

Usługa ATA składa się z Centrum usługi ATA, które można zainstalować na serwerze, i bram usługi ATA, które można zainstalować na oddzielnych komputerach lub przy użyciu bramy Lightweight bezpośrednio na kontrolerach domeny. Zanim można rozpocząć pracę, należy podjąć następujące decyzje dotyczące wdrażania:

|KONFIGURACJA|DECYZJI|
|----|----|
|Typ sprzętu|Fizycznych, wirtualnych, maszyny Wirtualnej Azure|
|Grupy roboczej lub domeny|Grupy roboczej, domeny|
|Ustalanie rozmiaru bramy|Pełne, lekkie bramy|
|Certyfikaty|Infrastruktura kluczy publicznych, z podpisem własnym|

Jeśli korzystasz z serwerów fizycznych, należy zaplanować pojemność. Można uzyskać pomoc od narzędzie ustalania wielkości, aby przydzielić miejsce dla usługi ATA:

[Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizing) — narzędzia do określania rozmiaru automatyzuje kolekcji ilość ruchu sieciowego, usługa ATA wymaga. Możliwość obsługi i zalecenia dotyczące zasobów automatycznie zapewnia dla Centrum usługi ATA i bram ATA Lightweight Gateway.

[Planowanie pojemności usługi ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/ata-capacity-planning)

## <a name="deploy-ata"></a>Wdrażanie usługi ATA

Te zasoby będą pomóc pobranie i zainstalowanie Centrum usługi ATA, połączyć z usługą Active Directory, Pobierz pakiet bramy usługi ATA, Konfigurowanie zbierania zdarzeń i opcjonalnie zintegrować z serwera VPN i skonfiguruj wykluczenia i kont wystawionych jako przynęta.

[Pobierz usługę ATA](http://aka.ms/ataeval) — przed wdrożeniem usługi ATA, jeśli nie utworzono decyzji w celu zakupu usługi ATA, możesz pobrać wersję ewaluacyjną. 

[Fazy weryfikacji Koncepcji ATA podręcznikowym](http://aka.ms/atapoc) — przewodnik wszystkich kroków wymaganych w celu pomyślnego wdrożenia usługi ATA fazy weryfikacji Koncepcji.

[Wdrożenie usługi ATA wideo](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) — ten klip wideo zawiera omówienie wdrożenia usługi ATA czynności w mniej niż 10 minut.

## <a name="ata-settings"></a>Ustawienia usługi ATA

Podstawowe ustawienia niezbędne w usłudze ATA są skonfigurowane jako część Kreatora instalacji. Istnieje jednak wiele innych ustawień, które można skonfigurować w celu dostosowania ATA wchodzące wykryć większej dokładności dla danego środowiska, takich jak integracji SIEM a ustawień inspekcji.

[Ustawienia inspekcji](https://aka.ms/ataauditingblog) — inspekcji Twojej kondycji kontrolera domeny, przed i po wdrożeniu usługi ATA.

[Dokumentacja ogólna usługi ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Praca z usługi ATA

Po skonfigurowaniu i uruchomieniu usługi ATA będzie mogła wyświetlać podejrzanych działań wykrytych na osi czasu ataków. Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można również sprawdzić ważność przypisaną do poszczególnych działań. Sprawdź poszczególne podejrzane działania przez przechodzenie jednostek (komputerów, urządzeń, użytkowników) otwieranie stron ich profilu, które dostarczają więcej informacji. Te zasoby będą pomocne podczas pracy z podejrzanych działań usługi ATA:

[Podręcznika dotyczącego podejrzanego działania usługa ATA](http://aka.ms/ataplaybook) — w tym artykule przedstawiono ataku technik kradzieży poświadczeń, za pomocą narzędzi research łatwo dostępne w Internecie. W każdym punkcie ataku widać, jak usługa ATA pomaga uzyskać wgląd w tych zagrożeń.

[Przewodnik po podejrzanych działań usługi ATA](http://aka.ms/atasaguide)



## <a name="security-best-practices"></a>Najlepsze rozwiązania

[Najlepsze rozwiązania w zakresie usługi ATA](https://aka.ms/atasecbestpractices) — najlepsze rozwiązania dotyczące zabezpieczania usługi ATA.

[Często zadawane pytania dotyczące usługi ATA](http://aka.ms/atafaq) — ten artykuł zawiera listę często zadawanych pytań dotyczących usługi ATA oraz wskazówki i odpowiedzi.

## <a name="additional-resources"></a>Dodatkowe zasoby

[Strona 9 kanału zabezpieczeń firmy Microsoft](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zasoby społeczności

[Blog usługi ATA](https://aka.ms/ATABlog)
[społeczności ATA](https://aka.ms/ATACommunity)
[Prześlij opinię dotyczącą usługi ATA](https://aka.ms/ATAUserVoice)
