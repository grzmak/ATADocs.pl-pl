---
title: Advanced Threat Analytics zasobów i gotowości roadamp | Dokumentacja firmy Microsoft
description: Zawiera listę ATA zasoby, materiały wideo, wprowadzenie, wdrażania i linki plan gotowości.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 39451c20d934c0d3e49f8790dc55169a230e238c
ms.sourcegitcommit: a9b8bc26d3cb5645f21a68dc192b4acef8f54895
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2018
ms.locfileid: "39064053"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*

# <a name="ata-readiness-roadmap"></a>Plan gotowości usługi ATA 
Ten dokument zawiera mapę gotowości, która pomoże Ci rozpocząć pracę z usługi Advanced Threat Analytics.

## <a name="understanding-ata"></a>Opis usługi ATA

Usługa Advanced Threat Analytics (ATA) jest lokalną platformą, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych, ukierunkowanych ataków cybernetycznych oraz zagrożeniami wewnętrznymi. Użyj następujących zasobów, aby dowiedzieć się więcej na temat usługi ATA:

- [Omówienie usługi ATA](what-is-ata.md)

- [Usługa ATA wideo z wprowadzeniem — krótki](https://aka.ms/ATAShort)

- [Usługa ATA klip wideo z wprowadzeniem — pełny](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Decyzji dotyczących wdrożenia

Usługa ATA składa się z Centrum usługi ATA, które można zainstalować na serwerze, i bram usługi ATA, które można zainstalować na oddzielnych komputerach lub przy użyciu bramy uproszczonej bezpośrednio na kontrolerach domeny. Zanim można rozpocząć pracę, należy podjąć następujące decyzje dotyczące wdrażania:

|KONFIGURACJA|DECYZJA|
|----|----|
|Typ sprzętu|Fizycznych, wirtualnych i maszyn wirtualnych platformy Azure|
|Grupie roboczej lub domenie|Domena, grupy roboczej|
|Ustalanie rozmiaru bramy|Pełne bramy uproszczonej bramy|
|Certyfikaty|Infrastruktury kluczy publicznych z podpisem własnym|

Jeśli używasz serwerów fizycznych należy zaplanować pojemność. Możesz uzyskać pomoc przy użyciu narzędzia określania rozmiaru do alokowania miejsca dla usługi ATA:

[Narzędzia do określania rozmiaru usługi ATA](ata-capacity-planning.md) — narzędzia do określania rozmiaru automatyzuje zbiór ilość ruchu sieciowego w ATA potrzebuje. Zalecenia dotyczące zasobów i możliwości obsługi automatycznie zapewnia Centrum usługi ATA i uproszczonych bram usługi ATA.

[Planowanie pojemności usługi ATA](ata-capacity-planning.md)

## <a name="deploy-ata"></a>Wdrożenia usługi ATA

Te zasoby pomoże pobieranie i instalowanie Centrum usługi ATA, nawiązać połączenie z usługi Active Directory, pobieranie pakietu bramy usługi ATA, Konfigurowanie zbierania zdarzeń i opcjonalnie zintegrować z sieci VPN i konfigurowanie konta wystawione jako przynęta i wykluczenia.

[Pobierz usługę ATA](http://aka.ms/ataeval) — przed wdrożeniem usługi ATA, jeśli nie utworzono decyzję o zakupie usługi ATA, możesz pobrać wersję ewaluacyjną. 

[Podręcznik Prototypu ATA](http://aka.ms/atapoc) — Przewodnik po wszystkich kroków wymaganych w celu pomyślnego wdrożenia weryfikacji Koncepcji usługi ATA.

[Wdrożenie usługi ATA wideo](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) — to wideo zawiera omówienie wdrożenia usługi ATA kroków w mniej niż 10 minut.

## <a name="ata-settings"></a>Ustawienia usługi ATA

Podstawowe ustawienia niezbędne w usłudze ATA są konfigurowane jako część Kreatora instalacji. Jednak istnieje szereg innych ustawień, które można skonfigurować w celu dostosowania ATA wprowadzić bardziej precyzyjne dla danego środowiska, takie jak integracja rozwiązania SIEM wykrywania, które ustawienia inspekcji.

[Ustawienia inspekcji](https://aka.ms/ataauditingblog) — Inspekcja usługi kondycji kontrolera domeny, przed i po wdrożeniu usługi ATA.

[Ogólna dokumentacja usługi ATA](https://docs.microsoft.com/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Praca z usługi ATA

Po skonfigurowaniu i uruchomieniu usługi ATA będzie można wyświetlić podejrzanych działań, które są wykrywane na osi czasu ataków. Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można również sprawdzić ważność przypisaną do poszczególnych działań. Badanie każdego podejrzanego działania, przechodzenie jednostek (komputerów, urządzeń, użytkowników) aby otworzyć ich strony profilów, które zawierają więcej informacji. Te zasoby ułatwiają pracę z podejrzanych działań usługi ATA:

[Podręcznik dotyczący podejrzanych działań usługa ATA](http://aka.ms/ataplaybook) — w tym artykule opisano przy użyciu technik ataku kradzieży poświadczeń przy użyciu łatwo dostępnych narzędzi badawczych w Internecie. W każdym punkcie ataku zobaczysz, jak usługa ATA pomaga uzyskać wgląd w te zagrożenia.

[Przewodnik po podejrzanych działań usługi ATA](suspicious-activity-guide.md)



## <a name="security-best-practices"></a>Najlepsze rozwiązania dotyczące zabezpieczeń

[Najlepsze rozwiązania ATA](https://aka.ms/atasecbestpractices) — najlepsze rozwiązania dotyczące zabezpieczania usługi ATA.

[Często zadawane pytania dotyczące usługi ATA](ata-technical-faq.md) — ten artykuł zawiera listę często zadawanych pytań dotyczących usługi ATA oraz wskazówki i odpowiedzi.

## <a name="additional-resources"></a>Dodatkowe zasoby

[Strona firmy Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zasoby społeczności

[Blog usługi ATA](https://aka.ms/ATABlog)
[społeczności usługi ATA](https://aka.ms/ATACommunity)
[opinią na temat usługi ATA](https://aka.ms/ATAUserVoice)
