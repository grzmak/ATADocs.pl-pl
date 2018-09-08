---
title: Opis konsoli usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Opis sposobu logowania się do konsoli usługi ATA oraz składników konsoli
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 021a8dba5e750d76e14caa3d0c58862f254499eb
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166752"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="working-with-the-ata-console"></a>Praca z konsolą usługi ATA

Konsola usługi ATA służy do monitorowania podejrzanych działań wykrytych przez usługę ATA i reagowania na nie.

Wpisywanie `?` klucz zapewnia skrótów klawiaturowych dla ułatwień dostępu w portalu usługi ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Włączanie dostępu do konsoli usługi ATA
Aby pomyślnie zalogować się do konsoli usługi ATA, musisz zalogować się jako użytkownik, który został przypisany do właściwej roli usługi ATA, uzyskać dostęp do konsoli usługi ATA. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w usłudze ATA, zobacz [Praca z grupami ról usługi ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Logowanie się do konsoli usługi ATA

>[!NOTE]
 > Począwszy od usługi ATA 1.8, proces logowania do konsoli usługi ATA odbywa się przy użyciu logowania jednokrotnego.

1. Na serwerze centrum usługi ATA kliknij ikonę **Konsola usługi Microsoft ATA** na pulpicie lub otwórz przeglądarkę i przejdź do konsoli usługi ATA.

    ![Ikona serwera usługi ATA](media/ata-server-icon.png)

 >[!NOTE]
 > Możesz również otworzyć przeglądarkę z poziomu centrum usługi ATA lub bramy usługi ATA i przejść na adres IP skonfigurowany dla konsoli usługi ATA w instalacji centrum usługi ATA.    

2.  Jeśli dołączono do komputera, na którym zainstalowano Centrum usługi ATA i komputer, z którego próbujesz uzyskać dostęp do konsoli usługi ATA są zarówno domeny, usługa ATA obsługuje logowanie jednokrotne zintegrowane z uwierzytelniania Windows — Jeśli użytkownik został już zalogowany do komputera, usługa ATA używa ten token do logowania się do konsoli usługi ATA. Możesz również się zalogować przy użyciu karty inteligentnej. Swoje uprawnienia w usłudze ATA odnoszą się do Twojej [roli administrator](ata-role-groups.md).

 > [!NOTE]
 > Upewnij się, że do logowania się do komputera, z którego chcesz uzyskać dostęp do konsoli usługi ATA przy użyciu usługi ATA nazwę i hasło administratora. Zamiast tego możesz też uruchomić przeglądarkę jako inny użytkownik lub wylogować się z systemu Windows i zalogować jako administrator usługi ATA. Monit konsoli usługi ATA zapytała o poświadczenia, uzyskują dostęp do konsoli przy użyciu adresu IP adres i monit o podanie poświadczeń.

3. Aby zalogować się przy użyciu logowania jednokrotnego, upewnij się, witryna konsoli usługi ATA jest zdefiniowana jako lokalna witryna intranetowa w przeglądarce i czy możesz uzyskać do niego dostęp za pomocą nazwy skróconej lub hosta lokalnego.

> [!NOTE]
> Oprócz rejestrowania każdego podejrzanego działania i alertu kondycji, każda zmiana konfiguracji wprowadzona w konsoli usługi ATA podlega inspekcji w dzienniku zdarzeń systemu Windows na komputerze z centrum usługi ATA, w obszarze **Dziennik aplikacji i usług**, a następnie **Microsoft ATA**. Każde logowanie do konsoli usługi ATA również podlega inspekcji.<br></br>  Konfiguracja wpływająca na bramę usługi ATA jest również rejestrowana w dzienniku zdarzeń systemu Windows na komputerze bramy usługi ATA. 



## <a name="the-ata-console"></a>Konsola usługi ATA

Konsola usługi ATA zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. W konsoli są również wyświetlane alerty i powiadomienia wyróżniające problemy dotyczące sieci usługi ATA lub nowe działania uznane za podejrzane.

Są to kluczowe elementy konsoli usługi ATA.


### <a name="attack-time-line"></a>Oś czasu ataków

Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można filtrować wiersz czasu ataku, aby wyświetlać wszystkie, Otwórz, odrzucone lub Suppressed podejrzanych działań. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków usługi ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Pasek powiadomień

Po wykryciu nowego podejrzanego działania pasek powiadomień zostanie otwarty automatycznie po prawej stronie. Jeśli od czasu ostatniego zalogowania miały miejsce nowe podejrzane działania, pasek powiadomień zostanie otwarty po pomyślnym zalogowaniu. W dowolnym momencie można uzyskać dostęp do paska powiadomień, klikając strzałkę po prawej stronie.

![Obraz paska powiadomień usługi ATA](media/notification-bar-1.7.png)

### <a name="whats-new"></a>Co nowego

Po wydaniu nowej wersji usługi ATA **What's new** okna pojawi się u góry po prawej stronie informacją o tym, co zostało dodane w najnowszej wersji. Umożliwia także możesz z linkiem umożliwiającym pobranie wersji.

### <a name="filtering-panel"></a>Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### <a name="search-bar"></a>Pasek wyszukiwania

W górnym menu można znaleźć na pasku wyszukiwania. Możesz wyszukać konkretnego użytkownika, komputera lub grupy w usłudze ATA. Aby go wypróbować, po prostu zacznij wpisywać tekst.

![Obraz wyszukiwania w konsoli usługi ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Centrum kondycji

Centrum kondycji zapewnia alerty, gdy coś nie działa prawidłowo we wdrożeniu usługi ATA.

![Obraz centrum kondycji usługi ATA](media/ATA-Health-Issue.jpg)

Dowolnym momencie, gdy system napotka problem, takie jak błąd łączności lub rozłączona brama usługi ATA, ikona Centrum kondycji poinformuje Cię przez wyświetlenie czerwonej kropki. ![Obraz czerwonej kropki centrum kondycji usługi ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="sensitive-groups"></a>Wrażliwe grupy

Grupy na poniższej liście są uważane za **wrażliwe** przez usługę ATA. Każda jednostka, która należy do poniższych grup, jest traktowana jako wrażliwa:

- Kontrolery domeny tylko do odczytu na poziomie organizacji 
- Administratorzy domeny 
- Kontrolery domeny 
- Administratorzy schematu,
- Enterprise Admins 
- Twórcy-właściciele zasad grupy 
- Kontrolery domeny tylko do odczytu 
- Administratorzy  
- Użytkownicy zaawansowani  
- Operatorzy kont  
- Operatorzy serwerów   
- Operatorzy drukowania
- Operatorzy kopii zapasowych
- Replikatorzy 
- Użytkownicy pulpitu zdalnego 
- Operatorzy konfiguracji sieci 
- Konstruktorzy przychodzących zaufań lasu 
- Administratorzy usługi DNS 


### <a name="mini-profile"></a>Mini profil

Jeśli możesz najechać kursorem myszy jednostki, w konsoli w dowolnym miejscu w przypadku, gdy jest pojedynczą jednostką przedstawiony przykład użytkownika lub komputera, mini profilu zawierającego automatycznie otwiera wyświetlane następujące informacje, jeśli jest dostępny:

![Obraz mini profilu usługi ATA](media/ATA-mini-profile.jpg)

-   Nazwa

-   Obraz

-   Poczta e-mail

-   Telefon

-   Liczba podejrzanych działań według ważności



## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
