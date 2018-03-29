---
title: Praca z profilami jednostki w konsoli Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu badania jednostek z ekranu profilów użytkownika w konsoli usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f2fd6f28eb6bf11aa3705f5320fcdae01d02f6d0
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="investigating-entity-profiles"></a>Badanie profile jednostek

Profil jednostki udostępnia, możesz z pulpitu nawigacyjnego przeznaczone do badania pełnej szczegółowo użytkowników, komputerów, urządzeń i zasoby, które mają dostęp do historii. Strony profilu korzysta z nowych translator aktywności logicznej usługi ATA, co można przyjrzeć się grupy aktywności występujących (łącznie maksymalnie minutę) i grupować w pojedyncze działanie logiczne które pozwalają na lepsze zrozumienie działania rzeczywistego użytkownika Użytkownicy.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę podmiotu, takie jak nazwa użytkownika, na osi czasu podejrzanych działań.

Menu po lewej stronie umożliwia wszystkich informacji usługi Active Directory dostępne jednostki — adres e-mail, domeny, widziany Data. Jeśli jednostka jest poufnych go informuje dlaczego. Na przykład użytkownik zostanie oznaczony jako wrażliwe lub poufne grupy?
Jeśli poufnych użytkownika, pojawi się ikona pod nazwą użytkownika.

## <a name="view-entity-activities"></a>Wyświetl jednostki działania

Aby wyświetlić wszystkie działania wykonywane przez użytkownika lub wykonywane z jednostką, kliknij **działania** kartę. 

 ![działania profilu użytkownika](media/user-profile-activities.png)

Domyślnie są wyświetlane w okienku głównym profilu jednostki osi czasu działań jednostki o historii do 6 miesięcy, z którego można można także przejść do jednostek dostęp przez użytkownika lub dla jednostek, użytkowników, którzy dostęp do jednostki.

U góry można wyświetlić podsumowanie Kafelki, które zapewniają szybki przegląd muszą zrozumieć, w skrócie o jednostce. Te Kafelki zmiany oparte na typ jednostki go, jest dla użytkownika, zostanie wyświetlony:
- Ile Otwórz podejrzanych działań są dostępne dla użytkownika
- Ilu komputerach zalogowany użytkownik
- Liczby zasobów, dostęp do użytkownika
- Z lokalizacji, które użytkownik jest zalogowany do sieci VPN

  ![menu jednostki](media/entity-menu.png)

Dla komputerów można wyświetlić:
- Ile Otwórz podejrzanych działań są maszyny
- Ile użytkownicy zalogowani do komputera
- Liczby zasobów, dostęp do komputera
- Ile lokalizacji na komputerze uzyskano z sieci VPN
- Listę, której komputer adresów IP został użyty.

  ![komputer menu jednostki](media/entity-computer.png)

Przy użyciu **Filtruj według** przycisk powyżej osi czasu działań, możesz filtrować działania według typu działania. Można również odfiltrować (zakłócenia) określonego typu działania. Jest to naprawdę pomocne, aby umożliwić zbadanie problemu, gdy chcesz podstawy jednostki czynności w sieci. Można także przejść do określonej daty i działania można wyeksportować odfiltrowane do programu Excel. Wyeksportowany plik zawiera stronę zmian usług katalogowych (rzeczy, które zmienione w usłudze Active Directory dla konta) i osobnej stronie działań. 

## <a name="view-directory-data"></a>Wyświetl dane katalogu

**Danych katalogu** karta zawiera statyczny dostępnych informacji z usługi Active Directory, w tym flagi zabezpieczeń kontroli dostępu użytkownika. Usługi ATA są również wyświetlane członkostwa w grupach dla użytkownika, dzięki czemu można określić, czy użytkownik ma członkostwa bezpośredniego lub członkostwa cyklicznego. Dla grup usługi ATA zawiera członków grupy.

 ![dane katalogu profilu użytkownika](media/user-profile-dir-data.png)

W **kontroli dostępu użytkownika** sekcji, ustawienia zabezpieczeń, które mogą wymagać Twojej attentions udostępnia usługi ATA. Widać ważne flagi o użytkowniku, takie jak naciśnij użytkownik może wprowadzić do obejście hasła, czy użytkownik ma hasło nigdy nie wygasa, itd. 

## <a name="view-lateral-movement-paths"></a>Widok ścieżki penetracja sieci

Klikając **penetracji ścieżki przepływu** kartę można wyświetlić pełni dynamicznych i aktywne mapy, która oferuje wizualną reprezentację ścieżki penetracja sieci do i z tego użytkownika, który może służyć do miejscach sieci.

Mapy zawiera listę liczbę przeskoków między komputerami lub użytkowników, gdy osoba atakująca miałoby do i z tego użytkownika do atakowania kont poufnych oraz jeśli użytkownik ma się konto poufnych, ile zasobów i kont są bezpośrednio widoczne połączone. Aby uzyskać więcej informacji, zobacz [penetracji ścieżki przepływu](use-case-lateral-movement-path.md). 

 ![ścieżki penetracja sieci profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
