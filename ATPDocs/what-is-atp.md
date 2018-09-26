---
title: Co to jest Azure Advanced Threat Protection (ATP)? | Microsoft Docs
description: Wyjaśnia Azure Advanced Threat Protection (ATP) i jakiego rodzaju podejrzane działania może wykryć
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/16/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f3e03f5307a9a09ffb2a62e7313be4629f4bc060
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750474"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="what-is-azure-advanced-threat-protection"></a>Co to jest Zaawansowana ochrona przed zagrożeniami dla platformy Azure?
Azure zaawansowanych Threat Protection (ATP) jest rozwiązaniem zabezpieczenia oparte na chmurze, które identyfikuje, wykrywa i pomoże Ci zbadać akcje intruzowi skierowany przeciwko Twojej organizacji, których bezpieczeństwo zostało naruszone tożsamości i zaawansowanych zagrożeń. Narzędzie Azure ATP umożliwia analitykom SecOp i specjaliści ds. zabezpieczeń, który próbuje wykrywania zaawansowanych ataków w środowiskach hybrydowych na:  
- Monitorowanie użytkowników, zachowań jednostek i działań z analizy tekstu w uczeniu maszynowym  
- Ochrona tożsamości użytkowników i poświadczeń przechowywanych w usłudze Active Directory  
- Identyfikację oraz badanie podejrzanymi działaniami użytkowników i zaawansowanymi atakami w całym łańcuchu kończenia 
- Podaj informacje dotyczące Wyczyść zdarzenia na prostej osi czasu ułatwiającej klasyfikowanie 
 
## <a name="monitor-and-profile-user-behavior-and-activities"></a>Monitorowanie i profilu zachowania użytkowników i działania  
Narzędzie Azure ATP monitoruje i analizuje aktywność użytkowników i informacji w sieci, takich jak uprawnienia oraz członkostwa w grupie tworzenia zachowań punktu odniesienia dla każdego użytkownika. Narzędzie Azure ATP następnie wykrywa anomalie za pomocą wbudowanej inteligencji adaptacyjnej, dzięki czemu umożliwia wgląd w podejrzane działania i zdarzenia, odsłaniając zaawansowanych zagrożeń, których bezpieczeństwo zostało naruszone użytkowników i zagrożeniami wewnętrznymi połączonego z Twojej organizacji. Azure ATP własności czujników monitorowania kontrolerów domeny organizacji, zapewniając kompleksowy widok dla wszystkich działań użytkownika z każdego urządzenia. 
 
## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>Ochrona tożsamości użytkowników i zmniejszyć obszar narażony na ataki   
Narzędzie Azure ATP zawiera cenne informacje konfiguracje tożsamości i zabezpieczeń sugerowane najlepszych rozwiązań. Raporty dotyczące zabezpieczeń i analizy profilu użytkownika usługi Azure ATP pomaga znacznie zmniejszyć obszar ataków organizacji, co utrudnia złamanie poświadczeń użytkownika i Rozwijaj ataku. ATP visual bocznej ścieżki ruchu pomóc w szybkim poznaniu, dokładnie tak jak osoba atakująca może przemieszczają wewnątrz organizacji do naruszenia bezpieczeństwa kont poufnych i ułatwia zapobieganie te zagrożenia z wyprzedzeniem. Dodatkowe, zaawansowanej ochrony przed zagrożeniami bezpieczeństwa Raporty ułatwiają identyfikowanie użytkowników i urządzeń, które przeprowadzają uwierzytelnianie przy użyciu haseł w postaci zwykłego tekstu i zapewniania dodatkowego wglądu w celu zasad i poziom bezpieczeństwa organizacji.  
 
## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-attack-kill-chain"></a>Identyfikowanie podejrzanych działań i zaawansowanymi atakami w łańcuchu kończenia ataków 
Zazwyczaj ataków uruchamianych przeciwko dowolnej jednostce dostępne, takich jak użytkownika o niskich uprawnieniach, a następnie szybko przenieść bok do momentu osoba atakująca uzyska dostęp do najcenniejszych zasobów — takich jak wrażliwych kont, Administratorzy domeny i wysoce poufne dane. Narzędzie Azure ATP identyfikuje tych zaawansowanych zagrożeń w miejscu źródłowym w całym łańcuchu kończenia ataku całego: 
### <a name="reconnaissance"></a>Rekonesans 
Zidentyfikuj użytkowników nieautoryzowanych i osoby atakującej próby uzyskania informacji na temat nazw użytkowników, członkostwo w grupie użytkowników, adresów IP przypisanych do urządzenia, zasoby i więcej możliwości — przy użyciu różnych metod.  
### <a name="compromised-users"></a>Zagrożonych użytkowników
Zidentyfikuj próbuje naruszyć poświadczenia użytkownika za pomocą ataków siłowych, uwierzytelnianie nie powiodło się, zmian członkostwa w grupach użytkowników i dodatkowe metody.  

