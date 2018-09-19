---
title: Praca z profilami jednostki w konsoli usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu badania jednostki z ekranu profile użytkownika w konsoli usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a34d25e59183e496350216f5d3043430cd65bca6
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133462"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="investigating-entity-profiles"></a>Badanie profile jednostek

Profilu jednostki udostępnia Ci pulpit nawigacyjny zaprojektowany do zbadania szczegółowym omówieniu użytkowników, komputerów, urządzeń i zasobów, które mają dostęp do i ich historii. Strony profilu korzysta z zalet nowych translator aktywności logiczne usługi ATA, co można przyjrzeć się grupę działań, które pojawiają się (zagregowana maksymalnie minutę) i zgrupować je w jedno działanie logicznych daje lepsze zrozumienie działania rzeczywistego użytkownika Liczba użytkowników.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę jednostki, takie jak nazwa użytkownika, na osi czasu podejrzanych działań.

W menu po lewej stronie zapewnia wszystkie usługi Active Directory dostępnych informacji o jednostce — adres e-mail, domena, widziany Data. Jeśli jednostka jest wrażliwa go informuje dlaczego. Na przykład użytkownik zostanie oznaczone jako poufne lub członkiem grupy poufne?
Jeśli poufnych użytkownika, pojawi się ikona pod nazwą użytkownika.

## <a name="view-entity-activities"></a>Wyświetl jednostki działania

Aby wyświetlić wszystkie działania wykonywane przez użytkownika lub wykonywane na jednostce, kliknij pozycję **działania** kartę. 

 ![działania profilu użytkownika](media/user-profile-activities.png)

Domyślnie w okienku głównym profilu jednostki jest wyświetlana oś czasu jednostki działań z historii maksymalnie 6 miesięcy wstecz, z którego możesz także przejść do szczegółów jednostki używane przez użytkownika lub w przypadku jednostek, użytkownicy, którzy dostęp do jednostki.

U góry strony można wyświetlić podsumowanie Kafelki, dające z krótkim omówieniem co jest potrzebne zrozumieć, w skrócie o jednostki. Te Kafelki, które zmianom w zależności od typ jednostki go, jest dla użytkownika, zostanie wyświetlony:
- Ile otwierania podejrzanych działań, które są dla użytkownika
- Na ilu komputerach zalogowanego użytkownika
- Liczby zasobów, które użytkownik uzyskał dostęp
- Z lokalizacji, w których użytkownik jest zalogowany do sieci VPN

  ![menu jednostki](media/entity-menu.png)

Dla komputerów możesz zobaczyć:
- Ile otwierania podejrzanych działań, które istnieją maszyny
- Ilu użytkowników rejestrowane na komputerze
- Liczby zasobów, dostęp do komputera
- Jak wiele lokalizacji sieci VPN została otwarta z na komputerze
- Listę, z których komputer adresów IP został użyty.

  ![komputer menu jednostki](media/entity-computer.png)

Za pomocą **filtrowanie według** przycisku powyżej oś czasu działań, możesz filtrować działania według typu działania. Można również odfiltrować (hałas) określonego typu działania. Może to być bardzo przydatne do badania, gdy chcesz poznać podstawy jednostki działania w sieci. Możesz również przejść do określonej daty, a następnie wyeksportować działania jako dane odfiltrowane do programu Excel. Wyeksportowany plik zawiera strona zmian usług katalogowych (rzeczy, które zmienione w usłudze Active Directory dla konta) i osobnej strony dla działania. 

## <a name="view-directory-data"></a>Wyświetl dane katalogu

**Dane katalogu** karta zawiera statyczne dostępne informacje z usługi Active Directory, w tym flagi zabezpieczeń kontroli dostępu użytkownika. Usługa ATA wyświetla również członkostwa w grupach użytkownika tak, aby stwierdzić, czy użytkownik ma członkostwa bezpośredniego lub członkostwa cykliczne. Dla grup usługa ATA Wyświetla listę członków grupy.

 ![dane katalogu profilu użytkownika](media/user-profile-dir-data.png)

W **kontrola dostępu użytkownika** sekcji ATA wydobywa informacje dotyczące ustawień zabezpieczeń, które mogą wymagać Twojej attentions. Możesz zobaczyć ważne flagi o użytkowniku, takie jak naciśnięcie użytkownika można wprowadzić do obejście hasła, czy użytkownik ma hasło, które nigdy nie wygasa, itp. 

## <a name="view-lateral-movement-paths"></a>Ścieżki ruchu poprzecznego widoku

Klikając **ścieżki ruchu poprzecznego** karty, możesz wyświetlić mapę pełni dynamicznego i Zwiększyliśmy, która umożliwia wizualną reprezentację ścieżki ruchu poprzecznego do i z tego użytkownika, który może służyć do miejscach sieci.

Mapa zawiera listę ile przeskoki między komputerami lub użytkowników, gdy osoba atakująca musi do i z tego użytkownika do naruszenia bezpieczeństwa do kont poufnych i, jeśli użytkownik ma się kontem wrażliwym, możesz zobaczyć, ile zasoby i konta są bezpośrednio połączone. Aby uzyskać więcej informacji, zobacz [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md). 

 ![ścieżki ruchu poprzecznego profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
