---
title: Omówienie portalu usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu logowania się do portalu usługi Azure ATP oraz składniki portalu
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c4a437055c2fec0d242fe9de62ac9220ed2b66e6
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783801"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="working-with-the-azure-atp-portal"></a>Praca z portalem usługi Azure ATP

Monitorowanie i odpowiadanie na podejrzane działania wykrywane przez zaawansowanej ochrony przed zagrożeniami, użyj portalu usługi Azure ATP.

Wpisywanie `?` klucz znajdują się skróty klawiaturowe ułatwień dostępu z portalu usługi Azure ATP. 

Portal usługi Azure ATP zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. Portal usługi Azure ATP są również wyświetlane alerty i powiadomienia wyróżniające problemy występujące przez narzędzia Azure ATP lub nowe działania uznane za podejrzane.

W tym artykule opisano sposób pracy z kluczowych elementów portalu usługi Azure ATP.


## <a name="enabling-access-to-the-azure-atp-portal"></a>Umożliwianie dostępu do portalu usługi Azure ATP
Aby pomyślnie zalogować się do portalu usługi Azure ATP, musisz zalogować się jako użytkownik przypisany do grupy zabezpieczeń usługi Azure Active Directory dostępu do portalu usługi Azure ATP. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w usłudze Azure ATP zobacz [Praca z grupami ról usługi Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-portal"></a>Logując się do portalu usługi Azure ATP

1. Możesz użyć portalu usługi Azure ATP albo po zalogowaniu się do portalu [ https://portal.atp.azure.com ](https://portal.atp.azure.com) i wybierając odpowiedni obszar roboczy lub przechodząc do adresu URL obszaru roboczego: [https://*workspacename* . atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP obsługuje logowanie jednokrotne zintegrowane z uwierzytelnianiem Windows — Jeśli został już zalogowany do komputera, usługi Azure ATP używa tego tokenu do logowania się do portalu usługi Azure ATP. Możesz również się zalogować przy użyciu karty inteligentnej. Uprawnienia w usłudze Azure ATP odnoszą się do Twojej [roli administrator](atp-role-groups.md).

 > [!NOTE]
 > Upewnij się, że do logowania się do komputera, z którego chcesz uzyskać dostęp do portalu usługi Azure ATP przy użyciu usługi Azure ATP nazwę i hasło administratora. Alternatywnie można uruchomić przeglądarkę jako inny użytkownik lub wylogować Windows i dziennika użytkownikowi administrator usługi Azure ATP. 


### <a name="attack-time-line"></a>Oś czasu ataków

Oś czasu ataków to domyślna strona docelowa, którego nastąpi przejście na po zalogowaniu się do portalu obszaru roboczego usługi Azure ATP. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można filtrować wiersz czasu ataku, aby wyświetlać wszystkie, Otwórz, odrzucone lub Suppressed podejrzanych działań. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków w usłudze Azure ATP](media/atp-sa-timeline.png)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co nowego

Po wydaniu nowej wersji narzędzia Azure ATP **What's new** okna pojawi się u góry po prawej stronie informacją o tym, co zostało dodane w najnowszej wersji. Umożliwia także możesz z linkiem umożliwiającym pobranie wersji.

### <a name="filtering-panel"></a>Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### Pasek wyszukiwania <a name="search-bar"></a>

W górnym menu można znaleźć na pasku wyszukiwania. Możesz wyszukać konkretnego użytkownika, komputera lub grupy usługi Azure ATP. Aby go wypróbować, po prostu zacznij wpisywać tekst. W dolnej części paska wyszukiwania wskazuje liczbę wyników wyszukiwania. 

![Obraz wyszukiwania portalu usługi Azure ATP](media/atp-workspace-portal-search.png)

Możesz kliknąć pozycję numer, można przejść do strony wyników wyszukiwania, w którym można filtrować wyniki według typu jednostki w celu bliższego zbadania problemu.

![Wyniki wyszukiwania](media/search-results.png)

### <a name="health-center"></a>Centrum kondycji

Centrum kondycji zapewnia alerty gdy coś nie działa prawidłowo w obszarze roboczym usługi Azure ATP.

![Obraz Centrum kondycji usługi Azure ATP](media/atp-health-issue.png)

Dowolnym momencie, gdy system napotka problem, takie jak błąd łączności lub rozłączona czujnik autonomiczny narzędzia Azure ATP ikona Centrum kondycji poinformuje Cię przez wyświetlenie czerwonej kropki. 

![Obraz czerwonej kropki Centrum kondycji usługi Azure ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Wrażliwe grupy

Aby uzyskać informacji na temat wrażliwych grup w usłudze Azure ATP, zobacz [Praca z grupami poufnych](sensitive-accounts.md).

### <a name="mini-profile"></a>Mini profil

Jeśli możesz najechać kursorem myszy jednostki, w dowolnym miejscu portalu obszaru roboczego w przypadku, gdy istnieje pojedynczy element przedstawione, takie jak użytkownika lub komputera, mini profilu zawierającego automatycznie zostanie otwarty następujące informacje, jeśli jest dostępna i odpowiednie:

![Obraz mini profilu usługi Azure ATP](media/atp-mini-profile.png)

- Nazwa
- Tytuł
- Dział
- Tagi usługi AD
- Poczta e-mail
- Office
- Numer telefonu
- Domena
- Nazwa SAM
- Utworzone na — jednostka utworzenia w usłudze Active Directory. Jeśli zostało utworzone przed uruchomieniem narzędzia Azure ATP, monitorowanie, nie będzie ona wyświetlana.
- Pierwsze wystąpienie — narzędzia Azure ATP zaobserwowane działania z tej jednostki po raz pierwszy.
- Ostatnio widziano — czas ostatniego narzędzia Azure ATP zaobserwowane działania z tego obiektu.
- Wskaźnik SA — jest wyświetlany w przypadku podejrzanych działań skojarzone z tym obiektem.
- WD zaawansowanej ochrony przed zagrożeniami wskaźnik będą wyświetlane w przypadku podejrzanych działań w usłudze Windows Defender ATP skojarzone z tym obiektem.
- Ruchu poprzecznego, który ścieżki znaczków — będą wyświetlane, jeśli zostały ścieżki ruchu poprzecznego wykryto dla tej jednostki w ciągu ostatnich dwóch dni.


## <a name="see-also"></a>Zobacz też

- [Tworzenie obszarów roboczych usługi Azure ATP](install-atp-step1.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)