---
title: Praca z profilami użytkowników w portalu obszaru roboczego usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu badania użytkowników na ekranie profilów użytkowników w portalu obszaru roboczego usługi Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 357973698d9d53936c3fa308bc0021ae1cd98f60
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783512"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="understanding-entity-profiles"></a>Opis jednostki profilów

Profilu jednostki zapewnia kompleksowe jednostki strony z przeznaczony dla pełnej szczegółowe badanie użytkowników, komputerów, urządzeń i zasoby, które mają dostęp do i ich historii. Strona profilu korzysta z nowych translator aktywności logicznego usługi Azure ATP, można przyjrzeć się grupę działań, które pojawiają się (zagregowane maksymalnie minutę) i zgrupować je w jedno działanie logicznych daje lepsze zrozumienie działania rzeczywistych Użytkownicy.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę jednostki, takie jak nazwa użytkownika, na osi czasu podejrzanych działań.

W menu po lewej stronie zapewnia wszystkie usługi Active Directory dostępnych informacji o jednostce — adres e-mail, domena, widziany Data. Jeśli jednostka jest wrażliwa, określa dlaczego. Na przykład użytkownik zostanie oznaczone jako poufne lub członkiem grupy poufne?
Jeśli poufnych użytkownika, widzisz ikonę w obszarze nazwy użytkownika.

## <a name="view-entity-activities"></a>Wyświetl jednostki działania

Aby wyświetlić wszystkie działania wykonywane przez użytkownika lub wykonywane na jednostce, kliknij pozycję **działania** kartę. 

 ![działania profilu użytkownika](media/user-profile-activities.png)

Domyślnie w okienku głównym profilu jednostki jest wyświetlana oś czasu jednostki działań z historii maksymalnie sześć miesięcy wstecz, z którego możesz także przejść do szczegółów jednostki używane przez użytkownika lub w przypadku jednostek, użytkownicy, którzy dostęp do jednostki.

U góry strony można wyświetlić podsumowanie Kafelki, które zapewniają szybki przegląd co jest potrzebne zrozumieć, w skrócie o jednostce — jak wiele maszyn, które użytkownik zalogowany do uzyskano liczby zasobów i lokalizacji, z których użytkownik zaloguje się do sieci VPN (jeśli jest skonfigurowane) . 

Za pomocą **filtrowanie według** przycisku powyżej oś czasu działań, możesz filtrować działania według typu działania. Można również odfiltrować (hałas) określonego typu działania. Może to być przydatne do badania, gdy chcesz poznać podstawy jednostki działania w sieci. Możesz również przejść do określonej daty, a następnie wyeksportować działania jako dane odfiltrowane do programu Excel. Wyeksportowany plik zawiera strona zmian usług katalogowych (rzeczy, które zmienione w usłudze Active Directory dla konta) i osobnej strony dla działania. 

## <a name="view-directory-data"></a>Wyświetl dane katalogu

**Dane katalogu** karta zawiera statyczne dostępne informacje z usługi Active Directory, w tym flagi zabezpieczeń kontroli dostępu użytkownika. Narzędzie Azure ATP jest również wyświetlana członkostwa w grupach dla użytkownika, aby stwierdzić, czy użytkownik ma członkostwa bezpośredniego lub członkostwa cykliczne. Dla grup usługi Azure ATP Wyświetla listę członków grupy.

 ![dane katalogu profilu użytkownika](media/user-profile-dir-data.png)

W **kontrola dostępu użytkownika** sekcji Ustawienia zabezpieczeń na powierzchniach narzędzia Azure ATP, które mogą wymagać Twojej attentions. Widać ważne flagi o użytkowniku, na przykład w przypadku użytkownika można nacisnąć klawisz enter, aby pominąć hasła, i jeśli użytkownik ma hasło, które nigdy nie wygasa, itp. 

## <a name="view-lateral-movement-paths"></a>Ścieżki ruchu poprzecznego widoku

Klikając kartę ścieżki przepływu poprzecznych, możesz wyświetlić mapę pełni dynamicznego i Zwiększyliśmy, która umożliwia wizualną reprezentację ścieżki ruchu poprzecznego do i z tego użytkownika, który może służyć do miejscach sieci.

Mapa zawiera listę liczbę przeskoków między komputerów lub użytkowników musi do i z tego użytkownika do naruszenia bezpieczeństwa kont poufnych, a jeśli użytkownik ma poufne konto, możesz zobaczyć, ile zasoby i konta były bezpośrednio podłączone.

Jeśli działanie nie zostanie wykryty w ciągu ostatnich dwóch dni wykresu nie jest już wyświetlany, ale [raportu ścieżki ruchu poprzecznego](reports.md) jest dostępny uzyskać informacje na temat ścieżek penetracji sieci, które istniały w ciągu ostatnich 60 dni. 

Aby uzyskać więcej informacji, zobacz [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md). 

 ![ścieżki ruchu poprzecznego profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Zobacz też

- [Badanie ścieżek penetracji sieci za pomocą Zaawansowanej ochrony przed zagrożeniami na platformie Azure](use-case-lateral-movement-path.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)