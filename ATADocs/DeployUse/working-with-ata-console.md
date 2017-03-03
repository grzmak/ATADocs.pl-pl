---
title: "Opis konsoli usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opis sposobu logowania się do konsoli usługi ATA oraz składników konsoli"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: cb712537b42c4e86ed24607e70c614e8d37025c0


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="working-with-the-ata-console"></a>Praca z konsolą usługi ATA

Konsola usługi ATA służy do monitorowania podejrzanych działań wykrytych przez usługę ATA i reagowania na nie.

## <a name="enabling-access-to-the-ata-console"></a>Włączanie dostępu do konsoli usługi ATA
Aby pomyślnie zalogować się do konsoli usługi ATA, należy użyć konta użytkownika, który został przypisany do właściwej roli usługi ATA z dostępem do konsoli ATA. Aby uzyskać więcej informacji na temat kontroli dostępu opartego na rolach (RBAC) w usłudze ATA, zobacz [Praca z grupami ról usługi ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Logowanie się do konsoli usługi ATA

1. Na serwerze centrum usługi ATA kliknij ikonę **Konsola usługi Microsoft ATA** na pulpicie lub otwórz przeglądarkę i przejdź do konsoli usługi ATA.

    ![Ikona serwera usługi ATA](media/ata-server-icon.png)

>[!NOTE]
> Możesz również otworzyć przeglądarkę z poziomu centrum usługi ATA lub bramy usługi ATA i przejść na adres IP skonfigurowany dla konsoli usługi ATA w instalacji centrum usługi ATA.    

2.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij pozycję **Zaloguj**.

![Obraz ekranu logowania usługi ATA](media/ATA-log-in-screen.png)


## <a name="the-ata-console"></a>Konsola usługi ATA

Konsola usługi ATA zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. W konsoli są również wyświetlane alerty i powiadomienia wyróżniające problemy dotyczące sieci usługi ATA lub nowe działania uznane za podejrzane.

Są to kluczowe elementy konsoli usługi ATA.


### <a name="attack-time-line"></a>Oś czasu ataków

Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Oś czasu ataków można filtrować, aby wyświetlać Wszystkie, Otwarte, Odrzucone lub Rozwiązane podejrzane działania. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków usługi ATA](media/attack-timeline-1.7.png)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### <a name="notification-bar"></a>Pasek powiadomień

Po wykryciu nowego podejrzanego działania pasek powiadomień zostanie otwarty automatycznie po prawej stronie. Jeśli od czasu ostatniego zalogowania miały miejsce nowe podejrzane działania, pasek powiadomień zostanie otwarty po pomyślnym zalogowaniu. W dowolnym momencie można uzyskać dostęp do paska powiadomień, klikając strzałkę po prawej stronie.

![Obraz paska powiadomień usługi ATA](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### <a name="search-bar"></a>Pasek wyszukiwania

W menu u góry znajduje się pasek wyszukiwania. Umożliwia on wyszukiwanie określonych użytkowników, komputerów lub grup w usłudze ATA. Aby go wypróbować, po prostu zacznij wpisywać tekst.

![Obraz wyszukiwania w konsoli usługi ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Centrum kondycji

Centrum kondycji zapewnia alerty, gdy coś nie działa prawidłowo we wdrożeniu usługi ATA.

![Obraz centrum kondycji usługi ATA](media/ATA-Health-Issue.jpg)

Za każdym razem, gdy system napotka problem, taki jak błąd łączności lub rozłączona brama usługi ATA, ikona centrum kondycji poinformuje o nim użytkownika przez wyświetlenie czerwonej kropki. ![Obraz czerwonej kropki centrum kondycji usługi ATA](media/ATA-Health-Center-Alert-red-dot.png)

Alerty centrum kondycji można odrzucać lub rozwiązywać. Są również podzielone na kategorie Wysoka, Średnia lub Niska w zależności od ważności. W przypadku rozwiązania alertu, który jest nadal wykrywany przez usługę ATA jako aktywny, zostanie on automatycznie przeniesiony do listy otwartych alertów. Jeśli system wykryje, że przyczyna alertu już nie istnieje (problem został rozwiązany), alert zostanie przeniesiony do listy rozwiązanych.

### <a name="user-and-computer-profiles"></a>Profile użytkowników i komputerów

Usługa ATA tworzy profil dla każdego użytkownika i komputera w sieci. W profilu użytkownika usługi ATA wyświetlane są ogólne informacje, takie jak członkostwo w grupie, ostatnie logowania i ostatnio używane zasoby.

![Profil użytkownika](media/user-profile.png)

W profilu komputera usługi ATA wyświetlane są ogólne informacje, takie jak ostatnie logowania i ostatnio używane zasoby.

![Profil komputera](media/computer-profile.png)

Usługa ATA zapewnia dodatkowe informacje na temat jednostek (komputerów, urządzeń i użytkowników) na następujących stronach: Podsumowanie, Działania i Podejrzane działania.

Profil, który nie mógł zostać całkowicie rozwiązany przez usługę ATA, zostanie oznaczony ikoną koła wypełnionego do połowy umieszczoną obok niego.


![Obraz nierozwiązanego profilu usługi ATA](media/ATA-Unresolved-Profile.jpg)

### <a name="mini-profile"></a>Mini profil

W dowolnym miejscu w konsoli, gdzie wyświetlana jest pojedyncza jednostka, taka jak użytkownik lub komputer, umieszczenie wskaźnika myszy na jednostce spowoduje automatyczne otwarcie mini profilu zawierającego następujące informacje, jeśli są dostępne:

![Obraz mini profilu usługi ATA](media/ATA-mini-profile.jpg)

-   Nazwa

-   Obraz

-   Poczta e-mail

-   Telefon

-   Liczba podejrzanych działań według ważności



## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