### <a name="lateral-movements"></a>Ruchów poprzecznych
Wykryć, że próby przemieszczają wewnątrz sieci dalsze zapanowania wrażliwych użytkowników, przy użyciu metod, takich jak przekazać bilet, Przekaż wartość skrótu, Overpass wyznaczania wartości skrótu i inne.  

### <a name="domain-dominance"></a>Zdominowanie domeny
Wyróżnianie zachowania osoba atakująca, jeśli zostanie osiągnięty zdominowanie domeny, za pośrednictwem zdalne wykonywanie kodu na kontrolerze domeny i metody takie jak kontrolera domeny w tle, replikacji kontrolera domeny złośliwy, bilet uwierzytelniania Golden Ticket działań i.   

## <a name="investigate-alerts-and-user-activities"></a>Badanie alertów i działań użytkownika  
Narzędzie Azure ATP zaprojektowano w celu ograniczenia liczby niepotrzebnych alertów ogólne, zapewniając alerty zabezpieczeń tylko odpowiednie i ważnych na osi czasu proste, w czasie rzeczywistym organizacji ataku. Widok osi czasu ataków usługi Azure ATP umożliwia łatwe skoncentrowanie się na ważnych rzeczach, wykorzystując inteligencji funkcji analizy inteligentnej. Specjaliści ds. zabezpieczeń przy użyciu narzędzia Azure ATP pozwala na szybkie badanie zagrożeń i uzyskiwanie szczegółowych informacji w całej organizacji dla użytkowników, urządzeń i zasoby sieciowe. Bezproblemową integrację z usługą Windows Defender ATP zapewnia kolejną warstwę zwiększone zabezpieczenia dodatkowego procesu wykrywania i ochrony przed zaawansowane, trwałe zagrożenia w systemie operacyjnym.  

## <a name="additional-resources-for-azure-atp"></a>Dodatkowe zasoby dotyczące usługi Azure ATP  
Rozpocznij bezpłatny okres próbny: [ https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 ] (https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "pakietu Enterprise Mobility + Security E5")
 
Postępuj zgodnie z usługi Azure ATP w społeczność techniczna firmy Microsoft  
[https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection "Narzędzie Azure ATP w społeczność techniczna firmy Microsoft")
 
Dołącz do społeczności usługi Yammer usługi Azure ATP [ https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 ] (https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "społeczności Yammer usługi Azure ATP")
 
Odwiedź stronę produktu Azure ATP  
[https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/](https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/ "Strona produktu usługi Azure ATP")

Aby uzyskać więcej informacji na temat architektury usługi Azure ATP, zobacz [architektura zaawansowanej ochrony przed zagrożeniami platformy](atp-architecture.md).
 
## <a name="whats-next"></a>Co dalej? 

Zaleca się wdrożenie usługi Azure ATP w fazach 3:  

### <a name="phase-1"></a>Faza 1

1. Konfigurowanie usługi Azure ATP, aby chronić swoje podstawowego środowiska. Model szybkie wdrażanie usługi Azure ATP pozwala objąć ochroną Twojej organizacji — już dzisiaj. [Zainstaluj zaawansowanej ochrony przed zagrożeniami](install-atp-step1.md)  
2. Ustaw [wrażliwym kontom](sensitive-accounts.md) i [konta wystawione jako przynęta](install-atp-step7.md).   
3. Przejrzyj raporty i [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md).  


### <a name="phase-2"></a>Faza 2

1. Chroń wszystkie kontrolery domeny i [lasów](atp-multi-forest.md) w Twojej organizacji.  
2.  Monitoruj wszystkie [alerty](working-with-suspicious-activities.md) — badać alerty poprzecznego dominacji przenoszenie i domeny.  
3. Praca z [Alert zabezpieczeń przewodnik](suspicious-activity-guide.md) zrozumieć zagrożenia i oceniać ich istotność potencjalnych ataków.   


### <a name="phase-3"></a>Faza 3

1. Integruj alerty usługi Azure ATP do SecOp przepływów pracy. 

## <a name="see-also"></a>Zobacz też
- [Narzędzie Azure ATP — często zadawane pytania](atp-technical-faq.md)
- [Praca z alertami zabezpieczeń](working-with-suspicious-activities.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)