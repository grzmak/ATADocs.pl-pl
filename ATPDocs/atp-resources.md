---
title: Lista przydatnych zasobów Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera listę zasobów przydatne dla Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8d91468664a76436078772ad1fc8510ea56d67a
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298502"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Azure przewodnik gotowości ATP

Ten artykuł zawiera plan gotowości, który zapewnia listę zasobów, które ułatwiają rozpoczęcie pracy z Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Opis usługi Azure ATP

Azure zaawansowane zagrożenia ochrony (ATP) to usługa w chmurze, która pomaga chronić przedsiębiorstwa przed zaawansowanymi atakami ukierunkowanymi ataków i zagrożeń wewnętrznych wiele typów. Aby dowiedzieć się więcej na temat Azure ATP, użyj następujących zasobów: 
- [Omówienie usługi Azure ATP](what-is-atp.md)
- [Azure ATP wprowadzenie wideo - Full](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Decyzji dotyczących wdrożenia

Azure ATP składa się z usługą w chmurze znajdującej się na platformie Azure i czujników, które można zainstalować na kontrolerze domeny lub na dedykowanych serwerach. Zanim otrzymasz Azure ATP działa prawidłowo, należy wybrać typ innych typów czujników, które wdrożenia.<br>Jeśli korzystasz z serwerów fizycznych, należy zaplanować pojemność. Możliwe korzystanie z narzędzia do określania rozmiaru przydzielić miejsce dla Twojego czujników pomocy: 
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool) — narzędzia do określania rozmiaru automatyzuje kolekcji ilość ruchu sieciowego monitoruje Azure ATP. Automatycznie zapewnia możliwość obsługi i zalecenia dotyczące zasobów dla czujników. 
- [Wytyczne dotyczące planowania pojemności usługi ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Wdrażanie usługi Azure ATP

Te zasoby pomoże Ci skonfigurować Azure ATP, połączyć z usługą Active Directory, Pobierz pakiet czujnika, Konfigurowanie zbierania zdarzeń i opcjonalnie zintegrować z serwera VPN i konfigurowanie kont wystawionych jako przynęta i wykluczenia. 
- [Spróbuj ATP Azure (część pakietu EMS E5)](http://aka.ms/aatptrial) wersji próbnej jest ważny przez 90 dni.
- [Przewodnik wdrażania](install-atp-step1.md) wdrażanie ATP Azure w danym środowisku, wykonaj następujące kroki.
- [Integracja Azure ATP z usługi Windows Defender ATP](integrate-wd-atp.md)
- 
## <a name="azure-atp-settings"></a>Ustawienia usługi Azure ATP

Podstawowe ustawienia niezbędne w Azure ATP są skonfigurowane podczas tworzenia obszaru roboczego. Istnieje jednak kilka innych ustawień, które można skonfigurować w celu dostosowania Azure ATP wchodzące wykryć większej dokładności dla danego środowiska, takich jak integracji SIEM a ustawień inspekcji. 

- [Azure Dokumentacja ogólna ATP](what-is-atp.md)
- [Ustawienia inspekcji](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) — inspekcji Twojej kondycji kontrolera domeny, przed i po wdrożeniu usługi ATA. 

## <a name="work-with-azure-atp"></a>Praca z Azure ATP

Po skonfigurowaniu i uruchomieniu Azure ATP można wyświetlić podejrzanych działań wykrytych w osi czasu działania. Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do portalu Azure ATP. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można również sprawdzić ważność przypisaną do poszczególnych działań. Sprawdź poszczególne podejrzane działania przez przechodzenie jednostek (komputerów, urządzeń, użytkowników) otwieranie stron ich profilu, które dostarczają więcej informacji. Te zasoby pomocne podczas pracy z podejrzanymi działaniami Azure ATP: 

- [Przewodnik podejrzanych działań w usłudze Azure ATP](suspicious-activity-guide.md) Dowiedz się, jak klasyfikowanie i wykonać kolejne kroki z Twojej wykryć Azure ATP.
- [Tag grup jako poufne](sensitive-accounts.md) wgląd we widoczności poświadczeń na grupach zabezpieczeń poufnych.

## <a name="security-best-practices"></a>Najlepsze rozwiązania

- [Azure ATP — często zadawane pytania](atp-technical-faq.md) — ten artykuł zawiera listę często zadawanych pytań dotyczących Azure ATP oraz wskazówki i odpowiedzi. 
## <a name="community-resources"></a>Zasoby społeczności

Blog: [blog Azure ATP](https://aka.ms/aatpblog)

Społeczność publicznego: [społeczności technicznej platformy Azure ATP](https://aka.ms/AatpCom)

Społeczność prywatnych: [grupy Yammer ATP platformy Azure](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Kanał 9: [strony witryny Channel 9 zabezpieczeń firmy Microsoft](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Zobacz też

- [Praca z kontami poufnymi](sensitive-accounts.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)