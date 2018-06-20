---
title: Opis portalu Azure Advanced Threat Protection obszaru roboczego | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu logowania się do portalu Azure ATP obszaru roboczego oraz składniki portalu obszaru roboczego
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40e139cc5e7dc6396914b0314d2d698a4782af02
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444709"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Praca z portalu Azure ATP obszaru roboczego

Użyj portalu obszaru roboczego Azure ATP do monitorowania i reagowania na podejrzanych działań wykrytych przez ATP.

Wpisywanie `?` klucz znajdują się skróty klawiaturowe dla dostępności portalu Azure ATP obszaru roboczego. 

Portal obszaru roboczego Azure ATP zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. Portal obszaru roboczego są również wyświetlane alerty i powiadomienia wyróżniające problemy, które zostały odebrane przez Azure ATP lub nowe działania uznane za podejrzane.

W tym artykule opisano sposób pracy z kluczowych elementów portalu Azure ATP obszaru roboczego.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Włączanie dostępu do portalu Azure ATP obszaru roboczego
Aby pomyślnie zalogować się do portalu Azure ATP obszaru roboczego, trzeba Zaloguj się jako użytkownik, który został przypisany do odpowiedniej grupy zabezpieczeń usługi Azure Active Directory dostępu do portalu Azure ATP obszaru roboczego. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w Azure ATP, zobacz [Praca z grupami roli Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Logowanie do portalu Azure ATP obszaru roboczego

1. Portal obszaru roboczego można wprowadzić albo po zalogowaniu się do portalu zarządzania obszaru roboczego [ https://portal.atp.azure.com ](https://portal.atp.azure.com) a następnie wybranie odpowiedniego obszaru roboczego lub przechodząc do adresu URL obszaru roboczego: [https:// *workspacename*. atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP obsługuje logowanie jednokrotne zintegrowane z uwierzytelnianiem systemu Windows — Jeśli już po zalogowaniu do komputera, Azure ATP używa tego tokenu do logowania do portalu Azure ATP obszaru roboczego. Możesz również się zalogować przy użyciu karty inteligentnej. Uprawnienia w usłudze Azure ATP odpowiadają Twojej [roli administratora](atp-role-groups.md).

 > [!NOTE]
 > Upewnij się, że do logowania się do komputera, z którego chcesz uzyskać dostęp do portalu obszaru roboczego Azure ATP przy użyciu Azure ATP administrator nazwę użytkownika i hasło. Alternatywnie można uruchomić przeglądarki jako inny użytkownik lub dziennika spoza systemu Windows i dzienników na za pomocą usługi Azure ATP użytkownika Administrator. 


### <a name="attack-time-line"></a>Oś czasu ataków

Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do portalu Azure ATP obszaru roboczego. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można filtrować wiersz czasu ataku, aby wyświetlać wszystkie, otwarte, odrzucone lub Suppressed podejrzane działania. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków ATP Azure](media/atp-sa-timeline.png)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Co nowego

Po wydaniu nowej wersji Azure ATP **nowości** okno jest wyświetlane w górnej prawo do informacją o tym, co zostało dodane w najnowszej wersji. Umożliwia także możesz Link do pobierania wersji.

### <a name="filtering-panel"></a>Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### Pasek wyszukiwania <a name="search-bar"></a>

W menu górnym znajduje się pasek wyszukiwania. Możesz wyszukać określonego użytkownika, komputera lub grupy w Azure ATP. Aby go wypróbować, po prostu zacznij wpisywać tekst. W dolnej części pasek wyszukiwania wskazuje liczbę wyników wyszukiwania. 

![Obraz wyszukiwania portalu usługi Azure obszaru roboczego ATP](media/atp-workspace-portal-search.png)

Kliknij liczbę, można uzyskać dostępu do strony wyników wyszukiwania można filtrować wyniki według typu jednostki dla dalszego postępowania.

![wyniki wyszukiwania](media/search-results.png)

### <a name="health-center"></a>Centrum kondycji

Centrum kondycji zapewnia alerty gdy coś nie działa prawidłowo w obszarze roboczym Azure ATP.

![Obraz Centrum kondycji usługi Azure ATP](media/atp-health-issue.png)

Dowolnej chwili, gdy system napotka problem, takie jak błąd łączności lub rozłączona czujnik autonomiczny Azure ATP ikona Centrum kondycji informuje przez wyświetlenie czerwonej kropki. 

![Obraz czerwonej kropki Centrum kondycji Azure ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Wrażliwe grupy

Informacje dotyczące poufnych grup w ATP znajdują się w temacie [Praca z grupami poufnych](sensitive-accounts.md).

### <a name="mini-profile"></a>Mini profil

Jeśli umieść kursor nad jednostką, w dowolnym miejscu portalu obszaru roboczego, w przypadku, gdy jest pojedynczą jednostką przedstawione, np. użytkownika lub komputera, mini profilu zawierającego automatycznie otwiera następujące informacje, jeśli jest dostępny i odpowiednie:

![Obraz mini profilu usługi Azure ATP](media/atp-mini-profile.png)

- Nazwa
- Tytuł
- Dział
- Tagi AD
- Poczta e-mail
- Office
- Numer telefonu
- Domena
- Nazwa SAM
- Utworzony na — Jeśli została utworzona jednostka w usłudze Active Directory. Jeśli został utworzony przed uruchomieniem Azure ATP monitorowania, nie będzie on wyświetlany.
- Pierwszy raz widziane — obserwowanych działanie w tej jednostce ATP Azure po raz pierwszy.
- Godzina ostatniego kontaktu — ostatni ATP Azure obserwowanych działania z tego obiektu.
- Wskaźnika SA — jest wyświetlana, jeśli są podejrzane działania skojarzone z tym obiektem.
- WD ATP identyfikator — będzie można wyświetlić, jeśli istnieją podejrzanych działań w program Windows Defender ATP skojarzone z tym obiektem.
- Penetracja sieci, które ścieżki znaczków - będzie wyświetlana, jeśli zostały ścieżki penetracja sieci dla tej jednostki wykryte w ciągu ostatnich dwóch dni.


## <a name="see-also"></a>Zobacz też

- [Tworzenie obszarów roboczych usługi Azure ATP](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)