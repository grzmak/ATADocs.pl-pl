---
title: "Opis konsoli usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opis sposobu logowania się do konsoli usługi ATA oraz składników konsoli"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 26c093c4163593611b175f4f0002f443e593f952
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="working-with-the-ata-console"></a>Praca z konsolą usługi ATA

Konsola usługi ATA służy do monitorowania podejrzanych działań wykrytych przez usługę ATA i reagowania na nie.

Wpisywanie `?` klucz znajdują się skróty klawiaturowe dla ułatwień dostępu w portalu usługi ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Włączanie dostępu do konsoli usługi ATA
Pomyślnie zalogować się do konsoli usługi ATA, należy zalogować się użytkownik, który został przypisany do roli usługi ATA właściwy dostęp do konsoli usługi ATA. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w usłudze ATA, zobacz [Praca z grupami roli usługi ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Logowanie się do konsoli usługi ATA

>[!NOTE]
 > Począwszy od usługi ATA 1.8, proces logowania do konsoli usługi ATA odbywa się przy użyciu logowania jednokrotnego.

1. Na serwerze centrum usługi ATA kliknij ikonę **Konsola usługi Microsoft ATA** na pulpicie lub otwórz przeglądarkę i przejdź do konsoli usługi ATA.

    ![Ikona serwera usługi ATA](media/ata-server-icon.png)

 >[!NOTE]
 > Możesz również otworzyć przeglądarkę z poziomu centrum usługi ATA lub bramy usługi ATA i przejść na adres IP skonfigurowany dla konsoli usługi ATA w instalacji centrum usługi ATA.    

2.  Jeśli przyłączony komputer, na którym zainstalowano Centrum usługi ATA i komputera, z którego próbujesz uzyskać dostęp do konsoli usługi ATA są zarówno domeny, usługa ATA obsługuje rejestracji jednokrotnej zintegrowane z uwierzytelnianiem systemu Windows — Jeśli już po zalogowaniu do komputera, usługa ATA używa token do zalogowania do konsoli usługi ATA. Możesz również się zalogować przy użyciu karty inteligentnej. Uprawnienia w usłudze ATA odpowiadają Twojej [roli administrator](ata-role-groups.md).

 > [!NOTE]
 > Upewnij się, że do logowania się do komputera, z którego ma dostęp do konsoli usługi ATA przy użyciu usługi ATA admin nazwę użytkownika i hasło. Zamiast tego możesz też uruchomić przeglądarkę jako inny użytkownik lub wylogować się z systemu Windows i zalogować jako administrator usługi ATA. Monitowanie konsoli usługi ATA, aby poprosić o poświadczenia, dostęp do konsoli przy użyciu adresu IP i adres monit o wprowadzenie poświadczeń.

3. Aby zalogować się przy użyciu logowania jednokrotnego, upewnij się, witrynę konsoli usługi ATA jest zdefiniowany jako lokację lokalny intranet w przeglądarce i dostęp za pomocą nazwa_skrócona lub localhost.

> [!NOTE]
> Oprócz rejestrowania każdego podejrzanego działania i alertu kondycji, każda zmiana konfiguracji wprowadzona w konsoli usługi ATA podlega inspekcji w dzienniku zdarzeń systemu Windows na komputerze z centrum usługi ATA, w obszarze **Dziennik aplikacji i usług**, a następnie **Microsoft ATA**. Każde logowanie do konsoli usługi ATA również podlega inspekcji.<br></br>  Konfiguracja wpływająca na bramę usługi ATA jest również rejestrowana w dzienniku zdarzeń systemu Windows na komputerze bramy usługi ATA. 



## <a name="the-ata-console"></a>Konsola usługi ATA

Konsola usługi ATA zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. W konsoli są również wyświetlane alerty i powiadomienia wyróżniające problemy dotyczące sieci usługi ATA lub nowe działania uznane za podejrzane.

Są to kluczowe elementy konsoli usługi ATA.


### <a name="attack-time-line"></a>Oś czasu ataków

Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Można filtrować wiersz czasu ataku, aby wyświetlać wszystkie, otwarte, odrzucone lub Suppressed podejrzane działania. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków usługi ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Pasek powiadomień

Po wykryciu nowego podejrzanego działania pasek powiadomień zostanie otwarty automatycznie po prawej stronie. Jeśli od czasu ostatniego zalogowania miały miejsce nowe podejrzane działania, pasek powiadomień zostanie otwarty po pomyślnym zalogowaniu. W dowolnym momencie można uzyskać dostęp do paska powiadomień, klikając strzałkę po prawej stronie.

![Obraz paska powiadomień usługi ATA](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### <a name="search-bar"></a>Pasek wyszukiwania

W menu górnym znajduje się pasek wyszukiwania. Możesz wyszukać określonego użytkownika, komputera lub grupy w usłudze ATA. Aby go wypróbować, po prostu zacznij wpisywać tekst.

![Obraz wyszukiwania w konsoli usługi ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Centrum kondycji

Centrum kondycji zapewnia alerty, gdy coś nie działa prawidłowo we wdrożeniu usługi ATA.

![Obraz centrum kondycji usługi ATA](media/ATA-Health-Issue.jpg)

Dowolnej chwili, gdy system napotka problem, takie jak błąd łączności lub rozłączona brama usługi ATA, ikona Centrum kondycji informuje przez wyświetlenie czerwonej kropki. ![Obraz czerwonej kropki centrum kondycji usługi ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="user-and-computer-profiles"></a>Profile użytkowników i komputerów

Usługa ATA tworzy profil dla każdego użytkownika i komputera w sieci. W profilu użytkownika usługi ATA wyświetlane są ogólne informacje, takie jak członkostwo w grupie, ostatnie logowania i ostatnio używane zasoby. Umożliwia także listy lokalizacje, w którym użytkownik jest połączony za pośrednictwem sieci VPN. Lista członkostwa w grupach, które ATA uwzględnia wielkość liter Zobacz Następująca lista.

![Profil użytkownika](media/user-profile.png)

W profilu komputera usługa ATA wyświetla ogólne informacje, takie jak ostatnie logowania i ostatnio używane zasoby.

![Profil komputera](media/computer-profile.png)

Usługa ATA zapewnia dodatkowe informacje na temat jednostek (komputerów, urządzeń i użytkowników) na następujących stronach: Podsumowanie, Działania i Podejrzane działania.

Profil usługi ATA nie mogło zostać całkowicie rozwiązany jest identyfikowany ikoną koła wypełnionego do połowy obok niej.


![Obraz nierozwiązanego profilu usługi ATA](media/ATA-Unresolved-Profile.jpg)

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

Jeśli umieść kursor nad jednostki, w dowolnym miejscu konsoli w przypadku, gdy jest pojedynczą jednostką przedstawiony przykład użytkownika lub komputera, mini profilu zawierającego automatycznie otwiera wyświetlanie następujące informacje, jeśli są dostępne:

![Obraz mini profilu usługi ATA](media/ATA-mini-profile.jpg)

-   Nazwa

-   Obraz

-   Poczta e-mail

-   Telefon

-   Liczba podejrzanych działań według ważności



## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
