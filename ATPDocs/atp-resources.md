---
title: Lista przydatne zasoby usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera listę przydatne zasoby dla usługi Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 029077455f9b2800984065a10c3e221e62d7c606
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783155"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="azure-atp-readiness-guide"></a>Podręcznik gotowości usługi Azure ATP

Ten artykuł zawiera mapę gotowości, która udostępnia listę zasobów, które ułatwi rozpoczęcie korzystania z usługi Azure Advanced Threat Protection. 

## <a name="understanding-azure-atp"></a>Omówienie usługi Azure ATP

Azure zaawansowanych Threat Protection (ATP) to usługa w chmurze, która ułatwia identyfikowanie i Chroń swoje przedsiębiorstwo przed wieloma rodzajami zaawansowanych ukierunkowanych cyberataków i zagrożeniami wewnętrznymi. Aby dowiedzieć się więcej na temat usługi Azure ATP: 
- [Omówienie usługi Azure ATP](what-is-atp.md)
- [Usługa Azure ATP klip wideo z wprowadzeniem (25 minut) — pełny](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Wideo szczegółowe omówienie usługi Azure ATP (75 minut) — pełny](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Decyzji dotyczących wdrożenia

Narzędzie Azure ATP składa się z usługą w chmurze znajdującymi się na platformie Azure i zintegrowane czujniki, które mogą być instalowane na kontrolerze domeny lub autonomiczny czujników na dedykowanych serwerach. Przed zagłębieniem się narzędzia Azure ATP uruchomiona, jest należy wybrać typ czujniki, że najlepiej własnych wdrożenia i potrzeb. Azure zaawansowanej ochrony przed zagrożeniami zintegrowane czujników (czujników narzędzia Azure ATP) zapewniają większe bezpieczeństwo, obniżyć koszty operacyjne i łatwiejsze wdrażanie niż czujników autonomiczne narzędzia Azure ATP. Azure ATP autonomiczny czujników wymagają sprzętu fizycznego, czynności konfiguracyjne additionl i heavier koszty operacyjne. <br>Jeśli używasz serwerów fizycznych, planowania pojemności ma kluczowe znaczenie. Możesz uzyskać pomoc przy użyciu narzędzia rozmiaru do alokowania miejsca dla Twojego czujniki: 
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool) — narzędzia do określania rozmiaru automatyzuje zbiór natężenia ruchu, które monitoruje usługi Azure ATP. Automatycznie zapewnia wsparcie dla zasobów and recommendations for i czujniki. 
- [Wytyczne dotyczące planowania pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Wdrażanie usługi Azure ATP

Te zasoby ułatwia konfigurowanie usługi Azure ATP, nawiązać połączenie z usługi Active Directory, pobieranie pakietu czujnika, Konfigurowanie zbierania zdarzeń i opcjonalnie zintegrować z sieci VPN i skonfigurować konta wystawione jako przynęta i wykluczenia. 
- [Wypróbuj usługi Azure ATP (część pakietu EMS E5)](http://aka.ms/aatptrial) wersja próbna jest ważna przez 90 dni.
- [Usługa Azure ATP Konfigurowanie](install-atp-step1.md) wdrożenia usługi Azure ATP w danym środowisku, wykonaj następujące kroki.
- [Integracja usługi Azure ATP z usługą Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Ustawienia usługi Azure ATP

Podstawowe ustawienia niezbędne w przypadku narzędzia Azure ATP są skonfigurowane, podczas tworzenia obszaru roboczego. Istnieje jednak kilka dodatkowych ustawień, które można skonfigurować w usłudze Azure ATP, bardziej precyzyjne dla danego środowiska, takie jak integracja sieci VPN, SAM wykrywania upewnij wymagane uprawnienia i zaawansowane ustawienia zasad inspekcji. 

- [Integracja zestawów VPN](install-atp-step6-vpn.md)
- [SAM-R wymagane uprawnienia](install-atp-step8-samr.md)
- [Ustawienia zasad inspekcji](atp-advanced-audit-policy.md) — Inspekcja usługi kondycji kontrolera domeny, przed i po wdrożeniu zaawansowanej ochrony przed zagrożeniami. 

## <a name="work-with-azure-atp"></a>Praca z usługi Azure ATP

Po narzędzia Azure ATP jest uruchomiony i działa, wyświetlanie alertów zabezpieczeń na osi czasu aktywności portalu usługi Azure ATP. Oś czasu działania jest domyślna strona docelowa po zalogowaniu się do portalu usługi Azure ATP. Domyślnie wszystkie Otwórz alerty zabezpieczeń są wyświetlane na osi czasu ataków. Można również sprawdzić ważność przypisaną do każdego alertu. Badanie każdego alertu, przechodzenie do szczegółów do jednostek (komputerów, urządzeń, użytkowników) aby otworzyć ich strony profilu z większą ilością informacji. Te zasoby ułatwiają korzystanie z alertów zabezpieczeń usługi Azure ATP: 

- [Podręcznik usługi Azure ATP zabezpieczeń alertu](suspicious-activity-guide.md) Dowiedz się, jak klasyfikowanie i wykonaj kolejne kroki z usługi wykrywania usługi Azure ATP.
- [Tag grupy jako poufny](sensitive-accounts.md) wgląd w widoczności poświadczeń na grupach zabezpieczeń poufnych.

## <a name="security-best-practices"></a>Najlepsze rozwiązania dotyczące zabezpieczeń

- [Usługa Azure ATP — często zadawane pytania](atp-technical-faq.md) — ten artykuł zawiera listę często zadawanych pytań dotyczących usługi Azure ATP oraz wskazówki i odpowiedzi. 

## <a name="community-resources"></a>Zasoby społeczności

Blog: [blogu Azure ATP](https://aka.ms/aatpblog)

Społeczność publicznej: [społeczności technicznej usługi Azure ATP](https://aka.ms/AatpCom)

Społeczność prywatne: [grupie usługi Yammer usługi Azure ATP](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Witryna Channel 9: [strony programu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Zobacz też

- [Praca z kontami poufnymi](sensitive-accounts.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)