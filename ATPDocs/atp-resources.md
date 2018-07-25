---
title: Lista przydatne zasoby usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera listę przydatne zasoby dla usługi Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/23/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 498d1b4d14db079583da1999bfb68a5648111362
ms.sourcegitcommit: 63a36cd96aec30e90dd77bee1d0bddb13d2c4c64
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2018
ms.locfileid: "39227142"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="azure-atp-readiness-guide"></a>Podręcznik gotowości usługi Azure ATP

Ten artykuł zawiera mapę gotowości, która udostępnia listę zasobów, które umożliwia wprowadzenie do usługi Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Omówienie usługi Azure ATP

Azure zaawansowanych Threat Protection (ATP) to usługa w chmurze, która pomaga chronić przedsiębiorstwo przed wieloma rodzajami zaawansowanych ukierunkowanych cyberataków i zagrożeniami wewnętrznymi. Użyj następujących zasobów, aby dowiedzieć się więcej na temat usługi Azure ATP: 
- [Omówienie usługi Azure ATP](what-is-atp.md)
- [Usługa Azure ATP klip wideo z wprowadzeniem — pełny](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Decyzji dotyczących wdrożenia

Narzędzie Azure ATP składa się z usługą w chmurze znajdującymi się na platformie Azure i czujniki, które mogą być instalowane na kontrolerze domeny lub na dedykowanych serwerach. Przed zagłębieniem się narzędzia Azure ATP uruchomiona, jest należy wybrać typ lepiej spełniane były czujniki, które wdrożenie.<br>Jeśli używasz serwerów fizycznych należy zaplanować pojemność. Możesz uzyskać pomoc przy użyciu narzędzia rozmiaru do alokowania miejsca dla Twojego czujniki: 
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool) — narzędzia do określania rozmiaru automatyzuje zbiór natężenia ruchu, które monitoruje usługi Azure ATP. Automatycznie zapewnia wsparcie dla zasobów and recommendations for i czujniki. 
- [Wytyczne dotyczące planowania pojemności usługi ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Wdrażanie usługi Azure ATP

Te zasoby ułatwia konfigurowanie usługi Azure ATP, nawiązać połączenie z usługi Active Directory, pobieranie pakietu czujnika, Konfigurowanie zbierania zdarzeń i opcjonalnie zintegrować z sieci VPN i skonfigurować konta wystawione jako przynęta i wykluczenia. 
- [Wypróbuj usługi Azure ATP (część pakietu EMS E5)](http://aka.ms/aatptrial) wersja próbna jest ważna przez 90 dni.
- [Przewodnik dotyczący wdrażania](install-atp-step1.md) wdrożenia usługi Azure ATP w danym środowisku, wykonaj następujące kroki.
- [Integracja usługi Azure ATP z usługą Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Ustawienia usługi Azure ATP

Podstawowe ustawienia niezbędne w narzędzia Azure ATP są skonfigurowane, podczas tworzenia obszaru roboczego. Jednak istnieje kilka innych ustawień, które można skonfigurować w celu dostosowania narzędzia Azure ATP wprowadzić bardziej precyzyjne dla danego środowiska, takie jak integracja rozwiązania SIEM wykrywania, które ustawienia inspekcji. 

- [Ogólna dokumentacja usługi Azure ATP](what-is-atp.md)
- [Ustawienia inspekcji](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) — Inspekcja usługi kondycji kontrolera domeny, przed i po wdrożeniu usługi ATA. 

## <a name="work-with-azure-atp"></a>Praca z usługi Azure ATP

Po skonfigurowaniu i uruchomieniu narzędzia Azure ATP można wyświetlić podejrzanych działań, które są wykrywane na osi czasu działania. Jest to domyślna strona docelowa, którego nastąpi przejście na po zalogowaniu się do portalu usługi Azure ATP. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można również sprawdzić ważność przypisaną do poszczególnych działań. Badanie każdego podejrzanego działania, przechodzenie jednostek (komputerów, urządzeń, użytkowników) aby otworzyć ich strony profilów, które zawierają więcej informacji. Te zasoby ułatwiają pracę z narzędzia Azure ATP podejrzanych działań: 

- [Przewodnik po podejrzanych działaniach usługi Azure ATP](suspicious-activity-guide.md) Dowiedz się, jak klasyfikowanie i wykonaj kolejne kroki z usługi wykrywania usługi Azure ATP.
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
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)