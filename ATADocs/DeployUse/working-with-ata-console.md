---
title: "Praca z konsolą usługi ATA | Microsoft Advanced Threat Analytics"
description: "Opis sposobu logowania się do konsoli usługi ATA oraz składników konsoli"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 7f9ca7dcb227f5dde1225c55150fd1c737722ce1


---

# Praca z konsolą usługi ATA

Konsola usługi ATA służy do monitorowania podejrzanych działań wykrytych przez usługę ATA i reagowania na nie.

## Włączanie dostępu do konsoli usługi ATA
Każdy użytkownik należący do lokalnej grupy Administratorzy na serwerze centrum usługi ATA ma uprawnienia do logowania się do konsoli usługi ATA i zarządzania ustawieniami usługi ATA.
Aby zezwolić użytkownikowi na logowanie się do konsoli usługi ATA bez nadawania roli administratora lokalnego, dodaj go do grupy lokalnej **Administratorzy usługi Microsoft Advanced Threat Analytics**.

## Logowanie się do konsoli usługi ATA

1. Na serwerze centrum usługi ATA kliknij ikonę **Konsola usługi Microsoft ATA** na pulpicie lub otwórz przeglądarkę i przejdź do konsoli usługi ATA.

    ![Ikona serwera usługi ATA](media/ata-server-icon.png)

>[!NOTE]
> Możesz również otworzyć przeglądarkę z poziomu centrum usługi ATA lub bramy usługi ATA i przejść na adres IP skonfigurowany dla konsoli usługi ATA w instalacji centrum usługi ATA.    

2.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij pozycję **Zaloguj**.

![Obraz ekranu logowania usługi ATA](media/ATA-log-in-screen.jpg)

> [!NOTE]
> Należy zalogować się jako użytkownik, który należy do grupy administratorów lokalnych LUB grupy Administratorzy usługi Microsoft Advanced Threat Analytics.

## Konsola usługi ATA

Konsola usługi ATA zapewnia szybki przegląd wszystkich podejrzanych działań w kolejności chronologicznej. Umożliwia przejście do szczegółów dowolnego działania i wykonanie operacji w oparciu o te działania. W konsoli są również wyświetlane alerty i powiadomienia wyróżniające problemy dotyczące sieci usługi ATA lub nowe działania uznane za podejrzane.

Są to kluczowe elementy konsoli usługi ATA.


### Oś czasu ataków

Jest to domyślna strona docelowa wyświetlana po zalogowaniu się do konsoli usługi ATA. Domyślnie wszystkie otwarte podejrzane działania są wyświetlane na osi czasu ataków. Oś czasu ataków można filtrować, aby wyświetlać Wszystkie, Otwarte, Odrzucone lub Rozwiązane podejrzane działania. Można również sprawdzić ważność przypisaną do poszczególnych działań.

![Obraz osi czasu ataków usługi ATA](media/attack-timeline.png)

Aby uzyskać więcej informacji, zobacz [Praca z podejrzanymi działaniami](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Pasek powiadomień

Po wykryciu nowego podejrzanego działania pasek powiadomień zostanie otwarty automatycznie po prawej stronie. Jeśli od czasu ostatniego zalogowania miały miejsce nowe podejrzane działania, pasek powiadomień zostanie otwarty po pomyślnym zalogowaniu. W dowolnym momencie można uzyskać dostęp do paska powiadomień, klikając strzałkę po prawej stronie.

![Obraz paska powiadomień usługi ATA](media/notification-bar.png)

### Panel filtrowania

Podejrzane działania wyświetlane na osi czasu ataków lub na karcie podejrzanych działań profilu jednostki można filtrować na podstawie stanu i ważności.

### Pasek wyszukiwania

W menu u góry znajduje się pasek wyszukiwania. Umożliwia on wyszukiwanie określonych użytkowników, komputerów lub grup w usłudze ATA. Aby go wypróbować, po prostu zacznij wpisywać tekst.

![Obraz wyszukiwania w konsoli usługi ATA](media/ATA-console-search.png)

### Centrum kondycji

Centrum kondycji zapewnia alerty, gdy coś nie działa prawidłowo we wdrożeniu usługi ATA.

![Obraz centrum kondycji usługi ATA](media/health-center.png)

Za każdym razem, gdy system napotka problem, taki jak błąd łączności lub rozłączona brama usługi ATA, ikona centrum kondycji poinformuje o nim użytkownika przez wyświetlenie czerwonej kropki. ![Obraz czerwonej kropki centrum kondycji usługi ATA](media/ATA-Health-Center-Alert-red-dot.png)

Alerty centrum kondycji można odrzucać lub rozwiązywać. Są również podzielone na kategorie Wysoka, Średnia lub Niska w zależności od ważności. W przypadku rozwiązania alertu, który jest nadal wykrywany przez usługę ATA jako aktywny, zostanie on automatycznie przeniesiony do listy otwartych alertów. Jeśli system wykryje, że przyczyna alertu już nie istnieje (problem został rozwiązany), alert zostanie przeniesiony do listy rozwiązanych.

### Profile użytkowników i komputerów

Usługa ATA tworzy profil dla każdego użytkownika i komputera w sieci. W profilu użytkownika usługi ATA wyświetlane są ogólne informacje, takie jak członkostwo w grupie, ostatnie logowania i ostatnio używane zasoby.

![Profil użytkownika](media/user-profile.png)

W profilu komputera usługi ATA wyświetlane są ogólne informacje, takie jak ostatnie logowania i ostatnio używane zasoby.

![Profil komputera](media/computer-profile.png)

Usługa ATA zapewnia dodatkowe informacje na temat jednostek (komputerów, urządzeń i użytkowników) na następujących stronach: Podsumowanie, Działania i Podejrzane działania.

Profil, który nie mógł zostać całkowicie rozwiązany przez usługę ATA, zostanie oznaczony ikoną koła wypełnionego do połowy umieszczoną obok niego.


![Obraz nierozwiązanego profilu usługi ATA](media/ATA-Unresolved-Profile.jpg)

### Mini profil

W dowolnym miejscu w konsoli, gdzie wyświetlana jest pojedyncza jednostka, taka jak użytkownik lub komputer, umieszczenie wskaźnika myszy na jednostce spowoduje automatyczne otwarcie mini profilu zawierającego następujące informacje, jeśli są dostępne:

![Obraz mini profilu usługi ATA](media/ATA-mini-profile.jpg)

-   Nazwa

-   Obraz

-   Poczta e-mail

-   Telefon

-   Liczba podejrzanych działań według ważności



## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


