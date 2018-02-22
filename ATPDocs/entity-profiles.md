---
title: "Praca z profilami użytkowników w portalu Azure Advanced Threat Protection obszaru roboczego | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu badania użytkowników na ekranie profile użytkowników w portalu Azure ATP obszaru roboczego"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6ceefeeba6a52abf5da7ff44135cff55e9beab02
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="investigating-entity-profiles"></a>Badanie profile jednostek

Profilu jednostki zapewnia kompleksowe jednostki strony z przeznaczone do badania pełnej szczegółowo użytkowników, komputerów, urządzeń, i zasoby, które mają dostęp do historii. Strony profilu korzysta z nowych translator aktywności logicznej Azure ATP, można przyjrzeć się grupy działań występujących (zagregowane maksymalnie minutę) i grupować w pojedyncze działanie logiczne które pozwalają na lepsze zrozumienie działania rzeczywiste Użytkownicy.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę podmiotu, takie jak nazwa użytkownika, na osi czasu podejrzanych działań.

Menu po lewej stronie umożliwia wszystkich informacji usługi Active Directory dostępne jednostki — adres e-mail, domeny, widziany Data. Jeśli jednostka jest poufne, informuje, dlaczego. Na przykład użytkownik zostanie oznaczony jako wrażliwe lub poufne grupy?
Jeśli jest poufnych użytkownika, pojawi się ikona pod nazwą użytkownika.

## <a name="view-entity-activities"></a>Wyświetl jednostki działania

Aby wyświetlić wszystkie działania wykonywane przez użytkownika lub wykonywane z jednostką, kliknij **działania** kartę. 

 ![działania profilu użytkownika](media/user-profile-activities.png)

Domyślnie są wyświetlane w okienku głównym profilu jednostki osi czasu działań jednostki o historii do sześciu miesięcy, z którego można można także przejść do jednostek dostęp przez użytkownika lub dla jednostek, użytkowników, którzy dostęp do jednostki.

U góry można wyświetlić podsumowanie Kafelki, które zapewniają szybki przegląd muszą zrozumieć, w skrócie o jednostki - liczbę maszyn zalogowany użytkownik, ile zasoby były dostępne i lokalizacje, z których użytkownik zalogowany do sieci VPN (jeśli jest skonfigurowane) . 

Przy użyciu **Filtruj według** przycisk powyżej osi czasu działań, możesz filtrować działania według typu działania. Można również odfiltrować (zakłócenia) określonego typu działania. Jest to przydatne do badania, jeśli chcesz poznać podstawy jednostki czynności w sieci. Można także przejść do określonej daty i działania można wyeksportować odfiltrowane do programu Excel. Wyeksportowany plik zawiera stronę zmian usług katalogowych (rzeczy, które zmienione w usłudze Active Directory dla konta) i osobnej stronie działań. 

## <a name="view-directory-data"></a>Wyświetl dane katalogu

**Danych katalogu** karta zawiera statyczny dostępnych informacji z usługi Active Directory, w tym flagi zabezpieczeń kontroli dostępu użytkownika. Azure ATP wyświetla również członkostwa w grupach dla użytkownika, dzięki czemu można określić, czy użytkownik ma członkostwa bezpośredniego lub członkostwa cyklicznego. W przypadku grup Azure ATP Wyświetla listę członków grupy.

 ![dane katalogu profilu użytkownika](media/user-profile-dir-data.png)

W **kontroli dostępu użytkownika** sekcji ustawień zabezpieczeń powierzchni Azure ATP, które może wymagać Twojej attentions. Widać ważne flagi o użytkowniku, takie jak naciśnij użytkownik może wprowadzić do obejście hasła, czy użytkownik ma hasło nigdy nie wygasa, itd. 

## <a name="view-lateral-movement-paths"></a>Widok ścieżki penetracja sieci

Klikając kartę ścieżki przepływu penetracja, możesz wyświetlić pełni dynamicznych i aktywne mapy, która oferuje wizualną reprezentację ścieżki penetracja sieci do i z tego użytkownika, który może służyć do miejscach sieci.

Mapy zawiera listę liczbę przeskoków między komputerów lub użytkowników osoba atakująca do i z tego użytkownika do atakowania kont poufnych, a jeśli użytkownik ma konto poufne, można wyświetlić liczbę zasobów i kont były bezpośrednio podłączone.

Jeśli działanie nie została wykryta w ciągu ostatnich dwóch dni nie będzie już wyświetlany wykres, ale [penetracji przepływu Ścieżka raportu](reports.md) będzie można uzyskać informacje o penetracji sieci ścieżek w ciągu ostatnich 60 dni. 

Aby uzyskać więcej informacji, zobacz [penetracji ścieżki przepływu](use-case-lateral-movement-path.md). 

 ![ścieżki penetracja sieci profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Zobacz też

- [Zbadaj ścieżek penetracja sieci Azure ATP](use-case-lateral-movement-path.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)